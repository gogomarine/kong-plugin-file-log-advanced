# kong-plugin-file-log-advanced
Extension of the built-in Kong file-log plugin

## KONG文档升级

[KONG 3.X 插件自定义开发](https://docs.konghq.com/gateway/3.0.x/plugin-development/custom-logic/) ，有一些控件已经升级

```lua
--  DEPRECATED --
local BasePlugin = require "kong.plugins.base_plugin"
local CustomHandler = BasePlugin:extend()
CustomHandler.VERSION  = "1.0.0"
CustomHandler.PRIORITY = 10
```

需要切换一下代码

```lua
local CustomHandler = {
  VERSION  = "1.0.0",
  PRIORITY = 10,
}
```

## 版本会跟着KONG走


### 部署

这个比较有意思的是，rockspec 更像是一个声明，通过这个声明文件，告诉源码在什么地方。然后会从源码Clone后，再部署，意味着不会从本地发布；必须先Push

```shell
luarocks upload kong-plugin-file-log-advanced-3.0.0-1.rockspec --api-key=your-api-key
```

### 报错解决

```log

2022/10/09 11:51:25 [error] 187197#0: init_by_lua error: /usr/local/share/lua/5.1/kong/tools/utils.lua:701: error loading module 'kong.plugins.file-log-advanced.handler':
...share/lua/5.1/kong/plugins/file-log-advanced/handler.lua:6: module 'kong.plugins.base_plugin' not found:No LuaRocks module found for kong.plugins.base_plugin

```

