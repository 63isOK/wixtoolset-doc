# 写注册表

注册表有读就有写.

## 第一步描述对注册表的操作

注册表的操作也放到了Component.

    <DirectoryRef Id="TARGETDIR">
        <Component Id="RegistryEntries" Guid="PUT-GUID-HERE">
            <RegistryKey Root="HKCU"
                         Key="Software\Microsoft\MyApplicationName"
                         Action="createAndRemoveOnUninstall">
                <RegistryValue Type="integer" Name="SomeIntegerValue" Value="1" KeyPath="yes"/>
                <RegistryValue Type="string" Value="Default Value"/>
            </RegistryKey>
        </Component>
    </DirectoryRef>

创建了一个key,指定了两个value.

放在TARGETDIR下,是wix规定的,这表示这个注册表是要合并到目标机器上的.
Component用于分组.RegistryKey用于写注册表.读是用RegistrySearch.

Action属性表示安装时写,卸载时删掉.
下面的RegistryValue是两个value的描述.第一个value还设置了KeyPath=yes,
表示wix要将这个component安装.第二个value是默认值.

因为不需要对key和value做进一步引用,所以id就忽略了.
即使我们忽略了id,wix内部还是会自动生产id的.

## 告诉安装包,有个Component要添加到安装序列

在Feature中指定:

    <ComponentRef Id="RegistryEntries" />

这里面的id就是第一步中指定的.
