## JS深复制问题来源

> JS中有五种基本数据类型`string、number、boolean、null、undefined`和一种复杂数据类型`object`，ES6新增的四种数据类型`Set、WeakSet、Map、WeakMap`

对基本类型数据的复制与平时对变量进行赋值的操作并无特别之处，一般称之为浅复制（浅拷贝），示例如下：

```javascript
let name = 'andy'
let nameTo = name 
nameTo = 'andy1'
console.log(name) // 'andy'
console.log(nameTo) // 'andy1'
```

对复杂数据类型的复制则不同于基本数据类型的复制，一般称之为深复制（深拷贝），示例如下：

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

因为给变量直接赋予`object`类型只是对当前对象进行了引用，而并没有重新分配内存空间对当前对象的属性进行存储，所以当执行代码

```javascript
let self2 = self
let myBook2 = myBook
```
时，self2和myBook2并没有达到复制的目的！

## JS深复制的实现

以下几种方式实现深复制在不同情况下都存在较大弊端，所以使用时需要严格区分场景！

- JSON对象的parse和stringify，复制JSON格式对象时适用，如上面示例代码中`let self2 = self`时
- 数组对象的slice方法和concat方法，复制数组时适用，如上面示例代码中`let myBook2 = myBook`时
- ES6的Object.assign(这玩意儿本质上还是浅复制,慎用)

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

以上几种方式都不可用，所以还是自己手撸一个吧！

```javascript
function DeepCopy(obj){
    let res = obj;
    // 之所以判断obj !== null，是因为typeof null的值为'object'
    if (typeof obj === 'object' && obj !== null) {
        // 如果参数obj是对象并且不为null,就通过Object.prototype的toString方法来判断这个对象是数组还是对象
        // 如果obj是数组（"[object Array]"），则对res进行空数组赋值，否则对res进行空对象赋值
        res = Object.prototype.toString.call(obj) === "[object Array]" ? [] : {};
        // 通过for in来进行遍逆
        for (let key in obj) {
            // 通过递归再次执行DeepCopy
            res[key] = DeepCopy(obj[key]);
        }
    }
    // 如果此时obj为非，则直接复制
    return res;
}
```

> 欢迎收藏和提交issues讨论。[GitHub地址](https://github.com/kinm/kinm.github.io/issues)