---
layout: article
title: The summary of javascript
tags: javascript
key: article-js
---

> 本篇总结了关于Javascript的一些知识点，都是一些基础知识，其中包括那些容易让人混淆和相似的方法，当中有一些知识点也是面试过程中经常被问到的，特此总结起来，希望大家共勉。

<!--more-->


基本数据类型
------------

> **Number, String, Boolean, null, undefined, Object**六大类
>
> ES6新增**Symbol**(创建后独一无二且不可变的数据类型)

字符串（ES6新增特性）
------

1.  字符串模板: 反单引号括起来，内部变量引用`${}`,同时可以随意换行。反单引号括起来的内容原样输出。

    ```javascript
        let a = {
          name: 'will',
          age: 18
        };

        alert(`我是${a.name},今年${a.age}岁`);
    ```
2.  startsWith: 检测字符串是否以子字符串开头。

    > string.startsWith(searchvalue, start) -- 第一个参数必填，是要查找的字符串。 第二个参数选填，查找的开始位置，默认0。 该方法返回布尔值。

    ```javascript
        let str = 'Hello world!!';
        str.startsWith('Hello');    // true
        str.startsWith('hello');    // false
        str.startsWith('world', 6); // true
    ```

3.  endsWith: 检测字符串是否以子字符串结尾。

    > string.endsWith(searchvalue, length) -- 第一个参数必填，要查找的字符串。第二个选填，查找的字符串结尾位置，默认字符串长度。 返回布尔值。

    ```javascript
        let str = 'To be, or not to be, that is the question.';
        str.endsWith('question.');    // true
        str.endsWith('to be', 19);    // true
    ```

数组
----

1.	indexOf

    > 数组通过 **indexOf()** 来搜索一个元素的指定位置。

    ```javascript
        var arr = [1,3,5,7,'7'];
        arr.indexOf(7);     //元素的索引值为3
        arr.indexOf(30);    //元素30没有找到，返回-1
    ```

2.	slice

    > **slice()** 截取数组部分元素，返回一个新数组。

    ```javascript
        var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
        arr.slice(0, 3);  // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
        arr.slice(3);     // 从索引3开始到结束: ['D', 'E', 'F', 'G']
    ```

3.	push和pop

    > **push()** 向数组末尾添加元素。 **pop()** 删除数组最后一个元素。

4.	unshift和shift

    > **unshift()** 从数组头部添加元素。 **shift()** 删除数组第一个元素。

5.	sort

    > **sort()** 可以对当前数组进行排序，它会直接修改当前数组元素位置。直接调用时，会按默认顺序进行排序。

    ```javascript
        var arr = ['B', 'C', 'A'];
        arr.sort();
        console.log(arr);  //['A', 'B', 'C']
    ```

    ```javascript
        // 数组按大小排序
        let arr = [12,5,8,66,35,1,9];

        arr.sort(function(n1,n2) {
          return n1 - n2;
        });

        alert(arr);

        // 比较函数应该具有两个参数 a 和 b，其返回值如下：
        // 若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
        // 若 a 等于 b，则返回 0。
        // 若 a 大于 b，则返回一个大于 0 的值。
    ```

6.	reverse

    > **reverse()** 让数组倒序排列。

7.	splice

    > **splice()** 修改数组的“万能方法”，可以从指定的索引开始删除元素，然后再从该位置添加元素。

    ```javascript
        var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];

        //从索引2开始删除3个元素，并添加'Google'和'Facebook'
        arr.splice(2, 3, 'Google', 'Facebook');   //返回删除的元素['Yahoo', 'AOL', 'Excite']
        console.log(arr);   //['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']

        //只删除，不添加
        arr.splice(2, 2);   //返回删除的元素['Google', 'Facebook']
        console.log(arr);   //['Microsoft', 'Apple', 'Oracle']

        //只添加，不删除
        arr.splice(2, 0, 'Google', 'Facebook');   //由于没有删除元素，返回[]，从索引2的位置开始添加，原位置元素往后挤
        console.log(arr);   //['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
    ```

