# 2021.4.23 WPS更新了，邀请代码~~失效~~又能用了！！！···
#
## WPS 签到邀请
完成打卡得会员活动中的邀请任务，需要次日 6:00-13:00 手动打卡。推送消息中，添加了几个链接，方便手动打卡签到。无其他功能。
## 企业微信推送
通知推送使用的是企业微信，需要注册企业微信。
1. 使用电脑打开 [企业微信官网](https://work.weixin.qq.com/)，注册一个企业，资料按需如实填写即可。
2. 注册成功后，点【管理企业】进入管理界面，选择【应用管理】→ 【自建】 → 【创建应用】。
   应用的logo和名称随意，【可见范围】 选择你的企业。
3. 创建一个应用后，进入此应用的管理页面，可以看到应用的 **AgentId** 、 **Secret** ，复制并保存下来。
4. 在【我的企业】→【企业信息】中最下方可以看到 **企业ID** ，复制并保存下来。
5. 最后，点击【我的企业】→【微信插件】，扫描页面下方 二维码，关注企业。

## 创建仓库 secret 变量
1. fork 本仓库
2. 进入此仓库，`Settings` -> `Secrets` -> `New repository secret`，创建如下四个变量。
- ID_LIST: 需要做任务的 id，可以是多个，多个id需要用英文逗号隔开。（可在WPS个人中心看到）
- CORID：企业微信的 企业ID
- SECRET：应用密钥
- AGENTID：应用ID
![创建仓库秘密变量](create_secrets.png)

## 执行 Action
action设定为手动执行和定时执行，在 `Actions` -> `All Workflows` -> `wps_sign` 页面，有一个手动触发按钮 `Run workflow`, 点击可手动执行一次，除此之外，每天 6:06 会自动执行一次。
## 注意事项：
- github action 的定时执行并非准时运行，而是比你设定的时间要**晚约几十分钟至两小时**（推测是要排队）。
- yml配置文件中，定时设置的时间是UTC时间，如果要修改，要将北京时间减8小时，例如：修改为每天9:20执行，需要写 `- cron: "20 1 * * *"`
- 如果项目连续60天未有任何改动，action 会被终止，所以每隔一段时间要有变动，比如改一改 README.md 文件。

## 推送截图示例
![推送示例](notify_example.png)
...
