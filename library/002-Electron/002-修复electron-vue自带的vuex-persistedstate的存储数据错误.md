## 修复electron-vue自带的vuex-persistedstate的存储数据错误

vuex-persistedstate模块可以存储vuex的临时数据，在轻量使用的时候，可以代替数据库的功能，但使用上有两处不便：  
1.  未知vuex-persistedstate模块的数据存储位置，无法读取到已存储的数据
2. 如直接更改代码更新vuex状态，则vuex-persistedstate存储的数据会出错

所以，使用lowdb代替vuex-persistedstate默认的localStorage作为数据存储，便于读取数据和重置数据

vuex-persistedstate的文档说明了，自定义storage是通过storage选项实现的

```javascript
createPersistedState({
  storage: {
    getItem: key => Cookies.get(key),
    setItem: (key, value) =>
      Cookies.set(key, value, { expires: 3, secure: true }),
    removeItem: key => Cookies.remove(key),
  }
})
```
可以看到，自定义storage需要提供一个具有getItem, setItem, removeItem三个方法的对象。

但由于electron-vue模板自带的vuex-persistedstate模块未更新到github的最新版本，旧版本的vuex-persistedstate这三个方法的标识符实际是get, set, delete

故修改如下：
```javascript
createPersistedState({
  storage:{
    get: (key)=>{
      return db.get(key).value()
    },
    set: (key, value)=>{
      db.set(key, value).write()
    },
    delete: (key)=>{
      db.unset(key).write()
    }
  }
})
```