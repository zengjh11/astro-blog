---
title: "TypeScript基础入门"
description: "学习TypeScript的基本语法、类型系统和核心特性。"
date: 2024-03-02
tags: ["TypeScript", "JavaScript", "前端开发"]
author: "博客作者"
---

TypeScript 是 JavaScript 的超集，它添加了静态类型系统和其他高级特性，有助于提高代码质量和开发效率。本文将介绍 TypeScript 的基本语法、类型系统和核心特性，帮助你快速入门 TypeScript。

## 为什么选择 TypeScript

### 1. 类型安全

TypeScript 的静态类型系统可以在编译时检测出类型错误，避免运行时错误：

```typescript
// JavaScript
function add(a, b) {
  return a + b;
}

add("1", 2); // 返回 "12"，而不是预期的 3

// TypeScript
function add(a: number, b: number): number {
  return a + b;
}

add("1", 2); // 编译时错误：Argument of type 'string' is not assignable to parameter of type 'number'
```

### 2. 更好的开发体验

TypeScript 提供了丰富的代码补全、接口提示和重构功能，提高开发效率：

- 智能代码补全
- 接口提示
- 代码重构
- 导航功能

### 3. 更好的可维护性

TypeScript 的类型系统和接口定义可以提高代码的可读性和可维护性：

- 自文档化
- 明确的接口定义
- 更清晰的代码结构

### 4. 广泛的生态系统支持

TypeScript 得到了广泛的生态系统支持，包括：

- 主流框架：React、Vue、Angular
- 构建工具：Webpack、Vite、Rollup
- 开发工具：VS Code、WebStorm

## TypeScript 基础语法

### 1. 安装 TypeScript

使用 npm 或 yarn 安装 TypeScript：

```bash
# 使用npm
npm install -g typescript

# 使用yarn
yarn global add typescript
```

### 2. 创建 TypeScript 文件

创建一个名为`hello.ts`的 TypeScript 文件：

```typescript
function sayHello(name: string): void {
  console.log(`Hello, ${name}!`);
}

sayHello("TypeScript");
```

### 3. 编译 TypeScript 文件

使用`tsc`命令编译 TypeScript 文件：

```bash
tsc hello.ts
```

这将生成一个名为`hello.js`的 JavaScript 文件：

```javascript
function sayHello(name) {
  console.log("Hello, " + name + "!");
}

sayHello("TypeScript");
```

### 4. TypeScript 配置文件

创建一个名为`tsconfig.json`的配置文件：

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

## TypeScript 类型系统

### 1. 基本类型

TypeScript 支持以下基本类型：

- `number`：数字类型
- `string`：字符串类型
- `boolean`：布尔类型
- `undefined`：未定义类型
- `null`：空类型
- `symbol`：符号类型（ES6+）
- `bigint`：大整数类型（ES2020+）

```typescript
let num: number = 10;
let str: string = "Hello";
let bool: boolean = true;
let undef: undefined = undefined;
let nul: null = null;
let sym: symbol = Symbol("key");
let big: bigint = 100n;
```

### 2. 数组类型

TypeScript 支持两种数组类型的表示方式：

```typescript
// 方式1：类型[]
let numbers: number[] = [1, 2, 3, 4, 5];

// 方式2：Array<类型>
let strings: Array<string> = ["a", "b", "c", "d", "e"];
```

### 3. 元组类型

元组类型允许表示一个已知元素数量和类型的数组：

```typescript
let person: [string, number, boolean] = ["Alice", 25, true];

// 访问元组元素
console.log(person[0]); // Alice
console.log(person[1]); // 25

// 元组越界访问
person[3] = "extra"; // 编译时错误（严格模式下）
```

### 4. 联合类型

联合类型允许一个变量可以是多种类型中的一种：

```typescript
let value: string | number;
value = "Hello"; // 合法
value = 10; // 合法
value = true; // 编译时错误

// 类型守卫
function printValue(value: string | number): void {
  if (typeof value === "string") {
    console.log(`String: ${value}`);
  } else {
    console.log(`Number: ${value}`);
  }
}
```

