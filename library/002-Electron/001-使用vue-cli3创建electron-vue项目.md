## 使用vue-cli3创建electron-vue项目

electron-vue久未更新，创建项目的脚手架还停留在vue-cli2。  
vue-cli更新到3.x之后，使用模板创建项目的命令和2.x的有差异，如果安装的vue-cli是3.x的版本，需要安装@vue/cli-init

```javascript
npm install -g @vue/cli-init
```

再按文档拉取模板

```javascript
vue init simulatedgreg/electron-vue my-project
```