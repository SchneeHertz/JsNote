## 将puppeteer自带的Chromium打包进Electron安装包中

使用electron-vue模板  
引入puppeteer模块后，用`npm run build:dir`打包，electron会将node_module/puppeteer文件夹复制到resources/app.asar.unpacked文件夹内，未搜索到是electron-vue的功能还是puppeteer的功能。  
但打包的软件内有chromium，puppeteer还是不能正常工作，因为puppeteer.launch的option内没有默认将executablePath设置为chromium可执行文件的路径，需要手动设置

在执行puppeteer.launch时需增加如下代码

```javascript
const getExecuablePath = () => {
  if (process.env.NODE_ENV !== 'development') {
    return puppeteer.executablePath().replace('app.asar', 'app.asar.unpacked')
  } else {
    return puppeteer.executablePath()
  }
}
const browser = await puppeteer.launch({
  executablePath: getExecuablePath()
})
```

之后在production环境的puppeteer即可正常运行