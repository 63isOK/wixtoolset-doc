# 文件

安装包中最基本的元素是文件.

wix对文件的处理就3步.

## 定义目录结构

文件是跟着Directory节点走的,
下面是一个目录声明,而且是安装目录.

    <Directory Id="TARGETDIR" Name="SourceDir">
        <Directory Id="ProgramFilesFolder">
            <Directory Id="APPLICATIONROOTDIRECTORY" Name="My Application Name"/>
        </Directory>
    </Directory

分析一下:

- TARGETDIR是wix需要指明的,是所有安装目录的根
  - 每个wix项目中都需要指明这个
- ProgramFilesFolder是wix预定义的值,特指c盘的系统目录
- 第三个元素APPLICATIONROOTDIRECTORY就是我们需要安装的目录
  - 这个id对应的值后面还会用到的

最后,这段代码确定了安装目录 c:\Program Files\My Application Name .

## 添加文件

添加文件涉及两个节点:

- Component,表示安装的一个原子操作
- File,指明具体的文件

Component是用于描述资源的,不仅仅是文件,还不包含了注册表/快捷方式.
同时也可以利用Component来做逻辑功能的区分(完整/经典包含的资源是不一样的).

一个Component最好只包含一个File,这也是官方推荐的方式.
每个Component都有各自的guid.这两条规则最好遵循,
否则可能会出现奇奇怪怪的问题(微软告诉我们:只有这个场景是测试通过的).

    <DirectoryRef Id="APPLICATIONROOTDIRECTORY">
        <Component Id="myapplication.exe" Guid="PUT-GUID-HERE">
            <File Id="myapplication.exe"
             Source="MySourceFiles\MyApplication.exe"
             KeyPath="yes" Checksum="yes"/>
        </Component>
        <Component Id="documentation.html" Guid="PUT-GUID-HERE">
            <File Id="documentation.html"
             Source="MySourceFiles\documentation.html"
             KeyPath="yes"/>
        </Component>
    </DirectoryRef>

从上面的例子可以看出,Component可以挂在Directory的引用上.
APPLICATIONROOTDIRECTORY就是定义目录结构时指定的.

上面的例子是将两个文件安装到安装目录下,同时也遵循了两条规则:
每个Component只包含一个File;每个Component都带一个guid.

File节点才真正涉及打包,也有一个id,这个id其他地方会用到,
Source属性指明要打包文件的相对目录,KeyPath属性设置为yes,
是告诉wix这个文件是要安装的,如果KeyPath设置为no,
那么wix就选择下一个节点元素,直到选中为yes的.
不推荐让wix自己来选择,因为Component发生变动时会导致安装错误,
正确的姿势是手动指定KeyPath为yes,这个属性最好是放在不易变动的元素上,
什么意思?就是未来几个版本中都会出现的元素,指定为yes.
当然,如果一个Component只有一个File,那么很多问题就可以避免了.
无脑设置为yes即可.最后Checksum属性,对于可执行来说,设置为yes,
这是为了重装时进行校验.

## 告诉wix安装文件

第一步定义目录,第二步定义文件,第三步告诉wix哪些文件是要安装的.
在第三步会用到Feature节点,这里会有一个逻辑功能分支,
不同的分支安装不同的文件,对应我们常常看到的"典型安装/完整安装...".

    <Feature Id="MainApplication" Title="Main Application" Level="1">
        <ComponentRef Id="myapplication.exe" />
        <ComponentRef Id="documentation.html" />
    </Feature>

Feature也有id,这里用ComponentRef来引用第二步列出的文件.
