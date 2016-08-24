---
layout:     post
title:      javascript Array原型方法
subtitle:   ""
date:       2016-01-06 16:05:14
author:     "Cyclone77"
header-img: "img/post-bg-js-version.jpg"
permalink:  "/1472014211844"
tags:
    - 前端开发
    - JavaScript
---
以下内容有MDN整理所得。

**构造函数**
{% highlight ruby %}
new Array();
new Array(size);
new Array(element0, element1,……, elementn);
{% endhighlight %}
属性
    length 可以读写(改变length数组的元素不同).

----

方法(Array.prototype原型的方法):

**concat:(将传入的数组或非数组值与原数组合并,组成一个新的数组并返回.)**
{% highlight ruby %}
//语法: array.concat(value1, value2, ..., valueN);
var arr1 = new Array("x", "y", "z");
var arr2 = new Array("m", "n");
var arr = arr1.concat("a", "b", ["c", "d"], arr2);
//arr=[x,y,z,a,b,c,d,m,n];
{% endhighlight %}

---

**every() 方法测试数组的所有元素是否都通过了指定函数的测试。**
{% highlight ruby %}
//语法:arr.every(callback[, thisArg])
//callback 被调用时传入三个参数：元素值，元素的索引，原数组。
var passed = [12, 5, 8, 130, 44].every(function (value, index, array) {
        return value >= 10;
    })
// passed= false;

passed = [12, 54, 18, 130, 44].every(isBigEnough);
function isBigEnough(element, index, array) {
  return (element >= 10);
}
// passed= true;
{% endhighlight %}

---

**filter() 方法使用指定的函数测试所有元素，并创建一个包含所有通过测试的元素的新数组。**
{% highlight ruby %}
//语法:arr.filter(callback[, thisArg])
//callback 被调用时传入三个参数：元素值，元素的索引，原数组。
var arr = [12, 5, 8, 130, 44].filter(function (value, index, array) {
        return value >= 10;
})
// arr =[12,130,44];
{% endhighlight %}

---

**forEach() 方法让数组的每一项都执行一次给定的函数。**
{% highlight ruby %}
//语法:array.forEach(callback[, thisArg])
//callback 函数会被依次传入三个参数：数组当前项的值，数组当前项的索引，数组对象本身
[12, 5, 8, 130, 44].forEach(function (value, index, array) {
        console.log(value);
})
//结果:12, 5, 8, 130, 44
{% endhighlight %}
注意： 没有办法中止或者跳出 forEach 循环，除了抛出一个异常。如果你需要这样，使用forEach()方法是错误的，你可以用一个简单的循环作为替代。

---

**indexOf()方法返回给定元素能找在数组中找到的第一个索引值，否则返回-1。**
{% highlight ruby %}
//语法：arr.indexOf(searchElement[, fromIndex = 0])
var p = [12, 5, 8, 130, 44].indexOf(8);
//等价于[12, 5, 8, 130, 44].indexOf(8, 0);
//p==2
var p = [12, 5, 8, 130, 44].indexOf(8, 2);
//p==2
{% endhighlight %}

---

**join() 方法将数组中的所有元素连接成一个字符串。**
{% highlight ruby %}
//语法: str = arr.join([separator = ','])
//参数可选，用于指定连接每个数组元素的分隔符。
var a = ['Wind', 'Rain', 'Fire'];
var myVar1 = a.join();      // myVar1的值变为"Wind,Rain,Fire"
var myVar2 = a.join(', ');  // myVar2的值变为"Wind, Rain, Fire"
var myVar3 = a.join(' + '); // myVar3的值变为"Wind + Rain + Fire"
var myVar4 = a.join('');    // myVar4的值变为"WindRainFire"
{% endhighlight %}

---

**map() 方法返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组。**
{% highlight ruby %}
//语法:array.map(callback[, thisArg])
//callback 函数会被自动传入三个参数：数组元素，元素索引，原数组本身。
["1", "2", "3"].map(function (value) {
        return parseInt(value);
});
//[1,2,3]
{% endhighlight %}

---

**pop() 方法删除一个数组中的最后的一个元素，并且返回这个元素。**
{% highlight ruby %}
//语法:array.pop()
var arr=[2,3,1];
var last = arr.pop();
//last==1;arr =[2,3];
{% endhighlight %}

---

**push() 方法添加一个或多个元素到数组的末尾，并返回数组新的长度（length 属性值）。**
{% highlight ruby %}
//语法:arr.push(element1, ..., elementN)
var arr = [3, 1, 2];
var len = arr.push(5, 4);
//arr=[3, 1, 2, 5, 4]; len =5;

//合并两个数组
var vegetables = ['parsnip', 'potato'];
var moreVegs = ['celery', 'beetroot'];
Array.prototype.push.apply(vegetables, moreVegs);
//vegetables = ["parsnip", "potato", "celery", "beetroot"];
{% endhighlight %}

---

**reduce() 方法接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始合并，最终为一个值。**
{% highlight ruby %}
//语法:arr.reduce(callback,[initialValue])
//接受四个参数：初始值（或者上一次回调函数的返回值），当前元素值，当前索引，调用 reduce 的数组。
[0,1,2,3,4].reduce(function(previousValue, currentValue, index, array){
  return previousValue + currentValue;
});
//10
[0,1,2,3,4].reduce(function(previousValue, currentValue, index, array){
  return previousValue + currentValue;
}, 10);
//20
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
    return a.concat(b);
});
// flattened = [0, 1, 2, 3, 4, 5];
{% endhighlight %}

