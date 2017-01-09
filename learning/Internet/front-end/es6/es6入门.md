# es6 语法
> 这些是ES6最常用的几个语法，基本上学会它们，我们就可以走遍天下都不怕啦！
### 声明变量
> let, const, class, extends, super, arrow functions, template string, destructuring, default, rest arguments
#### let, const，const
>   ES5只有全局作用域和函数作用域，没有块级作用域，这带来很多不合理的场景。
>   let：用它所声明的变量，只在let命令所在的代码块内有效。
>   var：var声明的，在全局范围内都有效。
>   const：const也用来声明变量，但是声明的是常量,一般用于第三方库的声明。
#### class, extends, super
>   原型、构造函数，继承…你还在为它们复杂难懂的语法而烦恼吗？你还在为指针到底指向哪里而纠结万分吗？
#### arrow function
> 这个恐怕是ES6最最常用的一个新特性了，用它来写function比原来的写法要简洁清晰很多:
 <div><code>
function(i){ return i + 1; } //ES5(i) => i + 1 //ES6
   如果方程比较复杂，则需要用{}把代码包起来：
    function(x, y) { 
	    x++;
	    y--;    return x + y;
	}
	</code>
</div>
>   ES6语法
<code>	(x, y) => {x++; y--; return x+y}</code><br>
>   除了看上去更简洁以外，arrow function还有一项超级无敌的功能！
>   长期以来，JavaScript语言的this对象一直是一个令人头痛的问题，在对象方法中使用this，必须非常小心。例如：
    class Animal {
	constructor(){ 
	       this.type = 'animal'
	    }
	    says(say){
	        setTimeout(function(){ 
	           console.log(this.type + ' says ' + say)
	        }, 1000)
	    }
	} var animal = new Animal()
	 animal.says('hi')  //undefined says hi
*   运行上面的代码会报错，这是因为setTimeout中的this指向的是全局对象。所以为了让它能够正确的运行，传统的解决方法有两种：
   第一种是将this传给self,再用self来指代this
    says(say){ 
      var self = this;
       setTimeout(function(){ 
          console.log(self.type + ' says ' + say)
       }, 1000)
   2.第二种方法是用bind(this),即
    says(say){
       setTimeout(function(){           console.log(this.type + ' says ' + say)
       }.bind(this), 1000)
   但现在我们有了箭头函数，就不需要这么麻烦了：
    class Animal {
	constructor(){        this.type = 'animal'
	    }
	    says(say){
	        setTimeout( () => {            console.log(this.type + ' says ' + say)
	        }, 1000)
	    }
	} 
	var animal = new Animal()
	animal.says('hi')  //animal says hi
   当我们使用箭头函数时，函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
   并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，它的this是继承外面的，因此内部的this就是外层代码块的this。

#### template string
   这个东西也是非常有用，当我们要**大段的html内容到文档中时，传统的写法非常麻烦，所以之前我们通常会引用一些模板工具库，比如mustache等等。
   大家可以先看下面一段代码：
    $("#result").append(  "There are <b>" + basket.count + "</b> " +  "items in your basket, " +  "<em>" + basket.onSale +  "</em> are on sale!");
   我们要用一堆的’+’号来连接文本与变量，而使用ES6的新特性模板字符串``后，我们可以直接这么来写：
    $("#result").append(''
	  There are <b>${basket.count}</b> items
	   in your basket, <em>${basket.onSale}</em>
	  are on sale!
	');
#### destructuring
   ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
    let cat = 'ken'let dog = 'lili'let zoo = {cat: cat, dog: dog}console.log(zoo)  //Object {cat: "ken", dog: "lili"}
   用ES6完全可以像下面这么写：
    let cat = 'ken',
    let dog = 'lili',
    let zoo = {cat, dog}console.log(zoo);
    //Object {cat: "ken", dog: "lili"}
   反过来可以这么写：
    let dog = {type: 'animal', many: 2};let { type, many} = dog;console.log(type, many)   //animal 2
#### default, rest
   default很简单，意思就是默认值。大家可以看下面的例子，调用animal()方法时忘了传参数，传统的做法就是加上这一句type = type || ‘cat’ 来指定默认值。c
    function animal(type){    type = type || 'cat'  
	    console.log(type)
	}
	animal();
  如果用ES6我们而已直接这么写：
    function animal(type = 'cat'){
	    console.log(type)
	}
	animal();
  最后一个rest语法也很简单，直接看例子：
    function animals(...types){    console.log(types)
	}
	animals('cat', 'dog', 'fish') //["cat", "dog", "fish"]
