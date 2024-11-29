## AfdianToMarkdown

爱发电(afdian.com)爬虫，用于下载爱发电作者的动态和作品集并保存为markdown文件（目前只能保存纯文本内容，不支持保存图片）。

**！！！该软件不能直接帮你免费爬取订阅后才能查看的内容！！！**

### 准备

使用浏览器插件[cookie master](https://chromewebstore.google.com/detail/cookie-master/jahkihogapggenanjnlfdcbgmldngnfl)导出爱发电cookie，如下图所示点击`copy`

![image](https://github.com/user-attachments/assets/d27b0f59-95c0-4080-97b9-d544d5424a33)

将复制到的json文本粘贴进与在RELEASE中下载的可执行文件同级（或git clone的项目根目录）的`cookies.json`即可。

![image](https://github.com/user-attachments/assets/3c9a4a26-fa94-4c38-a69d-359a536446b1)

**注意主站域名可能需要手动指定（默认为afdian.com)**

### 构建

本程序在go1.23.0下构建，如无编译环境，也可到release页面自行下载对应的可执行文件

```
make build
```

### 帮助
注：--list功能尚未实现

```
$ .\AfdianToMarkdown.exe -h
NAME:
   AfdianToMarkdown - 爱发电下载器，支持按作者或按作品集爬取数据
                      Github Link: https://github.com/PhiFever/AfdianToMarkdown

USAGE:
   eg:
     AfdianToMarkdown.exe -au Alice motions
   eg:
     AfdianToMarkdown.exe -au Alice albums
   eg:
     AfdianToMarkdown.exe -l album_list.txt
   eg:
     AfdianToMarkdown.exe update

VERSION:
   0.3.0

COMMANDS:
   motions  下载指定作者的所有动态
   albums   下载指定作者的所有作品集
   update   更新所有已经下载的作者的动态和作品集

GLOBAL OPTIONS:
   --host value                主站域名，默认为afdian.com，被封可自行更改 (default: "afdian.com")
   --author value, --au value  待下载的作者id
   --list value, -l value      待下载的作品集id列表文件，每行一个id。(不能与参数-au同时使用)
   --help, -h                  show help
   --version, -v               print the version

```

### 使用

本程序为命令行程序，需要在`cmd`,`powershell`或`bash`等shell中输入参数调用刚才构建的（或在release中下载的）可执行程序

在windows平台上进行调用时，有如下示例

注：下文提到的作者id为作者主页url的最后一部分，如`https://afdian.com/a/作者id/`

#### 下载作者的所有动态

```shell
AfdianToMarkdown.exe --host="ifdian.net" -au "作者id" motions
```

#### 下载作者所有的作品集

```shell
AfdianToMarkdown.exe -au "作者id" albums
```

#### 更新所有已经下载的作者的动态和作品集
注：不会覆盖已经下载的文件，所以也不会更新评论。可以通过删除文件来强制更新

```shell
AfdianToMarkdown.exe --host="ifdian.net" update
```

#### 下载指定文件中按行分隔的作品集（尚未实现）

```shell
AfdianToMarkdown.exe -l "文件路径"
```

### 更新日志
### v0.4.0
增加了对于漫画作品集的支持（暂未发布）

#### v0.3.0
1. 修改默认域名为`afdian.com`
2. 将寻找`cookies.json`的逻辑修改为在程序目录下而非工作目录下
3. 修复了对域名`ifdian.net`解析不正确的问题

#### v0.2.2

缩短了等待时间，加快下载效率

#### v0.2.1

添加了对update指令的支持，修复了Refer中url不正确的问题

#### v0.2
由于主站(afdian.net)在7月15日被屏蔽，添加了对于手动更改临时域名(如afdian.com)的支持
