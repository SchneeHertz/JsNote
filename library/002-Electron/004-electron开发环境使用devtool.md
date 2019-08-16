## electron开发环境使用devtool

electron-vue默认是自带devtool的，但dev环境不能正常加载，只好自己添加。  
在main/index.js文件中的createWindow函数中添加以下代码，加载本机已安装的devtool。

```javascript
function createWindow () {
  \\...
  if (process.env.NODE_ENV === 'development') {
    BrowserWindow.addDevToolsExtension('C:\\Users\\用户名\\AppData\\Local\\Google\\Chrome\\User Data\\Default\\Extensions\\nhdogjmejiglipccpnnnanhbledajbpd\\5.1.1_0')
  }
  \\...
}
```