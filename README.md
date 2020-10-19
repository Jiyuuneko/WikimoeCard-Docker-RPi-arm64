# Docker for 维基萌抽卡系统Node.js版 on Raspberry Pi 

Docker by Jiyuuneko [自由ネコ](https://www.jiyuuneko.com)

源码 by 广树 [维基萌](https://www.wikimoe.com)

Docker版本GitHub项目地址：[Github](https://github.com/Jiyuuneko/WikimoeCard-Docker-RPi-arm64)

源码GitHub项目地址：[Github](https://github.com/eeg1412/wikimoeCardByNodeJS)

通过Docker进行维基萌抽卡系统安装。

使用NodeJs(搭配express-generator+mongoose)+MongoDB+Vue(搭配Vue-cli+Element-ui)

### 介绍

一款由玩家自由DIY卡牌的卡牌收集游戏。

🐳 WikimoeCard Docker image. 


### 使用方法

#### 1. 下载主程序

在[releases](https://github.com/eeg1412/wikimoeCardByNodeJS/releases)下载最新版。

#### 2. 下载Docker配置文件。

下载或克隆本仓库，并将主程序解压的`server`文件夹移入`card`文件夹。
 
#### 3. 配置服务器

编辑`server/config/default.js`文件，确认并自定义修改【是否开启https】、【站点域名】、【私钥文件路径】、【证书文件路径】、【mongoDB地址】。

mongoDB地址请修改成:```mongodb://mongodb:27017/wikimoecard```

网页端口/https端口无需修改，请直接修改映射宿主机端口。剩下的配置会在网页安装时设定。

```javascript
let baseConfig = {
	port: 3000,//网页端口
	https:false,//是否开启https,
	sslPort:667,//https端口
	site:'https://127.0.0.1:667',//站点域名
	keyFileSrc:'./bin/nodejs.wikimoe.com-key.pem',//私钥文件路径
	certFileSrc:'./bin/nodejs.wikimoe.com-chain.pem',//证书文件路径
	url: 'mongodb://mongodb:27017/wikimoecard',//mongoDB地址
	sessionSecret:'wikimoe',//session加密字符串
	JWTSecret:'wikimoe',//JWT加密字符串
	dailyChance:5,//每日抽卡次数
	smtpHost: '',//邮件发送host
	smtpPort: 465,//邮件发送端口
	smtpAuth: {
		user: '',//用户名
		pass: ''//密码
	},
	robotCheckStar:25,//机器人验证通过后送的星星
	robotCheckCanGetStar:25,//机器人可疑度低于这个值送星星
	deminingStarRatio:1,//挖矿获得星星的倍率
	deminingItemRatio:1,//挖矿获得宝石的倍率
	creatCardStar:100,//制卡审核通过后获得的星星
	creatCardWait:20,//单用户最多等待审核的制卡
	useMarketCardCount:30,//集齐多少种卡牌后能在市场交易
	battleRankGetItem:100,//竞技第一名额外获得结缘币的数量
	battleRankGetItemDecay:10,//后面陆续获得结缘币的衰减数量
	donateImgUrl:'',//捐赠图片URL地址
	creatCardExplainUrl:'',//制卡说明图片URL地址
	QQunURL:'',//加群链接
	courseURL:'',//教程链接
	browserTitle:'维基萌抽卡',//浏览器标签标题
	siteTitle:'维基萌抽卡',//网站标题
}
```

#### 4. 编译Docker

进入`card`文件夹，运行命令：

```docker build -t wikimoecard:latest .```

#### 5. 启动WikimoeCard服务器

进入`compose`文件夹

```
docker-compose up -d
```

mongoDB将使用`data`目录来存储WikimoeCard数据。


#### 6. 检查是否正常运行

 检查日志以查看服务器正在侦听连接：

```
docker logs wikimoecard
```

显示如下信息时启动成功:


```
[nodemon] 2.0.4
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): bin/**/*
[nodemon] watching extensions: pem,key
[nodemon] starting `node ./bin/www`
连接数据库成功
排行榜过旧，系统将自动生成！
更新排行榜中...
目前不存在猜卡数据，系统将自动生成！
生成猜卡数据中...
删除旧的用户猜卡数据!
未设置猜卡卡包！
更新排行榜完毕...
矿场开启！
```

你的WikimoeCard Docker服务器现在成功在ARM服务器上开始运行!

#### 7. 配置网站

在 `yourdomain.com:xxx/cardinstall` 安装网站。

在 `yourdomain.com:xxx/cardadmin` 进入管理员中心。

#### 在X86环境下安装

默认安装配置适用于ARM环境，X86请更换mongoDB和Node镜像。

### 环境变量

尚未配置，请直接修改设置文件或把配置文件挂载宿主机。

### 特色系统

#### 日常抽卡
![](https://github.com/eeg1412/wikimoeCardByNodeJS/wiki/images/home/2.gif)

#### 玩家DIY自制卡牌

![](https://github.com/eeg1412/wikimoeCardByNodeJS/wiki/images/home/1.gif)

#### 排位对战

![](https://github.com/eeg1412/wikimoeCardByNodeJS/wiki/images/home/3.gif)

#### 商店抽卡

![](https://github.com/eeg1412/wikimoeCardByNodeJS/wiki/images/home/4.gif)

#### 矿场挖矿

![](https://github.com/eeg1412/wikimoeCardByNodeJS/wiki/images/home/5.gif)

### 所有系统

- [x] 日常抽卡
- [x] 每日签到
- [x] 矿场挖矿
- [x] 组建卡牌
- [x] 排位对战
- [x] 卡牌升级
- [x] 等级转换
- [x] 商店抽卡
- [x] 整点猜卡
- [x] 任务系统
- [x] 卡牌自由交易市场
- [x] 卡牌分解
- [x] 卡牌图鉴鉴赏
- [x] 玩家DIY自制卡牌
- [x] Live2D游戏向导

### License
The MIT License (MIT) Copyright (c) 2020 Jiyuuneko
