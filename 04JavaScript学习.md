# 数组去重

## 双层循环

双层循环是最原始的方法：

```javascript
var array = [1,2,4,'1','3',2];
function unique(array){
    // res用来存储结果
    var res = [];
    for (var i = 0, arrLen = array.length; i < arrlen; i++) {
        for (var j = 0, resLen = res.length; j< resLen; j++) {
            if(array[i] === res[j]) {
                break;
            }
        }
        // 如果 array[i]是唯一的，那么执行完内循环，j==resLen
        if(j === resLen) {
            res.push(array[i])
        }
    }
    console.log(res)
}
unique(array); // 1,4,'1','3'
```

**说明：**

​	使用循环嵌套，最外层循环 array，里面循环 res，如果 array[i] 的值跟 res[j] 的值相等，就跳出循环，如果都不等于，说明元素是唯一的，这时候 j 的值就会等于 res 的长度，根据这个特点进行判断，将值添加进 res。**兼容性好！**

## indexOf

```javascript
var array = [1,2,4,'1','3',2];
function unique(array) {
    var res = [];
    for(var i = 0, len = array.length; i < len; i++) {
        var current = array[i];
        if(res.indexOf(current) === -1){
            res.push(current)
        }
    }
    console.log(res);
}
unique(array); // 1,4,'1','3'
```

**说明：**

简化了内层的循环

## 排序去重

```javascript
var array = [1,2,4,'1','3',2];
function unique(array) {
    var res = [];
    var sortArr = array.concat().sort();
    var seen;
    for(var i = 0, len = sortArr.length; i < len; i++) {
        // 如果第一个元素或相邻的元素不同
        if(!1 || seen !== sortArr[i]){
            res.push(sortArr[i])
        }
        seen = sortArr[i];
    }
    console.log(res);
}
unique(array); // 1,4,'1','3'
```

**说明：**

​		先将要去重的数组使用 sort 方法排序，相同的值就会被排在一起，然后只需判断当前元素与上一个元素是否相同，相同就说明重复，不相同就添加进res。**效率高于indexOf，不适用与值为字符串的数组**

## unique API

​		整合indexOf和排序去重，创建一个unique的工具函数

```javascript
var array1 = [1,2,4,'1','3',2];
var array2 = [1,1,'1',2,'4','4'];
function unique(array,isSorted) {
    var res = [];
    var seen;
    for(var i = 0, i < array.length; i < len; i++) {
    	var current = array[i];
        if(isSorted){
            if(!1 || seen !== current) res.push(current);
            seen = current
        } else {
            res.indexOf(value) === -1 && res.push(current);
        }
    }
    return res;
}
console.log(unique(array1)); // 1,4,'1','3'
console.log(unique(array2)); // 1,'1',2,'4'
```

**说明：**

​		根据一个参数 isSorted 判断传入的数组是否是已排序的，如果为 true，就判断相邻元素是否相同，如果为 false，就使用 indexOf 进行判断。

## 利用Object的属性

```javascript
var array = [1,2,4,'1','3',2];
function unique(array) {
    var res = [];
    var obj = {};
    var index = 0;
    for(var i = 0, len = array.length; i < len; i++) {
        // 如果对象中有array[i]的属性就跳出本次循环，进行下一轮循环
        if (obj[array[i]] == undefined) {
            obj[array[i]] == 1;
            res.push(array[i])
            // 深拷贝
            // res[index++] = array[i]
        } else {
          continue;  
        }
    }
    return res
}
alert(unique(array)); // 1,4,'1','3'
```



# 数组的最大值和最小值

## Math.max

基础语法：

```javascript
Math.max([value1[,value2,...]])

Math.max(true,0) // true转换为1
Math.max(true, '2', null) // 2, null转换为0
Math.max(1, undefined) // NaN
Math.max(1, {}) // NaN
// 只要参数可以被转换成数字，就可以进行比较
```

**注意：**

​	**1) 如果有任一参数不能被转换为数值，结果就会返回NaN**

