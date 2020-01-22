# ES6 - Module

ES6 模块通过 `export` 命令显式指定输出的代码，再通过 `import` 命令输入，这种加载称为“编译时加载”或者静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 模块的加载方式高。当然，这也导致了没法引用 ES6 模块本身，因为它不是对象

除了静态加载带来的各种好处，ES6 模块还有以下好处

- 不再需要 `UMD` 模块格式了，将来服务器和浏览器都会支持 ES6 模块格式。目前，通过各种工具库，其实已经做到了这一点。
- 将来浏览器的新 API 就能用模块格式提供，不再必须做成全局变量或者 `navigator` 对象的属性
- 不再需要对象作为命名空间（比如 `Math` 对象），未来这些功能可以通过模块提供

ES6 的模块自动采用严格模式，不论是否加上 `"use strict"`;

严格模式的限制

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用 `with` 语句
- 不能对只读属性赋值，否则报错
- 不能使用前缀 0 表示八进制数，否则报错
- 不能删除不可删除的属性，否则报错
- 不能删除变量 `delete prop`，会报错，只能删除属性 `delete global[prop]`
- `eval` 不会在它的外层作用域引入变量
- `eval` 和 `arguments` 不能被重新赋值
- `arguments` 不会自动反映函数参数的变化
- 不能使用 `arguments.callee`
- 不能使用 `arguments.caller`
- 禁止 `this` 指向全局对象
- 不能使用 `fn.caller` 和 `fn.arguments` 获取函数调用的堆栈
- 增加了保留字（比如 `protected`、`static` 和 `interface`）

ES6 模块之中，顶层的 `this` 指向 `undefined`，即不应该在顶层代码使用 `this`

模块功能主要由两个命令构成：`export` 和 `import`。`export` 命令用于规定模块的对外接口，`import` 命令用于输入其他模块提供的功能

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取，若要让外部能够读取模块内部的某个变量，就必须使用 `export` 关键字输出该变量，`export` 命令除了输出变量，还可以输出函数或类（`class`）

```JavaScript
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;

// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export { firstName, lastName, year };
```

较为推荐的是下一种写法，因为这样就可以在脚本尾部，一眼看清楚输出了哪些变量

通常情况下，`export` 输出的变量就是本来的名字，但是可以使用 `as` 关键字重命名

需要特别注意的是，`export` 命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系

```JavaScript
// 报错
export 1;

// 报错
var m = 1;
export m;

// 正确写法如下

// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};
```

正确的写法，规定了对外的接口，其他脚本可以通过这个接口，取到对应的值，实质是，在接口名与模块内部变量之间，建立了一一对应的关系，`function` 和 `class` 的输出，也必须遵守这样的写法

另外，`export` 语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值

最后，`export` 命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错，`import` 命令也是如此，这是因为处于条件代码块之中，就没法做静态优化了，违背了 ES6 模块的设计初衷

`import` 命令接受一对大括号，里面指定要从其他模块导入的变量名。大括号里面的变量名，必须与被导入模块对外接口的名称相同，如果想为输入的变量重新取一个名字，`import` 命令要使用 `as` 关键字，将输入的变量重命名

`import` 命令输入的变量都是只读的，因为它的本质是输入接口。也就是说，不允许在加载模块的脚本里面，改写接口，但是，如果它是一个对象，改写它属性是允许的，不过，不要轻易改变它的属性

`import` 后面的 `from` 指定模块文件的位置，可以是相对路径，也可以是绝对路径，`.js`后缀可以省略。如果只是模块名，不带有路径，那么必须有配置文件，告诉 JavaScript 引擎该模块的位置

`import` 命令具有提升效果，会提升到整个模块的头部，首先执行

由于 `import` 是静态执行，所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构

```JavaScript
// 报错
import { 'f' + 'oo' } from 'my_module';

// 报错
let module = 'my_module';
import { foo } from module;

// 报错
if (x === 1) {
  import { foo } from 'module1';
} else {
  import { foo } from 'module2';
}
```

最后，`import` 语句会执行所加载的模块，如果多次重复执行同一句 `import` 语句，那么只会执行一次，而不会执行多次，也就是说，`import` 语句是 Singleton 模式

目前阶段，通过 Babel 转码，CommonJS 模块的 `require` 命令和 ES6 模块的 `import` 命令，可以写在同一个模块里面，但是最好不要这样做。因为 `import` 在静态解析阶段执行，所以它是一个模块之中最早执行的

除了指定加载某个输出值，还可以使用整体加载，即用星号（`*`）指定一个对象，所有输出值都加载在这个对象上面

注意，模块整体加载所在的那个对象，应该是可以静态分析的，所以不允许运行时改变

使用 `export default`，命令，为模块指定默认输出，其他模块加载该模块时，`import` 命令可以为该匿名函数指定任意名字，这时 `import` 命令后面，不使用大括号，一个模块只能有一个默认输出

本质上，`export default` 就是输出一个叫做 `default` 的变量或方法，所以它后面不能跟变量声明语句，可以直接将一个值写在 `export default` 之后

```JavaScript
// 正确
export var a = 1;

// 正确
var a = 1;
export default a;

// 错误
export default var a = 1;
```

可以与之前的 `import` 进行结合

