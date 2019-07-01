# JavaScript学习笔记

### 基础知识点

#### Array数组

###### 1. 常用方法

 + `concat()` 连接两个数组；

 + `join(str)` 用str连接数组的每一项；

 + `push(value)` 向数组的末尾追加元素；

 + `pop()` 在数组末尾移除一项；

 + `shift()` 在数组的头部移除一项；

 + `unshift(value)` 在数组的头部插入元素；

 + `splice(index,cont,value,value,...)` 从数组的第index个元素开始移除cont个元素，并把后面的元素插入数组的index处（会改变原数组）；

 + `slice(start,end)` 从数组中截取start到end的元素并返回截取的部分（不会改变原数组）；

 + `sort(function(value1,value2){...}` 排序数组元素；

 + `reverse()` 颠倒数组元素位置；

 + `indexOf([inex],value)` index可选，如果指定index，index表示起始位置，返回value在数组中第一次出现的位置（使用的是`===`比较的）；

 + `lastIndexOf([index],value)` 从后往前查，其余与`indexOf()`一样；

 + 遍历方法

    + `for`:

      ~~~
      var arr = [1,2,3,4,5];
      for (var i = 0,j = arr.length; i<j;i++){
      	alert(arr[i]);
      }
      ~~~

      

    + `forEach`: 循环数组中的每一项，并用指定方法处理；

      ```
      var arr = [1,2,3,4,5];
      arr.forEach(function(value,index,array){
      	console.log(value);
      })
      ```

      

    + `every` :遍历数组中的每一项执行指定方法，都返回`true`则整体返回`true` ,有一项为`false` 则返回`false`；

      ``` 
      var arr = [1,2,3,4,5];
      var state = arr.every(function(value,index,array){
      	return value>0;
      })
      ```

      

    + `filter`: 遍历数组的每一项，筛选出符合需求的元素，并以新数组返回

      ```
      var arr = [1,2,3,4,5];
      var newArr = arr.filter(function(value,index,array){
      	return value>2;
      })
      ```

      

    + `map` ：遍历数组中的每一项，指定方法处理，并返回处理后的结果数组；

      ```
      var arr = [1,2,3,4,5];
      var newArr = arr.map(function(value,index,array){
      	return value*2;
      })
      ```

      

    + `some`：用法与`every`一样,作用相反，只要有一个为`false` 则返回`false`;

#### Object 对象

 1. 枚举对象属性；

    ```
    var obj = {};
    obj.name = "bulang";
    obj.age = "18";
    obj.sex = "boy";
    for(attr in obj){
    	console.log(attr+":"+obj[attr]);
    };
    ```

    

 2. `Constructor`:

    ```
    console.log(obj.constructor);
    ```

    

 3. `hasOwnProperty(str)`:判断某个值是不是对象的属性；

    ```
    obj.hasOwnProperty("name");
    ```

    

 4. `isPrototypeOf(Object)`:判断传入的对象是不是另一个对象的原型；

 5. `instanceof` 判断某个对象是不是另一个对象的实例；

 6. `propertyIsEnumerable(propertyName)`:判断某个对象是否可以被`for in`枚举；

 7. `toString()`、`valueOf()`、`toLocalString()`;

#### 单体对象

 1. `Global`对象

    * `encodeURI()`编码部分不标准的文字或者字符；

    * `encodeURIComponent()`编码所有浏览器不认识的字符（常用）；

    * `decodeURI()`对应`encodeURI()`解码;

    * `decodeURIComponent()`对应`encodeURIComponent()`解码；

    * `eval()`小型的javascript解析器；

      ```
      var strArr = "[1,2,3,4,5]";
      var arr = eval(strArr);
      console.log(arr);
      var strObj = "{'name':'bulang','age':'18'}";
      var obj = eval('('+strObj+')');
      console.log(obj);
      ```

      

    * `escape`、`unescape`函数可对字符串进行编解码，这样就可以在所有的计算机上读取该字符串。

    * `isNaN`判断一个变量是不是不是`number`类型；

      注：`NaN`不等于`NaN`；

    * `parseInt()`、`parseFloat()`;

      

 2. `Math`对象

 3. `Date()`对象

 4. 基本包装类型

    `Boolen`、`String`、`Number`等；

 5. `Function`类型

 6. `RegExp`类型

