# 如何引用DriectorySearch元素

场景:需要找到统一目录下的不同文件,或不同子目录,
并给这些文件和目录附上不同的属性,此时就需要这篇文章来指导.

DirectorySearch元素不能定义多次,所以要用DirectorySearchRef,

## 第一步,定义DirectorySearch

先定义一个DirectorySearch作为搜索的父目录

    <Property Id="SHDOCVW">
        <DirectorySearch Id="WinDir" Path="[WindowsFolder]">
            <DirectorySearch Id="Media" Path="Media">
                <FileSearch Id="Chimes" Name="chimes.wav" />
            </DirectorySearch>
        </DirectorySearch>
    </Property>

这个是搜索Media目录下的chimes.wav,如果这个文件找到了,
文件的全路径就会被赋值给SHDOCVM.

## 定义DirectorySearchRef

此时我们需要查找Media目录下的其他文件,那需要3个信息:
id,父id,Path属性.

    <Property Id="USER32">
        <DirectorySearchRef Id="Media" Parent="WinDir" Path="Media">
            <FileSearch Id="Chord" Name="chord.wav" />
        </DirectorySearchRef>
    </Property>

通过Id/Parent/Path,我们引用了第一步中的DirectorySearch节点,
如果我们要查找其他父目录下的Media元素,怎么办?
此时不能复用id为Media的DirectorySearch了,
应该按步骤1中的方式重新定义一个DirectorySearch.
