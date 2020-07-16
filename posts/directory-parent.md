# 获取一个文件的父目录

## 第一步,定义查找的根节点

不定义这个查找根节点,wix会查找所有符合条件的目录,
这样就不好处理了,所以源码中要定义根节点的.

    <Property Id="NGEN2DIR">
        <DirectorySearch Id="Windows" Path="[WindowsFolder]">
            <DirectorySearch Id="MS.NET" Path="Microsoft.NET">
            </DirectorySearch>
        </DirectorySearch>
    </Property>

要搜索的目录是[WindowsFolder]Microsoft.NET 

## 定义要查找的父目录

这个是在上面的基础上继续做的.

    <Property Id="NGEN2DIR">
        <DirectorySearch Id="Windows" Path="[WindowsFolder]">
            <DirectorySearch Id="MS.NET" Path="Microsoft.NET">
                <DirectorySearch Id="Ngen2Dir" Depth="2" AssignToProperty="yes">
                    <FileSearch Id="Ngen_exe" Name="ngen.exe" MinVersion="2.0.0.0" />
                </DirectorySearch>
            </DirectorySearch>
        </DirectorySearch>
    </Property>

AssignToProperty设置为yes,最后文件找到后,父目录的全路径丢在了Ngen2Dir.
