---
layout: post
title:  "Electron与ADB"
date:   2023-12-06 22:40:00 +0800
categories: jekyll update
---

一些报错：
{% highlight cmd %}
failed to asynchronously prepare wasm: CompileError: WebAssembly.instantiate(): Refused to compile or instantiate WebAssembly module because 'unsafe-eval' is not an allowed
{% endhighlight %}


{% highlight cmd %}
Refused to load the script 'https://cdn.jsdelivr.net/npm/tesseract.js@v5.0.3/dist/worker.min.js' because it violates the following Content Security Policy directive: "script-src 'self' 'unsafe-inline'". Note that 'script-src-elem' was not explicitly set, so 'script-src' is used as a fallback.
{% endhighlight %}

解决办法，修改`Content-Security-Policy`

{% highlight html %}
    <meta
      http-equiv="Content-Security-Policy"
      content="script-src 'self' 'unsafe-inline' 'wasm-unsafe-eval' https://cdn.jsdelivr.net; worker-src 'self' blob:"
    />
{% endhighlight %}