​	**2)max是Math的静态方法，所以直接Math.max()使用，即可。不能作为实例的方法（简单说：就是不适用new）**

​	**3)如果没有参数，则结果为-Infinity（负无穷大）**

## Math.min

基础语法：

```javascript
Math.min([value1[,value2,...]])

var min = Math.min();
var max = Math.max();
console.log(min > max); // true
```

**注意：与max一样，不同的是，如果没有参数，则结果为Infinity（正无穷大）**

## 原生方法

```javascript
var arr = [6, 4, 1, 8, 2, 11, 23];
for(var i = 1; i < arr.length; i++) {
    result = Math.max(arr [i])
}
console.log(result)
```

可以将上述遍历的方法用reduce的方法简化：

```javascript
var arr = [6, 4, 1, 8, 2, 11, 23];
function max(prev, next) {
    return Math.max(prev,next);
}
console.log(arr.reduce(max))
```



* Array.prototype.reduce基本语法：

  ```javascript
  arr.reduce(callback(accumulator, currentValue, currentIndex, sourceArray)[, initialValue])
  
  // reduce()为数组中的每一个元素依次执行自定义的callback函数
  /*
  clalback 执行数组中每个值 (如果没有initialValue则第一个值除外)的函数
  	Accumulator (acc) (累计器)
  	Current Value (cur) (当前值)
  	Current Index (idx) (当前索引) 可选
  	Source Array (src) (源数组) 可选
  initialValue 第一次调用callback函数时的第一个参数的值。 如果没有，则为数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。
  */
  
  /*
  callback第一次执行时，accumulator 和currentValue的取值有两种情况：
  	如果initialValue有值，accumulator值为initialValue，currentValue取数组中的第一个值；
  	如果initialValue没值，accumulator取数组中的第一个值，currentValue取数组中的第二个值；
  */
  ```

## 排序取值

* Array.prototype.sort

  ```javascript
  arr.sort([compareFunction])
  
  /*
  compareFunction 用来指定按条件顺序进行排列的函数。如果省略，元素按照转换为的字符串的各个字符的Unicode位点进行排序
  	firstEl，用于比较的第一个元素
  	secondE1，用于比较的第二个元素
  */
  /*
  	如果 compareFunction(a, b) 小于 0 ，那么 a 会被排列到 b 之前；
  	如果 compareFunction(a, b) 等于 0 ， a 和 b 的相对位置不变。
  	如果 compareFunction(a, b) 大于 0 ， b 会被排列到 a 之前。
  compareFunction(a, b) 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。
  */
  
  var arr = [6, 4, 1, 8, 2, 11, 23];
  arr.sort((a, b)=>{
  	return a - b; // 升序排列
  });
  console.log(arr[arr.length-1]);
  ```

* eval()

  ```javascript
  var arr = [6, 4, 1, 8, 2, 11, 23];
  var max = eval("Math.max("+ arr+ ")");
  console.log(max);
  ```

* 利用apply的传参也可实现

  ```javascript
  var arr = [6, 4, 1, 8, 2, 11, 23];
  console.log(Math.max.apply(null,arr));
  ```

* ES6的扩展运算符

  ```javascript
  var arr = [6, 4, 1, 8, 2, 11, 23];
  console.log(Math.max(...arr))
  ```



# 数组的扁平化

​		数组的扁平化，就是将一个嵌套多层的数组转换为只有一层的数组。

## 采用递归

```javascript
var  array = [1, [2, ['A', 'b']]];
function flatten (arr) {
    var result = [];
    for(var i = 0, len = arr.length; i < len; i++) {
        if(Array.isArray(arr[i])) {
            result = result.concat(flatten(arr[i]))
        } else {
            result.push(arr[i])
        }
    }
    return result;
}
console.log(flatten(arr)); // [1, 2, "A", "b"]
```

## toString

