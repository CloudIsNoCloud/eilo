# ES6 - Class

JavaScript 生成实例对象的传统方法是通过构造函数，这传统的面向对象语言（比如 C++ 和 Java）差异很大，所以引入了 Class（类）这个概念

ES6 的 `class` 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 `class` 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已，它跟普通构造函数的一个主要区别，后者不用 `new` 也可以执行

```JavaScript
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);

// 等同于

class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

ES6 的类，完全可以看作构造函数的另一种写法，类的数据类型就是函数，类本身就指向构造函数，使用时直接对类使用 `new` 命令，跟构造函数的用法完全一致

```JavaScript
class Point {
  // ...
}

typeof Point // "function"
Point === Point.prototype.constructor // true
```

类的所有方法都定义在类的 `prototype` 属性上面，在类的实例上面调用方法，其实就是调用原型上的方法

```JavaScript
class Point {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }

  toValue() {
    // ...
  }
}

// 等同于

Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
};
```

由于类的方法都定义在 `prototype` 对象上面，所以类的新方法可以添加在 `prototype` 对象上面。`Object.assign` 方法可以很方便地一次向类添加多个方法，当然，也可以用 `...{}` 的方式

```JavaScript
class Point {
  constructor(){
    // ...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});

Point.prototype = { ...{
    toString(){},
    toValue(){}
  }
}
```

类的内部所有定义的方法，都是不可枚举的（non-enumerable）

`constructor` 方法默认返回实例对象（即 `this`），完全可以指定返回另外一个对象

```JavaScript
class Foo {
  constructor() {
    return Object.create(null);
  }
}

new Foo() instanceof Foo
// false
```

类的所有实例共享一个原型对象，这也意味着，可以通过实例的 `__proto__` 属性为“类”添加方法，使用实例的 `__proto__` 属性改写原型，必须相当谨慎，不推荐使用，因为这会改变“类”的原始定义，影响到所有实例

```JavaScript
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__.printName = function () { return 'Oops' };

p1.printName() // "Oops"
p2.printName() // "Oops"

var p3 = new Point(4,2);
p3.printName() // "Oops"
```

在“类”的内部可以使用 `get` 和 `set` 关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为，存值函数和取值函数是设置在属性的 Descriptor 对象上的

```JavaScript
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

类的属性名，可以采用表达式

```JavaScript
let methodName = 'getArea';

class Square {
  constructor(length) {
    // ...
  }

  [methodName]() {
    // ...
  }
}
```

类也可以使用表达式的形式定义

```JavaScript
const MyClass = class Me {
  getClassName() {
    return Me.name;
  }
};

let inst = new MyClass();
inst.getClassName() // Me
```

采用 Class 表达式，可以写出立即执行的 Class

```JavaScript
let person = new class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}('张三');

person.sayName(); // "张三"
```

需要注意

- 类和模块的内部，默认就是严格模式
- 类不存在变量提升（hoist）
- ES6 的类只是 ES5 的构造函数的一层包装，所以函数的许多特性都被 Class 继承，包括 `name` 属性
- 如果某个方法之前加上星号（`*`），就表示该方法是一个 Generator 函数
- 类的方法内部如果含有 `this`，它默认指向类的实例，但是单独使用该方法，很可能报错

关于静态方法

- 如果在一个方法前，加上 `static` 关键字，就表示该方法不会被实例继承，而是直接通过类来调用，称为“静态方法”
- 如果在实例上调用静态方法，会抛出一个错误，表示不存在该方法，如果静态方法包含 `this` 关键字，这个 `this` 指的是类，而不是实例
- 父类的静态方法，可以被子类继承
- 静态方法也是可以从 super 对象上调用的

静态属性指的是 Class 本身的属性，即 `Class.propName`，而不是定义在实例对象（`this`）上的属性

```JavaScript
// 老写法
class Foo {
  // ...
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
```

私有方法和私有属性，是只能在类的内部访问的方法和属性，外部不能访问，但 ES6 不提供，只能通过变通方法模拟实现

- 在命名上加以区别，即在静态方法的命名前加上 `_`，但是，在类的外部，还是可以调用到这个方法
- 将私有方法移出模块，因为模块内部的所有方法都是对外可见的
- 利用 `Symbol` 值的唯一性，将私有方法的名字命名为一个 `Symbol` 值，一般情况下无法获取到它们，因此达到了私有方法和私有属性的效果，`Reflect.ownKeys()` 依然可以拿到它们

ES6 为 `new` 命令引入了一个 `new.target` 属性，该属性一般用在构造函数之中，返回 `new` 命令作用于的那个构造函数。如果构造函数不是通过 `new` 命令或 `Reflect.construct()` 调用的，`new.target` 会返回 `undefined`，因此这个属性可以用来确定构造函数是怎么调用的

Class 内部调用 `new.target`，返回当前 Class，需要注意的是，子类继承父类时，`new.target` 会返回子类，利用这个特点，可以写出不能独立使用、必须继承后才能使用的类

```JavaScript
class Shape {
  constructor() {
    if (new.target === Shape) {
      throw new Error('本类不能实例化');
    }
  }
}

class Rectangle extends Shape {
  constructor(length, width) {
    super();
    // ...
  }
}

var x = new Shape();  // 报错
var y = new Rectangle(3, 4);  // 正确
```

Class 可以通过 extends 关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多，父类的静态方法，也会被子类继承

`Object.getPrototypeOf` 方法可以用来从子类上获取父类

`super` 这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同

- `super` 作为函数调用时，代表父类的构造函数。ES6 要求，子类的构造函数必须执行一次 `super` 函数，`super()` 只能用在子类的构造函数之中，用在其他地方就会报错，`super()` 内部的 `this` 指向的是子类
- `super` 作为对象时，在普通方法中，指向父类的原型对象，所以定义在父类实例上的方法或属性，是无法通过 `super` 调用的；在静态方法中，指向父类

在子类普通方法中通过 `super` 调用父类的方法时，方法内部的 `this` 指向当前的子类实例，所以如果通过 `super` 对某个属性赋值，这时 `super` 就是 `this`，赋值的属性会变成子类实例的属性

如果 `super` 作为对象，用在静态方法之中，这时 `super` 将指向父类，而不是父类的原型对象，另外，在子类的静态方法中通过 `super` 调用父类的方法时，方法内部的 `this` 指向当前的子类，而不是子类的实例

注意，使用 `super` 的时候，必须显式指定是作为函数、还是作为对象使用，否则会报错

由于对象总是继承其他对象的，所以可以在任意一个对象中，使用 `super` 关键字

Class 作为构造函数的语法糖，同时有 `prototype` 属性和 `__proto__` 属性，因此同时存在两条继承链

- 子类的 `__proto__` 属性，表示构造函数的继承，总是指向父类
- 子类 `prototype` 属性的 `__proto__` 属性，表示方法的继承，总是指向父类的 `prototype` 属性

```JavaScript
class A {
}

class B extends A {
}

B.__proto__ === A // true
B.prototype.__proto__ === A.prototype // true

// 这样的结果是因为，类的继承是按照下面的模式实现的

class A {
}

class B {
}

// B 的实例继承 A 的实例
Object.setPrototypeOf(B.prototype, A.prototype);

// B 继承 A 的静态属性
Object.setPrototypeOf(B, A);

const b = new B();

// Object.setPrototypeOf方法的实现
Object.setPrototypeOf = function (obj, proto) {
  obj.__proto__ = proto;
  return obj;
}

// 结果
Object.setPrototypeOf(B.prototype, A.prototype);
// 等同于
B.prototype.__proto__ = A.prototype;

Object.setPrototypeOf(B, A);
// 等同于
B.__proto__ = A;
```

这两条继承链，可以这样理解：作为一个对象，子类的原型（`__proto__` 属性）是父类；作为一个构造函数，子类的原型对象（`prototype` 属性）是父类的原型对象（`prototype`属性）的实例

```JavaScript
B.prototype = Object.create(A.prototype);
// 等同于
B.prototype.__proto__ = A.prototype;
```

由于函数都有 `prototype` 属性（除了 `Function.prototype` 函数），所以 `extends` 后可以是任意函数

子类继承 `Object` 类的话,其实就是构造函数 `Object` 的复制，实例就是 `Object` 的实例

不存在任何继承的情况

```JavaScript
class A {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true
```

`A` 作为一个基类（即不存在任何继承），就是一个普通函数，所以直接继承 `Function.prototype`。但是，`A` 调用后返回一个空对象（即 `Object` 实例），所以 `A.prototype.__proto__` 指向构造函数（`Object`）的 `prototype` 属性

子类实例的 `__proto__` 属性的 `__proto__` 属性，指向父类实例的 `__proto__` 属性。也就是说，子类的原型的原型，是父类的原型，因此，通过子类实例的 `__proto__.__proto__` 属性，可以修改父类实例的行为

ECMAScript 的原生构造函数大致有：`Boolean()`、`Number()`、`String()`、`Array()`、`Date()`、`Function()`、`RegExp()`、`Error()`、`Object()`，以前，这些原生构造函数是无法继承的，即使定义了一个继承 `Array` 的类，这个类的行为与 `Array` 完全不一致

因为子类无法获得原生构造函数的内部属性，通过 `Array.apply()` 或者分配给原型对象都不行。原生构造函数会忽略 `apply` 方法传入的 `this`，也就是说，原生构造函数的 `this` 无法绑定，导致拿不到内部属性

ES5 是先新建子类的实例对象 `this`，再将父类的属性添加到子类上，由于父类的内部属性无法获取，导致无法继承原生的构造函数，ES6 允许继承原生构造函数定义子类，因为 ES6 是先新建父类的实例对象 `this`，然后再用子类的构造函数修饰 `this`，使得父类的所有行为都可以继承，这意味着，ES6 可以自定义原生数据结构（比如 `Array`、`String` 等）的子类，这是 ES5 无法做到的，所以，`extends` 关键字不仅可以用来继承类，还可以用来继承原生的构造函数。因此可以在原生数据结构的基础上，定义自己的数据结构。

继承 `Object` 的子类，有一个行为差异：ES6 改变了 `Object` 构造函数的行为，一旦发现 `Object` 方法不是通过 `new Object()` 这种形式调用，ES6 规定 `Object` 构造函数会忽略参数

Mixin 指的是多个对象合成一个新的对象，新对象具有各个组成成员的接口

```JavaScript
// 简单实现

const a = {
  a: 'a'
};
const b = {
  b: 'b'
};
const c = {...a, ...b}; // {a: 'a', b: 'b'}

// 完备的实现，将多个类的接口“混入”（mix in）另一个类

function mix(...mixins) {
  class Mix {
    constructor() {
      for (let mixin of mixins) {
        copyProperties(this, new mixin()); // 拷贝实例属性
      }
    }
  }

  for (let mixin of mixins) {
    copyProperties(Mix, mixin); // 拷贝静态属性
    copyProperties(Mix.prototype, mixin.prototype); // 拷贝原型属性
  }

  return Mix;
}

function copyProperties(target, source) {
  for (let key of Reflect.ownKeys(source)) {
    if ( key !== 'constructor'
      && key !== 'prototype'
      && key !== 'name'
    ) {
      let desc = Object.getOwnPropertyDescriptor(source, key);
      Object.defineProperty(target, key, desc);
    }
  }
}
```

上面代码的 `mix` 函数，可以将多个对象合成为一个类。使用的时候，只要继承这个类即可

```JavaScript
class DistributedEdit extends mix(Loggable, Serializable) {
  // ...
}
```
