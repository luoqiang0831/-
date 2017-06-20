# -
加载错误的event中 canBubble: false, cancelable: false。自然用通常的冒泡机制不能捕捉加载错误，需要用捕获的方式来捕捉加载错误。

仅仅能够捕获加载错误还是不够的，还需要区分加载错误和其他错误，因为该方法也能够捕捉语法错误等一系列错误事件。

细心的你可能会发现，普通的错误会有message错误信息，而加载错误是没有message错误信息。

网页错误收集,针对不用的环境 js发生错误 发送到服务器分析


ErrorEvent继承与Event是显然的，而且ErrorEvent比Event多了message、filename、lineno、colno、error这些信息。执行错误、语法错误以及自定义抛出的异常错误，都源自ErrorEvent，都包含了message等错误信息。而加载错误并不是源自ErrorEvent，而是直接源自Event，不包含message等错误信息。由!e instanceof ErrorEvent即可辨别出加载错误。

通过搜索查阅W3C文档，named error event都是由于资源加载失败而抛出的，根据文件类型过滤出来css和js即可。

由此可见，可以区分加载错误和其他错误。

优点：准确

缺点：低版本IE浏览器存在兼容性问题，但大部分浏览器支持情况较好

参考:http://mp.weixin.qq.com/s/bJv-hPSSscfljsB4eJVpIQ