### 5. 交叉类型

交叉类型允许将多个类型合并为一个类型：

```typescript
interface Person {
  name: string;
  age: number;
}

interface Employee {
  id: number;
  department: string;
}

// 交叉类型
type Staff = Person & Employee;

let staff: Staff = {
  name: "Bob",
  age: 30,
  id: 1001,
  department: "IT",
};
```

### 6. 字面量类型

字面量类型允许指定变量只能是特定的值：

```typescript
// 字符串字面量类型
let direction: "up" | "down" | "left" | "right";
direction = "up"; // 合法
direction = "east"; // 编译时错误

// 数字字面量类型
let dice: 1 | 2 | 3 | 4 | 5 | 6;
dice = 3; // 合法
dice = 7; // 编译时错误

// 布尔字面量类型
let isActive: true;
isActive = true; // 合法
isActive = false; // 编译时错误
```

### 7. any 类型

any 类型允许变量可以是任何类型：

```typescript
let anyValue: any;
anyValue = 10;
anyValue = "Hello";
anyValue = true;
anyValue = [];
anyValue = {};
```

### 8. unknown 类型

unknown 类型是 TypeScript 3.0 引入的类型，用于表示未知类型的值：

```typescript
let unknownValue: unknown;
unknownValue = 10;
unknownValue = "Hello";
unknownValue = true;

// 需要类型断言才能使用
let str: string = unknownValue as string;
let num: number = <number>unknownValue;
```

### 9. void 类型

void 类型表示函数没有返回值：

```typescript
function logMessage(message: string): void {
  console.log(message);
}
```

### 10. never 类型

never 类型表示那些永不存在的值的类型：

```typescript
// 抛出错误的函数
function throwError(message: string): never {
  throw new Error(message);
}

// 无限循环的函数
function infiniteLoop(): never {
  while (true) {
    // 循环体
  }
}
```

## TypeScript 接口

### 1. 接口定义

接口用于定义对象的形状：

```typescript
interface Person {
  name: string;
  age: number;
  email?: string; // 可选属性
  readonly id: number; // 只读属性
}

let person: Person = {
  name: "Alice",
  age: 25,
  id: 1001,
};

person.email = "alice@example.com"; // 合法
person.id = 1002; // 编译时错误：Cannot assign to 'id' because it is a read-only property
```

### 2. 函数接口

接口用于定义函数的类型：

```typescript
interface AddFunction {
  (a: number, b: number): number;
}

let add: AddFunction = function (a, b) {
  return a + b;
};
```

### 3. 索引接口

接口用于定义索引类型：

```typescript
interface StringArray {
  [index: number]: string;
}

let fruits: StringArray = ["apple", "banana", "orange"];
console.log(fruits[0]); // apple

interface Dictionary {
  [key: string]: number;
}

let scores: Dictionary = {
  math: 90,
  english: 85,
  science: 95,
};
console.log(scores["math"]); // 90
```

### 4. 类接口

接口用于定义类的结构：

```typescript
interface Animal {
  name: string;
  eat(): void;
}

class Dog implements Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  eat(): void {
    console.log(`${this.name} is eating.`);
  }
}

let dog = new Dog("Buddy");
dog.eat(); // Buddy is eating.
```

## TypeScript 类

### 1. 类的定义

定义一个名为`Person`的类：

```typescript
class Person {
  // 属性
  name: string;
  age: number;

  // 构造函数
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  // 方法
  sayHello(): void {
    console.log(
      `Hello, my name is ${this.name} and I'm ${this.age} years old.`
    );
  }
}

// 创建类的实例
let person = new Person("Alice", 25);
person.sayHello(); // Hello, my name is Alice and I'm 25 years old.
```

### 2. 类的继承

使用`extends`关键字实现类的继承：

```typescript
class Employee extends Person {
  // 新增属性
  id: number;

