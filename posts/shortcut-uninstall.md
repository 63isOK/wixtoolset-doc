# 创建卸载的快捷方式

这个在每个安装包中,也是必需品.

## 新增卸载快捷方式

利用Shortcut节点来实现

    <Shortcut Id="UninstallProduct"
              Name="Uninstall My Application"
              Target="[SystemFolder]msiexec.exe"
              Arguments="/x [ProductCode]"
              Description="Uninstalls My Application" />

这里是利用cmd命令直接来卸载.最好还是配合RemoveFolder节点一起.
如何和注册表/文件删除节点一起,可以避免一些ice错误.