---

**reverse() 方法颠倒数组中元素的位置。第一个元素会成为最后一个，最后一个会成为第一个。**
{% highlight ruby %}
//语法: arr.reverse()
//[1,2,4,3,5].reverse()
//[5, 3, 4, 2, 1]
{% endhighlight %}

---

**shift() 方法删除数组的 第一个 元素，并返回这个元素。该方法会改变数组的长度。**
{% highlight ruby %}
//语法:arr.shift()
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];
var shifted = myFish.shift(); 
//myFish = ["clown", "mandarin", "surgeon"]
//shifted = "angel"
{% endhighlight %}

---

**slice() 方法把数组中一部分的浅复制（shallow copy）存入一个新的数组对象中，并返回这个新的数组。**
{% highlight ruby %}
//语法:array.slice(begin[, end])
 ["Banana", "Orange", "Lemon", "Apple", "Mango"].slice(1, 3);
//["Orange", "Lemon"]
//如果省略 begin，则 slice 从索引 0 开始。
["Banana", "Orange", "Lemon", "Apple", "Mango"].slice(null,3)
["Banana", "Orange", "Lemon"]
//如果 end 被省略，则slice 会一直提取到原数组末尾。
["Banana", "Orange", "Lemon", "Apple", "Mango"].slice(3)
//["Apple", "Mango"]
Array.prototype.slice.call("hello world",6,11).join("")
//"world"
{% endhighlight %}

---

**some() 方法测试数组中的某些元素是否通过了指定函数的测试。**
{% highlight ruby %}
//语法:arr.some(callback[, thisArg])
//callback 被调用时传入三个参数：元素的值，元素的索引，被遍历的数组。
var passed = [12, 5, 8, 130, 44].some(function (value, index, array) {
        return value >= 10;
})
//passed = true;
var heo = Array.prototype.some.call("hello world!", function (item) {
        return item == "a";
})
//heo = false;
{% endhighlight %}

**sort() 方法对数组的元素做原地的排序，并返回这个数组。 sort 可能不是稳定的。默认按照字符串的UNICODE码位点（code point）排序。**
{% highlight ruby %}
//语法:arr.sort([compareFunction])
var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
//[1, 2, 3, 4, 5]
{% endhighlight %}

---

**splice() 方法用新元素替换旧元素，以此修改数组的内容。**
{% highlight ruby %}
//语法:array.splice(start, deleteCount[, item1[, item2[, ...]]])
var myFish = ["angel", "clown", "mandarin", "surgeon"];

//从第 2 位开始删除 0 个元素，插入 "drum"
var removed = myFish.splice(2, 0, "drum");
//运算后的 myFish:["angel", "clown", "drum", "mandarin", "surgeon"]
//被删除元素数组：[]，没有元素被删除

//从第 3 位开始删除 1 个元素
removed = myFish.splice(3, 1);
//运算后的myFish：["angel", "clown", "drum", "surgeon"]
//被删除元素数组：["mandarin"]

//从第 2 位开始删除 1 个元素，然后插入 "trumpet"
removed = myFish.splice(2, 1, "trumpet");
//运算后的myFish: ["angel", "clown", "trumpet", "surgeon"]
//被删除元素数组：["drum"]

//从第 0 位开始删除 2 个元素，然后插入 "parrot", "anemone" 和 "blue"
removed = myFish.splice(0, 2, "parrot", "anemone", "blue");
//运算后的myFish：["parrot", "anemone", "blue", "trumpet", "surgeon"]
//被删除元素的数组：["angel", "clown"]

//从第 3 位开始删除 2 个元素
removed = myFish.splice(3, Number.MAX_VALUE);
//运算后的myFish: ["parrot", "anemone", "blue"]
//被删除元素的数组：["trumpet", "surgeon"]
{% endhighlight %}

---

**toLocaleString() 返回一个字符串表示数组中的元素。数组中的元素将使用各自的 toLocaleString 方法转成字符串，这些字符串将使用一个特定语言环境的字符串（例如一个逗号 ","）隔开。**
{% highlight ruby %}
//语法:arr.toLocaleString();
["a",1,new Date()].toLocaleString();
//"a,1,2016/1/7 上午11:46:45"
{% endhighlight %}

---

**toString() 返回一个字符串，表示指定的数组及其元素。**
{% highlight ruby %}
//语法:arr.toString()
var monthNames = ['Jan', 'Feb', 'Mar', 'Apr'];
var myVar = monthNames.toString();
//"Jan,Feb,Mar,Apr"
{% endhighlight %}

---

**unshift() 方法在数组的开头添加一个或者多个元素，并返回数组新的 length 值。**
{% highlight ruby %}
//语法:arr.unshift(element1, ..., elementN)
var arr = [1, 2];
arr.unshift(0); //result of call is 3, the new array length
//arr is [0, 1, 2]

arr.unshift(-2, -1); // = 5
//arr is [-2, -1, 0, 1, 2]

arr.unshift( [-3] );
//arr is [[-3], -2, -1, 0, 1, 2]
{% endhighlight %}