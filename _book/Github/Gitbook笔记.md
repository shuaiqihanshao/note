<h1 style="text-align:center;">gitbook之葵花宝典</h1>

> 警告：安装过程中，出现问题很正常，要学会百度。
>
> 常见的BUG本文都有解决方法，祝你安装成功。


GitBook 是开源书籍写作方法，可以把Markdown 文件汇集成电子书，并提供 PDF、HTML 等多种格式输出。

技术栈：`Node.js + GitHub + Git + Typora + GitBook`

JavaScript 运行环境:Node.js

markdown文本编辑器:Typora

代码管理工具：Git

代码托管仓库：Github

### 一、Git Book安装过程

#### 1、安装 Node.js

Git Book 是基于 Node.js的，所以我们首先需要安装对应版本的 Node.js（下载网址：https://nodejs.org/en/download/）

<img src="https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201110215842.png" style="zoom:80%;" />

目前Node.js的最新稳定版本的 v 12.18.3。但这个版本对Git-book可能不兼容（在后续安装和启动 Git-book 命令时会出现错误提示），建议直接安装v 10.22.0。

当然，如果开始时选择了最新版本也不用慌，可以先尝试后续步骤，如果出现错误提示，参考[避坑指南-Node.js版本问题](#jump)尝试解决。

#### 2、安装Git Book

现在安装 Node.js 都会默认安装 NPM（node 包管理工具）(类似python和pip的关系)

Dos命令行输入

```
npm install -g gitbook-cli
```

耐心等待，安装完成后会显示 gitbook-cli 的版本。

#### 3、确认Git Book安装完成

```
Dos命令行输入 gitbook -V （注意：V要大写）
```

如果在上一步骤Git Book安装成功，命令行中会出现以下信息。至此，恭喜你安装成功。

```
E:\node>
CLI version: 2.3.2
GitBook version: 3.2.3
```



---

### 二、避坑指南

#### 1、安装速度问题

**问题**：执行 `gitbook -V` 时显示：`Installing GitBook 3.2.3 …….`，之后出现长时间卡顿
**解决办法1:** 科学上网

**解决办法2:** 安装源切换为国内淘宝镜像。
在cmd执行命令：

```shell
npm config set registry=http://registry.npm.taobao.org -g  # 先切换安装源
npm install -g gitbook-cli                                 # 安装gitbook
gitbook -V                                                 # 查看版本信息
```



#### <span id="jump">2、Node.js版本问题</span>

**问题:**Git Book安装或查看版本信息时出现报错，报错信息如下：

```
if (cb) cb.apply(this, arguments)
^
TypeError: cb.apply is not a function
或# Fatal error in , line 0
# Check failed: U_SUCCESS(status)
#
#
#FailureMessage Object: 00000013F6B1D570
```

说明Node.js的版本环境有问题，需要降低Node版本。最新稳定版本是v12.18.3，试下来在Windows -10上v10.22.0是可以正常使用的，下面以该版本的安装为例，展示上述报错的解决方案。（注：该方法可能只使用于Windows10操作系统）



​	**解决办法1：** 卸载已下载版本，重新下载<font color = #ff0000>10.22.0</font>版本的Node.js（下载网址：https://nodejs.org/zh-cn/download/releases/）

​	<font color = #ff0000>缺点</font>：对未来Node.js版本的更新或多个版本之间的切换使用不太方便

​	**解决办法2：** 使用Windows系统下的Node.js的版本管理器<font color = #ff0000>nvm-windows</font>（Node.js Version Manager for Windows）。

​	<font color = #ff0000>优点</font>：nvm-windows可以帮助实现在同一台设备上进行多个node版本之间的切换。

​	主要步骤：

1. 下载nvm：在github地址：https://github.com/coreybutler/nvm-windows，选择nvm-setup.zip，下载后直接安装（一路下一步即可）。

   > **提高下载速度方法：复制安装包的下载链接，使用迅雷下载即可**

2. 配置nvm的环境变量[^3]：一些教程中提到安装完nvm后需要手动配置环境变量，但最新版本（我下载的是v 1.7.7）的nvm-windows在安装完成之后已经自动配置了环境变量。可以再次确认你的环境变量中是否包含了nvm的路径。




使用nvm命令实现多版本node的下载和切换：

```
nvm -v                 查看nvm版本信息：
nvm install 10.22.0    安装某一版本 node/npm（以v10.22.0为例）：
nvm use 10.22.0        使用特定Node版本（以v10.22.0为例）：
nvm ls available       查看远程服务器上的可用Node版本：
nvm ls                 查看本机的可用Node版本
```

一个小tip[^1]：有时使用 nvm install 命令下载新的Node版本会比较慢，这时可以直接从网址：https://nodejs.org/zh-cn/download/releases/上下载所需版本，并安装到nvm的源文件夹下。

---

### 三、Git Book使用简介

#### 1、Git Book创建及预览

​	**创建书籍：**

新建一个文件夹，在文件夹下打开命令窗口（在文件夹地址栏输入cmd后回车），初始化文件夹：

```
gitbook init
```

执行上述命令后，会自动生成两个必要的文件 `README.md` 和 `SUMMARY.md`。

`README.md`: 书的介绍文字，如前言、简介，在章节中也可做为章节的简介。

`SUMMARY.md`[^2]: 设计书籍的章节结构和顺序。

​	**预览书籍：**

```
gitbook serve
```

执行命令，Git-book 会启动一个 4000 端口（[http://localhost:4000](http://localhost:4000/)）用于预览。

同时生成一个_book文件夹，内部存放编译后静态HTML文件。

_book文件夹内部结构：

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201110215954.png)



但由于Git-book版本不稳定，有时运行serve命令会出现报错：

```
Error: ENOENT: no such file or directory, stat '~~~.js'1
```

​	**解决办法：** 

在用户目录下找到以下文件.gitbook\versions\3.2.3\lib\output\website\copyPluginAssets.js ，把所有的 confirm: true 替换为 confirm: false。

​	**构建书籍：**

```
gitbook build
```

上述命令默认将生成的静态网站输出到 `_book `目录。实际上，这一步也包含在 gitbook serve 里面，但 gitbook build 可以指定路径：

```
gitbook build [书籍路径] [输出路径]
```

**	生成其它格式的电子书：**

```
gitbook pdf ./ ./mybook.pdf

gitbook epub ./ ./mybook.epub

gitbook mobi ./ ./mybook.mobi
```

#### 2、Git Book插件

> 本质：美化静态HTML页面

官方获取插件地址： https://plugins.gitbook.com/

安装插件只需要在书籍目录下增加 `book.json` 文件，例如增加折叠目录的插件，需要在 `book.json `内增加下面代码:

```
{"plugins": ["expandable-chapters-small"],

"pluginsConfig": {

"expandable-chapters-small":{}

}

}
```

然后终端执行 install 来安装插件即可：

```
gitbook install
```

#### 3、Git Book连接Github

安装好Git软件后

进入写笔记的目录

右键空白区域--【Git bash here】

----

### 番外篇

#### summary目录结构设计

```
# Summary

* [前言](README.md)
* [Github笔记](Github/README.md)
* [第1节：Github下载速度](Github/Github下载速度.md)
* [第2节：Git和Github](Github/Git和Github.md)
* [第3节：Github图床](Github/Github图床.md)
* [第4节：Gitbook笔记](Github/Gitbook笔记.md)
* [Linux笔记](Linux笔记/README.md)
* [Python笔记](Python笔记/README.md)
* [第1节：爬虫](Python笔记/爬虫.md)
* [第2节：数据分析](Python笔记/数据分析.md)
* [第3节：自动化](Python笔记/自动化.md)
* [第4节：人工智能](Python笔记/人工智能.md)
* [HTML笔记](HTML笔记/README.md)
* [网络安全笔记](网络安全笔记/README.md)
* [shell命令行](shell命令行/README.md)

```

---

#### 使用nvm安装node的两种方式

##### 方法一：换成淘宝镜像源

验证nvm是否安装成功：在cmd输入nvm version，有提示nvm版本信息，即安装成功

![](https://gitee.com/hundred-star-tutor/pic-go/raw/master/img/20201110215811.png)

输入nvm root，查看nvm的安装路径，我的是`E:\nvm\nvm`，打开这个路径，找到`settings.txt`文件并打开，在文本的最后一行中加入以下两行代码：

```
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

然后保存

我的`settings.tx`t文件的数据是这样的

```txt
root: E:\nvm\nvm
arch: 64
proxy: none
originalpath: .
originalversion: 
node_mirror: http://npm.taobao.org/mirrors/node/ 
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

保存文件之后，关掉cmd，再重新打开cmd，输入：nvm install [version]，就会启用淘宝镜像自动下载安装对应的node和npm版本。



##### 方法二：直接从淘宝镜像下载node zip版本

淘宝镜像地址：https://npm.taobao.org/mirrors/node

例如：https://npm.taobao.org/mirrors/node/v4.6.0/node-v4.6.0-win-x64.zip

进入nvm所在的路径【E:\nvm\nvm】，

将node压缩包解压到当前文件夹，并改文件夹名为v 4.6.0，删除zip文件，Dos命令行输入`nvm use 4.6.0`即可。

nvm原理：每次切换只是替换快捷方式。

>注意：
>
>>nvm管理的多个npm版本各需独立配置淘宝镜像！
>>
>>C:\Program Files\node.js 这里保存的只是一个快捷方式而已

​			

----

#### 环境变量的配置



git-book出现Type-error: cb.apply is not a function解决办法

执行git-book -V的时候出现如下错误

```
E:\node>gitbook -V
CLI version: 2.3.2
Installing GitBook 3.2.3
C:\Users\hante\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\_npm@5.1.0@npm\node_modules\graceful-fs\polyfills.js:287
      if (cb) cb.apply(this, arguments)
                 ^


TypeError: cb.apply is not a function
    at C:\Users\hante\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\_npm@5.1.0@npm\node_modules\graceful-fs\polyfills.js:287:18
    at FSReqCallback.oncomplete (fs.js:184:5)
```

解决方法：

> 此方法不推荐使用，更换node版本是最好的　

打开polyfills.js文件，找到这个函数

```
function statFix (orig) {
if (!orig) return orig
// Older versions of Node erroneously returned signed integers for
// uid + gid.
return function (target, cb) {
return orig.call(fs, target, function (er, stats) {
if (!stats) return cb.apply(this, arguments)
if (stats.uid < 0) stats.uid += 0x100000000
if (stats.gid < 0) stats.gid += 0x100000000
if (cb) cb.apply(this, arguments)
})
}
}
```

在第62-64行调用了这个函数

```
fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)
```

把这三行代码注释掉就解决报错了

```
现在输入显示正常

E:\node>gitbook -V
CLI version: 2.3.2
GitBook version: 3.2.3
```

-----



输入git book init 后正常反应

```
E:\note>gitbook init
warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
```

错误反应

```powershell
E:\note>gitbook init
warn: no summary file in this book
info: create README.md
info: create SUMMARY.md


TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be of type string or an instance of Buffer, TypedArray, or DataView. Received an instance of Promise
```

解决方法，下载node.js稳定版本

使用nvm进行版本管理

```powershell
C:\Users\hante>nvm install 10.22.0      # 安装 node 10.22.0版本
Downloading node.js version 10.22.0 (64-bit)...
Complete
Creating E:\nvm\nvm\temp


Downloading npm version 6.14.6... Complete
Installing npm v6.14.6...


Installation complete. If you want to use this version, type


nvm use 10.22.0


C:\Users\hante>nvm use 10.22.0       # 切换到 node 10.22.0 版本
Now using node v10.22.0 (64-bit)


C:\Users\hante>nvm ls                # 查看已安装的node版本


    14.14.0
  * 10.22.0 (Currently using 64-bit executable)
```



[^1]: 教程详见番外nvm安装方法二

[^2]: 目录结构的设计详见番外
[^3]: 环境变量的配置详见番外