# web-short-video

介绍

## Getting Started

介绍

### 部署

开发

```
-Dconf.env=Test -Dconf.key=web-short-video  -Dapp.name=web-short-video -Dlocal.ip=192.168.10.131 -Dproject.path=xxx
```

office 打包

```
mvn clean package -Dlz.env=office
```

## http接口文档
### 统一返回json格式
> 
 {"rCode":0,"message":"成功","data":...}
```
rCode:0成功
rCode:1失败
message:返回信息
data:返回数据
```

### 1.获取小视频
**接口：shortvideo/list**
**参数：**
name|type|必填| desc
-------- | ---
index|string |是| 小视频开始位置（0开始）
count|string |是| 拉取数量
firstRecordId |string|否| 小视频id，分享连接会带
token|string |是| 用户token

**返回：**
name|type| desc
-------- | ---
id|long| 小视频id, 
authId|long| 作者id,
authNickName|string|作者名
authPortraitImgUrl|string| 作者头像
authLastUpdateTime|long|小视频最后更新时间戳
publishTime|long|小视频发布时间戳
likeCount|int |小视频点赞数
videoUrl|string|小视频链接
thumbImgUrl|string|小视频封面链接
videoDuration|int |废弃
state|int |小视频状态 -1未发布，0已发布，1审核未通过，2审核通过
alreadyLike|boolean|用户是否赞过改视频
alreadyFocus|boolean|用户是否关注作者 
shareLink|string|小视频分享链接
shareTitle|string|小视频分享标题
shareContent|string|小视频分享内容


**示例：从index=2（含）开始拿4条** 
shortvideo/list?index=2&count=4&firstRecordId=10004&token=0e83f54b14f95e62946c0288655eafde
```
{
    "rCode": 0, 
    "message": "成功。", 
    "data": [
        {
            "id": 10004, 
            "authId": 2608368780316892700, 
            "authNickName": "L什么鬼", 
            "authPortraitImgUrl": "http://cdnoffice.lizhi.fm/user/2016/12/02/2571490256224331266.png", 
            "authLastUpdateTime": 1514365340000, 
            "publishTime": 1514451743000, 
            "likeCount": 0, 
            "videoUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643675458010481737.mp4", 
            "thumbImgUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643660595276153417.gif", 
            "videoDuration": 0, 
            "state": 2, 
            "alreadyLike": false, 
            "alreadyFocus": false, 
            "shareLink": "localhost?id=10004", 
            "shareTitle": "分享了一个小视频", 
            "shareContent": "分享内容文字，点我点我"
        }, 
        {
            "id": 10002, 
            "authId": 2118027, 
            "authNickName": "lzxtest06@126.com", 
            "authPortraitImgUrl": "http://cdnoffice.lizhi.fm/user/avatar_132.jpg", 
            "authLastUpdateTime": 1514367676847, 
            "publishTime": 1514340628000, 
            "likeCount": 99, 
            "videoUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643675458010481737.mp4", 
            "thumbImgUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643660595276153417.gif", 
            "videoDuration": 0, 
            "state": 0, 
            "alreadyLike": false, 
            "alreadyFocus": false, 
            "shareLink": "localhost?id=10002", 
            "shareTitle": "分享了一个小视频", 
            "shareContent": "分享内容文字，点我点我"
        }, 
        {
            "id": 10000, 
            "authId": 2117587, 
            "authNickName": "若chen尘（跑骚FM）", 
            "authPortraitImgUrl": "http://cdnoffice.lizhi.fm/user/2015/12/29/2508549524816023042.png", 
            "authLastUpdateTime": 1514284439000, 
            "publishTime": 1514284442000, 
            "likeCount": 100, 
            "videoUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643675458010481737.mp4", 
            "thumbImgUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643660595276153417.gif", 
            "videoDuration": 0, 
            "state": 2, 
            "alreadyLike": false, 
            "alreadyFocus": true, 
            "shareLink": "localhost?id=10000", 
            "shareTitle": "分享了一个小视频", 
            "shareContent": "分享内容文字，点我点我"
        }, 
        {
            "id": 10003, 
            "authId": 2591879449599295000, 
            "authNickName": "建辉1", 
            "authPortraitImgUrl": "http://cdnoffice.lizhi.fm/user/2017/11/13/2635670729892438530.jpg", 
            "authLastUpdateTime": 1514367611048, 
            "publishTime": 1514365251000, 
            "likeCount": 102, 
            "videoUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643675458010481737.mp4", 
            "thumbImgUrl": "http://cdnoffice.lizhi.fm/shortvideo/2017/12/26/2643660595276153417.gif", 
            "videoDuration": 0, 
            "state": 2, 
            "alreadyLike": false, 
            "alreadyFocus": true, 
            "shareLink": "localhost?id=10003", 
            "shareTitle": "分享了一个小视频", 
            "shareContent": "分享内容文字，点我点我"
        }
    ]
}
```



### 2.小视频点赞接口
**接口：shortvideo/like**

**参数：**
name|type|必填| desc
-------- | ---
token|string |是| 用户token
id|string |是| 小视频id

**返回：**
name|type| desc
-------- | ---
data|int| 点赞数


**示例：**
```
 请求：shortvideo/like?token=05aeaad7f66a6687e97400c3f22832fb&id=10001
 返回：{"rCode":0,"message":"成功。","data":2}
```







