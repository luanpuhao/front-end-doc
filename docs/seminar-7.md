# 大前端内部技术交流会第七期（2020-12-24）  
## 1、js基础知识  
- 1.1、JavaScript数据类型和数据结构  
    最新的ECMAScript标准定义了8种数据类型:  
    + 原始类型:Boolean、Null、Undefined、Number、BigInt、String、Symbol  
    + 引用类型:Object  
    除Object以外的所有类型都是不可变的（值本身无法被改变）。   
    
    ```javascript
    const foo = [1, 2];
    const bar = foo;
    bar[0] = 9;
    console.log(foo[0], bar[0]); // => 9, 9
    ```

## 2、css基础知识
## 3、vue组件通信
