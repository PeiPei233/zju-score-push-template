# zju-score-push-template
你的成绩更新钉钉通知推送助手😋

使用了 [https://github.com/PeiPei233/ZJUScoreAssistant](https://github.com/PeiPei233/ZJUScoreAssistant)

## 使用帮助

首先使用本模板项目创建自己的 repo（点Use this template -> Create a new repository），为了您的信息安全，请将自己的 repo 设置为私有仓库（在 Settings -> General -> Danger Zone 中 change repository visibility）。

添加钉钉机器人（可选）：在钉钉的新手体验群中选择设置，添加机器人，自定义。在安全设置中选择自定义关键词，并输入自定义关键词为 `成绩` ，勾选同意协议后点击完成，复制显示的 Webhook 作为接下来要用的钉钉机器人 Webhook。

然后在自己 repo 的 Settings -> Secrets and variables -> Actions 选择右侧 New repository secret，添加以下 Secrets:

- `USERNAME`：你的浙大统一认证用户名
- `PASSWORD`：你的浙大统一认证密码
- `WEBHOOK`：你的钉钉机器人Webhook地址（可选）

请注意，是分别填写三条 Secrets，每条 Secret 的 Name 是冒号前的全大写单词，Value 应填写冒号后所提示的内容，且不要有多余的空格和回车。

不出意外，完成以上操作后，每隔五分钟会刷新一次，并推送更新的成绩。你也可以在 Actions -> Auto Push Updated Score Info 中手动运行或 Disable/Enable workflow。

如果想修改间隔时间，可以修改 `.github/workflows/update_push.yml` 中的 `schedule` 字段，将其中 `- cron: '*/5 * * * *'` 中的数字 5 改为你想要的数字（分钟数）即可。

由于 GitHub 限制，最终间隔时间不一定是设定的间隔时间，导致推送有延迟，有能力建议将推送服务挂在自己的服务器上。

由于钉钉限制了机器人的推送频率，因此在第一次刷新时可能会出现只推送了部分成绩的情况，不影响后续使用。

已知存在的 bug：二级制（如水测等）成绩也会计入均绩中，重修、弃修错误计算均绩等，导致均绩计算不准确。