8.	concat

    > **concat()** 把当前数组和另一个数组连接起来，并返回一个新数组。

    ```javascript
        var a = ['a', 'b', 'c'];
        var b = a.concat([1, 2, 3]);
        console.log(b);   //['a', 'b', 'c', 1, 2, 3]
        console.log(a);   //['a', 'b', 'c']
    ```

    > **concat()** 可以接手任意个元素和数组，并自动把数组拆开，然后全部添加到新的数组里。

    ```javascript
        var arr = ['a', 'b', 'c'];
        var arred = arr.concat(1, 2, [3, 4]);
        console.log(arred);   //['a', 'b', 'c', 1, 2, 3, 4]
    ```

9.	join

    > **join()** 把当前数组的每个元素都用指定的字符串连接起来，然后返回连接后的字符串。

    ```javascript
        var arr = ['A', 'B', 'C', 1, 2, 3];
        arr.join('-');    //A-B-C-1-2-3
    ```

判断对象自身拥有的属性用hasOwnProperty()
----------------------------------------

```javascript
    var xiaoming = {
      name: '小明'
    };
    xiaoming.hasOwnProperty('name');      //true
    xiaoming.hasOwnProperty('toString');  //false
```

for循环
-------

1.	for...in 循环对象的所有属性（**键值**）

	```javascript
	  var a = {
	    name: '张三',
	    age: 25,
	    sex: 'man',
	    city: '北京'
	  };
	  for(var key in a) {
	    console.log(key);   //name,age,sex,city
	  }
	```

	> 由于**数组**也是对象，而它的每个元素的**索引**被视为对象的属性，因此for..in循环可以直接循环出**数组**的索引

	```javascript
	  var a = ['A','B','C'];
	  for(var index in a) {
	    console.log(index);       //0,1,2
	    console.log(a[index]);    //A,B,C
	  }
	```

2.	for...of ES6开始引入，作为遍历所有数据结构的统一的方法

	-	遍历数组： 直接返回数组元素（for...in 返回数组索引）

	for...of 怎么获取数组索引值？

	```javascript
	    var a = [1,3,5,99,88,56];
	    for(let [index, item] of a.entries()) {
	      console.log(index);   //0,1,2,3,4,5
	      console.log(item);    //1,3,5,99,88,56
	    }
	```

	> **entries()** 返回一个遍历器对象，用来遍历[键名,键值]组成的数组。对于数组，键名就是索引值。对于set，键名与键值相同。Map结构的Iterator接口，默认就是调用entries方法。

	-	遍历对象：不能循环普通对象，需要配合new Map()和Object.keys()、Object.values()使用

	```javascript
	    var student = new Map();
	    student.set('name', '张三').set('age','25');
	    for(let key of student.keys()) {
	      console.log(key);     //name,age
	    }
	    for(let value of student.values()) {
	      console.log(value);   //张三,25
	    }
	    for(let [key, value] of student) {
	      console.log(key);
	      console.log(value);
	    }
	```

	> **keys()** 返回一个遍历器对象，用来遍历所有的键名。
	>
	> **values()** 返回一个遍历器对象，用来遍历所有的键值。

3.	forEach 调用数组的每个元素，并将元素返回给回调函数。只是个数组的方法。

	```javascript
	  //语法
	  var arr = ['a', 'b', 'c'];
	  arr.forEach(function(element, index, array){
	    //element: 当前元素
	    //index: 当前元素的索引
	    //array: Array对象本身
	  });
	```

	> `forEach`循环无法用**break**和**return**中断。

	`Set`与`Array`类似，但是Set没有索引。所以前两个参数都是对应当前元素。

	```javascript
	  var set = new Set([1, 2, 3]);
	  set.forEach(function(element, sameElement, set){
	    //element: 当前元素
	    //sameElement: 当前元素
	    //set: Set本身
	  });
	```

	`Map`的回调参数依次为`value`,`key`和`map`。

	```javascript
	  var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
	  m.forEach(function(value, key, map){
	    //value: x,y,z
	    //key: 1,2,3
	    //map: Map{1 => 'x', 2 => 'y', 3 => 'z'}
	  });
	```

while和do...while
-----------------

> **for** 循环在已知循环的初始和结束条件时非常有用。而上述忽略了条件的for循环容易让人看不清循环的逻辑，此时用**while**循环更佳。
>
> **while** 循环只有一个判断条件，条件满足，就不断循环，条件不满足时则退出循环。比如我们要计算100以内所有奇数之和，可以用while循环实现

```javascript
    var x = 0;
    var n = 99;

    while (n > 0) {
      x = x + n;
      n = n - 2;
    }

    x;    // 2500
```

