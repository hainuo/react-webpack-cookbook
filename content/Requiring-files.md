## 模块

Webpack 允许你使用不同的模块类型，但是 “底层”必须使用同一种实现。所有的模块可以直接在盒外运行。

#### ES6 模块

```javascript
import MyModule from './MyModule.js';
```

#### CommonJS

```javascript
var MyModule = require('./MyModule.js');
```

#### AMD

```javascript
define(['./MyModule.js'], function (MyModule) {

});
```

## 理解文件路径

一个模块需要用它的文件路径来加载，看一下下面的这个结构：

- /app
  - /modules
    - MyModule.js
  - main.js (entry point)
  - utils.js

打开 *main.js* 然后可以通过下面两种方式引入 *app/modules/MyModule.js* 

*app/main.js*
```javascript
// ES6
import MyModule from './modules/MyModule.js';

// CommonJS
var MyModule = require('./modules/MyModule.js');
```

最开始的 `./` 是 “相对当前文件路径” 

让我们打开 *MyModule.js* 然后引入 **app/utils**：

*app/modules/MyModule.js*
```javascript
// ES6 相对路径
import utils from './../utils.js';

// ES6 绝对路径
import utils from '/utils.js';

// CommonJS 相对路径
var utils = require('./../utils.js');

// CommonJS 绝对路径
var utils = require('/utils.js');
```

**相对路径**是相对当前目录。**绝对路径**是相对入口文件，这个案例中是*main.js*

### 我需要使用文件后缀么？

不，你不需要去特意去使用 *.js*，但是如果你引入之后高亮会更好。你可能有一些 .js 文件和一些 .jsx 文件，甚至一些图片和 css 可以用 Webpack 引入，甚至可以直接引入 node_modules 里的代码和特殊文件。

记住，Webpack 只是一个模块合并！也就是说你可以设置他去加载任何你写的匹配，只要有一个加载器。我们稍后会继续深入这个话题。