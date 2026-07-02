# 2.1.0.0 分支策略

## 当前判断

- `daily-checkin-v2` 已发布到 `2.0.0.3`，这个版本可以作为稳定可用的实验正式版保存。
- 后续 AI 陪伴、App 打包、轻社交、页面架构升级、数据结构升级等大突破，不建议继续直接在 `daily-checkin-v2` 里做。
- 新突破线从 `2.1.0.0` 开始，使用独立 GitHub 仓库和独立 GitHub Pages 地址。

## 仓库分工

- 正式主站：`mindspire56/daily-checkin`
- 稳定实验站：`mindspire56/daily-checkin-v2`
- 2.1 突破实验站：`mindspire56/daily-checkin-v21`

## 版本关系

- `2.0.0.3`：稳定可用基线，后续只做必要修复，不做大突破。
- `2.1.0.0`：基于 `2.0.0.3` 复制出的新突破起点。

## 数据隔离

`2.1.0.0` 使用新的 localStorage 主键：

- `daily-checkin-v21`

这样做是为了避免 2.1 后续实验污染 `2.0.0.3` 的本地数据。GitHub Pages 的不同仓库路径同属 `mindspire56.github.io` 这个浏览器源，如果继续使用同一个 localStorage key，就会互相影响。

## 发布要求

每次修改仍然必须遵守：

- 更新版本号。
- 保存 `versions/<version>/index.html` 快照。
- 更新 `VERSIONS.md`。
- 上传 GitHub。
- 验证线上页面真实版本。
- 最后给用户可点击链接。