> **do { ... } while()** 循环，它和while循环的唯一区别在于，不是在每次循环开始的时候判断条件，而是在每次循环完成的时候判断条件：

```javascript
    var n = 0;

    do {
      n = n + 1;
    } while (n < 100);

    n; // 100
```

> 用**do { ... } while()** 循环要小心，循环体会至少执行1次，而**for**和**while**循环则可能一次都不执行。

Map和Set（ES6引入）
-------------------

-	**Map** 是一组键值对的结构，具有极快的查找速度。

	**Map** 实现方法：

	```javascript
	  var m = new Map([['刘备', 95], ['关羽', 97], ['张飞', 67]]);
	  m.get('张飞');    //67
	```

	```javascript
	  var m = new Map();
	  m.set('张三', 77);
	  m.set('李四', 56);
	  m.has('李四');      //true
	  m.get('李四');      //56
	  m.delete('李四');   //删除key
	  m.get('李四');      //undefined
	```

-	**Set** 对象是值的集合，你可以按照插入的顺序迭代它的元素。**Set** 中的元素是唯一的。

	```javascript
	  var s = new Set([1, 2, 3, 3, '3']);
	  s;    //Set {1,2,3,'3'}
	```

	Set通过`add(key)`方法添加元素，`delete(key)`方法删除元素。

	```javascript
	  var s1 = new Set([1, 2, 3]);
	  s1.add(4);
	  s1;
	  s1.delete(4);
	  s1;
	```

	> 获取**Set**长度不能用`length`，而是用`size`。

**iterable**（可迭代对象）
--------------------------

> ES6标准引入的新类型。**Array**、**Map**和**Set**都属于`iterable`类型。
> 具有 **iterable** 类型的集合都可以通过`for...of`遍历。
> iterable内置`forEach`方法，它接收一个函数，每次迭代就自动回调该函数。

数组的方法
----------

1.  map -- 映射

    > 一对一，生成一个新数组，与原有数组关系一一对应

    ```javascript
        // 判断学生成绩是否及格
        let arr1 = [55,62,85,32,41,5,92];

        let arr2 = arr1.map(function(item) {
          if(item >= 60) {
            return true;
          }else {
            return false;
          }
        });

        // arr2可以简写
        // let arr2 = arr1.map(item => item >= 60);

        console.log(arr2);    // [false, true, true, false, false, false, true]
    ```

2.  reduce -- 汇总：一堆 => 一个

    ```javascript
        // 求平均值
        let arr = [55,62,85,32,41,5,92];

        let ave = arr.reduce((tmp, item, index) => {
          if(index < arr.length - 1) {
            return tmp + item;
          }else {
            return (tmp + item)/arr.length;
          }
        });

        // tmp: 中间值, item: 当前值, index: 索引

        console.log(ave);   // 53.142857142857146
    ```

3.  filter  -- 过滤

    > 返回新数组，原数组不改变

    ```javascript
        // 有一个数组[55,62,85,32,41,5,92]，只保留偶数。
        let arr1 = [55,62,85,32,41,5,92];

        let arr2 = arr1.filter(function(item){
          if(item%2 == 0) {
            return true;
          }
        });

        // 简写为：let arr2 = arr1.filter(item => item%2 == 0);

        // 保留奇数
        let arr3 = arr1.filter(item => item%2);

        console.log(arr2);    // [62, 32, 92]
        console.log(arr3);    // [55, 85, 41, 5]
    ```

4.  forEach  -- 遍历

    ```javascript
        //数组求和
        let arr = [55,62,85,32,41,5,92];

        let sum = 0;
        arr.forEach(item => {
          sum += item;
        });

        console.log(sum);   // 372
    ```

5.  from -- 把类数组元素转换成数组

    > Array.from([array-like]) => [x,x,x];

    ```javascript
        let aDiv = document.getElementsByTagName('div');

        Array.from(aDiv).forEach(item => item.style.background = 'yellow');
    ```

json在ES6中的简写
--------------------

1. key: value -- 名字和值相同时，可以省略

    ```javascript
        let a = 5;
        let b = 8;

        //正常写法
        let jsonA = {a: a, b: b};
        //简写
        let jsonB = {a, b};
        console.log(jsonA);    // {a: 5, b: 8}
        console.log(jsonB);    // {a: 5, b: 8}
    ```

