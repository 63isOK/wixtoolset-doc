# 预处理

其中一个预处理是编译期的条件分支.

或许对运行库的判断可以用上.

    如果是企业版,会多编译一个东东
    <?if $(env.MySku) = Enterprise ?>
      <?include EnterpriseFeature.wxi ?>
    <?endif ?>

上面的例子中有个include节点.
一般include节点都是作为根节点出现的.

## 变量

除了自定义变量,还有一些wix定义的变量:

- $(env._NtPostBld), 表示环境变量 %_NtPostBld%
- $(sys.CURRENTDIR), 表示系统变量中的当前目录
- $(var.A), 表示源码中定义的A变量

对于环境变量,是区分大小写的.

对于系统变量,都是大写的:

- CURRENTDIR,构建活动针对的目录
- SOURCEFILEPATH,文件的全路径
- SOURCEFILEDIR,文件目录
- BUILDARCH,构建的平台,编译时可以通过参数-arch来指定

所有系统内置目录都是以\结尾的.

自定义变量有两种:源码定义和candle编译时指定.
这些变量可以用在判断逻辑上.

    自定义变量
    <?define MyVariable = “Hello World” ?>
    <?define MyVariable = “$(var.otherVariableContainingSpaces)” ?>
    <?define MyVariable = $(var.BuildPath)\x86\bin\ ?>
    取消定义
    <?undef MyVariable ?>

    candle时定义变量
    candle.exe -dMyVariable="Hello World" ...

## 判断逻辑

if else elseif, 这块后面使用的不多,所以略过.

## 错误和警告

    可用在版本冲突上
    <?ifndef RequiredVariable ?>
        <?error RequiredVariable must be defined ?>
        <?warning warning-message?>.
    <?endif?>

## 迭代语句/转义

无

## 函数

    $(fun.AutoVersion(x.y))

这是唯一的预处理函数,支持自动生产版本.

