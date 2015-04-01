你可能不知道的ES6特性

我们都很期待ECMAScript6给我们带来的新特性。我今天早上浏览了一下ES6 Compatibility Table，其中列出了不少目前还没被广泛介绍过的ES6新特性，以及一些需要注意的地方。结合这张Table以及现有的ES6 Draft，本文为大家做一些简短介绍。Just for fun！

## Class

class实际上是function的一个语法糖，而并不是一个类型。下面的例子可以说明这点。

```
class C {}
typeof C === 'function';  // true
```

`class`也可以直接用作表达式。

```
typeof class C {} === 'function';
```

class也可以是匿名的。在ES6 Rev35中class的BNF语法定义为

```
ClassDeclaration:
  class BindingIdentifier ClassTail // 非匿名类
  [+default] class ClassTail        // 匿名类
```

我们可以用简单的匿名类表达式来验证
```      
typeof class {} === 'function';
```

匿名类最常用的形式将是书写一个简短的，继承自某个类的子类。例如
``` 
foo(new class extends Comparator {
  compare(a, b) {
    // do something
  }
});
```

这里实际上和Java里面的匿名类很像，在保持了OOP封装性的同时，又保证了代码的简明。
```java
// Java匿名类示例代码
Arrays.sort(array, new Comparator<MyClass> {
  int compare(MyClass lhs, MyClass rhs) {
    // do something
  }
});
```

## new.target

在类中，new.target指向该实例被实例化时所用的类。这样的话，父类就可以判断一个对象是由自己new出来的，还是从子类new出来的。这个说法或许不是太清楚，我们来看看实例。

```
class A {
  constructor() {
    console.log(new.target === B); // true
  }
}
class B extends A {
  constructor() {
    super();
  }
}
let newObj = new B();
```

在这里，B继承自A，并且初始化了一个B的实例。初始化B的实例的过程中，调用了A的构造函数时，new.target将是指向B的一个引用。因为我们是用B来初始化这个对象的。

## Default parameters

默认参数（Default parameters）是一项JavaScript工程师们已经YY了很久了的特性。有了它，我们可以给函数传入默认参数。

```
function foo(a = 1, b = 2) {
  return a === 1 && b === 2; 
}
foo(); // true
```

有趣的是，位于右边的参数的默认值可以指定成左边的参数的值。

```
function foo(a, b = a) {
  return a * b;
}
foo(2); // 4
```

## Computed properties

在ES5中，如果要将一个变量的值作为属性名（Property name）的时候，我们要分步完成。
```
var objA = {};
var keyName = "my key";
objA[keyName] = "my value";
console.log(objA[keyName]); // my value
```

在ES6中，Computed properties帮助我们让这一过程一步到位。代码也将因此更加容易维护。
```
let keyName = "my key";
let objA = {
  [keyName]: "my value"
};
console.log(objA[keyName]); // my value
```

这个特性还可以用在很多其他的地方，例如类方法的名称定义。
``` 
let myMethodName = "this is a method name, do you believe it?";
class MyClass {
  [myMethodName]() {
    console.log("Wow!!");
  }
}
let foo = new MyClass();
foo[myMethodName](); // Wow!!
```

## Object destructing

Object destructing在for .. in语句中也可以使用，这再次使得我们能够写出更加简短且简明的代码。
```
let people = [
  {name:'John', age: 20},
  {name:'Linda', age: 20}
];
for ([name, age] in people) {
  console.log(name, age);
}
// John 20
// Linda 20
```

Object destructing可以是层叠嵌套的。这个特性太棒了！这样我们可以快速地解析一个复杂的对象。
```
let [e, {x, t:{g}}] = [1, {x: 2, t: {g: 3}}]; // e: 1, x: 2, g: 3
```

Object destructing可以提供默认值，这样我们就不必逐个检查提取出来的值是否为undefined。
```
var {c} = {a:1}; // c: undefined
var {c:2} = {a:1}; // c: 2
```

 