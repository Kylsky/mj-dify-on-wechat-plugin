## 插件描述
基于[midjourney-proxy-on-wechat](https://github.com/mouxangithub/midjourney-proxy-on-wechat)二开，兼容 new-api

## 现有功能
- [x] midjourney `imgine` 想象
- [x] midjourney `upscale` 放大
- [x] midjourney `variation` 变幻
- [x] midjourney `describe` 识图，使用方式：（1）私聊窗口（非群聊模式）发图直接生成；（2）发送describe_prefix配置的指令，然后发送一张图片进行识别（此方法不限群聊还是私聊方式）
- [x] midjourney `blend` 混图，使用方式：发送blend_prefix配置的指令，然后发送多张图片进行混合（此方法不限群聊还是私聊方式）
- [x] midjourney 垫图，使用方式：发送pad_prefix配置的指令+prompt描述，然后发送一张图片进行生成（此方法不限群聊还是私聊方式）
- [x] 绘图进度百分比查询
- [x] 发送/queue 任务队列查询
- [x] 解决webp图片无法发送问题
- [x] mj_tip可关闭多条消息发送（最终只发图片或者描述）
- [x] 可自定义添加修改各种功能prefix前缀
- [x] 聊天窗口管理员指令可修改管理员密码，配置mj_url,mj_api_secret，暂停启用mj服务
- [x] 聊天窗口管理员指令可增删改查白名单群组和白名单用户，从而限制用户使用，减少损耗
- [x] 增加图片代理地址discordapp_proxy配置，解决图片本地国内无法发送的问题，可配置discordapp_proxy或配置chatgpt-on-wechat配置的proxy
- [x] 新增每日图片上限，限制普通用户每日作图数，管理员和白名单用户不受限（daily_limit）
- [x] 新增指令设置每日作图数数量和重置清空用户作图数

## MJ指令说明

### 通用指令
- [x] $mj_help 说明文档
- [x] $mj_admin_password 口令 进行管理员认证(如未配置，临时管理员密码为123456)
- [x] $mj_admin_cmd 查询管理员指令

### 管理员指令
- [x] $set_mj_admin_password 新口令 进行设置新密码（此方式会直接写入config.json方便重启直接使用）
- [x] $set_mj_url mj代理地址 mj_api_secret请求参数 discordapp代理地址 进行设置MJ服务器信息（此方式会直接写入config.json方便重启直接使用）
- [x] $stop_mj: 暂停MJ服务
- [x] $enable_mj: 启用MJ服务
- [x] $clean_mj: 清除MJ服务缓存
- [x] $g_prefix : 查询前缀
- [x] $s_prefix 前缀类名 前缀: 设置前缀
- [x] $r_prefix 前缀类名 前缀或序列号: 移除前缀
- [x] $set_mj_admin_password 口令: 修改管理员口令
- [x] $g_admin_list : 查询管理员列表
- [x] $s_admin_list 用户ID或昵称: 设置管理员列表
- [x] $r_admin_list 用户ID或昵称或序列号: 移除管理员列表
- [x] $c_admin_list : 清空管理员列表
- [x] $g_wgroup : 查询白名单群组
- [x] $s_wgroup 群组名称: 设置白名单群组
- [x] $r_wgroup 群组名称或序列号: 移除白名单群组
- [x] $c_wgroup : 清空白名单群组
- [x] $g_wuser : 查询白名单用户
- [x] $s_wuser 用户ID或昵称: 设置白名单用户
- [x] $r_wuser 用户ID或昵称或序列号: 移除白名单用户
- [x] $c_wuser : 清空白名单用户
- [x] $g_bgroup : 查询黑名单群组
- [x] $s_bgroup 群组名称: 设置黑名单群组
- [x] $r_bgroup 群组名称或序列号: 移除黑名单群组
- [x] $c_bgroup : 清空黑名单群组
- [x] $g_buser : 查询黑名单用户
- [x] $s_buser 用户ID或昵称: 设置黑名单用户
- [x] $r_buser 用户ID或昵称或序列号: 移除黑名单用户
- [x] $c_buser : 清空黑名单用户
- [x] $s_limit : 设置每日作图数限制

## 一些问题说明以及解决方案
·超时问题：首先在discord输入/info查看你的`Fast Time Remaining`快速出图时间，然后我了解到有些朋友的是某宝某鱼上租的共享账号，这类账号的特点问题就是人多使用，加上上面的快速出图时间可能用完了，造成了你提交的作图一直在排队中，针对这类问题的解决方案如下：首先将midjourney-proxy更新到最新版，然后在他的配置项里面有一个`mj.queue.timeout-minutes`配置，即为任务超时时间，默认是五分钟，由于你的是多人使用的账号，所以次数可以延长些，改到十分钟甚至更长，具体自己试试，如果是专业版的话还可以修改`mj.queue.core-size`和`mj.queue.queue-size`并发数和等待队列长度，具体参考[`MidJourney订阅级别`](https://docs.midjourney.com/docs/plans)


## 使用说明
在 config.json 中配置 new-api 地址 和 key

或者

配置 midjourney-proxy 地址 和 key

### 配置参数说明

```shell
{
    "mj_url": "", // midjourney-proxy的服务地址
    "mj_api_secret": "", // midjourney-proxy的api请求头，如果midjourney-proxy没配置此处可以不配
    "mj_tip": true, // 是否发送请求提示，让漫长的等待不会枯燥，如果嫌啰嗦可关闭，即：发送一些成功的内容
    "mj_admin_password": "", // MJ管理员密码
    "daily_limit": 3, // 普通用户每日作图数
    "discordapp_proxy": "", // cdn.discordapp.com反代地址
    "mj_groups": [], // 白名单群组，通过管理员指令添加
    "mj_users": [], // 白名单用户，通过管理员指令添加
    "mj_admin_users": [], // 认证后管理员用户，通过管理员认证
    "imagine_prefix": "[\"/i\", \"/mj\"]", // imagine画图触发前缀
    "fetch_prefix": "[\"/f\"]", // fetch任务查询触发前缀
    "up_prefix": "[\"/u\"]", // up图片放大和变换触发前缀
    "pad_prefix": "[\"/p\"]", // 垫图画图触发前缀
    "blend_prefix": "[\"/b\"]", // 混图画图触发前缀
    "describe_prefix": "[\"/d\"]", // 图生文触发前缀
    "queue_prefix": "[\"/q\"]",  // 查询正在执行中任务触发前缀
    "end_prefix": "[\"/e\"]",  // 结束存储打包发送任务（目前用于混图）触发前缀
    "reroll_prefix": "[\"/r\"]"  // 重新绘制触发前缀
}
```

配置文件优先级：先使用env环境变量 => 使用config.json/config.json.template配置 => 使用代码中gconf

最终都会在插件目录下重新生成一个config.json文件，方便以后重启进行读取，当然重启的时候env环境变量依然会优先读取写入


### 安装

在微信聊天窗口配置：
```shell
## 第一步：进入聊天窗口，先认证管理员，如果是临时密码，请重启 dify-on-wechat前往logs查看，上方日志中有临时密码
#auth＋密码
## 第二步：认证成功后进行安装
#installp https://github.com/Kylsky/mj-dify-on-wechat-plugin
## 第三步：#scanp扫描插件，提示发现MidJourney插件即为成功
#scanp
## 第四步：输入$mj_help有提示说明插件安装成功
## 第五步：输入$mj_admin_password 密码（未配置mj_admin_password则临时密码为123456，认证完后请尽快输入$set_mj_admin_password进行修改）
## 第六步：$set_mj_url mj代理地址 mj_api_secret请求参数 discordapp代理地址 进行设置MJ服务器信息
## 无需重启服务，即配即用
```
