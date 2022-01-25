# 枝网查重系统 API 文档(version 1.0)

这里是枝网查重系统的 API 文档，API 地址为 `https://api.asoulcnki.asia/`

## 目录

### 枝网查重/枝江作文展

- [查重](#枝网查重-查重)
- [作文展](#枝网查重-枝江作文展)

### 枝网 OAuth

- [接入说明](#枝网-oauth-接入说明)
- [获取用户信息](#枝网-oauth-获取信息)

### 惯例

1. 返回的 code 不为 0 时即为错误情况。
2. 非特殊说明，请求参数均为必选项，可选的参数会在解释中单独标注

## 枝网查重-查重

请求类型：POST

请求地址：/main/v1/check

Content-Type: application/json

### 请求参数

| 参数名称 | 释义     | 备注                |
| -------- | -------- | ------------------- |
| text     | 查重文本 | 长度在 10-1000 之间 |

### 响应参数

注：由于 related 中的 reply 进行复用，所以单独解释

| 参数名称   | 释义                             | 备注                                  |
| ---------- | -------------------------------- | ------------------------------------- |
| rate       | 查重小作文的重复率               | 范围 0-1，1 为 100%                   |
| message    | 查询状态的相关信息，默认 success | ​<br />                               |
| code       | 查询状态码                       | 0 以外的值为查询失败                  |
| start_time | 查询范围的起始时间               | 10 位时间戳(秒)                       |
| end_time   | 查询范围的结束时间               | 10 位时间戳(秒)，最后小作文收录的时间 |
| related    | 重复文本的数组                   | 该部分和其他接口复用，下文单独解释    |

#### related 部分

| 参数名称               | 释义                          | 备注                                                          |
| ---------------------- | ----------------------------- | ------------------------------------------------------------- |
| rate                   | 原文从本评论中复制的占比      | 仅查重 API 使用 <br />范围 0-1，1 为 100%                     |
| reply_url              | 指向该条评论的链接            | 该链接可以根据 typeid 和 oid 自行构造                         |
| reply.rpid             | 该评论的回复 ID               | 0 以外的值为查询失败                                          |
| reply.type_id          | 评论的类型 ID                 | 1：视频 <br />12：专栏 <br />11/17：动态                      |
| reply.uid              | 动态/视频/专栏 发布者的 UID   |                                                               |
| reply.oid              | 动态/视频/专栏 对应的 ID      | 对于视频是 AV 号<br />对于动态是动态 ID<br />对于专栏是 CV 号 |
| reply.ctime            | 评论的创建时间                | 10 位时间戳(秒)                                               |
| reply.mid              | 评论发布者的 UID              |                                                               |
| reply.m_name           | 评论发布者的用户名            |                                                               |
| reply.content          | 评论正文                      |                                                               |
| reply.like_num         | 评论获得的点赞数              |                                                               |
| reply.origin_rpid      | 该评论引用的评论的 rpid       | 如果是原创，该项为 -1                                         |
| reply.similar_count    | 与该评论相似的评论数          |                                                               |
| reply.similar_like_sum | 该评论赞数 + 所有相似评论赞数 | 如果该评论非原创，则不会累加                                  |

### 样例

请求样例

```http
POST /main/v1/check HTTP/1.1
Content-Type: application/json

{"text":"字符串长度需要在10-1000之间"}
```

响应样例

```json
{
  "code": 0,
  "message": "success",
  "data": {
    "rate": 1,
    "start_time": 1606137506,
    "end_time": 1628654399,
    "related": [
      {
        "rate": 1,
        "reply": {
          "rpid": "5004265317",
          "type_id": 17,
          "dynamic_id": "552086903093256371",
          "mid": 5421504,
          "uid": 672328094,
          "oid": "552086903093256371",
          "ctime": 1627381220,
          "m_name": "恰柠檬儿丶",
          "content": "11111111111 0 \n1111111111111 0 111 0\n1111111111111111111",
          "like_num": 166,
          "origin_rpid": "-1",
          "similar_count": 0,
          "similar_like_sum": 166
        },
        "reply_url": " https://t.bilibili.com/552086903093256371/#reply5004265317"
      }
    ]
  }
}
```

## 枝网查重-枝江作文展

请求类型：GET

请求地址：/main/v1/ranking

### 请求参数

| 参数名称      | 释义                     | 备注                                                                                                                    |
| ------------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| pageSize      | 每页展示的评论数         | 目前仅支持 pageSize=10                                                                                                  |
| pageNum       | 评论页码                 | 从 1 开始                                                                                                               |
| timeRangeMode | 时间范围选择             | 0 全部时间<br />1 一周内<br />2 三天以内                                                                                |
| sortMode      | 排序模式                 | 0 总点赞数（参见 related.reply.similar_like_num）<br />1 点赞数<br />2 相似小作文数（引用次数）                         |
| ids           | 指定动态发布者（非评论） | 可选参数，默认为全部<br />传值为 uid 数组 例：ids=uid1,uid2.....                                                        |
| keywords      | 指定关键词               | 可选参数，默认无限制条件<br />传值为关键词数组 例 keywords=k1,k2,...<br />每个关键词不超过 10 个字符 最多支持三个关键词 |

### 响应参数

| 参数名称        | 释义           | 备注            |
| --------------- | -------------- | --------------- |
| code            | 见查重 API     |                 |
| message         | 见查重 API     |                 |
| data.all_count  | 查到评论的总数 | 用于计算页数    |
| data.replies    | 见查重 API     |                 |
| data.start_time | 评论起始时间   | 10 位时间戳(秒) |
| data.end_time   | 评论结束时间   | 10 位时间戳(秒) |

### 样例

请求样例

```http
GET /main/v1/ranking/?pageSize=5&pageNum=1&timeRangeMode=0&sortMode=0 HTTP/1.1
```

响应样例

```json
{
  "code": 0,
  "message": "success",
  "data": {
    "replies": [
      {
        "rpid": "5004265317",
        "type_id": 17,
        "dynamic_id": "552086903093256371",
        "mid": 5421504,
        "uid": 672328094,
        "oid": "552086903093256371",
        "ctime": 1627381220,
        "m_name": "恰柠檬儿丶",
        "content": "11111111111 0 \n1111111111111 0 111 0\n1111111111111111111",
        "like_num": 166,
        "origin_rpid": "-1",
        "similar_count": 0,
        "similar_like_sum": 166
      }
    ],
    "all_count": 5379,
    "start_time": 1606137506,
    "end_time": 1628654399
  }
}
```

## 枝网 OAuth-接入说明

这里是枝网 OAuth 的使用文档，供开发者查阅

### 使用说明

#### 验证流程

1. 第三方网站携带重定向地址作为参数访问 `https://oauth.asoulcnki.asia/`
2. 用户在枝网 OAuth 完成登陆，并点击授权按钮
3. 在用户授权后，会跳转到第三方网站提供的网址，并在 URL 的 hash 部分携带 token
4. 第三方网站获取 URL 中的 token，携带 token 访问 `/oauth/v1/verify` 以获取用户信息

#### 备注

1. 目前 token 失效时间为 1 小时，如果 token 失效，请引导用户获取新的 token
2. 使用 URI hash 传值是因为 hash 不会随请求发送到服务器，更能保证用户安全

### 样例

假如现有第三方网站 `https://www.example.com`, 并使用 `https://www.example.com/redirect` 来处理返回的 token

流程

1. 该网站重定向到 `https://oauth.asoulcnki.asia/?redirect_uri=https://www.example.com/redirect`
2. 用户完成授权，OAuth 页跳转至 `https://www.example.com/redirect#token=b026324c6904b2a9cb4b88d6d61c81d1`
3. 第三方网站处理并获取 token 内容，例如这里的 token 为 `b026324c6904b2a9cb4b88d6d61c81d1`
4. 使用获取的 token 来获取信息

## 枝网 OAuth-获取信息

目前仅支持获取用户 UID，后续可能会增加用户名等信息

```http
GET /oauth/v1/verify/

Authorization: <获取到的token>
```

### 返回值

| 名称    | 解释                |
| ------- | ------------------- |
| code    | 为 0 时，验证成功   |
| message | 报错信息，默认为 ok |
| uid     | 和对应用户的 uid    |

```json
{
  "uid": 114514,
  "code": 0,
  "message": "ok"
}
```
