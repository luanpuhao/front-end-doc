# 大前端内部技术交流会第七期（2020-12-24）  
## 1、js基础知识  
- 1.1、JavaScript数据类型和数据结构  
    + JavaScript 是一种弱类型或者说动态语言。
    + 这意味着你不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。
    + 这也意味着你可以使用同一个变量保存不同类型的数据：
    
    ```javascript
    var foo = 42; // foo is a Number now
    foo = "bar"; // foo is a String now
    foo = true;  // foo is a Boolean now
    ```
    
    + 最新的ECMAScript标准定义了8种数据类型:  
    + 原始类型：Boolean、Null、Undefined、Number、BigInt、String、Symbol  
    + 引用类型：Object  
    + 除Object以外的所有类型都是不可变的（值本身无法被改变）。
    
    ```javascript
    const foo = [1, 2];
    const bar = foo;
    bar[0] = 9;
    console.log(foo[0], bar[0]); // => 9, 9
    ```

## 2、css基础知识
## 3、vue组件通信
