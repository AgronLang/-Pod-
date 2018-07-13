# 创建开源私有Pod流程

1.利用pod默认模版创建新工程 

-  pod lib create MyLibrary

----------


2.创建远端代码库，将本地仓库与远端代码库进行关联

- 关联命令：git push -u origin master

----------

3.创建远端版本库，只用于存放.podspec文件，和代码库互相独立；
&nbsp;&nbsp;&nbsp;注意：多个项目可以共用一个版本库 附图

![图片描述](/tfl/pictures/201807/tapd_20072991_1531447691_49.png)


----------

4.将远程版本库添加到本地，SOURCE_URL指的是版本库的地址

- pod repo add REPO_NAME SOURCE_URL

----------

5.编辑.podspec文件，常用属性解释

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


----------


8.发布

- pod repo push REPO_NAME SPEC_NAME.podspec
