# 哔哩哔哩轻小说_bilinovel

# 书源编辑注意
1. 自己的配置中，翻页动画必须得是滑动的才能看见图片，如果不是滑动的，在设置为滑动前先在到详情页清除缓存。
2. User-Agent：必须包含手机标识
    1. 获取方法：在浏览器切换为mobile模式后的User-Agent
3. 搜索页：必须要cookie.key=haha，时限只有900s（加密里含时间）。无则响应设置Cookie的页面，然后自动在3s后重新加载。
    最佳解决方法：每次都在搜索前使用js调用java.webView先请求一次。
    其他：
        解析Cookie：设置CookieHTML中，somework.js，使用k函数(Base64)转换a(key)，b(iv)，c(data)，AES/CTR解密（haha的值）。
4. 章节页：需要Host，Accept-Language
    1. 图片：需要Referer（可能需要科学上网才能访问图片）
    2. 在翻页规则中，有时候会报错，debug发现通常是503，可能并发太高了，用户自己在本页多刷新一下或者等待一下刷新即可
        1. 这个503错误有很多，只是大多数都可以无视，但是这里因为需要下一页URL，因此无法无视
5. 正文字符替换：
    1. 在正文页body后有一个readtool.js，最后有一些hex字符（JS方法名）和一堆unicode码点（Js替换正文字符代码）。
    2. 假设encodeJS那一堆unicode码点，如果方法名没变的情况下
String.fromCharCode(...encodeJS.split(/[a-zA-Z]{1,}/))，这个返回值就是Js替换代码。
不需要执行[].filter.constructor(JS)();来创建一个Function传入Js字符串代码执行这个Function对象。
    3. 目前104个替换值，如果没有变则应该不需要改。
替换代码形式如 ：replace(new RegExp("", "gi"), "一")

# 更新
## 2025/03/12 version=3
1. 内容ID由 acontentz 改为 acontent 
2. 优化查找下一页URL逻辑
## 2024/7/20
1. 搜索改为不要webView，正文改为要webView
   1. 问题：搜索不需要2次，但是每次重新启动app后，正文需要先加载一次，后续才不会出现"内容加载失败"这样的错误（不知道为什么，看cookie都是一样的，都是第一次第一页有问题）
## 2024/7/18：
1. 设置默认请求头
2. 现在cookie只需要night=1;即可
3.3.24.070817最新版的webView有问题，获取不了cookie了，但是由于cookie变简单了，就暂时不用webView
## 2024/3/16：
1. 设置链接验证：其会在搜索页响应详情页时，转到详情页解析，并加入搜索结果中
## 2024/3/8：
1. 正文: Accept-Encoding=gzip，Cookie=night=0，
Accept=text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8。
但是在这里好像只需要加Accept即可

