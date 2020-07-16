# 安装时读注册表

大部分打包程序也会有这种需求.
读到的注册表一般用于条件判断.

## 读注册表,将结果放到一个属性上

RegistrySearch节点是读注册表的入口

    <Property Id="NETFRAMEWORK20">
        <RegistrySearch Id="NetFramework20"
                        Root="HKLM"
                        Key="Software\Microsoft\NET Framework Setup\NDP\v2.0.50727"
                        Name="Install"
                        Type="raw" />
    </Property>

这是一个典型的读注册表,读完的结果放到NETFRAMEWORK20上.
RegistrySearch的几个属性都是和注册表相关.

## 在条件判断中使用这个属性

下面的例子是,如果.net2.0没有安装,就阻止安装包的安装.

    <Condition Message="This application requires .NET Framework 2.0.
      Please install the .NET Framework then run this installer again.">
        <![CDATA[Installed OR NETFRAMEWORK20]]>
    </Condition>

如果.net2.0安装了,那么对应的属性是有值的,消息也不会弹出,
如果没安装,就会提示,并结束安装.

当然通过注册表还能做很多事,eg:检测.net的版本.