2. 函数 -- 函数可省略`function`

    ```javascript
        let json_a = {
          a: 5,
          b: 8,
          sum: function(){
            alert(this.a + this.b);
          }
        };

        //简写
        let json_b = {
          a: 5,
          b: 8,
          sum(){
            alert(this.a + this.b);
          }
        };

        json_a.sum();   // 13
        json_b.sum();   // 13
    ```

函数
----

1.  箭头函数(实际就是function的简写)(ES6)

    ```javascript
        function(参数，参数) {
          // 函数体
        }

        (参数，参数) => {
          // 函数体
        }
    ```

    - 如果有且仅有一个参数，()可以省。
    - 如果函数体只有一句话并且是return，{}可以省。

    > 关于`this`

2.  默认参数

    > (a,b=xx,c=xx)

    ```javascript
        // ES5默认值写法
        function show(a,b,c) {
          b = b||5;
          c = c||21;

          console.log(a,b,c);
        }

        show(12);   // 12,5,21

        // 传参时，有一个特殊值：0，传0相当于false，所以参数还是等于默认值。
        // 传0 => if(!b) b = 5;
    ```

    ```javascript
        // ES6新增默认参数写法
        function show(a,b=5,c=21) {
          console.log(a,b,c);
        }

        show(12);   // 12,5,21
    ```

3.  参数展开（剩余参数、数组展开）-- 实际就是rest参数

    - “三个点”的第1个用途：接受剩余参数

      > function 函数名(a, b, ...变量名)
      >
      > 剩余参数必须在参数列表的最后

    - “三个点”的第2个用途：展开一个数组


    -	arguments

    只在函数内部起作用，并且永远指向当前函数的调用者所传入的所有参数。**arguments不支持箭头函数**

    ```javascript
        function foo(x){
          for(var item of arguments) {
            console.log(item);
          }
        }

        foo(10,20,30);    //10,20,30
    ```

    -	rest参数（`...变量名`）

    ES6为了解决传入的参数数量不一定的情况下而引入。**rest参数** 本身就是数组，数组的方法都适用。

    ```javascript
        function foo(a,b,...rest) {
          console.log(a);   //1
          console.log(b);   //2
          console.log(rest);    //[3,4,5]
        }

        foo(1,2,3,4,5);
    ```

    -	return语句可以拆成两行。但要注意加`{}`。这时候返回的是对象。

    ```javascript
        function foo() {
          return {
            name: 'lisa'
          };
        }
    ```

变量作用域
----------

-	Javascript的函数在查找变量时，从自身函数定义开始，从‘内’向‘外’查找。如果内部函数定义了与外部函数同名的变量，则内部函数的变量将‘屏蔽’外部函数的变量。

```javascript
    function foo() {
      var x = 1;
      function bar() {
          var x = 'A';
          console.log('x in bar() = ' + x); // 'A'
      }
      console.log('x in foo() = ' + x); // 1
      bar();
    }

    foo();

    //运行结果：
    //x in foo() = 1
    //x in bar() = A
```

-	变量提升

> JavaScript函数定义有个特点，先扫描整个函数体的语句，把所有声明的变量“提升”到函数顶部。但不会提升**变量的赋值**

-	全局作用域

> JavaScript实际上只有一个全局作用域。任何变量（函数也视为变量），如果没有在当前函数作用域中找到，就会继续往上查找，最后如果在全局作用域中也没有找到，则报`ReferenceError`错误。

-	局部作用域

> JavaScript的变量作用域实际上是函数内部，在for循环等语句块中无法定义具有局部作用域的变量。

```javascript
    function foo() {
      for (var i=0; i<100; i++) {
        //...
      }

      i += 100;   //仍然可以引用变量i
    }
```

> 为了解决**块级作用域**，ES6引入了新的关键字**let**。

```javascript
    function foo() {
      var sum = 0;
      for (let i=0; i<100; i++) {
          sum += i;
      }
      // SyntaxError:
      i += 1;
    }
```

- 变量(`var/let`)

