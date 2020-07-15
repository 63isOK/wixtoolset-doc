# 文件的版本

在安装过程中,可能有检查文件版本的需求.
一般文件版本的检测和条件语句配合,
常用在文件丢失,或依据文件版本来显示不同的安装界面.

## 文件搜索

使用Property/DirectorySearch/FileSearch节点来搜索文件,

    <Property Id="USER32VERSION">
        <DirectorySearch Id="SystemFolderDriverVersion" Path="[SystemFolder]">
            <FileSearch Name="user32.dll" MinVersion="6.0.6001.1750"/>
        </DirectorySearch>
    </Property>

Property节点也有id属性,后面的条件语句会用到这个id.
DirectorySearch节点用于构建目录层次结构,用来做搜索用,
她的Path可以指定为系统路径.
FileSearch指明要搜索的文件和最低版本.

wix对最低版本有点不好处理,所以源码中要搜索的版本要比实际版本小一点,
这样才能正确搜索到,如果版本一样,wix是搜索不到的.

## 配合条件逻辑使用

一旦找到符合版本的文件,就可以配合条件语句来做一些事情

    <Condition Message="The installed version of user32.dll
      is not high enough to support this installer.">
        <![CDATA[Installed OR USER32VERSION]]>
    </Condition>

这里面的Installed表示安装包处于安装状态,而不是修复或卸载状态.
整个意思是达到某个条件,显示一条信息.

USER32VERSION就是上面Property节点的id属性,如果版本符合且文件存在,
那么这个id对应的是文件的全路径.
