## 简介
`release.js`用来合并RCE pc端和web端的代码。 

&emsp;该工具将合并后的代码输出到特定目录，不影响项目源码。

## 规则

1. 使用前必须已正确安装全局node以及npm。
2. 需要合并的js，css必须以script或link标签的形式定义在inc/head-static.html中。
3. 合并的规则由用户在head-static.html中的引入决定，在head-static.html中相同_group命名的文件将合并在一起。
4. 相同\_group的js或css，引入必须相邻，中间不能插入不同名字\_group的引入。
5. js定义必须遵循js模块化规范。
6. js文件中'use strict'; 不能全部放到全局，可以在js文件的最外层函数开始处加'use strict’;

 #### head-static.html示例：
 ```
 <script src="modules/upload/qiniu.js" _group="upload"></script>
 <script src="modules/upload/upload.js" _group="upload"></script>
 <script src="modules/upload/init.js" _group="upload"></script>

 <script src="lib/moment-2.17.1.js" _group="cmpt"></script>
 <script src="js/utils.js" _group="cmpt"></script>
 <script src="js/common.js" _group="cmpt"></script>
 ```
 
## 格式
```
node release.js <path> [output] [-c]
```

## 参数：

|参数名|描述|是否必填|
|------|------|----|
|path|源码目录|Yes|
|output|合并后代码的输出目录|No|
|-c|是否压缩|No|

## 示例
1. **`推荐`**将release.js与RCE源码放在同一个目录。执行如下终端命令：

    ```
    node release.js ./desktop-client -c
    ```
    结果：将会把./desktop-client目录中的源码合并压缩，输出到当前目录的release文件夹中。

2. 	只合并不压缩。设置源码路径./desktop-client，设置输出路径../desktop-release：

	```
	node release.js ./desktop-client ../desktop-release
	```
	结果：将./desktop-client目录中的源码合并，但不压缩，输出到../desktop-release文件夹中。

3. 压缩且合并。设置源码路径./desktop-client，设置输出路径../desktop-release：

	```
	node release.js ./desktop-client ../desktop-release -c
	```
	结果：将./desktop-client目录中的源码合并压缩，输出到../desktop-release文件夹中。
