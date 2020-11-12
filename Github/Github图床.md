<h1 style="text-align:center;">图床搭建</h1>

### 前言：

本人因为无代理，无法翻墙，放弃使用github作为图床

github图床缺点如下（无代理情况）：

即使图片已经通过PicGo成功上传到github仓库，

- 由于网络延迟大，外链插入到typora中，无法显示，只会显示一个链接

- 外链放入Chrome搜索引擎中，无法查看（可能是域名污染造成）

- PicGo相册图片全黑


---

**技术栈**：`node.js + PicGo +Gitte +Typora`

**图床**：一般是指储存图片的服务器，这样我们就可以通过Markdown外链的方式访问图片。

**原理**：在 Typora 上写笔记，插入图片后，图片自动同步到 PicGo 上，Picgo将图片上传到Gitte仓库保存。

> 温馨提示：
>
> > 学会查看PicGo日志文件，会帮你更好的解决问题
> >
> > 本文给出了一些常见错误的解决方法
> >
> > 失败不可怕，要学会百度

---

### 1.安装 Node.js

PicGo 的插件功能是基于 Node.js的，所以首先安装Node.js。

（下载网址：https://nodejs.org/en/download/）

<img src="https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201110215842.png" style="zoom:80%;" />

### 2.下载 PicGo

链接：https://github.com/Molunerfinn/PicGo/releases

复制链接，使用迅雷下载，速度很快

> 注意beta为测试版，不稳定；下载稳定版即可

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050710.png)

### 3.下载 gitee 插件

输入gitee，下载第一个即可

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050735.png)



### 4.配置 PicGo

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050803.png)

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050832.png)

### 5.配置 Gitee

1. 注册 gitee 账号，创建一个仓库专门放图片

   - 在gitee上搭建一个仓库具体方法，请看官方教程https://gitee.com/help/articles/4169

   - 生成私人令牌（token）

     注意：令牌生成后请立即保存，不会显示第二次。

     ![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/点击设置.png)

   <img src="https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/真令牌.png"  />

   ![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/私人令牌.png)

2. gitee插件配置

   > 注意：
   >
   > > 不同 Gitee 插件界面不一致，不要生搬硬套


![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050910.png)



3. 验证上传图片是否成功，如果出错，请看[避坑指南](#jump)

   成功后，相册内可以看见一张图片；同时PicGo也有提示

   <font color=red>**警告**</font>：相册里保存的图片，不要随便删除，当你点击删除后，Gitee仓库保存的图片也会同时删除



![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/图片上传.png)



### 6.Typora配置

- 打开typora，依次进入【文件】-【偏好设置】-【图像】

  > 注意：Typora0.9.84及以上版本才支持PicGo

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050954.png)

- 点击【验证图片上传选项】后，出现以下提示即成功

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111050938.png)

### 7.避坑指南



- ##### typora验证失败（本质为端口冲突）

  Typora 默认监听端口为36677，每次运行picgo后，系统会分配一个端口给picgo，默认为36677。

当更改picgo配置或多次启动后，picgo将会获得新的端口号,，两个端口不一致，此时typora就会验证失败。

> 养成好习惯：每次配置picgo后，重启后使用



<font size=2 color=red>下图为picgo日志文件,打开后，发现picgo新开启一个36678端口</font>

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111051016.png)

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201111051043.png)



- ##### <span id='jump'>图片上传失败的原因</span>

  1.当我们把名字相同的照片，上传两次时，picgo和typora都会有报错提示。

  <img src="https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/上传失败.png" style="zoom: 67%;" />

  <img src="https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/typora报错.png"  />

  

  ![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/同名.png)

  

  解决方法一：禁止将同名图片上传两次及以上

  解决方法二：配置picgo时，打开时间戳重命名，这样每一张上传图片就不会重名了。

  但是名字都是时间戳，gitee仓库保存的图片无特征信息，不方便后续管理与查看。

  

  2.PicGo配置文件错误，例如仓库名或用户名写错

  我记得我用github图床时，配置PicGo时将分支写成master，picgo上传图片就会报错，查看picgo日志文件，才发现问题所在。(由于黑人运动，现在github新建的仓库，默认分支都变成main)

  <img src="https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/github配置.png"/>

  

- **烦人的问题**
  在typora插入新图片后，会立即上传到Gitte仓库，但是当我们发现图片插入位置错误后，直接剪切会重复上传图片

  解决方法一：

  typora开启源码模式进行写作

  解决方法二：

  进入typora偏好设置，将【上传图片】修改为【无特殊操作】，后续右键图片，手动上传到Gitte即可。

  ![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/无特殊操作.png)

---







