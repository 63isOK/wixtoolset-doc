# 设置安装卸载时的图标

wix有个标准属性 ARPPRODUCTICON,这个属性决定了显示那个图标.

我们只需要做两件事:定义Icon,其次将Icon和ARPPRODUCTION关联起来.

    <Icon Id="icon.ico" SourceFile="MySourceFiles\icon.ico"/>
    <Property Id="ARPPRODUCTICON" Value="icon.ico" />

这两句话放在Product节点下即可.