1.  var

    缺点：可以重复定义、不能限制修改、函数级作用域

    ```javascript
        var a = 12;

        // ......
        // ......

        var a = 5;
        alert(a);   // 5
    ```

    ```javascript
        // 函数级作用域的缺点
        let aBtn = document.getElementsTagName('button');

        for(var i = 0;i < 3;i++) {
          aBtn[i].onclick = function() {
            alert(i);     // 每次点击按钮弹出 3
          }
        }


    ```

    ```javascript
        // 正常弹出对应数字，需把循环var定义的 i 用 let定义
        for(let i = 0;i < 3;i++) {
          aBtn[i].onclick = function() {
            alert(i);     // 每次点击按钮弹出对应0,1,2
          }
        }
    ```

    > 用`var`定义变量时解决此类问题可以使用**闭包**

    ```javascript
        let aBtn = document.getElementsTagName('button');

        for(var i = 0;i < 3;i++) {
          (function(i) {
            aBtn[i].onclick = function() {
              alert(i);     // 每次点击按钮弹出0,1,2
            }
          })(i);
        }
    ```

2.  let

    特点：不能重复定义、块级作用域

    ```javascript
        let a = 12;

        //......
        //......

        let a = 5;
        alert(a);   // 报错：提示a已定义
    ```

- 闭包

> 闭包可以让你从内部函数访问外部函数作用域。可以理解成**定义在函数内部的函数**。

```javascript
    function init() {
      var name = 'William';

      function displayName() {
        alert(name);
      };

      displayName();    // displayName函数就是一个闭包
    }
    init();
```

-	常量

> 在ES6之前声明常量通常用全部大写的变量来表示。ES6标准引入了新的关键字**const**来定义常量。
> `const`和`let`都是块级作用域

-	解构赋值(ES6)

    - 左右两边必须一样
    - 必须定义和赋值同步完成

> 可以同时对多个变量同时赋值。

```javascript
    var [x, y, z] = ['hello', 'javascript', 'ES6'];
    console.log(x + ',' + y + ',' + z);   //hello,javascript,ES6
```

> 对数组元素进行解构赋值是，多个变量要用`[...]`括起来。
>
> 如果数组本身有嵌套，注意嵌套层次和位置要和数组本身保持一致。

```javascript
    let [x, [y, z]] = ['hello', ['JavaScript', 'ES6']];
    x; // 'hello'
    y; // 'JavaScript'
    z; // 'ES6'
```

> 解构赋值还可以忽略某些元素。

```javascript
    let [, , z] = ['hello', 'javascript', 'ES6'];
    z;    //'ES6'
```

> 如果需要从一个对象中取出若干属性，也可以使用解构赋值。

```javascript
    var person = {
      name: '小明',
      age: 20,
      gender: 'male',
      passport: 'G-12345678',
      school: 'No.4 middle school'
    };
    var {name, age, passport} = person;

    // name, age, passport分别被赋值为对应属性:
    console.log('name = ' + name + ', age = ' + age + ', passport = ' + passport);

    // 输出结果：name = 小明, age = 20, passport = G-12345678
```

> 同样对象的嵌套也可以用解构赋值。

```javascript
    var person = {
      name: '小明',
      age: 20,
      gender: 'male',
      passport: 'G-12345678',
      school: 'No.4 middle school',
      address: {
        city: 'Beijing',
        street: 'No.1 Road',
        zipcode: '100001'
      }
    };
    var {name, age, address:{city, zip}} = person;

    city; // 'Beijing'
    zip;  // undefined  属性名是：zipcode

    //注意：address不是变量名，而是为了取得嵌套的address对象的属性。
    address;  // Uncaught ReferenceError: address is not defined
```

> 使用解构赋值对对象进行赋值时，如果想自定义变量名，可使用`key: 变量名`的方式来获取。

```javascript
    var person = {
      name: '小明',
      age: 20,
      gender: 'male',
      passport: 'G-12345678',
      school: 'No.4 middle school',
      address: {
        city: 'Beijing',
        street: 'No.1 Road',
        zipcode: '100001'
      }
    };
    var {name, passport: id} = person;

    console.log(id);  //'G-12345678'
```

方法
----

在一个对象中绑定函数，称为这个对象的方法。

> 在一个方法内部，**this** 是一个特殊变量，它始终指向当前对象。
>
> JavaScript的函数内部如果调用了`this`，指向谁视情况而定。
> 如果单独调用函数，比如getAge()，此时，该函数的 `this` 指向全局对象，也就是 **window**。
>
> 要保证 `this` 指向正确，必须用 `obj.xxx()` 的形式调用！

