# TypeScript基础

## 什么是 TS

TS 是以 JavaScrip 为基础的，一个以 JavaScript 的超集

TS 拓展了 JavaScript，并添加了类型

浏览器目前不支持直接执行 TS

TS 要先编译成 JavaScript，然后通过 JS 解析器执行

环境安装
1、下载 node.js
2、下载 TypeScript

TS 文件经过 tsc 编译成 js，js 再通过 node 进行运行

建议使用 webStorm 进行 ts 练习

学会多看文档进行定义的理解

## 类型

定义类型格式为 let 变量名:变量类型;

声明一个变量 a ，类型为 number,在之后的使用， a 只能为 number

```ts
let a: number

a = 10
```

当 a 赋值为其他类型时会报错

```ts
a = 'hi'
```

**自动类型检测**

即，但一个变量在最初声明时赋值，那么会对变量进行类型检测，最初的值所属类型则为该变量的类型

声明变量 C，C 的类型为 string

```ts
let c = 'hi'
```

因此，在赋值 boolean 时会报错

```
c = true
```

可以给方法的形参定义参数类型

### function 方法名():函数的返回值类型{}

```ts
function sum(one: number, two: number): number {
  return one + two
}
```

由于方法中形参规定了参数类型，所以当参数不为 number 时则会报错

接收的参数必须与函数返回值的类型相同

```ts
let sums: number = sum(123, 234)
```

### 使用字面量进行类型声明,在该类型中，则限制了 f 的值为 10

```
let f: 10;
```

### 使用|来链接多个值（联合类型），限制变量在某些值之间

```ts
let sex: 'male' | 'female'
```

### any 任意类型

显式 any

```ts
let d: any;

d = 10;

d = 'hi'
```

隐式 any

```ts
let d1;

d1 = 10;

d1 = "hi";
```

### unknown 未知类型

```ts
let e: unknown

e = 10

e = 'hi'
```

any 可以赋给其他类型的变量，会关闭其他变量的类型判断

但是 unknown 不能随意赋值给其他变量

### 类型断言,可以告知解析器 e 的类型就是 string

```TypeScript
let str: string;

// 语法1

str = e as string

// 语法2

str = <string>e
```

### void nerve 主要用于设置函数返回值

```ts
function fn(): void {
  // void表示函数没有返回值

  // 也可以return null 或者 undefined

  // return null

  return undefined
}

function fn5(): never {
  // nerve表示永远不会返回结果

  // 用于设置抛出异常

  throw new Error('报错！')
}
```

### object 对象，在 js 中一切皆是对象，所有一般是为了限制对象中的属性

在属性名后面加上一个问号，表示该属性为可选属性

```ts
let obj: { name: string; age?: number }

// 当没有设置限定的属性时，则会报错

// obj = {}

obj = { name: '小李' }
```

[propName:string]:any 表示可以有任意属性

```ts
let obj1: { name: string; [propName: string]: unknown }

obj1 = { name: '小黄', a: 10, c: 'sh' }
```

### 函数

```TS、
// 设置函数结果的类型声明

// 语法：(形参:类型,形参:类型...)=> 返回值

let fn2: (a: number, b: number) => number

fn2 = function (n1, n2): number {

    return n1 + n2

}
```

### array 数组

```ts
// 表示number类型的数组 格式为 let 变量名:类型[] 或者 let 变量名:Array<类型>

let arr: number[]

arr = [1, 2, 3]



let arr1: Array<string>

arr1 = ['1', 'hs']
```

### 元组，固定长度的数组，如果长度过长，建议使用数组

```ts
let h: [string, string]

// 值与定义要一一对应

h = ["he", "hi"]
```

### enum 枚举

```ts
// 定义一个枚举类

// 枚举类，将可能的情况都列举出来进行使用

enum Sex {

    male = 0,

    female = 1

}

let en: { name: string, sex: Sex }



en = {

    name: '小李',

    sex: Sex.male

}
```

### 类型别名,简化类型的使用

```ts
type myType = 1 | 2 | 3 | 4 | 5

let type1: myType

let type2: myType
```

### 接口，可用来定义类型

```ts
interface type {
  name: string
  age: number
  sex: string
}

const preson: type = {
  name: 'preson',
  age: 1,
  sex: 'male',
}
```

## 泛型

在定义函数或类是类型不明确时可以使用泛型

泛型的工具类
1、Partial 用来创建一个新的类型，将 type 的所有属性设置为可选项
2、Readonly 用来创建一个新的类型，将 type 的所有属性设置为只读
3、Pick 从 Type 中选择一组属性来构造新类型
4、Record 构造一个新的类型，属性值为 keys,类型为 Type

