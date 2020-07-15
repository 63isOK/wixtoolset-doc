# 开始菜单上创建一个快捷方式

这种需求,10个安装包就有8个会有.

添加快捷方式和添加一个文件的步骤是一样的.

## 定义目录

这个目录也应该在TARGETDIR下

    <Directory Id="ProgramMenuFolder">
        <Directory Id="ApplicationProgramsFolder" Name="My Application Name"/>
    </Directory>

和ProgramFilesFolder类似,这里使用ProgramMenuFolder来表示开始菜单.

## 添加快捷方式到安装包

和文件列表一样,这里是快捷方式列表

Component/Shortcut/RemoveFolder,可能还会涉及到注册表.

    <DirectoryRef Id="ApplicationProgramsFolder">
        <Component Id="ApplicationShortcut" Guid="PUT-GUID-HERE">
            <Shortcut Id="ApplicationStartMenuShortcut"
                      Name="My Application Name"
                      Description="My Application Description"
                      Target="[#myapplication.exe]"
                      WorkingDirectory="APPLICATIONROOTDIRECTORY"/>
            <RemoveFolder Id="CleanUpShortCut"
                          Directory="ApplicationProgramsFolder"
                          On="uninstall"/>
            <RegistryValue Root="HKCU"
                           Key="Software\Microsoft\MyApplicationName"
                           Name="installed"
                           Type="integer"
                           Value="1"
                           KeyPath="yes"/>
        </Component>
    </DirectoryRef>

Shortcut节点定义了快捷方式的各个顺序性,Description是可选的,
Target使用的File节点的id,还可以指定工作目录.
Shortcut还有一个可选子节点Icon,可用来指定图标,现在基本是标配.

Shortcut一般会关联两个密切的节点.

- RemoveFolder,确保卸载时能正确干掉残留
- RegistryValue,用在这里,主要当Shortcut的KeyPath没指定时,用这个节点来指定yes

## 告诉wix安装快捷方式

在Feature节点下指定就可以了.

    <ComponentRef Id="ApplicationShortcut" />

这点和文件的处理没什么两样.