  // 构造函数
  constructor(name: string, age: number, id: number) {
    super(name, age); // 调用父类构造函数
    this.id = id;
  }

  // 重写父类方法
  sayHello(): void {
    super.sayHello(); // 调用父类方法
    console.log(`My employee ID is ${this.id}.`);
  }
}

// 创建子类实例
let employee = new Employee("Bob", 30, 1001);
employee.sayHello();
// Hello, my name is Bob and I'm 30 years old.
// My employee ID is 1001.
```

### 3. 类的修饰符

TypeScript 支持以下类修饰符：

- `public`：公共的，可以在任何地方访问
- `private`：私有的，只能在类内部访问
- `protected`：受保护的，可以在类内部和子类中访问
- `readonly`：只读的，只能在构造函数中赋值

```typescript
class Person {
  public name: string; // 公共属性
  private age: number; // 私有属性
  protected id: number; // 受保护属性
  readonly gender: string; // 只读属性

  constructor(name: string, age: number, id: number, gender: string) {
    this.name = name;
    this.age = age;
    this.id = id;
    this.gender = gender;
  }
}

class Employee extends Person {
  constructor(name: string, age: number, id: number, gender: string) {
    super(name, age, id, gender);
  }

  getInfo(): void {
    console.log(`Name: ${this.name}`); // 合法
    // console.log(`Age: ${this.age}`); // 编译时错误：Property 'age' is private and only accessible within class 'Person'
    console.log(`ID: ${this.id}`); // 合法
    console.log(`Gender: ${this.gender}`); // 合法
  }
}

let person = new Person("Alice", 25, 1001, "female");
console.log(person.name); // 合法
// console.log(person.age); // 编译时错误：Property 'age' is private and only accessible within class 'Person'
// console.log(person.id); // 编译时错误：Property 'id' is protected and only accessible within class 'Person' and its subclasses
console.log(person.gender); // 合法
person.gender = "male"; // 编译时错误：Cannot assign to 'gender' because it is a read-only property
```

### 4. 类的静态属性和方法

使用`static`关键字定义静态属性和方法：

```typescript
class MathUtils {
  // 静态属性
  static PI: number = 3.1415926535;

  // 静态方法
  static calculateArea(radius: number): number {
    return this.PI * radius * radius;
  }
}

// 访问静态属性和方法
console.log(MathUtils.PI); // 3.1415926535
console.log(MathUtils.calculateArea(5)); // 78.5398163375
```

## TypeScript 泛型

### 1. 泛型函数

泛型函数允许函数接受不同类型的参数：

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("Hello"); // 类型为string
let output2 = identity<number>(10); // 类型为number
let output3 = identity("World"); // 类型推断为string
```

### 2. 泛型接口

泛型接口允许接口定义泛型类型：

```typescript
interface GenericIdentityFn<T> {
  (arg: T): T;
}

function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: GenericIdentityFn<number> = identity;
```

### 3. 泛型类

泛型类允许类定义泛型类型：

```typescript
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function (x, y) {
  return x + y;
};

let stringNumeric = new GenericNumber<string>();
stringNumeric.zeroValue = "";
stringNumeric.add = function (x, y) {
  return x + y;
};
```

### 4. 泛型约束

泛型约束允许限制泛型类型的范围：

```typescript
interface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length); // 现在可以访问length属性
  return arg;
}

loggingIdentity("Hello"); // 合法，string有length属性
loggingIdentity([1, 2, 3]); // 合法，数组有length属性
loggingIdentity(10); // 编译时错误：number没有length属性
```

## 总结

TypeScript 是 JavaScript 的超集，它添加了静态类型系统和其他高级特性，有助于提高代码质量和开发效率。通过学习 TypeScript 的基本语法、类型系统、接口、类和泛型等核心特性，你可以开始使用 TypeScript 开发应用程序。

随着 TypeScript 的不断发展和普及，它已经成为现代前端开发的重要工具之一。建议你在新项目中使用 TypeScript，并逐步将旧项目迁移到 TypeScript，以提高代码的可维护性和开发效率。
