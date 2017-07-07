# Go语言开发环境搭建

## 前言

由于最近做毕设，长时间处在Windows环境下，索性搞一个windows的开发环境。

## 准备

1. Go语言安装包
2. visual studio code
3. 一堆package \(见附件\)

## 安装Go语言

1. 安装go语言 .msi
2. 配置环境变量（我的系统是win7，基本配置大同小异）

* GOROOT : Go的安装目录
* GOPATH : 用于存放Go语言的Package的目录，这个目录不能再Go的安装目录中
* GOBIN : Go二进制文件存放目录，写成 %GOROOT%\bin就好
* GOOS : 操作系统
* GOARCH : 指定系统环境，i386表示x86，amd64表示x64
* PATH : 需要将%GOBIN%加在PATH变量的最后，方便在命令行下运行Go

在系统环境变量中新建上面的各项环境变量，参数根据实际情况选择。

**详细参考**

[http://jingyan.baidu.com/article/046a7b3eaade2cf9c37fa95d.html](http://jingyan.baidu.com/article/046a7b3eaade2cf9c37fa95d.html)



   3. 安装visual studio code

参考：[http://studygolang.com/articles/6204](http://studygolang.com/articles/6204)

个别Package在安装过程中会报错，显示下载失败。以下主要介绍我的解决方案。

* 安装上边的参考过一遍流程。

* 在配置的GOPATH（这个文件夹是什么作用应该明确了吧）目录中查看已经下载好的package，此时会有两种情况
* package源码已经下好使用go get -u -v却显示失败。在对应的package目录中，执行go install。手动安装。
* package没有下载好源码，这个比较复杂，三种方案
* 尝试翻墙吧，然后在重复执行上边的操作（有些package很有可能依旧不行）
* 使用刚刚安装好的visual studio code打开一共go的代码。这个编译器有个好处会提示你需要安装哪些package，然后选择安装。如果提示安装失败，依旧重复执行，之前的操作（这个package说不定什么时候会下载下来，所以需要不断重复\)
* 到各个package的官网或者github上下载源码安装（麻烦而且不一定找的到），这里可以通过我上传的package包，来进行安装。然后还缺少什么包重复执行之前的操作。

## 总结

这个安装过程其实并不复杂，但是需要的耐心，实际我在第一次配置的过程花了将近两个小时。如果你需要一个好看高效的编辑器，那么这个时间花的不亏；如果不需要，那么直接用第一个链接里的编辑器就可以了（我觉得那个好丑~~\)



