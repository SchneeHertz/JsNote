## Koa Post 长度限制

Koa配套的koa-bodyparser软件包，默认Post的参数长度不能超过一个大小，可在调用时修改这个大小，如下

```
app.use(bodyParser({
    jsonLimit: '32mb'
}))
```