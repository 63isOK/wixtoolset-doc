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

移除旧版本,并处理乱序安装,
使用MajorUpgrade节点来描述.

    <MajorUpgrade
      DowngradeErrorMessage=
        "A later version of [ProductName] is already installed. Setup will now exit.">

对于MajorUpgrade,还有些可选操作:

- 卸载掉已安装版本
- 调整提示出现的时机

## 版本构建

第一个版本正常构建(编译链接)即可.
第二个版本需要注意一下两点:

- Product节点中的版本Version值需要变大
  - windows只认版本的前3节,至少要在这3节中变大
- Product节点中的Id要赋一个新的值
