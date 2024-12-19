---
html:
  cdn_hosted: true
export_on_save:
  html: true
---

# TypeScript 基础知识笔记

<br>

<br>

<br>

## 1 TypeScript 基础

<br>

TypeScript 致力于解决 JavaScript 中几乎不存在的类型系统问题，例如对于这样一段 JavaScript 的代码：

``` javascript
let test_1 = "I love Huaier!";

let test_2 = {
  name: "AshGrey",
  print() {
    console.log(this.name);
  }
};

let test_3 = {
  name: "Huaier"
};

let test_4 = () => console.log("function");

function callAnyType(arg) {
  if (typeof(arg) === "string" || typeof(arg) === "number") {
    console.log(arg);
  } else if (typeof(arg) === "object") {
    arg.print?.();
  } else {
    arg?.();
  }
}

callAnyType(test_1);    // I love Huaier!
callAnyType(12);        // 12
callAnyType(test_2);    // AshGrey
callAnyType(test_3);    // (Nothing print)
callAnyType(test_4);    // function
```

为了确定 JavaScript 传入的参数，不得不不断使用`typeof`关键字去确定合适的调用方法，这是 JavaScript 无法提供良好的类型系统造成的问题。而使用 TypeScript 就能够提供类型系统的帮助：

``` typescript
const message = "I love huaier!";
message();
// ^^
// This expression is not callable.
//   Type 'String' has no call signatures.
```

使用`npm install -g typescript`下载 tsc 编译器，执行`tsc test.ts`命令后，同目录下将出现编译出的`test.js`文件，使用 tsc 编译器可以指定生成的 js 文件符合哪一版本的 ECMAScript 标准。

<br>

### 1.1 TypeScript 中的类型系统

<br>

TypeScript 的原始类型和 JavaScript 的原始类型是一样的：`number`、`string`和`boolean`。可以参考 JavaScript 笔记[^1]。接下来介绍 TypeScript 中独特的类型：
- 数组：对于 JavaScript 中的`[1, 2, 4]`这样的数组类型，TypeScript 可以用`number[]`或者`Array<number>`表示，后面会介绍 TypeScript 中的泛型`T<U>`；
- `any`：TypeScript 提供的这个类型指定了类型为`any`的变量不接受 TypeScript 的类型检查，它可以是任意一种类型；

``` typescript
const num: number = 3;
const message: string = "Test";
const bool: boolean = 1 === 2;
const arrayString: string[] = ["123", "AshGrey", "Huaier"];
const arrayNumber: Array<number> = [1, 2, 3];

let obj: any = { x: 0 };
obj.foo();
obj();
obj.alice = 100;
```

TypeScript 的类型系统可以自动推断一些变量的类型，例如：

``` typescript
let myName /* : string */ = "AshGrey";
let myNum /* : number */ = 10;
```

TypeScript 的类型系统也可以对函数的参数和返回值类型进行限定，例如：

``` typescript
function myLog(level: number, message: string, time: Date) : string {
  const levelString: string = level === 1 ? "Error"
                            : level === 2 ? "Info"
                            : level === 3 ? "Debug"
                            : "Unkown";
  return `${levelString} [${time}] : ${message}`;
}
```

[^1]: 我的 [JavaScript 基础知识笔记](../JavaScript/2024-02-16-JavaScript基础知识笔记.md)
