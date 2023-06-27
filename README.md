# zju-score-push-sample
你的成绩更新钉钉通知推送助手😋

使用了 [https://github.com/PeiPei233/ZJUScoreAssistant](https://github.com/PeiPei233/ZJUScoreAssistant)

## 使用帮助

首先 Fork 本项目，为了您的信息安全，请将自己的 Fork 设置为私有仓库（在 Settings -> General -> Danger Zone 中 change repository visibility）。

之后，在 GitHub 上创建一个新的 Personal Access Token。前往设置页 -> Developer settings -> Personal access tokens -> Tokens (classic)，选择右侧 Generate new token -> Generate new token (classic)。填写相关信息时，务必选择 `repo` 和 `workflow` 权限，然后点击最下方的 Generate token 按钮。生成的 Token 会显示在页面上，复制下来作为接下来要用的 GitHub Token。

添加钉钉机器人（可选）：在钉钉的新手体验群中选择设置，添加机器人，自定义。在安全设置中选择自定义关键词，并输入自定义关键词为 `成绩` ，勾选同意协议后点击完成，复制显示的 Webhook 作为接下来要用的钉钉机器人 Webhook。

然后在自己 Fork 仓库的 Settings -> Secrets and variables -> Actions 选择右侧 New repository secret，添加以下 Secrets:

- `USERNAME`：你的浙大统一认证用户名
- `PASSWORD`：你的浙大统一认证密码
- `WEBHOOK`：你的钉钉机器人Webhook地址（可选）
- `GH_TOKEN`：你的GitHub Token

不出意外，完成以上操作后，每隔五分钟会刷新一次，并推送更新的成绩。你也可以在 Actions -> Auto Push Updated Score Info 中手动运行或 Disable/Enable workflow。

如果想修改间隔时间，可以修改 `.github/workflows/update_push.yml` 中的 `schedule` 字段，将其中 `- cron: '*/5 * * * *'` 中的数字 5 改为你想要的数字（分钟数）即可。

已知存在的 bug：二级制（如水测等）成绩也会计入均绩中，重修后重复计算均绩等，导致均绩计算不准确。