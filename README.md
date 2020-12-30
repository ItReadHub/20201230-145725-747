# 浅谈安卓逆向协议- 抖音 - 设备注册

抖音最近加入了风控，大大限制了数据拉取的成功度，处理这个问题很棘手，具体自己探索。<br>同时抖音加强了对SO的加密，即使修复ida堆栈，也是jumpout，大大提升了代码追踪的繁琐度，所以最新版的SO还没有深入跟进分析。<br>那么回到今天的话题，抖音的设备如何注册<br>其实网上已经有公开的资料<br>的确可行，咱们老生常谈，简单的聊一下思路逻辑<br>一：首先通过抓包找到接口地址<br>[http://log.snssdk.com/service/2/device_register](http://log.snssdk.com/service/2/device_register)<br>二：通过JDAX对源代码的分析，我们可以发现它<br>![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1609251474815-9ca7e9bd-9683-4a53-9982-bac0d061d0be.png#align=left&display=inline&height=116&margin=%5Bobject%20Object%5D&name=image.png&originHeight=232&originWidth=669&size=20602&status=done&style=none&width=334.5)<br>先通过GZIP压缩，再TTEncryptUtils加密，最后POST发送出去请求<br>然后X-SS-STUB，发现它只是一个对post的body部分的md5<br>![](https://cdn.nlark.com/yuque/0/2020/png/97322/1609251460216-2e211de9-7ed2-4fa3-8e15-4f9afa9d9977.png#align=left&display=inline&height=65&margin=%5Bobject%20Object%5D&originHeight=65&originWidth=434&size=0&status=done&style=none&width=434)<br>三：最后我们可以拼装属于自己的请求包<br>![](https://cdn.nlark.com/yuque/0/2020/png/97322/1609251460252-53165ee9-6020-41b2-b900-8a1e638147eb.png#align=left&display=inline&height=172&margin=%5Bobject%20Object%5D&originHeight=172&originWidth=554&size=0&status=done&style=none&width=554)<br>

> 更多短视频数据实时采集接口，请查看文档： [TiToData](https://www.titodata.com?from=douyinarticle)


<br>免责声明：本文档仅供学习与参考，请勿用于非法用途！否则一切后果自负。