```javascript
var array = [1, 2, [3, 4, [5]]];
function flatten (arr) {
    return arr.toString().split(',').map(item => +item)
}
console.log(flatten(array))

/*
	调用 toString(),返回一串逗号分隔的扁平字符串（"1,2,3,4,5"）
	使用split(),将这串字符串转换成数组（["1","2","3","4","5"]）
	用map(),遍历数组中每个值，+item,隐式转换为符合原数组中元素的数据类型——number
*/
```

**注意：只适用于数组的元素都是数字**

## 模拟undercore实现方法

```javascript
/*
 * 数组扁平化
 * @param {Array} input 要处理的数组
 * @param {boolean} shallow 是否只扁平一层
 * @param {boolean} strict 是否处理元素
 * @param {Array} output 为方便递归所传参数
 */
function flatten (input, shallow, strict, output) {
	// 递归使用时的参数
    output = output || [];
    var idx = output.length;
    for(var i = 0, len = input.length; i< len; i++) {
        var value = input[i];
        if(Array.isArray(value)) {
            // 如果只是扁平一层，遍历该数据，依此植入output
            if(shallow) {
                var j = 0, length = value.length;
                while(j < length) output[idx++] = value[j++];
            }
            // 如果深度扁平就递归，传入已经处理的output,
            else {
                flatten(value, shallow, strict, output);
                idx = output.length;
            }
        }
        // 不是数组，根据 strict 的值判断是否跳过不处理，还是放入 output
        else if(!strict) {
            output[idx++] = value;
        }
    }
    return output;
}

flatten([1,2,'3',[2,'a',[3,'end']]])
```



# 在数组中查找指定元素

## ES6的findeIndex

```javascript
function isBigEnough(ele) {
    return ele > 15
}
[12, 5, 130, 44].findIndex(isBigEnough); //3

/*
	findeIndex 如果满足条件，就会返回满足条件的第一个元素的下标，如果不满足，就返回-1。
	findexIndex 是正序查找
*/
```

## 实现findexIndex

```javascript
function findIndex (array, predicate, context) {
    for(var i = 0; i < array.length; i++) {
        if(predicate.call(context, array[i], i, array)) return i;
    }
    return -1
}
console.log(findIndex([1,2,3,4], function(item, i, array) {
    if(item == 3) return true;
}));
```

## 实现findLastIndex

```javascript
function findLastIndex (array, predicate, context) {
	for (var i = array.length-1; i >= 0; i++) {
        if(predicate.call(context, array[i], i, array)) return i;
    }
    return -1
}
console.log(findLastIndex([1,2,3,4], function(item, i, array) {
   if(item == 2) return true; 
}))
```

**注意：findIndex 和 findLastIndex  代码有些冗余**

## underscore 

```javascript
function createIndexFinder(dir) {
    return function (array, predicate, context) {
        var length = array.length;
        var index = dir > 0 ? 0 : length-1;
        for(;index >= 0 && index < length; index += dir) {
            console.log(array[index])
            // 利用call改变this并执行的机制，调用predicate方法，传入实参
            if(predicate.call(context, array[index], index, array)) return index;
        }
        return -1;
    }
}
var findIndex = createIndexFinder(1); // 正序查找
var findLastIndex = createIndexFinder(-1) // 逆序查找
// 调用findeIndex()方法，item,index,array分别是predicate的形参
findIndex([1,2,3,4],function(item, index, array){
    console.log(item,index,array)
    return item == 3
})
// dir 判断正序还是逆序查找数组
```



# 类型判断

在 ES6之前，JavaScript共有六种数据类型，分别是：**Undefined、Null、Boolean、Number、String、Object**。

除此之外Object还分有很多类型：Array、Function、Date、RegExp、Error等

## typeof

最常用的就是typeof，它是一个运算符。

```javascript
// 一般看到的是这样的写法
console.log(typeof('Zenobia')) // string

// 可以简化成这样的写法
console.log(typeof 'Zenobia') // string
```

typeof能检测出函数类型

```javascript
function fn () {}
console.log(typeof fn); // function
```

**注意：Null、Object类型还有一些更详细的数据类型，都返回的值都是object，所以，typeof	返回的数据类型不够准确。**