面向对象（OOP--面向对象编程）
--------

    把现实生活的事物以及关系，抽象成类，通过继承，实现，组合的方式把万事万物都给容纳了。

    面向对象的底层其实还是面向过程，把面向过程抽象成类，然后封装，方便我们使用的就是面向对象。

    面向过程是具体化的，流程化的，解决一个问题，需要一步一步的分析，一步一步的实现。

    面向对象是模型化的，只需抽象出一个类，这是一个封闭的盒子，在这里你拥有数据也拥有解决问题的办法。

1.  面向对象的基本特征（三大特性）

    - 封装：隐藏对象的属性和实现细节，仅对外提供公共访问方式，将变化隔离，便于使用，提高复用性和安全性。

    - 继承：提高代码复用性。继承是多态的前提。继承的过程就是从一般到特殊的过程。

    - 多态：一个方法多种表现形式。父类或接口定义的引用变量可以指向子类或具体实现类的实例对象。提高了程序的拓展性。

2.  五大基本原则

    - 单一职责原则 SRP：类的功能要单一，不能包罗万象。

    - 开放封闭原则 OCP：一个模块对于拓展是开放的，对于修改是封闭的。

    - 里式替换原则 LSP：子类可以替换父类出现在父类能够出现的任何地方。

    - 依赖倒置原则 DIP：高层次的模块不应该依赖于低层次的模块，他们都应该依赖于抽象。具体实现应该依赖于抽象。比方说你出国要说你是中国人，而不能说你是哪个村子的。比如说中国人是抽象的，下面有具体的xx省，xx市，xx县。你要依赖的是抽象的中国人，而不是你是xx村的。

    - 接口分离原则 ISP：设计时采用多个与特定客户类有关的接口比采用一个通用的接口要好。

3.  Javascript是一种基于对象的语言。但是，它又不是一种真正的面向对象编程语言，因为它的语法这种没有class(类)--es6以前是这样的。所以es5只有使用函数模拟的面向对象。

    ```javascript
        function Person(name, age){
          this.name = name;
          this.age = age;
        }

        Person.prototype.showName = function(){
          alert('我叫' + this.name);
        };
        Person.prototype.showAge = function(){
          alert('我' + this.age + '岁');
        };

        let p = new Person('小哈', 18);
        p.showName();
        p.showAge();

        // 继承
        function Worker(name, age, job){
          Person.call(this, name, age)
          this.job = job;
        }

        Worker.prototype = new Person();
        Worker.prototype.constructor = Worker;  // 修正构造函数
        Worker.prototype.showJob = function(){
          alert('我的工作是' + this.job);
        };

        let w = new Worker('大哈', 19, '吃饭');
        w.showName();
        w.showAge();
        w.showJob();
    ```

    > ES6中面向对象的写法：

    ```javascript
        class Person{
          constructor(name, age) {
            this.name = name;
            this.age = age;
          }

          showName() {
            alert('我叫' + this.name);
          }

          showAge() {
            alert('我' + this.age + '岁');
          }
        }

        let p = new Person('小哈', 18);
        p.showName();
        p.showAge();

        // 继承
        class Worker extends Person{
          constructor(name, age, job) {
            super(name, age);
            this.job = job;
          }

          showJob() {
            alert('我的工作是' + this.job);
          }
        }

        let w = new Worker('大哈', 19, '吃饭');
        w.showName();
        w.showAge();
        w.showJob();
    ```

    >  super -- 超类（父类）

4.  this指向问题

  - 普通函数：this的指向是根据谁在调用。this老变。

  - 箭头函数：this指向是根据**所在的环境**。this恒定。

  - 用`xxx.bind()`绑定。实际上`bind`给函数定死一个`this`。

    ```javascript
        class Person{
          constructor(name, age) {
            this.name = name;
            this.age = age;
          }

          showName() {
            alert('我叫' + this.name);
          }

          showAge() {
            alert('我' + this.age + '岁');
          }
        }

        let p = new Person('小哈', 18);

        // es5的解决办法：包在函数里
        // document.onclick = function() {
        //   p.showName();
        // };

        // es6
        document.onclick = p.showName.bind(p);
    ```

Promise
-------

Promise -- 将异步操作同步化

`let p = new Promise((resolve, reject) => {});`

> Promise有两个参数，一个成功，一个失败。

```javascript
    Promise.all(
      $.ajax({url:'',dataType:'json'}),
      $.ajax({url:'',dataType:'json'}),
      $.ajax({url:'',dataType:'json'})
    ).then(()=>{
      let [a,b,c] = resolve;
    },()=>{
      alert("失败了");
    });
```

