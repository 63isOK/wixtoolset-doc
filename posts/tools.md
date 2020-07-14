# 工具链

所有的工具,帮助命令都是 xx /?

- candle,预处理,编译成wixobj
- light,链接,或是嵌入到db
- lit, 组合多个wixobj供light使用
- dark,将安装包逆向为wix源码
- heat,生成wxs格式的文件
- insignia,数字证书处理
- melt,将msm逆向为wix源码
- torch,根据差异,生成一个mst/msi
- smoke,检查有效性
- pyro,利用补丁文件/差异文件生成一个msp
- wixcop,wix标准检查,或是源码安装包一致性检查
- wixunit,源码检查
- lux/nit,自定义操作的测试

![工具链的关系](/posts/tools.png)

从图中可以看出,如果我们要制作一个链式安装包,
可以使用heat/candle/light.

所以除了这3个工具,其他无关的文档就不仔细看了.
