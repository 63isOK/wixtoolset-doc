# 大版本升级

如果安装包是基于msi,那么这篇文章基本上是必备的.

下面的例子是创建两个msi,不同版本,最后测试不同场景.

## 添加升级信息

添加一个唯一号,作为升级代码(也有叫产品代码)

    <Product Id="*"
             UpgradeCode="PUT-GUID-HERE"
             Name="My Application Name"
             Language="1033"
             Version="1.0.1"
             Manufacturer="My Manufacturer Name"/>

