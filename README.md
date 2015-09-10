# gorelease
[![Build Status](https://travis-ci.org/codeskyblue/gorelease.svg?branch=master)](https://travis-ci.org/codeskyblue/gorelease)
[![gorelease](https://dn-gorelease.qbox.me/gorelease-download-blue.svg)](http://gorelease.herokuapp.com/dn-gobuild5.qbox.me/gorelease/master)

For easily build go cross platform online and public go binary.

This project is not stable for now.

这个项目是用来帮助发布在线编译go，以及发布其二进制文件。

这种方案是我想出来最稳定的一种方法了。完全依赖于各种开源服务,目前已经证明了这种方法是完全可行的。

* 使用[travis-ci平台](https://travis-ci.org) 进行go代码的跨平台编译
* 使用[七牛CDN](http://qiniu.com)来发布编译好的文件
* 另外附加上我写的一些脚本[scripts](scripts). 完成编译的工作
* 一个简单的[发布界面](http://gorelease.herokuapp.com/)。托管在heroku平台上

## Step1
Save the following content into `.travis.yml`, and put it into your repository.

	language: go
	go:
	  - 1.4
	script:
	  - go test -v ./...
	after_success:
	  - bash -c "$(curl -fsSL http://bitly.com/gorelease)" gorelease

This script performs build and publish to qiniu.

## Step2
You need a account in [QiniuCDN](http://www.qiniu.com)

In `travis-ci.org` setting page. Set three environment variables. ex: 例如

	ACCESS_KEY=LKJFLSkdjfkj23lkjrl23kjflkzsjdfljwerf2w3
	SECRET_KEY=kljdlFLSDKFJo9iwejflkjLkjsdfoijw4elfkjsd
	BUCKET=gorelease

`BUCKET`也就是空间地址, 没有空间的话，选择创建一个新的空间就可以了. 不妨把这3个变量找个地方存起来,以后其他项目还能用。不要拷贝我上面写的, 从七牛上面拷贝

BTW, Qiniu CDN cache is 15mins, So you new released app will be refreshed after 15mins.

## Step3
Get download address page.

在七牛的 **空间设置/域名设置** 里面把域名拷贝出来. ex: `dn-gobuild5.qbox.me`

如你的项目名是 `gorelease`, 地址 <http://gorelease.herokuapp.com/dn-gobuild5.qbox.me/gorelease/master> 即为下载地址页面

## Step4
The badge

[![gorelease](https://dn-gorelease.qbox.me/gorelease-download-blue.svg)](http://gorelease.herokuapp.com/dn-gobuild5.qbox.me/gorelease/master)

Just change the download link.

	[![gorelease](https://dn-gorelease.qbox.me/gorelease-download-blue.svg)](http://gorelease.herokuapp.com/dn-gobuild5.qbox.me/gorelease/master)

## Contribute
All pull request and suggestions are welcomed. Just make sure the you have tested the code.

另外目前的发布界面有点丑，非常期待欢迎前端高手的参与。

Have a good day.

## Thanks
* <https://travis-ci.org>
* <http://qiniu.com>
* <http://shields.io>
* <https://github.com/mitchellh/gox>

## LICENSE
This repository is under [MIT](LICENSE).
