---
title: JavaScript 对象基础
slug: Learn/JavaScript/Objects/Basics
---

{{LearnSidebar}}{{NextMenu("Learn/JavaScript/Objects/Object_prototypes", "Learn/JavaScript/Objects")}}

在这学习 JavaScript 的对象的首篇文章中，我们将会学习有关对象基础的语法，并且回顾一些之前学过的 JavaScript 的一些特点，使你明白你所使用过的一些功能实际上是由对象提供的。

<table class="learn-box standard-table">
  <tbody>
    <tr>
      <th scope="row">前提：</th>
      <td>
        基础计算机基础，了解基础的 HTML 和 CSS, 熟悉 JavaScript 基础
        (基础知识看这里
        <a href="/zh-CN/docs/Learn/JavaScript/First_steps">First steps</a>
        和这里
        <a href="/zh-CN/docs/Learn/JavaScript/Building_blocks"
          >Building blocks</a
        >).
      </td>
    </tr>
    <tr>
      <th scope="row">目标：</th>
      <td>
        理解面向对象编程背后的基础理论，怎样理解 JavaScript ("一切皆对象 most
        things are objects"), 如何开始使用 JavaScript 对象。
      </td>
    </tr>
  </tbody>
</table>

## 对象基础

对象是一个包含相关数据和方法的集合（通常由一些变量和函数组成，我们称之为对象里面的属性和方法），让我们通过一个例子来了解它们。

首先，将 [oojs.html](https://github.com/mdn/learning-area/blob/main/javascript/oojs/introduction/oojs.html) 文件复制到本地。此文件包含非常少 — 一个供我们写源代码的 {{HTMLElement("script")}} 标签，一个供我们输入示例指令的 {{HTMLElement("input")}} 标签，当页面被渲染时，一些变量定义，一个输出任何输入到{{HTMLElement("input")}}的内容输出到{{HTMLElement("p")}}标签的函数。我们用这个文件做为基础探索对象的基础语法。

如同 Javascript 中的很多东西一样，创建一个对象通常先定义初始化变量。尝试在您已有的文件中 JavaScript 代码下面输入以下内容，保存刷新页面：

```js
var person = {};
```

如果你在浏览器的 [JavaScript 控制台](/zh-CN/docs/Learn/Common_questions/What_are_browser_developer_tools#javascript_控制台)输入 `person`，然后按下 Enter（确认）键，你可能会得到以下结果中的一种：

```js
[object Object]
Object { }
{ }
```

恭喜，你刚创建了你的第一个对象。干的漂亮！但这是一个空对象，所以我们做不了更多的事情。像下面一样更新下我们的对象：

```js
var person = {
  name: ["Bob", "Smith"],
  age: 32,
  gender: "male",
  interests: ["music", "skiing"],
  bio: function () {
    alert(
      this.name[0] +
        " " +
        this.name[1] +
        " is " +
        this.age +
        " years old. He likes " +
        this.interests[0] +
        " and " +
        this.interests[1] +
        ".",
    );
  },
  greeting: function () {
    alert("Hi! I'm " + this.name[0] + ".");
  },
};
```

保存刷新后，尝试在你的浏览器控制台输入下面的内容：

```js
person.name[0];
person.age;
person.interests[1];
person.bio();
person.greeting();
```

现在在你的对象里得到了一些数据和功能（functionality），现在可以通过简单的语法访问他们了！

> **备注：** 如果做上面的东西遇到了麻烦，尝试拿你的代码与我们的版本做对比——对比 [oojs-finished.html](https://github.com/mdn/learning-area/blob/main/javascript/oojs/introduction/oojs-finished.html) (也可以 [看实际效果](http://mdn.github.io/learning-area/javascript/oojs/introduction/oojs-finished.html))。一个对于初学者很常见的错误是在最后一个成员后面多了一个逗号，这会引发错误。

所以发生了什么？一个对象由许多的成员组成，每一个成员都拥有一个名字（像上面的 name、age），和一个值（如 \['Bob', 'Smith']、32）。每一个名字/值（name/value）对被逗号分隔开，并且名字和值之间由冒号（:）分隔，语法规则如下所示：

```js
var objectName = {
  member1Name: member1Value,
  member2Name: member2Value,
  member3Name: member3Value,
};
```

对象成员的值可以是任意的，在我们的 person 对象里有字符串 (string)，数字 (number)，两个数组 (array)，两个函数 (function)。前 4 个成员是资料项目，被称为对象的属性 (property)，后两个成员是函数，允许对象对资料做一些操作，被称为对象的方法 (method)

一个如上所示的对象被称之为对象的字面量 (literal)——手动的写出对象的内容来创建一个对象。不同于从类实例化一个对象，我们会在后面学习这种方式。

当你想要传输一些有结构和关联的资料时常见的方式是使用字面量来创建一个对象，举例来说，发起一个请求到服务器以存储一些数据到数据库，发送一个对象要比分别发送这些数据更有效率，而且比起数组更为易用，因为你使用名字 (name) 来标识这些资料。

## 点表示法

在上面的例子中，你使用了点表示法 (dot notation) 来访问对象的属性和方法。对象的名字表现为一个命名空间 (namespace)，它必须写在第一位——当你想访问对象内部的属性或方法时，然后是一个点 (.)，紧接着是你想要访问的项目，标识可以是简单属性的名字 (name)，或者是数组属性的一个子元素，又或者是对象的方法调用。如下所示：

```js
person.age;
person.interests[1];
person.bio();
```

### 子命名空间

可以用一个对象来做另一个对象成员的值。例如将 name 成员

```js
name : ['Bob', 'Smith'],
```

改成

```js
name : {
  first : 'Bob',
  last : 'Smith'
},
```

这样，我们实际上创建了一个子命名空间，听起来有点复杂，但用起来很简单，你只需要链式的再使用一次点表示法，像这样：

```js
person.name.first;
person.name.last;
```

**注意**：你需要改变你之前的代码，从

```js
name[0];
name[1];
```

改成

```js
name.first;
name.last;
```

否则，你的方法不再有效。

## 括号表示法

另外一种访问属性的方式是使用括号表示法 (bracket notation)，替代这样的代码

```js
person.age;
person.name.first;
```

使用如下所示的代码：

```js
person["age"];
person["name"]["first"];
```

这看起来很像访问一个数组的元素，从根本上来说是一回事儿，你使用了关联了值的名字，而不是索引去选择元素。难怪对象有时被称之为关联数组 (associative array) 了——对象做了字符串到值的映射，而数组做的是数字到值的映射。

## 设置对象成员

目前我们仅仅看到了如何访问对象的成员，而你其实也可以设置对象成员的值，通过声明你要设置的成员，像这样：

```js
person.age = 45;
person["name"]["last"] = "Cratchit";
```

尝试这些代码，然后再查看这些成员是否已经被改变了

```js
person.age;
person["name"]["last"];
```

设置成员并不意味着你只能更新已经存在的属性的值，你完全可以创建新的成员，尝试以下代码：

```js
person["eyes"] = "hazel";
person.farewell = function () {
  alert("Bye everybody!");
};
```

现在你可以测试你新创建的成员

```js
person["eyes"];
person.farewell();
```

括号表示法一个有用的地方是它不仅可以动态的去设置对象成员的值，还可以动态的去设置成员的名字。

比如说，我们想让用户能够在他们的数据里存储自己定义的值类型，通过两个 input 框来输入成员的名字和值，通过以下代码获取用户输入的值：

```js
var myDataName = nameInput.value;
var myDataValue = nameValue.value;
```

我们可以这样把这个新的成员的名字和值加到 person 对象里：

```js
person[myDataName] = myDataValue;
```

为了测试这个功能，尝试在你的代码里添加以下几行，就在 person 对象的右花括号的下面：

```js
var myDataName = "height";
var myDataValue = "1.75m";
person[myDataName] = myDataValue;
```

现在，保存并刷新，在输入框里输入以下代码：

```js
person.height;
```

这是使用点表示法无法做到的，点表示法只能接受字面量的成员的名字，不接受变量作为名字。

## "this"的含义

你也许在我们的方法里注意到了一些奇怪的地方，看这个例子：

```js
greeting: function() {
  alert('Hi! I\'m ' + this.name.first + '.');
}
```

你也许想知道"this"是什么，关键字"this"指向了当前代码运行时的对象 ( 原文：the current object the code is being written inside )——这里即指 person 对象，为什么不直接写 person 呢？当你学到下一篇[Object-oriented JavaScript for beginners](/zh-CN/docs/Learn/JavaScript/Objects/Object-oriented_JS)文章时，我们开始使用构造器 (constructor) 时，"this"是非常有用的——它保证了当代码的上下文 (context) 改变时变量的值的正确性（比如：不同的 person 对象拥有不同的 name 这个属性，很明显 greeting 这个方法需要使用的是它们自己的 name）。

让我们以两个简单的 person 对象来说明：

```js
var person1 = {
  name: "Chris",
  greeting: function () {
    alert("Hi! I'm " + this.name + ".");
  },
};

var person2 = {
  name: "Brian",
  greeting: function () {
    alert("Hi! I'm " + this.name + ".");
  },
};
```

在这里，person1.greeting() 会输出："Hi! I'm Chris."；person2.greeting() 会输出："Hi! I'm Brain."，即使 greeting 这个方法的代码是一样的。就像我们之前说的，this 指向了代码所在的对象 (其实代码运行时所在的对象)。在字面量的对象里 this 看起来不是很有用，但是当你动态创建一个对象（例如使用构造器）时它是非常有用的，之后你会更清楚它的用途。

## 你一直在使用对象

当你使用过这些例子之后，你可能会发现你对点表示法并不陌生，这是因为我们在这个课程里一直在使用它，每次我们学习的示例使用浏览器内建的 API 和 JavaScript 的一些对象时，我们就在使用对象，因为，这些功能是由跟我们所看到的对象同样的结构来构建的，虽然比我们自己定义的要复杂许多。

所以当我们这样使用字符串的方法时：

```js
myString.split(",");
```

你正在使用一个字符串实例上可用的方法，你随时都可以在代码里使用字面量创建一个字符串，字符串会自动的被创建为字符串 ([`String`](/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)) 的实例，因此会有一些常见的方法和属性可用。

当你这样访问 document 对象时：

```js
var myDiv = document.createElement("div");
var myVideo = document.querySelector("video");
```

你正在使用[`Document`](/zh-CN/docs/Web/API/Document)实例上可用的方法。每个页面在加载完毕后，会有一个 Document 的实例被创建，叫做 document，它代表了整个页面的结构，内容和一些功能，比如页面的 URL。同样的，这意味 document 有一些可用的方法和属性。

这同样适用许多其他内建的对象或 API，你使用过有—— [`Array`](/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)，[`Math`](/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)，等。

请注意内建的对象或 API 不会总是自动地创建对象的实例，举例来说，这个 [Notifications API](/zh-CN/docs/Web/API/Notifications_API)——允许浏览器发起系统通知，需要你为每一个你想发起的通知都使用构造器进行实例化。尝试在 JavaScript 终端里输入以下代码

```js
var myNotification = new Notification("Hello!");
```

我们会在之后的文章里学习到构造器。

> **备注：** 这样来理解对象之间通过消息传递来通信是很有用的——当一个对象想要另一个执行某种动作时，它通常会通过那个对象的方法给其发送一些信息，并且等待回应，即我们所知的返回值。

## 总结

恭喜，你已经阅读到了我们有关 JavaScript 对象的第一篇文章的末尾，你现在应该对如何在 JavaScript 中使用对象有了很好的认识，包括你自己创建一个简单的对象。你应该清楚对象有利于存储一些相关联的数据和函数，如果你尝试以分开的方式去保存 person 对象包含的所有的属性和方法，这是令人沮丧且效率低下的，而且会有很多的变量和函数之间同名的风险。对象使我们将一些信息安全地锁在了它们自己的包内，防止它们被损坏。

在下一篇文章，我们将会了解面对对象编程 (OOP) 理论，和许多在 JavaScript 中使用的技巧。

{{NextMenu("Learn/JavaScript/Objects/Object_prototypes", "Learn/JavaScript/Objects")}}