```JavaScript
import _ from 'lodash';

// 如果想在一条 import 语句中，同时输入默认方法和其他接口

import _, { each, forEach } from 'lodash';
```

`export default` 也可以用来输出类

如果在一个模块之中，先输入后输出同一个模块，`import` 语句可以与 `export` 语句写在一起

```JavaScript
export { foo, bar } from 'my_module';

// 可以简单理解为
import { foo, bar } from 'my_module';
export { foo, bar };
```

写成一行以后，`foo` 和 `bar` 实际上并没有被导入当前模块，只是相当于对外转发了这两个接口，导致当前模块不能直接使用 `foo` 和 `bar`

模块的接口改名和整体输出，也可以采用这种写法

```JavaScript
// 接口改名
export { foo as myFoo } from 'my_module';

// 整体输出
export * from 'my_module';

// 默认接口

export { default } from 'foo';

// 具名接口改为默认接口

export { es6 as default } from './someModule';

// 等同于
import { es6 } from './someModule';
export default es6;

// 默认接口改名为具名接口

export { default as es6 } from './someModule';
```

有三种 `import` 语句，没有对应的复合写法

```JavaScript
import * as someIdentifier from "someModule";
import someIdentifier from "someModule";
import someIdentifier, { namedIdentifier } from "someModule";
```

模块之间也可以继承

```JavaScript
export * from 'circle';
export var e = 2.71828182846;
export default function(x) {
  return Math.exp(x);
}
```

上面代码中的 `export *`，表示再输出 `circle` 模块的所有属性和方法。注意，`export *` 命令会忽略 `circle` 模块的 `default` 方法。然后，上面代码又输出了自定义的 `e` 变量和默认方法

也可以将 `circle` 的属性或方法，改名后再输出

```JavaScript
export { area as circleArea } from 'circle';
```

加载

```JavaScript
import * as math from 'circleplus';
import exp from 'circleplus';
console.log(exp(math.e));
```

由于 `const` 声明的常量只在当前代码块有效，如果想设置跨模块的常量（即跨多个文件），或者说一个值要被多个模块共享，可以采用下面的写法

```JavaScript
// constants.js 模块
export const A = 1;
export const B = 3;
export const C = 4;

// test1.js 模块
import * as constants from './constants';
console.log(constants.A); // 1
console.log(constants.B); // 3

// test2.js 模块
import {A, B} from './constants';
console.log(A); // 1
console.log(B); // 3
```

如果变量过多，可以建一个专门的 `constants` 目录，将各种常量写在不同的文件里面，保存在该目录下，然后，将这些文件输出的常量，合并在 `index.js` 里面，使用时，加载 `index.js`

HTML 网页中，浏览器通过 `<script>` 标签加载 JavaScript 脚本，默认情况下，浏览器是同步加载 JavaScript 脚本，即渲染引擎遇到 `<script>` 标签就会停下来，等到执行完脚本，再继续向下渲染。如果是外部脚本，还必须加入脚本下载的时间

如果脚本体积很大，下载和执行的时间就会很长，因此造成浏览器堵塞，所以浏览器允许脚本异步加载，下面就是两种异步加载的语法

```HTML
<script src="path/to/myModule.js" defer></script>
<script src="path/to/myModule.js" async></script>
```

`defer` 与 `async` 的区别是：`defer` 要等到整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），才会执行；`async` 一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染

如果有多个 `defer` 脚本，会按照它们在页面出现的顺序加载，而多个 `async` 脚本是不能保证加载顺序的

浏览器加载 ES6 模块，也使用 `<script>` 标签，但是要加入 `type="module"` 属性

```HTML
<script type="module" src="./foo.js"></script>
```

浏览器对于带有 `type="module"` 的 `<script>`，都是异步加载，不会造成堵塞浏览器，即等到整个页面渲染完，再执行模块脚本，等同于打开了 `<script>` 标签的 `defer` 属性

ES6 模块也允许内嵌在网页中，语法行为与加载外部脚本完全一致

对于外部的模块脚本，需要注意的是

- 代码是在模块作用域之中运行，而不是在全局作用域运行。模块内部的顶层变量，外部不可见
- 模块脚本自动采用严格模式，不管有没有声明 `use strict`
- 模块之中，可以使用 `import` 命令加载其他模块（`.js` 后缀不可省略，需要提供绝对 URL 或相对 URL），也可- 以使用 `export` 命令输出对外接口
- 模块之中，顶层的 `this` 关键字返回 `undefined`，而不是指向 `window`。也就是说，在模块顶层使用 `this` 关键字，是无意义的
- 同一个模块如果加载多次，将只执行一次

利用顶层的 `this` 等于 `undefined` 这个语法点，可以侦测当前代码是否在 ES6 模块之中

ES6 模块与 CommonJS 模块的两个重大差异

- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用
- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口

CommonJS 模块输出的是值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值，除非写成一个函数，才能得到内部变动后的值

ES6 模块的运行机制与 CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令 `import`，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值，因此，ES6 模块是动态引用，并且不会缓存值，模块里面的变量绑定其所在的模块

最后，`export` 通过接口，输出的是同一个值。不同的脚本加载这个接口，得到的都是同样的实例