#### 函数

 1. 声明方式：

    * `function`语句式（优先解释、静态、有函数作用域）

      ```
      function fn1(){}
      ```

      

    * 函数直面量（顺序执行、静态、有函数作用域）

      ```
      var fn1 = function(){}
      ```

      

    * 函数构造器(顺序执行、动态、顶级作用域)

      ```
      var fn1 = new Function()
      ```

      

 2. 参数：

    + 形参

      ```
      function fn1(a,b,c,d,e){
      	arguments.callee.length;   //形参个数
      	
      }
      ```

      

    + 实参

      ```
      function fn1(a,b,c,d,e){
      	alert(arguments.length);    //实参个数
      	alert(arguments[0]);        //获取实参值
      	arguments.callee			//指向函数自己
      }
      ```

      

 3. `this`在运行时期基于执行环境所绑定的、指向调用者；

    

 4. `call`、`applay` 用来绑定一些函数用于传递参数、扩充函数依赖的作用域（对象与方法可以实现很好的解耦）；

    ```
    /*传递参数*/
    function sum(x,y){
    	return x+y;
    }
    
    function fn1(a,b){
    	return sum.call(this,a,b);
    }
    
    function fn2(a,b){
    	return sum.apply(this,[a,b]);
    }
    
    alert(fn1(1,2));
    alert(fn2(1,2));
    ```

    ```
    /*扩充作用域*/
    var Obj1 = {
    	name:"bulang"
    }
    var Obj2 = {
    	name:"sha"
    }
    function say(){
    	alert(this.name);
    }
    say.call(Obj1);
    say.call(Obj2);
    ```

#### 垃圾收集机制

	1. 标记方法
 	2. 引用计数法

#### 闭包

```
function fn1(x){
	var y = x;
	return function(n){
		y+=n;
		alert(y);
	}
}
```



### 原型以及原型继承

	#### 构建一个对象

 1. 工厂模型

    ```
    function createCar(name,color){
    	var carObj = new Object();
    	carObj.name = name;
    	carObj.color = color;
    	return carObj;
    }
    
    var car  = createCar("audi","black");
    ```

    

 2. 构造函数模式（标准常用的模式）

    ```
    function Person(name,sex,age){
    	this.name = name;
    	this.sex = sex;
    	this.age = age;
    	this.say = function(){
    		alert("my name is"+this.name);
    	}
    }
    
    var person = new Person("bulang","boy","18");
    alert(person.sex);
    person.say(); 
    ```

#### 原型

```
function Person(name,age,sex){
	this.name = name;
	this.sex = sex;
	this.age = age;
}
//原型上的方法所有实例共享
//Person.prototype是一个原型对象；
Person.prototype.sayName = function(){
	alert("my name is "+this.name);
}

//实例化Persion对象
var p1 = new Person("bulang","18","boy");
var p2 = new Person("sha","18","girl");
alert(Person.prototype.isPrototypeOf(p1));//true 实例的原型是Person.prototype
alert(Person.prototype.constructor === Person);//true person.prototype的构造函数是Person；
alert(Object.getPrototypeOf(p1) === Person.prototype);//true 根据实例获取实例的原型；
alert("name" in p1);//true in操作符，用来判断某个参数是否在这个对象中；

```

##### 简单原型

构造函数发生了改变，需要手动指定一次；

有动态特新。实例化对象之前一定要把原型定义完毕；