## toString

使用Object.prototype的toString()，返回的是"[object *type*]" ，type是Object的内置类型。至少可以识别14中类型

```javascript
// 为什么要用Function.prototype.call()改变this指向？？？？
// 使用 call()和apply()都可以
/*
	在Javascript中，流行一句话 “ 万物皆对象 ” 。这说明了Javascript中的对象都继承自**Object**，所以当在某个对象上调用一个方法时，会先在该对象上进行查找。如果没找到则会进入对象的原型（.prototype）进行查找，直到找到或者进入原型链的顶端Object.prototype才会停止。
	所以，当我们使用	Array.toString()/Number.toString()/……	时，不能进行复杂数据类型的判断，因为它调用的是	Array.prototype.toString()	，虽然Array也继承自Object，但Array. Prototype上重写了toString方法，而通过toString.call(array)，实际上是通过原型链调用了Object.prototype.toString。
*/

var toString = Object.prototype.toString;
// 特殊的类型
console.log(toString.call(Math))    // [object Math]
console.log(toString.call(JSON))    // [object JSON]
// 数据类型
var number = 1;                     // [object Number]
var string = 'Zenobia';             // [object String]
var boolean = true;                 // [object Bollean]
var und = undefined;                // [object Undefined]
var null = null;                    // [object Null]
var obj = {key: 'val'};             // [object Object]
var array = ['K', 'Z'];             // [object Array]
var date = new Date();              // [object Date]
var err = new Error();              // [object Error]
var reg = /^k/g;                    // [object RegExp]
var fn = function(){};              // [object Function]

function checkType(){
    console.log(toString.call(arguments)); // [object Arguments]
    for (var i = 0; i< arguments.length; i++) {
        console.log(toString.call(arguments[i]))
    }
}
checkType(number,string,boolean,und,null,obj,array,date,err,reg,fn)
```

**注意：只有Object.prototype上的toString才能用来进行复杂数据类型的判断 **

## type API

整合typeof和Object.prototype.toString方法，创建一个checkType工具函数

​		由于typeof返回的值都是小写，checkType函数的结果也都为小写。且Math类型和JSON类型没有应用，去掉这两个类型的检测

```javascript
var array = "Boolean Number String Function Array Date RegExp Object Error Null Undefined"
var classType = {};
array.split(" ").map(item => {
    // 深拷贝
    classType[`[object ${item}]`] = item.toLowerCase();
})
//console.log(classType)
function checkType (obj) {
    // 兼容IE6，null和undefined 会识别为[objdect Object]
    if (obj == null) return obj + '';
    return typeof obj === "object" || typeof obj === "function" ?
        classType[Object.prototype.toString.call(obj)] || "object" :
    	typeof obj
}
```

* 有了checkType方法后，可以对常用的判断进行封装。例：

  ```javascript
  function isFunction (obj) {
  	reutrn checkType(obj) === "function"
  }
  ```

## instanceof

 用于判断一个变量是否某个对象的实例

```javascript
var arr=new Array();
console.log(arr instanceof Object); // true
```

**注意： instanceof 测试的 object 是指 Javascript 语法中的 object，不是指 DOM模型对象 **

##  plainObject 

https://mp.weixin.qq.com/s/UCLiU9IhR3p5dV6S_bRN6Q

判断该对象是否通过 "{}" 或 "new Object" 创建的，该对象含有零个或者多个键值对 

```javascript
$.isPlainObject()
```

##  EmptyObject 

https://mp.weixin.qq.com/s/UCLiU9IhR3p5dV6S_bRN6Q

 判断是否是空对象 

```javascript
// isEmptyObject的源码
isEmptyObject()
```

## Window对象

https://mp.weixin.qq.com/s/UCLiU9IhR3p5dV6S_bRN6Q

判断是否是window对象

```javascript
// isWindow的源码
function isWindow(obj) {
	return obj !== null && val === obj.window;
}
```

## isArrayLike