```ts
function fn1<T>(a: T): T {
  return a
}
// 不指定泛型
let res = fn1(10)
// 指定泛型
let res1 = fn1<string>('hello')

function fn4<T, K>(a: T, b: K): K {
  return b
}

fn4<number, string>(10, 'sd')

interface Inter {
  length: number
}

function fn3<T extends Inter>(a: T): number {
  return a.length
}

let res3 = fn3([1, 2, 3, 2])
console.log(res3)

interface Propo {
  id: number
  name: string
}

type Propo1 = Partial<Propo>
type Propo2 = Readonly<Propo>
```

## 面向对象

**在编程过程中，所有操作通过对象来进行**

对象：object，每一个对象都可以代表一个具体的事物

**类：对象的模型**
**包含属性和方法**

实例属性
直接定义的
类属性，在属性前加上 static 关键字

```ts
class Person {
  // 定义实例属性
  name: string = '小凯'
  // 在属性前加上static关键字可以定义一个类属性,又称静态属性
  static age: number = 19
}
```

**readonly 关键字 表示只读的属性，不能进行修改**

> 实例方法：
> 方法名() {}
>
> 类方法：
> static 方法名() {}
>
> say() {
> console.log("说话")
> }
> static eat() {
> console.log("吃饭")
> }

**构造函数**
constructor

**抽象类**
abstract，只能用于继承，不能用来创建实例
抽象类中可以添加抽象方法
抽象方法：定义结构，在子类中重写

接口：用来定义一个类的结构，可以限制一个类的结构
接口中的属性都不能有实际的值

**封装**
属性修饰符
public 可以在任意位置修改
private 只能在类内部被修改

```ts
;(function () {
  //定义一个接口
  interface myInterface {
    name: string
    age: number
    say(): void
  }
  // 实现一个接口
  class MycClass implements myInterface {
    age: number
    name: string
    constructor(name: string, age: number) {
      this.name = name
      this.age = age
    }

    say(): void {
      console.log('接口')
    }
  }
  abstract class Animal {
    name: string
    age: number
    constructor(name: string, age: number) {
      this.name = name
      this.age = age
    }
    say(sayWord: string) {
      console.log(sayWord)
    }
    //抽象方法
    abstract eat(): void
  }

  class Dog extends Animal {
    say(sayWord: string) {
      super.say(sayWord)
    }
    eat() {
      console.log('狗粮')
    }
  }

  class Cat extends Animal {
    sayWord = '喵喵喵'
    say() {
      super.say(this.sayWord)
    }
    eat() {
      console.log('猫粮')
    }
  }

  const dog = new Dog('旺财', 5)
  dog.say('汪汪汪')
  const cat = new Cat('咪咪', 3)
  cat.say()

  class Person {
    private _name: string
    age: number
    constructor(name: string, age: number) {
      this._name = name
      this.age = age
    }
    get name() {
      return this._name
    }
    set name(val: string) {
      this._name = val
    }
  }
  const per = new Person('小李', 20)
  per.age = 21
  console.log(per.name)
})()
```

## 编译选项配置

### 1、可以在控制台窗口运行 tsc ... -w 进行监听，当 ts 文件改变是，会进行自动编译

但是在该方法中，一个文件会开启一个命令行窗口

### 2、tsconfig.json 文件配置

在 ts 文件目录下添加 tsconfig.json 文件，然后运行 tsc 会编译该目录下所有 ts 文件
运行 tsc -w 会监听所有 ts 文件

tsconfig.json 是 ts 编译器的配置文件，ts 编译器可以根据它的信息来对代码进行编译

### 配置选项

include：用来指定需要被编译的 ts 文件 \** 代表任意目录，*代表任意文件
"include": ["路径"]

exclude：用来指定不需要被被编译的 ts 文件

extends：定义被继承的配置文件

files：设置需要编译的文件列表

compilerOptions：编译器选项
compilerOptions 子选项配置：
(1)、target 用来指定 ts 被编译的 ES 版本

(2)、module 模块 用来指定使用的模块化的规范

(3)、lib 用来指定要使用的库

(4)、outDir 用来指定编译后文件所在的目录

(5)、outFile 将编译之后的代码合并到一个文件

(6)、allowJs 默认是 false，不对 js 文件进行编译

(7)、checkJs 检查 js 代码是否符合规范

(8)、removeComments 是否移除注释

(9)、noEmit 不生成编译后的文件

(10)、noEmitOnError 有错误时不生成编译后的文件

(11)、alwaysStrict 用于设置编译后的文件是否使用严格模式

(12)、noImplicitAny 不允许使用隐式 any

(13)、noImplicitThis 不允许使用不明确类型的 this

(14)、strictNullChecks 严格检查空值

(15)、strict 是否开启所有严格校验