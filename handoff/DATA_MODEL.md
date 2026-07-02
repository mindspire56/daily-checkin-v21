# DATA_MODEL：localStorage 数据结构

## 存储键

当前主存储键：

```js
daily-checkin-v2
```

旧版迁移键：

```js
daily-checkin-v1
```

## 顶层结构

当前数据大致结构：

```js
{
  version: 2,
  appVersion: "1.4.4.2",
  activeMode: "focus",
  modes: {},
  habits: [],
  dailyLog: {},
  skipLog: {},
  todayTasks: {},
  settings: {}
}
```

## modes

模式对象。

```js
modes: {
  focus: {
    id: "focus",
    name: "专注",
    accent: "#df7951",
    habitIds: ["read", "meditate", "write"]
  }
}
```

系统模式：

- `focus`：专注
- `rest`：恢复
- `learn`：学习
- `sport`：运动
- `routine`：作息
- `create`：创作

自定义模式 ID 格式：

```js
custom-时间戳
```

## habits

习惯对象数组。

```js
{
  id: "read",
  name: "阅读20分钟",
  emoji: "📖",
  modeIds: ["focus", "learn", "create"],
  energy: "low",
  category: "learn",
  weekendBonus: true,
  history: {
    "2026-07-01": true
  }
}
```

字段说明：

- `id`：习惯 ID。
- `name`：习惯名称。
- `emoji`：展示图标。
- `modeIds`：属于哪些模式。
- `energy`：`low` 或 `high`。
- `category`：习惯类别。
- `weekendBonus`：周末推荐加权。
- `history`：旧/兼容记录，每个日期是否完成。

## todayTasks

今日任务列表，以“日期 + 模式”作为键。

```js
todayTasks: {
  "2026-07-02|focus": ["read", "write"]
}
```

推荐任务加入今日后，会写入这里。

## dailyLog

每日详情日志。

```js
dailyLog: {
  "2026-07-02": {
    items: [
      {
        habitId: "read",
        modeId: "focus",
        name: "阅读20分钟",
        emoji: "📖",
        time: "2026-07-02T20:00:00.000Z",
        energy: "low",
        category: "learn"
      }
    ],
    diary: "今天状态不错",
    weather: "晴"
  }
}
```

字段说明：

- `items`：当天完成的打卡记录。
- `diary`：当天日记。
- `weather`：手动天气文本。

## skipLog

推荐任务“换一个”记录。

```js
skipLog: {
  "2026-07-02": {
    focus: {
      ids: ["read"],
      count: 1,
      rest: false
    }
  }
}
```

字段说明：

- `ids`：当天当前模式已跳过的习惯。
- `count`：替换次数，当前上限 10。
- `rest`：是否主动休息。

## settings

设置对象。

```js
settings: {
  currentPush: {},
  quoteIndex: 0,
  customQuoteIndex: 0,
  customQuotes: [],
  modeOrder: ["focus", "rest", "learn"],
  modePinned: false,
  modeShuffleDate: ""
}
```

字段说明：

- `currentPush`：每天每模式当前推荐的习惯。
- `quoteIndex`：当前显示的鼓励语索引。
- `customQuoteIndex`：自定义鼓励语切换索引。
- `customQuotes`：用户自定义鼓励语。
- `modeOrder`：模式排列顺序，前三个展示在首页。
- `modePinned`：是否固定用户排列。
- `modeShuffleDate`：每日随机刷新模式的日期。

## customQuotes

自定义鼓励语数组。

```js
customQuotes: [
  {
    text: "慢慢来，也是在前进",
    icon: "🌱"
  }
]
```

当前限制：

- 最多 30 条。
- 文字和图标合计长度不宜超过 32。
- 图标建议 1 到 2 个字符。

## 积分计算

当前积分不单独存储，而是根据 `dailyLog` 动态计算。

### 单日单模式积分

```js
Math.min(20, completedItems(date, modeId).length)
```

规则：

- 一个完成项 1 分。
- 每日同一模式最多 20 分。
- 取消打卡后，对应分数自动消失。

### 当前模式总积分

当前模式所有日期的单日积分相加。

### 所有积分

所有模式积分直接相加。

### 有效积分

按日期计算，每天只取所有模式里的最高单模式积分，再相加。

## 数据迁移建议

2.0.0 如果改变数据结构，应保留迁移函数：

- 读取 `daily-checkin-v2`。
- 转换为新结构。
- 写入新键，例如 `daily-checkin-v3` 或 `daily-checkin-2`.
- 不要直接删除旧数据。
- 提供导出/导入功能。
