## Excel Add ins 踩坑

使用共享文件夹添加加载项，需在受信任的加载项目录添加xml所在目录，并勾上在列表中显示，否则加载项清单页面不显示

先用yeoman office建立Add in的HTML+CSS+JS框架，再加入Vue全家桶
配置vue-loader, css-loader, vue-style-loader, stylus-loader
element-ui正常使用需给ttf配置file-loader

#### 关闭https  

如果不上AppSource 用npm包Office-js代替CDN脚本


object.load 是一个异步的方法，要调用context.sync()后才能做进一步操作

用await context.sync()代替教程中提到的sync的promise写法