> Jquery里的ajax实际上就是 Promise。then()里有两个参数，一个成功，一个失败。

- Promise.all()     与：所有的都成功才触发成功事件

- Promise.race()    或：只要有一个完成就可以触发成功事件

> Promise实际是一个构造函数，自身拥有all,race,resolve,reject方法，原型上有then,catch方法。

> catch()  捕获异常，第一个作用和then里的失败函数一样，抛出错误信息。另一个作用：在执行resolve的回调（也就是then中的第一个参数）时，如果抛出异常（代码出错），那么并不会报错卡死js，而是会进到这个catch方法中。

```javascript
    let p = new Promise((resolve, reject) => {
      setTimeout(
        () => {
          let num = Math.ceil(Math.random()*20);
          console.log('随机数生成的值：' + num);

          if(num <= 10) {
            resolve(num);
          }else {
            reject('由于随机数大于10，即将执行失败回调');
          }
        },
      2000);
    });

    p.then(data => {
      console.log('成功回调接受的值：', data);
      console.log(noData);
    }).catch((reason, data) => {
      console.log('catch失败执行抛出的原因：', reason);
    });
```

generator - 生成器 (过渡)
------------------

```
function *xxx() {
  .........
  .........
  let res = yield xx;
  ......
  ...
}
```

> 生成器函数用 `*` 星号表示。箭头函数不能声明生成器。

```javascript
    function *show() {
      alert('aaa');

      yield;

      alert('bbb');
    }

    let gen = show();

    gen.next();   // aaa
    gen.next();   // bbb
```

> 生成器函数中间可以暂停 -- yield

- yield

    - 参数：传参是在下一步中传值。在yield前面声明。

    - 返回：（相当于return）返回值是第一步。放在yield之后。

  ```javascript
      function *show() {
        alert('aaa');

        let a = yield 55;

        //传多个参数可以用解构赋值
        // let {a,b} = yield 55;

        alert('bbb' + a);

        return 88;
      }

      let gen = show();

      let res1 = gen.next();
      let res2 = gen.next(12);    // bbb12

      // 传多个参数
      // let res2 = gen.next({a: 5, b: 12});

      console.log(res1);          // {value: 55, done: false}
      console.log(res2);          // {value: 88, done: true}
  ```

generator和Promise配合
-----------------------

由于Promise不能执行带逻辑的数据请求，所以需要用到generator来做逻辑性的判断、执行。

```javascript
    function *show() {
      let data1 = yield $.ajax({url:'1.txt', dataType: 'json'});

      if(data1.a + data1.b <= 10) {
        let data2 = yield $.ajax({url:'2.txt', dataType: 'json'});
      }else {
        let data3 = yield $.ajax({url:'3.txt', dataType: 'json'});
      }
    }
```

async/await
------------

```
async function () {
  .........
  .........
  let res = await 异步操作（promise,generator,async）;
  ......
  ...
}
```

> async -- JS中异步操作的最终解决方案

```javascript
    async function show() {
      let data1 = await $.ajax({url: '1.txt', dataType: 'json'});

      if(data1.a + data1.b <= 10) {
        let data2 = await $.ajax({url: '2.txt', dataType: 'json'});
        alert(data2[0]);
      }else {
        let data3 = await $.ajax({url: '3.txt', dataType: 'json'});
        alert(data3.name);
      }
    }

    show();
```

> async 也支持箭头函数

```javascript
    (async function () => {
      let data1 = await $.ajax({url: '1.txt', dataType: 'json'});

      if(data1.a + data1.b <= 10) {
        let data2 = await $.ajax({url: '2.txt', dataType: 'json'});
        alert(data2[0]);
      }else {
        let data3 = await $.ajax({url: '3.txt', dataType: 'json'});
        alert(data3.name);
      }
    })();
```
> 如果await后面跟的不是异步操作，后面步骤会直接同步执行。

- await的错误处理：在aysnc里用try/catch捕获异常。

```javascript
    async function show() {
      try{
        let data2 = await $.ajax({url: '2.txt', dataType: 'json'});
        let data3 = await $.ajax({url: '3.txt', dataType: 'json'});
        let data1 = await $.ajax({url: '1.txt', dataType: 'json'});
        console.log(data1, data2, data3);
      }catch(e){
        alert('出错了');
      }
    }

    show();
```
