# Maven

## 安装maven
1. 下载maven
2. 解压
3. 将bin目录加入环境变量

## 设置本地仓库位置
  修改setting.xml，添加<localRepository>标签，设置本地仓库位置。
> setting.xml位于maven目录下的/conf


## 新建项目
在项目目录下，执行
`mvn archetype:generate`