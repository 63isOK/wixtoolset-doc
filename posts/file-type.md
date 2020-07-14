# 文件类型

wix工具链中,每个工具都会生成一些中间文件,
这个部分就是来认识这些不同类型的文件.

从顶层来看,输入的wxs源文件,输出的是安装包文件.

- wxi,wix include file, 类似头文件(对应c++中的.h文件)
- wxl,wix localization file, 本地化文件
- wxs,wix source file, 源文件(对应c++中的.cpp文件)
- wixobj,wix object file, 每个源文件编译之后的中间文件
- wixout,wix xml output file, 链接器输出的文件,是最终文件的xml版本
- wxipdb,wix debug file, 链接器为最终文件生成的调试文件
- wixmsp,wix xml patch file, 补丁文件的xml版本
- wixmst,wix transform file, 两个最终文件的差异文件,也是xml版本
- msi,安装包
- msm,合并到msi中的合并模块
- mst,变更包
- pcp,分支包

## wxs文件结构

- 有个根节点Wix
- Wix节点下可以包含Product/Module/Patch/Fragment
  - 编译过后,每个子节点在wixobj中会生成一个section
  - 一般会有3个section经常会被引用
- Product/Module/Patch只会出现一个
  - 因为这个被称为入口,对应的section叫入口section
  - 入口section也是链接程序处理的开始点
- section节点下的子元素定义在db中
  - 这个db称为安装包数据库,有专门的工具可以查看
  - 可以用Property子元素定义属性表
  - 可以用Directory子元素定义目录表
  - 大部分子元素都有一个id属性
    - 这个id决定了编译顺序(可理解为数据库中的主键)

## wixobj文件中的符号和引用

wixobj中,每个符号都是子元素名+唯一号组成,
唯一号取值上节的id属性.

- 符号很重要,尤其是引用其他源文件中的其他section
  - eg:文件可以输出到不同目录
    - Directory定义在Fragment,Fragment可能在另一个源文件
- 显示地将DirectoryRef作为Component的父节点
  - 此时链接器会将Directory的符号拼接起来,放到一个安装包中
  - 有时,隐式引用是编译器生成的

wix工具链还支持复杂引用.链接器生成额外信息可以使用复杂引用.
Feature/Component就是复杂引用的一个例子.
当Feature通过ComponentRef显式引用一个Component时,
链接器需要将Feature和Component的符号和一个入口
添加到FeatureComponents表中.

Feature/Component的关系很复杂,因为Component可能还有Shortcut.
Component下元素的引用称为反向引用或者反向链接.
链接器处理的困难工作在于复杂引用和反向链接.

## wixobj文件结构

一个源文件,一个obj.obj遵循的是object.xsd.
obj包含很多section,也包含符号和引用.

obj中最重要片段就是符号和引用.但这块占用的非常少,
大部分是table/row/field元素,这些元素用于描述db.