判断类数组对象，数组和类数组都会返回true.

```javascript
// isArrayLike的源码
function isArrayLike (obj) {
    // val 必须有length属性
    var length = !!obj && "length" in obj && val.length;
    var typeRes = checkType(obj); 
    // 排除掉Function和Window对象
    if(typeRes === 'function' || isWindow(obj)) {
        return false；
    }
    return typesRes === 'array' || length === 0 || 
        typeof length === "number" && length > 0 && (length - 1) in val;
}

/*
	return 使用了 || 语句，只要一个为 true，结果就返回 true。
	所以如果 isArrayLike 返回true，至少要满足三个条件之一：是数组、长度为0和length 属性是大于 0 的数字类型，并且val[length - 1]必须存在。
*/
```

##  isElement 

 判断是不是 DOM 元素。 它是 underscore 提供的方法

```javascript
isElement = function (obj) {
    return !!(obj && obj.nodeType === 1);
}
```



# Javascript深浅拷贝

## 数组的浅拷贝

* 如果是数组，可以利用数组的一些方法如：slice()、concat()返回一个新数组的特性来实现拷贝。

  ```javascript
  var arr = ['old', 1, true, null, undefined];
  var newArr = arr.concat();
  // var  newArr = arr.slice();
  newArr[0] = 'new';
  console.log(arr); // ['old', 1, true, null, undefined]
  console.log(newArr); // ['new', 1, true, null, undefined]
  ```

* 如果 数组嵌套数组或对象

  ```javascript
  var arr = [{old: 'old'},['old']];
  var newArr = arr.concat();
  arr[0].old ='new';
  arr[1][0] = 'new';
  console.log(arr); // [{old: 'new'},['new']]
  console.log(newArr); // [{old: 'new'},['new']]
  ```

  **注意：这种情况下，拷贝的并不彻底。旧数组的值改变会影响新的数组。所以浅拷贝只适合基本数据类型，对象和数组则不是将值赋值给新的变量，只是可以引用。**

  concat()、slice()属于技巧类的浅拷贝，所以不彻底的复制引用的拷贝方法就是**浅拷贝**

* 浅拷贝的原生实现

  ```javascript
  var shallowCopy = function (obj) {
      // 只拷贝被对象
      if (typeof obj !== 'object') return;
      var newObj = obj instanceof Array ? [] : {};
     // 遍历val,并且判断是val属性才拷贝
      for(var key in obj) {
          if(obj.hasOwnProperty(key)) {
              newObj[key] = val[obj];
          }
      }
      return newObj;
  }
  console.log(shallowCopy([1,'x','s',[3,4]]))
  
  // hasOwnProperty() 方法会返回一个布尔值，指示对象自身属性中是否具有指定的属性（也就是，是否有指定的键）
  ```

  

## 数组的深拷贝

不管数据如何嵌套，拷贝的数据和原数据，不会互相影响，就是**深拷贝**。

* JSON字符串转换实现

  ```javascript
  var arr = ['old', 1, true, ['Zen', 'Win'], {old: 1}];
  var newArr = JSON.parse(JSON.stringify(arr));
  newArr[0] = 'new'
  newArr[4].old = 2;
  console.log(arr); //  ['old', 1, true, ['Zen', 'Win'], {old: 1}]
  console.log(newArr); // ["new", 1, true, ['Zen', 'Win'], {old: 2}]
  
  // 这个方法利用JSON转换了arr的数据类型，将它变为了一个普通数据类型
  ```

* 深拷贝原生实现

  ```javascript
  var deepCopy = function (obj) {
      if (typeof obj !== 'object') return;
      var newObj = obj instanceof Array ? [] : {};
      for(var key in obj) {
          if(obj.hasOwnProperty(key)) {
              newObj[key] = typeof obj[key] === 'object' ? deepCopy(obj[key]) : obj[key];
          }
      }
      return newObj;
  }
  
  // 拷贝的时候判断一下属性值的类型，如果是对象，用递归调用函数
  ```

  