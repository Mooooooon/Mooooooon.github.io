---
layout: post
title:  "Electron与ADB"
date:   2023-12-05 22:40:51 +0800
categories: jekyll update
---

让用户自己配置ADB环境变量似乎不是好的处理方法。

在 [developer.android.com](https://developer.android.com/tools/adb?hl=zh-cn) 下载ADB套件。

解压到Electron项目目录。

获取路径建议使用 `process.cwd()` 不管开发环境还是打包后都会输出项目根目录。

举例：
{% highlight js %}
const adbPath = path.join(process.cwd(), 'platform-tools', 'adb.exe')
{% endhighlight %}

执行命令：
{% highlight js %}
exec(adbPath + ' connect 地址:端口', (error, stdout, stderr) => {
  console.log(stdout)
}
{% endhighlight %}

至此，开发环境已经可以直接使用，但是打包后无法执行，因为exe文件被打包进了`app.asar`。

在`package.json`或`electron-builder.json5`中设置：

{% highlight json %}
  "extraFiles": [
    "./platform-tools"
  ] 
{% endhighlight %}

OK，排除之后不会被打包，可以在正式环境执行ADB了。