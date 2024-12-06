---
html:
  cdn_hosted: true
export_on_save:
  html: true
---

# Standard ML 基础知识笔记

<br>

<br>

<br>

## 1 基础知识

<br>

- Standard ML 使用`;`表示一个语句的结束。Standard ML 源文件的后缀为`.sml`，可以在终端中使用`use "filename.sml";`编译源文件；在终端中，`-`表示提示用户输入，`=`表示终端没找到`;`结束符，继续等待用户输入；
-  

<br>

### 1.1 变量

<br>

Standard ML 使用`val`关键字给一个变量进行赋值（下面的`static environment`指的是类型检查环境，`dynamic environment`指的是对变量进行求值的环境）：

``` sml
val x = 34;
(* static  environment : x : int *)
(* dynamic environment : x --> 34 *)
val y = ~20;
(* static  environment : x : int, y : int *)
(* dynamic environment : x --> 34, y --> ~30 *)
val abs_of_y = if y < 0 then -y else y;
(* static  environment : ... abs_of_y : int *)
(* dynamic environment : ... abs_of_y --> 20 *)
```

- 变量的命名：字母、数字以及`_`的组合，要求不能以数字开头，Standard ML 区分大小写；
- 变量的类型检查（Type check）：在当前的静态环境（static environment）中进行类型检查，如果失败，将发生错误；
- 变量的求值（Evaluation）：在当前的动态环境（dynamic environment）中进行求值。
- 变量的类型系统：
  - boolean 类型，在 Standard ML 中的类型构造函数为`bool`，具有`true`与`false`的值；

    ``` sml
    true;  (* val it = true : bool *)
    false; (* val it = false : bool *)
    ```

  - integer 类型，在 Standard ML 中的类型构造函数为`int`，整数的字面值不可以以`0`开头，负数的字面量使用`~`开头；

    ``` sml
    val x = 3;  (* val x = 3 : int *)
    val y = ~6; (* val y = ~6 : int *)
    ```

  - real 类型，在 Standard ML 中的类型构造函数为`real`，形式为`integer.integer`或者科学计数法`integer1 E integer2`（字母`E`可以为小写，注意实际上数字和字母`E`/`e`之间是没有空格的）： 

    ``` sml
    val x = 3.90; (* val x = 3.9 : real *)
    val y = 3E3;  (* val y = 3E3 : real *)
    ```

  - string 类型，在 Standard ML 中的类型构造函数为`string`，和大多数语言一样都是包裹在`""`中的字符串，如果要使用多行的字符串，则需要在下一行的字符串前后加上`\`（因为这里的多行字符串没有渲染正确，所以我全部放进注释当中了）：

    ``` sml
    val str1 = "I love huaier!";
    (* val str1 = "I love huaier! : string *)
    (*
     * val str2 = "Huaier is \
     *            \my wife, and \
     *            \she loves me too!";
     *)
    (* val str2 = "Huaier is my wife, and she loves me too!" : string *)
    ```

<br>

