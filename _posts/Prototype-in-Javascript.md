title: Prototype in Javascript
date: 2014-08-14 23:03:20
tags:
 - Javascript
---

最近又有机会重新学习了一下Javascript的基础语法，越发觉得这门语言和传统的、面向对象的静态类型语言的区别很明显。多语言使用者经常出现的问题就是使用A语言写出B语言风格的程序，这种情况屡见不鲜——话说我写Java风格的C++程序也是非常流畅的。

Javascript语言基础里有两个特性我觉得值得深入了解一下，分别是原型（Prototype）和闭包（Closure）。当然，Javascript也有很多其他高级特性比如函数式编程，也许以后有机会我们可以深入探究一下。今天主要看一下Javascript里原型式继承是怎么做的。

<!-- more -->

首先，我们使用几份材料来学习Javascript原型的概念以及原型式继承的方式（排序难易程度不分先后）：

 - http://www.slideshare.net/PaweDorofiejczyk/lets-javascript （学习Javascript语言基础的首选）
 - http://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html （原型式继承的深入讲解）
 - http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html （阮一峰老师当然不能放过）
 - http://www.w3schools.com/js/js_object_prototypes.asp （学习基本概念）
 - http://coolshell.cn/articles/6441.html （耗子叔叔大作，推荐阅读）

如果上述幻灯片或文章你都能一扫而过、微微一笑而且嘴角上扬的话，就不用往下看了。如果你居然还微微皱了一下眉头，那么我们可以用第一个幻灯片的例子来说明一下类继承和原型式继承的差别：

```javascript
/*
 * 类继承: 不推荐，丑陋
 */

function Animal(name){
        this.name = name; // this指向构造函数返回的实例对象
}

Animal.prototype.getName = function(){
        return this.name;
}

var dophin = new Animal("Dophin");

console.log("A new Animal is created: " + dophin.getName());

function WalkingAnimal(name){
        // 调用“父”对象构造函数
        Animal.call(this, name)
}

WalkingAnimal.prototype = new Animal();
WalkingAnimal.prototype.walk = function(){
        console.log(this.getName() + " is walking");
}

var cow = new WalkingAnimal('Cow');
cow.getName(); // 来自Animal.prototype.getName()
cow.walk(); // WalkingAnimal自己的prototype函数
```

在改用原型式继承之后，就不用new Animal对象了，而是用下面的语句表达，这样是不是显得“原型”一些？

```javascript
WalkingAnimal.prototype = Object.create(Animal.prototype);
WalkingAnimal.prototype.walk = function(){
        console.log(this.getName() + " is walking");
}
```

而在最近的Javascript语言风格中，可以看见类似如下的写法（使用NodeJS语法），

```javacript
// 定义子对象
function WalkingAnimal(name){
        // 调用“父”对象构造函数
        // 使用super_而不是$parent
        WalkingAnimal.super_.call(this,name);
}

util.inherits(WalkingAnimal, Animal);

WalkingAnimal.prototype.walk = function(){
        console.log(this.getName() + " is walking");
}
```

这样就更符合原型式继承的写法了，不过这里有两个问题需要进一步研究一下：

 - Javascript语言规范的通常写法是什么
 - 原型式继承其实是使用原型做一个代理，最终将“对象定义”传播到子对象，这样做除了风格区别还有什么优势？

总结：文中我没有具体解释原型的概念，反而使用一些经典的参考资料比较阅读并结合实例说明原型式继承的写法，希望通过这样的学习更能加深印象。
