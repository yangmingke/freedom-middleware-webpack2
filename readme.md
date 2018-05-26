### freedom-middleware-webpack2构建中间件

该中间件使用webpack2对项目进行构建，中间件统一管理了项目开发中大概95%以上的构建配置。使用该中间件对项目构建时，中间件在运行的时候会自动合并项目中的webpack.config.js(**构建项目必须存在此文件**)文件，然后再进行项目的构建。

### freedom-middleware-webpack2构建中间件支持构建的项目

- 使用less、sass、ts、vue、ejs,jade以及es6开发的项目
- 中间件生成的webpack.config.js**允许开发者根据项目需要自行扩展项目的构建配置或者覆盖中间件本身的配置**
- 中间件生成的.babelrc文件**允许开发者自行定义babel相关构建配置**
- 中间件生成的tsconfig.json**允许开发者自行定义ts编译选项**
- postcss.config.js**允许开发者自行定义样式处理方式**

### freedom-middleware-webpack2安装

```
npm install freedom-middleware-webpack2
```

### freedom-middleware-webpack2构建中间件使用

```js
var webpackBuild = require("freedom-middleware-webpack2");
(async function () {
  var params = {
    port: 9090,
    env: "dev",
    publicPath: `//static.51talk.com/oneTomany/0.0.1`,
    build: `build`,
    proxy: {
      context: ["/api", "/auth","/award"],
      options: {
        target: 'http://localhost:8080'
      }
    }
  };
  await webpackBuild(params);
})();
```



### freedom-middleware-webpack2构建中间件的参数说明

```json
{
  "port":"本地环境dev启动的端口后",
  "env":"环境变量，dev:开发环境；prod：生成环境",
  "publicPath":"构建资源的替换路径，比如：css中的图片路径",
  "build":"生产环境prod构建的资源存放的目录，在dev环境中该值忽略",
  "proxy":{//反向代理设置
    "context":["/api", "/auth","/award"],//要拦截的url
    "options":{//设置代理端口
      "target": 'http://localhost:8080'	
    }
  }
}
```

### 备注

构建项目下必须要有webpack.config.js文件，配置(**webpack的配置格式**)如下:

```js
module.exports = function () {
  var extendConf = {
    plugins: [
      
    ],
    resolve: {
     
    },
    module: {
      rules: [
        
      ]
    }
  };
  return extendConf;
};
```


