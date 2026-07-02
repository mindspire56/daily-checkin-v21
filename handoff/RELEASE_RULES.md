# RELEASE_RULES：发布与快照规则

## 核心规则

每次用户要求版本修改并确认完成时，必须同步做完：

1. 修改本地代码。
2. 更新版本号。
3. 运行本地检查。
4. 保存版本快照。
5. 更新版本记录。
6. 上传 GitHub。
7. 验证线上版本。
8. 给用户可点击网站链接。

不能只改本地，不上传。
不能只上传，不验证。
不能忘记快照。

## 版本号规则

- 大版本：`2.0.0`
  - 架构、数据模型、页面方向大变化。
- 中版本：`1.5.0`
  - 新功能或明显模块变化。
- 微调版本：`1.4.4.3`
  - 小视觉、小交互、小 bug 修复。

当前正式版本是 `1.4.4.2`。

## 必改位置

在 `index.html` 中至少检查：

- `<meta name="app-version" content="...">`
- `APP_VERSION='...'`

## 本地检查

修改后运行 JS 语法检查，确认 `<script>` 内容可解析。

推荐检查：

```powershell
& 'C:\Users\SONG\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\bin\node.exe' -e "const fs=require('fs'); const s=fs.readFileSync('index.html','utf8'); const a=s.indexOf('<script>')+8; const b=s.indexOf('</script>'); new Function(s.slice(a,b)); console.log('JS syntax OK');"
```

## 快照规则

每个正式交付版本都要保存：

```text
versions\版本号\index.html
```

例如：

```text
versions\1.4.4.2\index.html
```

## 版本记录

每次修改都要更新：

```text
VERSIONS.md
```

记录内容包括：

- 版本号
- 主要变化
- 修复点
- 快照路径

## GitHub 上传

正式站仓库：

```text
mindspire56/daily-checkin
```

正式站地址：

```text
https://mindspire56.github.io/daily-checkin/
```

如果 Pages 分支曾经切换过，上传前应确认当前 Pages source。为了稳妥，必要时可以同步上传到 `main` 和 `gh-pages`。

## 线上验证

上传后需要访问带缓存破除参数的链接，例如：

```text
https://mindspire56.github.io/daily-checkin/?v=版本号
```

验证页面源码或返回内容中是否包含：

```html
<meta name="app-version" content="版本号">
```

## 最终回复要求

给用户最终回复时，必须说明：

- 已完成的版本号。
- 本地是否保存快照。
- 是否已上传 GitHub。
- 是否已验证线上版本。
- 给出可点击链接。

示例：

```text
已完成 1.4.4.2，本地快照已保存，GitHub 已上传并验证。
线上链接：[每日打卡](https://mindspire56.github.io/daily-checkin/?v=14442)
```

## 安全规则

- 不把 GitHub token 写进任何项目文件。
- 不把 AI API Key 写进任何项目文件。
- 不把 Android 签名密钥提交到公开仓库。
- 不删除用户未要求删除的文件。
- 不覆盖用户已有改动，除非用户明确要求。
