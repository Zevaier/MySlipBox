# 《Maven实战》笔记

# 1. Maven坐标
**Maven坐标**是指在maven仓库中能够唯一标识构件的信息，一组maven坐标包括：

1. **groupId**: maven项目隶属的实际项目。一个实际项目往往会被划分为多个模块，因此可能不仅仅包含一个maven项目。此外，一个常见的误区是，groupId定义为隶属组织或公司的名称，因为一个公司不可能只有一个项目。
2. **artifactId**: 实际项目中的maven项目（模块）。推荐的做法是，groupId作为artifactId的前缀。而groupId中，可以使用公司名称作为前缀。
3. **version**: 版本号。
4. **packaging**: 打包方式。与扩展名对应，例如jar或者war。