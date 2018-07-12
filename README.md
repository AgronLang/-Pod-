# 创建开源私有Pod流程

1.利用pod默认模版创建新工程  pod lib create MyLibrary


----------


2.创建远端项目仓库，将本地仓库与远端仓库进行关联

- git命令：git push -u origin master
- 创建podspec仓库，此仓库只用于存放.podspec，跟项目仓库彼此独立；
- 多个项目可以公用一个podspec仓库，多项目目录结构：
![图片描述](/tfl/pictures/201807/tapd_20072991_1531370841_72.png)


----------



3. 编辑.podspec文件，常用属性解释
   name：名称，pod search 搜索的关键词,注意这里一定要和.podspec的名称一样,否则报错
.version：版本号
.ios.deployment_target:支持的pod最低版本
.source:项目地址
.source_files:需要包含的源文件
.dependency：依赖的三方库
.frameworks：依赖的系统的框架
详细参考：https://guides.cocoapods.org/syntax/podspec.html

----------


4.上传
提交修改并给这次提交打上tag并push


----------


5.Add your Podspec to your repo
打完tag后运行命令：
pod repo push REPO_NAME SPEC_NAME.podspec


----------


6.验证
pod lib lint SPEC_NAME.podspec 有警告不会通过此命令验证
pod lib lint SPEC_NAME.podspec --allow-warnings 可以忽略警告


----------


7.发布
pod repo push REPO_NAME SPEC_NAME.podspec
