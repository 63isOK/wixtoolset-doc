# 本地化

主要就是在编译链接时来处理

    常规编译
    candle.exe myinstaller.wxs -out myinstaller.wixobj
    链接指定语言
    light.exe myinstaller.wixobj -cultures:en-us -loc en-us.wxl -out myinstaller-en-us.msi
    light.exe myinstaller.wixobj -cultures:fr-fr -loc fr-fr.wxl -out myinstaller-fr-fr.msi

-loc标识就是指定语言的的,-cultures用于指定文化区域.

除此之外还可以通过其他方式来实现本地化,这里就不展开了,
更多可以查看文档.
