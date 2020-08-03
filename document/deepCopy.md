## JS深复制问题来源

> JS(ES5)中有基本数据类型`string、number、boolean、null、undefined`和引用数据类型`Object、Array、Date、RegExp、Function`，ES6新增的四种数据结构`Set、WeakSet、Map、WeakMap`以及一种基础数据类型`symbol`

对基本类型数据的复制与平时对变量进行赋值的操作并无特别之处，一般称之为浅复制（浅拷贝），示例如下：

```javascript
let name = 'andy'
let nameTo = name 
nameTo = 'andy1'
console.log(name) // 'andy'
console.log(nameTo) // 'andy1'
```

对引用数据类型的复制则不同于基本数据类型，一般称之为深复制（深拷贝），示例如下：

```javascript
// 先定义一个对象和一个数组
let self = {
    name:'andy',
    age:25,
}
let myBook = ['javascript高级程序设计','深入理解ES6','数据结构与算法javascript描述']

// 将对象和数组赋值给新的变量
let self2 = self
let myBook2 = myBook

// 修改新变量self2和myBook2的值，然后打印self和myBook
self2.name = 'tom'
self2.age = 23
myBook2[2] = '深入浅出NodeJS'

console.log(self) // {name: "tom", age: 23}
console.log(myBook) // ["javascript高级程序设计", "深入理解ES6", "深入浅出NodeJS"]
console.log(self2) // {name: "tom", age: 23}
console.log(myBook2) // ["javascript高级程序设计", "深入理解ES6", "深入浅出NodeJS"]
```

> 以上代码中并无明显修改self和myBook的操作，但self和myBook随着self2和myBook2的改动而改动了！

因为给一个变量直接赋值引用数据类型，该变量只是对其进行了引用，而并没有重新分配内存空间对其进行存储，所以当执行代码
`let self2 = self`、
`let myBook2 = myBook`
时，self2和myBook2并没有达到复制的目的！

以上示例要达到深复制的目的，可以使用如下方式：

- JSON对象的parse和stringify，复制JSON格式对象时适用

```javascript
let self = {
    name:'andy',
    age:25,
}
let self2 = JSON.parse(JSON.stringify(self))
self2.name = 'tom'
self2.age = 23
console.log(self) // {name: "andy", age: 25}
console.log(self2) // {name: "tom", age: 23}
```

- 数组对象的slice方法和concat方法，复制一维基础数据类型的数组时适用

```javascript
let myBook = ['javascript高级程序设计','深入理解ES6','数据结构与算法javascript描述']
let myBook2 = myBook.slice(0,myBook.length)
myBook2[2] = '深入浅出NodeJS'
console.log(myBook) // ["javascript高级程序设计", "深入理解ES6", "数据结构与算法javascript描述"]
console.log(myBook2) // ["javascript高级程序设计", "深入理解ES6", "深入浅出NodeJS"]
```

但当我要复制一个复杂对象时，如下：

```javascript
{
    'myBook':['javascript高级程序设计','深入理解ES6','数据结构与算法javascript描述'],
    'self':{name: "andy", age: 25},
    'skill':function(){
        console.log('kungfu')
    }
}
```

- ES6的扩展运算符`...`和`Object.assign`（这两种方法都是只对所要复制的数据进行一层深复制，仅适用于简单的一维数据结构）


以上几种方式都不可用，所以还是自己手撸一个吧！

## JS深复制的实现

```javascript
function DeepCopy(obj){
    let res = obj;
    // 之所以判断obj !== null，是因为typeof null的值为'object'
    if (typeof obj === 'object' && obj !== null) {
        // 通过Object.prototype的toString方法来判断这个对象是数组还是对象
        // 如果obj是数组，则对res进行空数组赋值，否则对res进行空对象赋值
        res = Object.prototype.toString.call(obj) === "[object Array]" ? [] : {};
        // 通过for in对obj进行遍逆
        for (let key in obj) {
            // 通过递归再次执行DeepCopy
            res[key] = DeepCopy(obj[key]);
        }
    }
    // 如果此时typeof obj不是‘object’，则直接复制
    return res;
}
```

> 以上代码并非完全没有问题，因为如果一个对象的原型链太深，递归时会出现内存溢出的问题！所以在使用时还需要自行斟酌复制的对象是否有较深的原型链！

> 欢迎收藏和提交issues讨论。[GitHub地址](https://github.com/kinm/kinm.github.io/issues)