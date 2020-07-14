# ui

wix内置了几套ui,也可以自己动手扩展.

## 内置ui的讨论

- 高级版
- 功能树版
- 安装目录版
- 最小定制版
- mondo版

这些内置版本也支持自定义的,eg:图标等.

源码中添加ui的步骤:

- 在源码最前面添加UIRef
- 在链接时带上相应的库

    源码中指定哪种内置ui

      <Product ...>
        <UIRef Id="WixUI_InstallDir" />
      </Product>

    light -ext WixUIExtension -cultures:en-us Product.wixobj -out Product.msi

## 对内置ui的定制

    license文件
    <WixVariable Id="WixUILicenseRtf" Value="bobpl.rtf" />

对界面图标的替换;退出对话框的定制(很多软件有安装完启动或检查更新).

还有替换欢迎语;修改ui顺序.添加自定义对话框.

## 本地化

之前本地化放在wxl文件中,记得以前用wix都是自己写wxl,
现在已经有汉化版本了.

light -ext WixUIExtension -cultures:zh-CN Product.wixobj -out Product.msi

## 内置ui的引用

这块就不进一步研究了,以前修改过,现在没有相应的需求.
