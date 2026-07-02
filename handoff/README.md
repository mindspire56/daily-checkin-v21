# 每日打卡项目交接说明

这个文件夹用于把当前项目状态交接给新的 Codex 对话、实验仓库或后续维护者。

这些文件不参与网页运行，不会被 `index.html` 自动加载，也不会影响 GitHub Pages 的页面功能。它们只是项目说明文档，可以安全放在当前正式站代码仓库里。

## 当前正式站

- 正式仓库：`mindspire56/daily-checkin`
- 正式网站：`https://mindspire56.github.io/daily-checkin/`
- 当前正式版本：`1.4.4.2`
- 本地项目路径：`C:\Users\SONG\Documents\每日打卡网页`
- 主页面文件：`C:\Users\SONG\Documents\每日打卡网页\index.html`
- 版本快照目录：`C:\Users\SONG\Documents\每日打卡网页\versions`

## 新对话读取顺序

新对话开始维护本项目时，建议按下面顺序读取：

1. `CURRENT_STATE_1.4.4.2.md`
2. `RELEASE_RULES.md`
3. `DESIGN_NOTES.md`
4. `DATA_MODEL.md`
5. `CUSTOMIZATION_NOTES.md`
6. `ROADMAP.md`
7. `AI_APP_SOCIAL_PLAN.md`

## 2.0.0 实验策略

2.0.0 不建议直接修改当前正式仓库主页面。推荐新建实验仓库：

- `mindspire56/daily-checkin-v2`
- 或 `mindspire56/daily-checkin-lab`

实验站可以单独部署到：

- `https://mindspire56.github.io/daily-checkin-v2/`
- 或 `https://mindspire56.github.io/daily-checkin-lab/`

等 2.0.0 效果满意后，再把稳定版本发布回正式库 `daily-checkin`。

## 交接原则

- 当前 1.x 是正式稳定线。
- 2.x 是实验重构线。
- 正式线不能因为实验功能崩坏。
- 每次发布必须保留快照、上传 GitHub、验证线上版本、给用户可点击链接。
- 不把 GitHub token、AI API Key、签名密钥等秘密写入项目文件。
