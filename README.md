#h5package

## 总览
``h5package`` 是高等教育出版社发布的HTML5程序打包规范。
为了更好的展现和管理HTML5资源包，本项目约定HTML5程序包的目录和文件结构。
本项目是一个样例包。


## 细则

1 每个资源包都需要有一个索引文件 命名为 ``index.html`` 

2 文件名中不可包含非英文字符，包括中文符号、全角标点符号等。

3 对于每个资源包 都有一个``package.json`` 描述本资源包，例子文件见package.json

4 文件中只允许有相关连的文件，如果一个文件没有关联，则不应出现在包中。

5 文件中不允许出现 ``exe`` ``php`` ``jsp`` ``asp`` 等可执行文件或者脚本。

6 所有文件中不可以出现违反互联网及相关法律的内容和文字，不得包含木马、病毒等的恶意代码和插件。

7 所有文件 以``zip``压缩，后缀为 .hep5 的方式提交

8 单个文件大小不超过10M，总项目包大小不超过100M

## 建议
1 所有文件文件名都采用小写英文字母和数字构成。

2 所有文件都在同一级目录下，不新建子目录。

3 可以选用js css cdn库，推荐的库有：

``https://www.staticfile.org/``
``http://www.bootcdn.cn/``
等,使用CDN的时候，请在package中注明。


## 权限

如果上传到二维码平台，则跳转到这个包的时候会给授权token，加上token的权限判断，则这个包就可以实现只能从二维码平台跳转过来的才可以访问

示例代码如下
```
<script src="//2d.hep.cn/libs/jquery/dist/jquery.min.js"></script>
<script>
  var reg = `(^|&)token=([^&]*)(&|$)`
  var token = window.location.search.substr(1).match(reg)
  $(document).ready(function () {
    if (token) {
      $.getJSON("//2d.hep.cn/api/v1/validToken?" + token, {},
        function (data, textStatus, jqXHR) {
          if (data.success === false) {
            if (data.fromURL) {
              window.location = data.fromURL
            } else {
              // 这里 可以直接关闭当前页面，跑到这里面来，说明不是从二维码平台跳过去的，
              // 所以我也不知道原始路径是哪里，直接不让访问即可。
            }
          }
        }
      )
    }
  })
</script>

```

## 其他

如果你用webpack 可以直接在脚本中增加打包的功能 代码示例如下：

```
npm i webpack-zip-plugin --save-dev


var WebpackZipPlugin = require('webpack-zip-plugin')
new WebpackZipPlugin({
      initialFile: './dist', //需要打包的文件夹(一般为dist)
      endPath: './', //打包到对应目录（一般为当前目录'./'）
      zipName: 'dgs.hep5' //打包生成的文件名
    })

```
有意见和建议，请提交到 ``issue``中，欢迎fork并贡献代码。


