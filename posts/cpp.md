# 安装c++运行库

基于vc做的产品,基本都需要带运行库的,
这篇是以运行库作为合并版本来说明的.

## 第一步,选中运行时合并模块

找的名称是`Microsoft_VC90_CRT_x86.msm`,
VC90可能是其他的,x86也可能是x64,这个合并包就在开发机上找,
目录是Merge Modules,如果找不到就用everything查找.

因为我们要的是运行库,所以找的是crt.

## 第二步,将合并包丢到安装包中

使用Merge/mergeRef节点来解决这个问题.

    <DirectoryRef Id="TARGETDIR">
        <Merge Id="VCRedist"
               SourceFile="MySourceFiles\Microsoft_VC80_CRT_x86.msm"
               DiskId="1"
               Language="0"/>
    </DirectoryRef>

    <Feature Id="VCRedist"
             Title="Visual C++ 8.0 Runtime"
             AllowAdvertise="no"
             Display="hidden"
             Level="1">
        <MergeRef Id="VCRedist"/>
    </Feature>

Merge有个id,后面会用到.在Feature中引用这个Merge.

注意:包含vc运行库会导致wix打印一些ice警告,忽略即可.