```
function Person(){
	
}
//这种声明方式把原型指向了一个新的对象导致原型的构造函数变成了Object(),所以手动赋值一个constructor
Person.prototype = {
	constructor:Person,
	name:"bulang",
	sex:"boy",
	age:"18"
}
//上面的方式会让constructor能被枚举，所有使用es5提供的这个方法
Object.defineProperty(Person.prototype,"constructor",{
	enumerable:false,//不可枚举
	value:Person
})
```

##### 动态原型模式

动态原型方法：判断有没有要判断的方法，没有的话在原型链上声明

```
function Person(name){
	this.name = name;
	if(typeof this.sayName != "function"){
		Person.prototype.sayName = function(){
		alert(this.name);
		}
	}
}
```

##### 稳妥构造函数式

特点：没有公共的属性，不能使用this对象；

```
function Person(name,age){
	var myAge = age;
	var obj = new Object();
	obj.sayName = function(){
		alert(name);
	}
	return obj;
}

var p1 = new Person("bulang");
p1.sayName() //bulang 只能通过接口访问对象属性
```

##### 继承

1. 原型继承

   把子类的`prototype`指向父类的一个实例（子类的原型上就有了父类的所有属性与方法）;

   缺点：实例化子类的时候有些参数需要实例化父类来指定，不符合书写习惯；

   ```
   function Person(name,age){
   	this.name = name;
   	this.age = age;
   }
   
   function Boy(sex){
   	this.sex = sex;
   }
   
   Boy.prototype = new Person("bulang","18");
   var b1 = new Boy("boy");
   alert(b1.name);
   ```

   

2. 类继承（只继承模板不继承原型对象）利用构造函数继承

   把父类的作用于绑定到子类上并传参；

   缺点：不能继承父类原型链上的属性与方法；

   ```
   function Person(name,age){
   	this.name = name;
   	this.age = age;
   }
   Person.prototype.sayName = function(){
   	alert(this.name);
   }
   function Boy(sex,name,age){
   	Person.call(this,name,age);
   	this.sex = sex;
   }
   
   var b1 = new Boy("boy","bulang","18");
   alert(b1.age);
   b1.sayName();//报错 不是一个方法
   ```

   

3. 混合继承（上面两种一起使用）

   缺点：会继承两次模板，效率受损

4. 写一个extends函数实现继承

   ````
   //继承函数
   function extends(sub,sup){
   	var F = new Function();//声明一个空函数
   	F.prototype = sup.prototype;//赋值空函数的原型等于父类的原型
   	sub.prototype = new F();//子类继承空函数，空函数的模板为空的所以间接只继承了父类的原型
   	sub.prototype.constructor = sub;//恢复子类的构造函数
   	sub.supperClass = sup.prototype;//把父类的原型保存在子类的一个静态属性中方便解耦与使用；
   	if(sup.prototype.constructor == Object.prototype.constructor){
   		sup.prototype.constructor = sup;
   	}
   }
   //父类
   function Person(name,age){
   	this.name = name;
   	this.age = age;
   }
   //父类原型
   Person.prototype={
   	sayName:function(){
   		alert(this.name);
   	}
   }
   //子类
   function Boy(sex,name,age){
   	//继承父类的模板
   	Boy.supperClass.constructor.call(this,name,age);
   	this.sex = sex;
   }
   //使用方法
   //实现继承
   extend(Boy,Person);
   //子类原型方法覆盖父类的方法
   Boy.prototype.sayHello = function(){
   	alert("hello Boy");
   }
   //实例化子类
   var b1 = new Boy("boy","bulang",18);
   
   alert(b1.age);
   b1.sayName();
   b1.sayHello();
   //调用父类的方法
   Boy.supperClass.sayHello.call(b1);
   
   ````

### 设计模式

#### 接口

 1. 注解描述方法

    在注释里面写类的接口描述，以文档的方式告诉开发者该类实现了那些接口，太过松散，不检测接口是否实现

 2. 属性检测方法

 3. 鸭式辨型方法
