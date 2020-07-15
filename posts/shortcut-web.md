# 创建指向网页的快捷方式

这个部分,展现一下如何使用工具库.

## 将工具库添加到项目

在使用light时,命令行多加两个参数 -ext WiXUtilExtension

## 在项目中添加工具库的命名空间

    <Wix xmlns="http://schemas.microsoft.com/wix/2006/wi"
         xmlns:util="http://schemas.microsoft.com/wix/UtilExtension">

下面这条,就是util工具库的命名空间.

## 添加指向网页的快捷方式

使用Util:InternetShortcut节点.

    <DirectoryRef Id="ApplicationProgramsFolder">
        <Component Id="ApplicationShortcut" Guid="PUT-GUID-HERE">
            <Shortcut Id="ApplicationStartMenuShortcut"
                      Name="My Application Name"
                      Description="My Application Description"
                      Target="[#MyApplicationExeFileId]"
                      WorkingDirectory="APPLICATIONROOTDIRECTORY"/>
            <util:InternetShortcut Id="OnlineDocumentationShortcut"
                                   Name="My Online Documentation"
                                   Target="http://wixtoolset.org/"/>
            <RemoveFolder Id="ApplicationProgramsFolder" On="uninstall"/>
            <RegistryValue Root="HKCU"
                           Key="Software\Microsoft\MyApplicationName"
                           Name="installed"
                           Type="integer"
                           Value="1"
                           KeyPath="yes"/>
        </Component>
    </DirectoryRef>

InternetShortcut 会有一个id
