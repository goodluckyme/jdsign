# 声明
```text
请熟知本程序版权并非 https://t.me/InteTU 所有
本程序仅限学习测试使用,请在使用过程中遵循所在国家法律
因使用程序造成的一切损失皆有使用者承担所有责任
本版本最终由 https://t.me/InteTU 组织编译而来的高并发GoLang版本
本版本早期模板由 https://t.me/xiaohuochechat 创建者提供py版本为主要模板
后群内群友转发 https://t.me/KingRan521/5444 jdsign.py的11.2.8 的文件二次改动而成
如果作者需要删除去 https://t.me/InteTU 频道留言让删除
```
多架构构建有问题自己构建自己的吧
下面文件 转文件目录执行 README.md是说明文档
生成容器和镜像
```shell
docker kill jdsign
docker rm -f jdsign
docker rmi -f jdsign:latest
```
构建镜像
```shell
docker build -t jdsign:latest .
```
创建容器命令
```shell
DOCKER_BUILDKIT=1
docker run -dit \
  -p 17840:17840 \
  -e TZ=Asia/Shanghai \
  --name jdsign \
  --restart unless-stopped \
  xgzk/jdsign:latest
```
支持  application/json 和 application/x-www-form-urlencoded 两种传递参数方式
[教程地址](https://hub.docker.com/repository/docker/xgzk/jdsign/general)
具体看docker日志
## sign 相关调用
接口
```text
http://ip:端口/sign
```
传参方式
- application/json
```json
{
  "fn": "",
  "functionId": "",
  "body": {}
}
```
```text
fn 和 functionId 二选一 body必须
```
- application/x-www-form-urlencoded
```text
functionId = "" &
body = {}
```
测试案例
```http request
POST http://ip:端口/sign
Content-Type: application/json

{
  "fn": "isvObfuscator",
  "body": {"id": "", "url": "https://lzkj-isv.isvjcloud.com"}
}
```
```http request
POST http://ip:端口/sign
Content-Type: application/json

{
  "functionId": "isvObfuscator",
  "body": {"id": "", "url": "https://lzkj-isv.isvjcloud.com"}
}
```
```http request
POST http://ip:端口/sign
Content-Type: application/x-www-form-urlencoded

fn = "isvObfuscator" &
body = {"id": "", "url": "https://lzkj-isv.isvjcloud.com"}
```

## h5st相关调用
#### 非缓存机制
```http request
POST http://127.0.0.1:17840/h5st
Content-Type: application/json

{
  "appId": "d709c",
  "appid": "feother",
  "ua": "jdapp;android;12.3.5;;;M/5.0;appBuild/99073;ef/1;ep/%7B%22hdid%22%3A%22JM9F1ywUPwflvMIpYPok0tt5k9kW4ArJEU3lfLhxBqw%3D%22%2C%22ts%22%3A1706640218658%2C%22ridx%22%3A-1%2C%22cipher%22%3A%7B%22sv%22%3A%22CJC%3D%22%2C%22ad%22%3A%22EJPtYzU0YJq2DwG2YtGnEG%3D%3D%22%2C%22od%22%3A%22CtHuCQG3CWHvYtDuZtdsDWUmCNS4ENG1ZwCnZWZuDWHvCJu4EJcyCzc4ZtDuCWYzDtG3YwCzDtG4C2HvCWPtDK%3D%3D%22%2C%22ov%22%3A%22CzC%3D%22%2C%22ud%22%3A%22EJPtYzU0YJq2DwG2YtGnEG%3D%3D%22%7D%2C%22ciphertype%22%3A5%2C%22version%22%3A%221.2.0%22%2C%22appname%22%3A%22com.jingdong.app.mall%22%7D;jdSupportDarkMode/0;Mozilla/5.0 (Linux; Android 13; V2118A Build/TP1A.220624.014; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/89.0.4389.72 MQQBrowser/6.2 TBS/046247 Mobile Safari/537.36",
  "version": "4.2",
  "functionId": "huafei_coupon_status",
  "body": {"paramData":{"actKey":"f78Ox-aoqTs=","channel":"116","traceId":"app.app-index.BmainPopup.Rechargepop","hunterParam":{"originId":"","inviterId":""},"type":"2","displayType":1}},
  "pin": "jd_cxyHxRVVZoUl",
  "clientVersion": "12.0.0",
  "client": "wh5"
}
```
#### 缓存机制
```http request
POST http://127.0.0.1:17840/h5st
Content-Type: application/json

{
  "appId": "d709c",
  "appid": "feother",
  "ua": "jdapp;android;12.3.5;;;M/5.0;appBuild/99073;ef/1;ep/%7B%22hdid%22%3A%22JM9F1ywUPwflvMIpYPok0tt5k9kW4ArJEU3lfLhxBqw%3D%22%2C%22ts%22%3A1706640218658%2C%22ridx%22%3A-1%2C%22cipher%22%3A%7B%22sv%22%3A%22CJC%3D%22%2C%22ad%22%3A%22EJPtYzU0YJq2DwG2YtGnEG%3D%3D%22%2C%22od%22%3A%22CtHuCQG3CWHvYtDuZtdsDWUmCNS4ENG1ZwCnZWZuDWHvCJu4EJcyCzc4ZtDuCWYzDtG3YwCzDtG4C2HvCWPtDK%3D%3D%22%2C%22ov%22%3A%22CzC%3D%22%2C%22ud%22%3A%22EJPtYzU0YJq2DwG2YtGnEG%3D%3D%22%7D%2C%22ciphertype%22%3A5%2C%22version%22%3A%221.2.0%22%2C%22appname%22%3A%22com.jingdong.app.mall%22%7D;jdSupportDarkMode/0;Mozilla/5.0 (Linux; Android 13; V2118A Build/TP1A.220624.014; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/89.0.4389.72 MQQBrowser/6.2 TBS/046247 Mobile Safari/537.36",
  "version": "4.4",
  "functionId": "huafei_coupon_status",
  "body": {"paramData":{"actKey":"f78Ox-aoqTs=","channel":"116","traceId":"app.app-index.BmainPopup.Rechargepop","hunterParam":{"originId":"","inviterId":""},"type":"2","displayType":1}},
  "pin": "jd_cxyHxRVVZoUl",
  "clientVersion": "12.0.0",
  "client": "wh5",
  "IsNormal": "function test(tk,fp,ts,ai,algo){var rd='qt6G7mJboyk6';var str=\"\".concat(tk).concat(fp).concat(ts).concat(ai).concat(rd);return algo.MD5(str);}",
  "Token": "tk03wac261c9b18nuy1UxQ2QDpKUBC_m8lwOp39j8wEenViF0egFG9IG-pJhltvVJ-oZm2YlwJlM5lwxF9nlrQ7uPfx8",
  "Fingerprint": "waawaipg9twt3mp5"
}
```
## 口令解析
```http request
POST http://127.0.0.1:17840/jComExchange
Content-Type: application/json

{
  "code": "17:/雅诗兰黛邀新开卡赢正装好礼￥X0q4Q35NxJ￥，⇛⤴️ī🆖◕岽"
}
```
## 版本日期
 - 2023/11/27 02:00
   - 对gin日志进行覆盖处理
 - 2024/03/09 17:00
   - 支持 h5st 4.1 4.2 4.3 4.4
   - 支持口令解析