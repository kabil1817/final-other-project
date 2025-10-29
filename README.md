![](https://img.shields.io/badge/train_ticket-reaper-lightgrey.svg?colorA=d9d0c7&colorB=9fe0f6)

### 本项目已关闭

> 由于对应站点限制相同ip的访问频率,导致不能快速的进行车票查询.
>
> 如需使用本项目进行抢票,可自行集成代理ip池即可 (但这样比较麻烦,建议直接使用第三方抢票app)
>
> 如之后有较好的解决方案,将重新开启更新





### 吐槽

---
>在正式开始文档前，一定要深深的吐槽一波！！！
>想当年，我也是一个天真的抢票族，常年用去哪儿网的抢票。
>平常抢个票感觉还不错，但一到节假日！他就开始！掉！链！子！！！
>前端页面写着，95%成功率抢票成功，我天真的选了好几个班次。结果发现！我被前端的95%骗了！（虽然我也知道那就是随便写上去的数字）
>然后我的心情就*&……@*&#！*@……（）(*@&$(*）！（@&%（）&*！（￥——*
>实在没办法，只能自己手动撸一段抢票代码，哎 （手动滑稽）

>吐槽归吐槽，去哪儿网毕竟是免费给大家用的，也不可能太快嘛~ 你懂的~ 所以还是要谢谢去哪儿网那些年帮我抢过的票票~

---

### Q&A
- Q：这个项目是抢<kbd>www.12306.cn</kbd>(中国铁路客户服务中心)的票吗？
- A：不是。这个是抢<kbd>12306.com</kbd>(点点出行)的票。

- Q：为什么要抢点点出行的票，而不是中国铁路客户服务中心？
- A：<kbd>www.12306.cn</kbd>(中国铁路客户服务中心)里面抛开登陆验证不说，之后的各种数据获取足以让人头痛。要做成纯HTTP请求难度非常大，所以目前大部分都是以Selenium或Chrome脚本的形式在<kbd>www.12306.cn</kbd>进行抢票。

- Q：<kbd>12306.com</kbd>(点点出行)是个什么网站，会不会有风险？
- A：这个网站其实就和携程、去哪儿网一样是第三方票务代售，他也是在国内备案过的。而使用<kbd>12306.com</kbd>估计他只是想从<kbd>www.12306.cn</kbd>偷偷的获取一部分流量。

- Q：在这里抢票是否会产生除了票价外其它费用？
- A：不会，价格和<kbd>www.12306.cn</kbd>一样的。

## 项目介绍
![](https://img.shields.io/badge/build-passing-brightgreen.svg) ![](https://img.shields.io/badge/downloads-190KB-brightgreen.svg) ![](https://img.shields.io/badge/jdk-1.8-blue.svg) ![](https://img.shields.io/badge/springboot-2.0.1-blue.svg)   ![](https://img.shields.io/badge/maven-3.3.9-blue.svg)  ![](https://img.shields.io/badge/IDEA-2017.2.3-blue.svg)
- `train-ticket-reaper` 的目标是以简单的使用方法、和高效的抢票让小伙伴们安心的抢到回家的票
- 抢票的原理是模拟http请求调用<kbd>12306.com</kbd>（非<kbd>www.12306.cn</kbd>）API进行查询、下单、确认等（没有付款步奏，保证小伙伴钱包的安全，抢到后自行登陆<kbd>http://12306.com/</kbd>付款即可）。
- 没有复杂的环境配置和依赖，只需要把该填的参数填上，run一下就可以一直放着等他抢到票为止
- 提供4种不同的抢票模式（极速模式、丧心病狂模式、为了抢票不要命模式、无脑下单模式），后两种非万不得已，不建议使用

## 快速启动 （2种启动方式，选一种即可）

1. IDE启动
- 导入项目并在配置文件中填入信息

![](https://i.imgur.com/oWayV9W.png)
- 启动项目

![](https://i.imgur.com/qQqTDSd.png)
- 佛性的等待，并在抢票成功后，登陆<kbd>http://12306.com/</kbd>进行付款

---

2. jar包启动
- 进入源代码根目录
- 使用maven进行打包
```
mvn clean package -DskipTests
```
- 运行命令
```
java -jar train-ticket-reaper --from-station=*** --to-station=*** --just-gd=true=*** --dept-date=*** --seat-name=*** --account=*** --password=*** --passenger-name=*** --passport-no=*** --sex=* --contact-mobile=*** --contact-name=*** --timeRange=*** --webhook-token=*** --mode=*
```
- 参数说明
```
######### [车次信息] #########
#出发站 如 深圳
from-station =
#目的站 如 上海
to-station =
#是否只看高铁/动车 (非必填，默认值 true)
just-gd =
#车次日期 如 2018-04-09
dept-date =
#时间范围 （火车发车时间范围限制，不填默认不限制） 如：10:30-14:50 注意冒号使用英文的:
timeRange =
#座位名称 如：二等座，一等座，无座
seat-name =

######### [登陆信息] #########
#登陆用户名
account =
#登陆用户密码
password =

######### [乘客信息] #########
#乘客姓名
passenger-name =
#乘客身份证号码
passport-no =
#乘客性别 男M 女F
sex=M

######### [联系人信息] #########
#联系人号码 如 13888888888
contact-mobile =
#联系人姓名 如 张三
contact-name =

######### [钉钉通知] ######### （非必填）
#钉钉自定义机器人的webhookToken，不使用钉钉机器人进行通知则不填 如 https://oapi.dingtalk.com/robot/send?access_token=4a637ce2b7ce6c0be48fc3388265345ee1cd4ea036ce705112ed618924f987aa
webhook-token =

######### [抢票模式] ######### （非必填，不填使用默认值）
#1 极速模式  2 丧心病狂模式  3 为了抢票不要命模式  (默认1) 4 无脑下单模式
mode =
```
- 佛性的等待，并在抢票成功后，登陆<kbd>http://12306.com/</kbd>进行付款


## 通知方式

1.钉钉自定义机器人（如果使用阿里巴巴的钉钉）
- 在application.properties中的webhook-token填上钉钉机器人的webhook（一串url）即可
- 不填写则默认不使用钉钉机器人进行通知
- 钉钉机器人开发文档 ：https://open-doc.dingtalk.com/docs/doc.htm?spm=a219a.7629140.0.0.mQpC3N&treeId=257&articleId=105735&docType=1

2.佛性通知
- 当抢票成功后，程序会自动退出（不用担心资源浪费等问题）。
- 当下单成功的15分钟后，<kbd>12306.com</kbd>会主动发信息到你填的 联系人号码 上（因为<kbd>12306.com</kbd>想催你给钱啊~）
- 所以不用担心抢票成功后又被超时取消

## 抢票模式
1.极速模式 
- 只需按照快速启动，即时极速模式。
- 默认每秒检测一次（从早上6点到24点）。
- 遇到有位置，占座时直接 while(true) 进行占座请求。普通浏览器5秒一次占座

2.丧心病狂模式
- mode设为2
- 每秒平均10次检测
- 占座也是 while(true)

3.为了抢票不要命模式
- mode设为3
- 在 丧心病狂 模式基础上使用100条线程运行
- 占座也是 while(true)

4.无脑下单模式
- mode设为4
- 不进行票数检测
- 对符合要求的车次直接进行下单请求



## Tips
	列车发车时间的前一天晚上，19:30-22:00，通常会比较多人退票。这时候抢票成功概率非常搞。
