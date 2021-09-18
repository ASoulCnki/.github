# ASoulCnki 枝网

<div class="banner">
  <a href="#简介"><div>简介</div></a>
  <a href="#A-Soul简介"><div>A-Soul简介</div></a>
  <a href="#已有项目"><div>已有项目</div></a>
  <a href="#api"><div>API</div></a>
  <a href="#关于部署项目"><div>项目部署</div></a>
  <a href="#如何贡献"><div>如何贡献</div></a>
</div>

<style>
  .banner {
    display: grid;
    margin:0 20%;
    grid-template-columns: repeat(6, minmax(0, 1fr));
  }
  @media screen and (max-width: 1000px) and (min-width: 768px) {
    .banner {
      margin: 0 10%;
    }
  }
  @media screen and (max-width: 768px) {
    .banner {
      margin: 0;
      grid-template-columns: repeat(3, minmax(0, 1fr));
    }
  }
  .banner div {
    margin: 10px;
    text-align: center;
    color: rgb(8, 142, 231);
  }
</style>

## 简介

### 想法起源

#### NGA ASoul板块 

[想搞一个 ASoul 知网查重小作文](https://bbs.nga.cn/read.php?tid=27186618)<br><br>

#### 豆瓣相关讨论

[一个想法，发病小作文查重系统， 来征求一下豆油的意见](https://www.douban.com/group/topic/230466414/)<br><br>

[ASoul评论区发病小作文 枝网查重系统 需求讨论楼](https://www.douban.com/group/topic/230489644/?start=0)<br><br>

简单总结就是做一个A-Soul评论区的小作文数据库，并提供查重能力。

让广大au可以精准甄别评论是是原偷/原创，还是从之前的评论区复制粘贴改词偷来的😈

## A-Soul 简介

A-SOUL是乐华娱乐于2020年11月23日公开的其旗下首个虚拟偶像团体，由5名成员组成。

<div class="member">
  <div>
    <a href="https://space.bilibili.com/672346917">
      <img
        src="./assets/member_image/ava.jpg"
        style="border-color: #9ac8e2"
        alt="向晚大魔王"
      />
      <p style="color: #9ac8e2">向晚大魔王</p>
    </a>
  </div>
  <div>
    <a href="https://space.bilibili.com/672353429">
      <img
        src="./assets/member_image/bella.jpg"
        style="border-color: #db7d74"
        alt="贝拉Kira"
      />
      <p style="color: #db7d74">贝拉Kira</p>
    </a>
  </div>
  <div>
    <a href="https://space.bilibili.com/351609538">
      <img
        src="./assets/member_image/carol.jpg"
        style="border-color: #b8a6d9"
        alt="珈乐Carol"
      />
      <p style="color: #b8a6d9">珈乐Carol</p>
    </a>
  </div>
  <div>
    <a href="https://space.bilibili.com/672328094">
      <img
        src="./assets/member_image/diana.jpg"
        style="border-color: #e799b0"
        alt="嘉然今天吃什么"
      />
      <p style="color: #e799b0">嘉然今天吃什么</p>
    </a>
  </div>
  <div>
    <a href="https://space.bilibili.com/672342685">
      <img
        src="./assets/member_image/ellien.jpg"
        style="border-color: #576690"
        alt="乃琳Queen"
      />
      <p style="color: #576690">乃琳Queen</p>
    </a>
  </div>
  <div>
    <a href="https://space.bilibili.com/703007996">
      <img
        src="./assets/member_image/asoul.jpg"
        style="border-color: #666666"
        alt="A-Soul Official"
      />
      <p style="color: #666666">A-Soul Official</p>
    </a>
  </div>
</div>
<style>
  a, a:hover {
    text-decoration: none;
  }
  .member {
    display: grid;
    margin: 20px 0;
    grid-template-columns: repeat(6, minmax(0, 1fr));
    box-sizing: border-box;
  }
  @media screen and (max-width: 768px) and (min-width: 501px) {
    .member {
      grid-template-columns: repeat(3, minmax(0, 1fr));
    }
  }
  @media screen and (max-width: 500px) {
    .member {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }
  }
  .member div {
    padding: 15px;
    height: 100px;
    text-align: center;
    width: full;
  }
  img {
    width: 80px;
    border-radius: 50%;
    border: 2px solid;
  }
  p {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana,
      sans-serif;
    color: rgb(155, 152, 152);
    font-weight: bold;
    font-size: 13px;
    letter-spacing: 0.5px;
  }
</style>

在未来学院中，五位性格迥异的少女，为了成为偶像这一共同目标走到一起，并且为之努力奋斗。

设定中，她们生活在虚拟城市枝江。所以系统名为枝网查重系统（化用知网）。

## 已有项目

|名称|详情|
|----|----|
|ASoulCnki|枝网爬虫|
|ASoulCnkiBackEnd|枝网后端|
|ASoulCnkiFrontEnd|枝网前端|
|ASoulCnkiFrontEndV3|重构的枝网前端|
|ASoulCnkiStaticBFF|枝网前端的BFF|

## API

### 数据共享

目前已有一份从数据库导出的 JSON，数据截至到 2021 年 8 月 中旬，托管在[Google Drive](https://drive.google.com/file/d/151oz560vj2T2uwxYrRbxq1NPYwvx_dNf/view)

具体JSON格式可以参考后端的接口文档

如果有其他合作相关意向，欢迎在 GitHub 提 Issue ，或私信B站 [@查重姬Official](https://space.bilibili.com/1809170490/)

### API调用

枝网欢迎大家使用API

API 文档可以参见[这里](./../api/README.md)

## 关于部署项目

参见[这里](./../deploy/README.md)

## 如何贡献

1. Fork 对应的项目到您自己的仓库并 Clone 到本地
2. 修改后向对应仓库提交 PR
