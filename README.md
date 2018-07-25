# 创建开源私有Pod流程

1.利用pod默认模版创建新工程 

-  pod lib create MyLibrary

----------


2.创建远端代码库，将本地仓库与远端代码库进行关联

- 关联命令：git remote add origin 远程仓库地址

----------

3.创建远端版本库，只用于存放.podspec文件，和代码库互相独立；
&nbsp;&nbsp;&nbsp;注意：多个项目可以共用一个版本库 附图

![图片描述](/tfl/pictures/201807/tapd_20072991_1531447691_49.png)


----------

4.将远程版本库下载到本地，SOURCE_URL指的是版本库的地址；通过这个命令就能搜索和安装私有库了

- pod repo add REPO_NAME SOURCE_URL

----------

5.编辑.podspec文件，如果要依赖其它私有库
常用属性解释

- name：名称，pod search 搜索的关键词,注意这里一定要和.podspec的名称一样,否则报错
- version：版本号
- ios.deployment_target:支持的pod最低版本
- source:项目地址
- source_files:需要包含的源文件
- dependency：依赖的三方库
- frameworks：依赖的系统的框架
详细参考：https://guides.cocoapods.org/syntax/podspec.html

----------

6.push代码并打上tag

----------

7.验证

- pod lib lint SPEC_NAME.podspec 有警告不会通过此命令验证
- pod lib lint SPEC_NAME.podspec --allow-warnings 可以忽略警告

注意：如果依赖其它私有库，需要在验证命令后面加上如下参数
 --sources='私有podspec库地址, https://github.com/CocoaPods/Specs.git'
并在工程podfile中添加指定source，例如：

![图片描述](/tfl/pictures/201807/tapd_20072991_1531452117_14.png)

如果报错 ··· error: include of non-modular header inside framework module ··· [-Werror,-Wnon-modular-include-in-framework-module]
解决办法：在pod lib lint 或者 pod spec lint 以及 pod repo push ....时候加上   --use-libraries

----------


8.发布

- pod repo push REPO_NAME SPEC_NAME.podspec

- pod lib lint SPEC_NAME.podspec --allow-warnings 可以忽略警告


----------
