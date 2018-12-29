# CLI - Command line interface:

A utility in your computer that you use to type commands rather than using your mouse. That's what it all means. Examples are Terminal on Mac, Command Prompt on Windows etc.

This is the way things used to be in old school days.

Working with NodeJS will require CLI's usage mostly.

## Arguments

Arguments to commands are just like parameters passed to the function. They effect the behaviour of the command.

# V8 JavaScript Engine

V8 engine is at the core/heart of NodeJS. NodeJS is adding on top of it to extend it capabilities.

## Machine code

Microprocessor is a tiny machine sitting on to our computers, that accepts instructions and performs task. There are different languages that Microprocessor speaks, I-32, x86-64, ARM, MIPS etc. These languages that are spoken by computer processors are called **Machine code/language**. All programming languages eventually ends up (compiled) in machine code.

JavaScript sits very high (far away) in the machine language's abstraction layer. C/C++ are much closer. There are engines like V8 that converts our JS code into machine code.

### Node is written in C++

Yes, Node is written in C++ because V8, the engine that converts JS to machine code is written in C++.

## ECMAScript

It is the standard that JS is based on. JS was invented first, but later different companies created their own version. So ECMA came up with a core standard known as ECMASCRIPT. This standard is needed because there are many standards out there.

V8 makes sure that the machine code that it writes is based on the Ecmascript standard.

So a JS engine is a program that converts JS code into something the computer processor can understand, and it should follow the ECMAScript standard.

## V8 - Under the hood

V8 is Google's open source JavaScript Engine, written in C++, that converts JavaScript into machine code.

Google Chrome uses V8.

## Adding features to JS

V8 can be embedded in any C++ application. This is the stronger feature of V8 which allows to extend JavaScript to have features that are not possible in JS, features like file access, database access, manipulating DOM etc. Our own C++ program can embed V8 and add these kinds of extra features to enhance JS. This is exactly what NodeJS does.

# Servers and Clients

**Request** - Clients requests for services in a standard format.
**Response** - Servers perform services requested by the client and sends the response in a standard format.

## Webserver and Browsers

In internet terminology servers are mainly called **Webserver** and the clients are mainly **Browsers**.

The standard format that webserver and the browser uses to communicate is **HTTP**

JS is the language that the browser uses to communicate (send a request). While on server there are options like PHP, C#, Ruby etc.

# The Node Core

So NodeJS was designed to run JS on the webserver as well, in order to uniform the language on both client and server. This means that you only need to worry about only one programming language for writing client and server side code. Libraries can also be shared between client and server code.

## What does JS needs to manage a server?

These are the things that are required to be done by JS to manage a webserver. This is where NodeJS helps;

* Better ways to organise our code into reusable pieces
* Ways to deal with files
* Ways to deal with databases
* The ability to communicate over the internet
* The ability to accept requests and send responses (in the standard format)
* A way to deal with work that takes a long time

## C++ & JavaScript Core

NodeJS comes with C++ and JavaScript code. JS code is mainly being used as a wrapper that wraps the C++ feature for you.

### io.js

NodeJS was being managed by Joyent, the company where it was created. Its update cycle was not coping up with the release of the new V8 version. That's how io.js came into being which took up the node code and kept it updated with the newest and the latest feature. Later NodeJS team decided to integrate io.js within NodeJS itself to avoid confusion. So now the current node version is latest and up to date.

### Commands & Tools

To check if node is installed try `node -v`

To run a JS file in terminal using node `node app.js`

Visual Studio Code is a great tool for writing NodeJS programs. You can set breakpoints within the editor, in the same way we do in browsers.

# Modules, Exports and Require

## Modules

A reusable block of code whose existance doesn't accidentally impact other code.

Major programming languages have this feature, but JS didn't before ES6. At the time of NodeJS creation JS didn't have it. So NodeJS had to give us the ability to write modules.

### CommonJS

An agreed upon standard for how code modules should be structured.

So NodeJS says that we are going to design a way for you to structure your code in modules that will follow this standard.

### First-Class Functions

Everything you can do with other types, you can do with functions. You can use functions like strings, numbers, etc. (pass them around, set variables equal to them, put them in arrays, and more)

```
function logGreeting(fn) {
	fn(); //invoke the function
}
```

### Function Expressions

A block of code that results in a value

```
var greetMe = function() {
	console.log('Hi!');
}
greetMe();
```

It's still first class, as I created the above function on the fly and passed it around

```
logGreeting(greetMe);
```

Use a function expression on the fly

```
logGreeting(function() {
	console.log('Hello!');
})
```

### Building a Module using `require`

```
// greet.js

function greet() {
	console.log('Hello!');
}
greet();
```

`require()` command is include the needed file

```
// app.js

require('./greet.js');
```

Now `node app.js` will print `Hello!` in console.

The `require` function will execute the file that is being passed as an argument.

You can't call `greet()` in `app.js` directly, because modules are encapsulated.

In order to achieve this NodeJS provides a feature to export it using

```
// greet.js

module.exports = greet;
```
```
// app.js

var greet = require('./greet');
greet();
```

### Objects in JS

In JS Object is nothing but a collection of name value pairs. The values can be a primitive value (string, number etc), a function or another object.

Object properties can be accessed using a `.` notation or using brackets `[]`.

```
person.firstname
// or
person['firstname']
```

### Prototypal Inheritance

One object gets access to the properties and methods of another object.

Every object has a builtin property called `__proto__` that actually points to another object. It is the object's **prototype**. Any property associated to the prototype is available to that object. That `__proto__` property can have it's own prototype. This way they form a **Prototypal Chain**.

#### Function Constructors

A normal function that is used to construct object.

The `this` variable points a new empty object, and that object is returned from the function automatically. We can do this by using `new` keyword.

```
function Person(firstname, lastname) {

	this.firstname = firstname;
	this.lastname = lastname;

}

var john = new Person('John', 'Doe');
```

In the above code, because we used the `new` keyword the function constructor creates an empty object that points to it's `this` variable and associaties the passed properties to it, and *automatically returns* it to my `john` variable.

Whenever you create an object using the function constructor, its prototype (i.e the `__proto__` property) will point to the `prototype` of the function that use to construct that object.

```
Person.prototype.greet = function () {
	console.log('Hello' + this.firstname + ' ' + this.lastname);
}
```

All the objects created from the `Person` function with the `new` keyword will have access to this `greet` method, because the JS engine will search down the prototype chain to find `greet`, and it will find it in its prototype.


### By Reference or by Value

#### By value
Primitives values are passed by value. Primitive values are type that are not an object - a number, string etc.

```
var a = 1;
var b = a;
```

Separate memory spots are created for the two variables.

#### By reference
Objects are passed by reference. If one object is being assigned to another or passed to a function, then changes to one will affect other because both points to the same spot/address in memory.


### Immediately Invoked Function Expressions (IIFE)

A way to immediately invoke a function to avoid scope pollution. The code inside the function is protected from its outside context.

#### Scope
Where in code you have access to a particular variable or function

```
// 	IIFE

(function () {

})();
```

## How do Node modules really work

NodeJS wraps our code into IIFE before passing it to V8 for execution.

The `require` function loads the JS file, wrapped it, ran the code, and returns whatever is sitting on `module.exports`.

Here is our code
```
var greet = function() {
	console.log('Hello!');
};

module.exports = greet;
```

NodeJS wraps this into a function expression
```
(function (exports, require, module, __filename, __dirname) {

	// my code
	var greet = function() {
		console.log('Hello!');
	};

	module.exports = greet;
});
```
and then calls it using the `apply()` method returns `module.exports`.

### Summary

`require` is a function, that you pass a path too

`module.exports` is what the require function returns

this works because **your code is actually wrapped in a function** that is given these things as function parameters.

## JSON - JavaScript Object Notation

A standard for structuring data that is inspired by JavaScript object literals. JS engines are built to understand it.

JSON files can be imported using `require`. JS will treat it as an object.

## More on `require`

Require can be used to wrap complex modules. It looks by default for a `.js` file when no extension is passed to it, but if a folder is passed then it looks for `index.js` in it. So `index.js` can be a central point of access to all the nested modules by exporting an object that contains those modules. See the example below:

```
// greet/english.js

module.exports = function() {
	console.log('Hello!');
}
```

```
// greet/spanish.js

module.exports = function() {
	console.log('Hola!');
}
```

In `index.js` export an object that contains english and spanish modules

```
// greet/index.js

var english = require('./english');
var english = require('./english');

module.exports = {
	english: english,
	spanish: spanish
}
```

Now in `app.js` `require('greet')` will look for `index.js` in the `greet` folder as there is no `greet.js`.

```
// app.js

var greet = require('./greet');

console.log(greet.english);
console.log(greet.spanish);
```

## Module Patterns

Ways to structure our modules in NodeJS

### Pattern 1
Replacing the empty object (`module.exports`) with a function.

```
// greet1.js

module.exports = function() {

}
```
and then you can call the function in `app.js`

```
// app.js

var greet = require('./greet1');

greet(); // invoking the function
```

### Pattern 2
Since `module.exports` is an empty object, we can directly add properties to it.

```
// greet2.js

module.exports.greet = function() {
	console.log('Hello!');
}
```
Since require returns `module.exports`, we can access it like;

```
// app.js

var greet2 = require('./greet2').greet;
greet2();
```

### Pattern 3
Using a function constructor

```
// greet3.js

var Greetr = function() {
	this.greeting = 'Hello!';
	this.greet = function() {
		console.log(this.greeting);
	}
}

module.exports = new Greetr();
```

```
// app.js

var greet = require('./greet3');
greet3.greet();
```

NodeJS cache the modules. So when you require a module twice, then it is being returned from the cache.

```
// app.js

var greet3 = require('./greet3');
greet3.greetings = 'New Greeting!';

var greet3b = require('./greet3');
greet3b.greet(); // outputs 'New Greeting!' because greet3 module is being returned from the cache
```

This feature allows us to reuse a module throughout our application without recreating them in the memory (objects are passed by reference).

### Pattern 4

What if you don't want to pass the modules as references, then instead of storing the new object created by function constructor `Greetr`, pass the function constructor itself. In this way you give it the ability to create new objects

```
// greet4.js

var Greetr = function() {
	this.greeting = 'Hello!';
	this.greet = function() {
		console.log(this.greeting);
	}
}

// pass the function constructor instead
module.exports = Greetr;
```

```
// app.js

var Greet4 = require('./greet4');
var grtr = new Greet4();

console.log(grtr.greet);
```

### Pattern 5 - The most popular!
You encapsulate your logic within the module and return only what should be exposed. This is called the **Revealing Module Pattern**. Exposing only the properties and methods you want via the returned object. A very common and clean way to structure and protect code with methods.

```
// greet5.js

var greeting = 'Hello World!';

function greet() {
	console.log(greeting);
}

module.exports = {
	greet: greet
};
```

You won't have access to `greeting` variable in `app.js`.

```
var greet5 = require('./greet5').greet;
greet5();
```

## `exports` vs `module.exports`

`exports` is a shorthand for `module.exports` but it doesn't work with all the above patterns. Therefore `module.exports` is a recommended way.

When we require a module, NodeJS wraps our module/code into a function that has `exports` as its first parameter, and then it calls that function. While calling that function the argument to `exports` property is `module.exports`, which means that both of them points to the same memory location.

```
// greet.js

exports = function() {
	console.log('Hello!');
}
```

The above will not work because `module.exports` and `exports` originally pointed to the same value but when you assign a new value to `exports` the reference is broken. What is returned from `require` is `module.exports`, since the reference is broken you won't get your desired module using `require`.

### Solution
Rather than replacing `exports` with a new value, you can mutate (change) the object by adding properties to it, because they point to the same object.

```
// greet.js
exports.greet = function() {
	console.log('Hello!');
}
```

Still the recommendation is to use **`module.exports`**.

## Requiring Native (Core) Modules

NodeJS comes with a set of modules to make our life easier. It can be found Node's API docs.

In order to require these modules use them without `./`;

```
var util = require('util'); // without ./ because it is a native module
```

## Modules and ES6
NodeJS introduced concepts of modules in JS before ES6. But now since ES6 is being adopted gracefully you can export your modules in ES6 syntax because V8 supports ES6.

```
// greet.js

// anything with the export keyword is being exported as a module in ES6
export function greet() {
	console.log('Hello!');
}
```

```
// app.js

import * as greetr from 'greet';
greetr.greet();
```

# Events and Event Emitter

## Events
Something that has happened in our app that we can respond to

In node we talk about two different kinds of events

### System Events
That comes from C++ core that is part of NodeJS (libuv). These are the events that comes from the computer system (e.g I have finished reading a file etc, I have received data from internet etc.). Those C++ events allows us to respond to those events.

So **libuv** is sending events happening closer to the machine.

### Custom Events
They are inside JS core of NodeJS (Event Emitter). These events are inside the file in JS Core.

So the **Event Emitter** is where we have custom events.

An event occurs in **libuv** it generates a custom JS event to help us manage our code and decide what code should run when that event happens.

In other words, the JS side is faking event. There is no eventing concept in JS. But we can create our own event handling library using the technique the Node Event Emitter uses.

## Understanding the Event Emitter

Let's create our own simple event emitter to understand it.

```
// emitter.js

var Emitter = function() {
	this.events = {};
}

Emitter.prototype.on = function(type, listener) {
	this.events[type] = this.events[type] || [];
	this.events[type].push(listener);
}

Emitter.prototype.emit = function(type) {
	if (this.events[type]) {
		this.events[type].forEach(function(listener) {
			listener();
		});
	}
}

module.exports = Emitter;
```

Event listener is just a code that responds to an event. In JS it will be a function.

Now in `app.js`

```
// app.js

var Emitter = require('./emitter.js');

var emtr = new Emitter();

// creating a listener
emtr.on('greet', function() {
	console.log('Somewhere, someone said hello!');
});

// you can add another listener to the same event
emtr.on('greet', function() {
	console.log('A greeting occurred!');
});

emtr.emit('greet');
```

```
// output
// Somewhere, someone said hello!
// A greeting occurred!
```

This is a barebone concept behind the Node's Event Emitter, which then adds more advanced features on top of it. You can use it using require `require('events')` - check the API for more details on what the Node's Event Emitter provides.

### Magic Strings
A string that has some special meaning in our code. This is bad because it makes it easy for a typo to cause a bug, and hard for tools to help us to find it.

To use the event names as string all the time which can cause potential typos, a better approach is to save this in a config module.

```
// config.js

module.exports = {
	events: {
		GREET: 'greet',
	}
}
```

```
// app.js
var eventConfig = require('./config').events;

emtr.on(eventConfig.GREET, function() {

});
```


## Object.create and Prototype - Inheritance

As mentioned above, every object has a prototype which can be accessed through its `__proto__` property and that has its own prototype and so forth, forming a prototypal chain.

There are different ways to handle that, one of them is function constructors. The other method is `Object.create`.

```
var person = {
	firstname: '',
	lastname: '',
	greet: function() {
		console.log('Hello ' + firstname + ' ' + lastname);
	}
}

var john = Object.create(person);
```

In both ways `john` empty object will be created where its prototype will point to this object.

### Inheriting from EventEmitter - Part 1

#### `util.inherits(obj1, obj2)`

`utils` is a NodeJS core features that has an inherit function. `inherits()` function enables the objects that are created from `obj1` to have access to prototype properties and methods of `obj2`.

So `obj2.__proto__.__proto__` will have the prototype of `obj1`

This is the way you can extend the features of NodeJS's EventEmitter and add your listeners to it. Here is an example;

```
var EventEmitter = require('events');
var util = require('util');

function Greetr() {
	this.greeting = 'Hello World!';
}

// give access to all EventEmitter features to objects created from Greetr
util.inherits(Greetr, EventEmitter);

Greetr.prototype.greet = function() {
	console.log(this.greeting);
}

// Create a new object from Greetr that has access to EventEmitter prototype
var greetr1 = new Greetr();

// .on() sits on the prototype property of the EventEmitter
greetr1.on('greet', function() {
	console.log('Someone greeted!');
});

greetr1.emit('greet');
```

In the above scenerio `utils.inhertis` sets the `Greetr.prototype` to `EventEmitter.prototype`, which means any object created from `Greetr` now have access to all the `EventEmitter` method and we can add more to it, as we added the `greet` method.


### Node, ES6 and Template Strings

V8 supports ES6, so does NodeJS. To use ES6 in the browser use a tool like `babeljs.io`. It converts ES6 code into ES5 so that it can run on non-supported browsers.

#### Template literals

A handy way to concatenate strings in ES6. This is done by wrapping our string within backticks.

```
var name = 'John Doe';

var greet = `Hello ${ name }`;
```

### `.call()` and `.apply()`

Functions can be invoked using these two methods. These ways are useful when we want to bind the `this` keyword inside the function.

```
var obj = {
	name: 'John Doe',
	greet: function() {
		console.log(`Hello ${ this.name }`);
	}
}

obj.greet();

// call allows me to pass what the this will be within the function
obj.greet.call({ name: 'Jane Doe' });

// apply is same as call but you can pass an array of parameters
obj.greet.apply({ name: 'Jane Doe' }, [param2, param2]);
```

### Inheriting from EventEmitter - Part 2

In the above EventEmitter code we have one missing feature. What if the EventEmitter adds properties to itself. We don't have access to that as we are only inheriting its prototype. So to cover that there is a neat trick inside our `Greetr` function constructor: We tell EventEmitter to use our newly constructed object as it's `this` keyword. So whatever the EventEmitter adds, it will be added to our object instead.

```
function Greetr() {
	EventEmitter.call(this);
	this.greeting = 'Hello!';
}
```

### Creating objects in ES6 - Using Classes

Classes is a new way to creating objects. They are an alternative to function constructors. They are just a **Syntactic Sugar**. Syntactic Sugar is a feature that only changes how you type something, but nothing changes under the hood. Classes in JS are not like in other languages (Java, C#, C++ etc). It is important to understand what is happening under the hood so we don't make decisions based on flawed assumptions.

So the above function constructor (our `Person` object) can be written in a simplied manner using ES6.

```
'use strict'; // it is better to use stricter mode, specially when dealing with ES6

class Person {

	// anything added inside constructor, works like a function constructor,
	// and the properties are being added to the object created

	constructor(firstname, lastname) {
		this.firstname = firstname;
		this.lastname = lastname;
	}

	// while other methods added after the constructor are being added to the prototype,
	// so all the objects that are created from this class have access to it

	greet() {
		console.log(`Hello ${ firstname } ${ lastname }!`);
	}

}

var john = new Person('John', 'Doe');
var jane = new Person('Jane', 'Doe');

john.greet(); // Hello John Doe!
jane.greet(); // Hello Jane Doe!
```

### Inheriting from EventEmitter - Part3

Convert our previously coded EventEmitter code to use ES6 Classes

```
'use strict';

var EventEmitter = require('events'); // from node core

module.exports = class Greetr extends EventEmitter {

	// the constructor replaces our function constructor logic
	constructor() {
		super();
		this.greeting = 'Hello';
	}

	// will be added to the prototype
	greet(data) {
		console.log(`${ this.greeting }: ${ data }!`);
	}

}

var greeter1 = new Greetr();
greeter1.greet('Tony'); // Hello: Tony!
```

`module.exports` turns it into a module, so it is available for use by other modules.

`extends EventEmitter` replaces `utils.inherits(Greetr, EventEmitter)`.

`super()` is an alternative to `EventEmitter.call(this)`.

# Asynchronous code, Libuv, The Event Loop, Streams and more ...

## JavaScript is Synchronous

**Asynchronous** means more than one process running simultaneously.

*Node does things asynchronously, V8 does not.*

**Synchronous** one process executing at a time.

*JavaScript is synchronous.* Think of it as one line of code executing at a time.

*NodeJS is asynchronous.*

While V9 (which is synchronous) is doing things, NodeJS can do other things at that time.

## Callbacks

A function passed to some other function, which we assume will be invoked at some point.

The function 'calls back' invoking the function you give it when it is done doing its work.

## libuv

It is the C library that makes Aysnchronous I/O possible.

As mentioned previously, there are two types of events in Node. System events (C++ core) and JS events (EventEmitter). *libuv* is related to the system events (C++ core).

Inside Node we have V8 which runs code synchronously. Also inside node there is another library called **libuv**. This is written specially to deal with things happening lower level, events occuring in the OS. libuv connects by request something from the OS (let's say to download something from the internet). It maintains a queue of events from the OS inside itself. It has a constant loop running inside it to check if something is happening to the events in the queue. That loop is called **Event loop**. All this is happening while V8 is running parallelly.

On every loop libuv checks the queue, while checking in that loop it sees that something is complete. It process it and it invokes a callback, that is the code that meant to be run when the event completes. V8 will process the callback after finishing its current task because V8 is syncrhonous. But the entire process is asynchronous because both V8 and libuv are working parallelly.

### Event Driven Non-blocking I/O

This input/output is actually happening at the OS level - opening files, connecting to DBs.

**Non-blocking** - Doing other things without stopping your program from running.

Node has made this possible by doing things asynchronously. This non-blocking architecture is at the core of NodeJS, and this is what makes Node very performant, because many people can ask for the server to do many things without blocking. And it responds as things finish.

## Streams & Buffers

### Buffer

A temparory holding spot for data being moved from one place to another. Intentionally limited in size. It is there for us to gather some data and move it along ...

### Streams

A sequence of data made available over time. Pieces of data that eventually combines into a whole. Usually we're processing that data some way.

Streaming a movie is a similar concept. If you download the entire movie, it will take time but if you stream, you are downloading the entire movie but you are watching it as it comes. So we are processing that stream of data.

So data comes down the stream, it is being stored into the buffer and then gets passed to the process and other stream data comes into the buffer and so on, until the data is complete.

## Binary data, Character Sets, and Encodings

### Binary data

Data stored in binary (sets of 1s and 0s). This is the core of the math that computers are based on. Each one or zero is called a **bit** or **binary digit**.

Everything we store in computers is in binary.

### Character Set

A representation of characters as numbers. Each characters gets a number. **Unicode** and **ASCII** are character sets.

Each character in the word "Hello" has a number associated. What number should be assigned to that character is determined by the "Character Set".
h = 104, e = 101, l = 108, o = 111.

### Character Encodings (e.g. UTF-8)

How characters are stored in binary. Every number has to be finally converted into binary. h = 104 = 01101000 in UTF-8. We can use 8 bits to represent a number in UTF-8 that means we can represent a larger number, which means more number of characters can be represented. So languages are Chinese, Japenese which have more characters can be represented using UTF-8.

#### Node provides encoding feature to JS

JS is not good in dealing with binary data. So node expands itself to allow this feature in JS.

### Buffers in Node

NodeJS stores characters into the buffer and provides encoding and other features. The size of the buffer is finite. In the below example it is 5 as 'hello' has 5 characters.

```
var buf = new Buffer('Hello', 'utf8'); //utf8 is default

console.log(buf); // shows hex values
console.log(buf.toString()); // outputs the hello string
console.log(buf.toJSON()); // outputs the JSON with the unicode characters
console.log(buf[2]); // as an array
```
Since buffers are of finite size, what we write to it is overwritten.

```
buff.write('wo');
console.log(buff.toString()); // wollo - 'he' has been overwritten by 'wo'
```

## ES6 Typed Arrays

We said buffers exist in NodeJS because JS didn't have good ways to deal with binary data. However, that is changing in ES6. ES6 has Typed arrays that can deal with binary data.

```
var buffer = new ArrayBuffer(8); // 8 bytes = 8 * 8 or 64 bits
var view = new Init32Array(buffer); // a 32 bit array with max capcity of 64 bits.

view[0] = 5;
view[1] = 15;

console.log(view);

view[3] = 20; // won't be added as the buffer size exceeds
```

## Callbacks (Revisited)

```
// app.js

function greet(callback) {
	console.log('Hello!');
	var data = {
		name: 'John Doe'
	};
	callback(data); //invoking the callback function
}

// now our greet function and passing it the function to be called
greet(function(data) {
	console.log('The callback was invoked!');
	console.log(data);
});
```

## Files and fs
Node's core file management module

```
// greet.txt

Hello World!
```

Below is a synchronous approach to read a file. This will block the process until the file is read. This is not a good approach for larger files.

```
// app.js

var fs = require('fs');

// It will read the binary data and use utf8 to know what that binary data means.

var greet = fs.readFileSync(__dirname__ + '/greet.txt', 'utf8');

```

So the asynchronous appraoch is below. It asks libuv to run our callback when it is done with reading the file. It might take a long time to read the file but it's OK. This is the most common and popular way to read file in Node.

```
var greet2 = fs.readFile(__dirname__ + '/greet.txt', function(err, data) {

	// this is our callback which is run when the file reading is done.

	console.log(data); // outputs the buffer
	console.log(data.toString()) // outputs Hello World!
});
```

### Error-First callback

Callbacks that take an error object as their first parameter. `null` if no error, otherwise will contain an object defining the error. This is a standard pattern in NodeJS, so we know in what order to place our parameters in callbacks.

If you don't pass any encoding to the `readFile` by default it outputs the buffer in the callback function `data` property. To encode the data, just pass `utf8` as a second parameter to `readFile`.

## Streams (Revisited)

Chunks of data. A **chunk** is a piece of data being sent through a stream.

Streams are extended (inherited) from EventEmitter, therefore they have access to methods like `on`, `emit` etc.

Stream in NodeJS is an **abstract class**. It is a type of constructor you never work directly with, but inherit from.

#### Types of Streams
* Readable
* Writable
* Duplex
* Transform
* Custom (our own)

##### Scenerio

Browser request is a *Readable* stream for node.
Node's response is a *Writable* stream.

#### Streams in `fs`

We are creating a readable stream below, which will read the file and fill up the buffer. If the data size is smaller than the buffer then you will get all the data. But if the text file is bigger than the buffer size than you'll get pieces of the text file at a time, where each piece is of the size of the buffer. So it will read the text file, fill up the fire, emit a `data` event, run all the listeners, then it keeps going back to read the file, fill the buffer, emit `data` event, run all the listeners, and this process continues till the entire file has been read.

Every time it emits the `data` event, it will pass the data that is in the buffer to the listener (`chunk` in below code example).

```
// app.js

var fs = require('fs');

// a readable stream
var readable = fs.createReadStream(__dirname__ + '/greet.txt');

readable.on('data', function(chunk) {
	console.log(chunk);
});
```

`chunk` by default logs binary data that is in the buffer. In order to get the string pass config object to the `createReadStream` function.

```
var readable = fs.createReadStream(__dirname__ + '/greet.txt', {
	encoding: 'utf8',
	highWaterMark: 32 * 1024 // buffer/chunk size
});
```

Let's write this stream

```
var writable = fs.createWriteStream(__dirname__ + '/greetcopy.txt');

readable.on('data', function(chunk) {
	console.log(chunk);
	writable.write(chunk);
});
```

## Pipes
Connecting two streams by writing to one stream what is being read from another.

In node you pipe from a Readable stream to a Writable stream.

Pipes can be chained. As the chunk is being read by a Readable stream it's being passed to a writable stream, which can also pipe it to another writable stream.

To implement piping, NodeJS has a function called `pipe` that is being implemented on a Readable stream.

Piping in NodeJS involves the same idea that has been shown in the above example.

So above code can be simplified as;

```
var readable = fs.createReadStream(__dirname__ + '/greet.txt');
var writable = fs.createWriteStream(__dirname__ + '/greetcopy.txt');

readable.pipe(writable);
```
It send the chunk from the readable to writable using th eevent listener. If our `writable` above was readable, we can pipe it again.

It is not necessary that we pipe the chunk from one file to another. In theory a chunk of data can be piped to any stream. Lets use another node module called `zlib` - a zipping/compressing module.

```
var fs = require('fs');
var zlib = require('zlib');

var readable = fs.createReadStream(__dirname__ + '/greet.txt');
var writable = fs.createWriteStream(__dirname__ + '/greetcopy.txt');
var compressed = fs.createWriteStream(__dirname__ + '/compressed.gz');

var gzip = zlib.createGzip(); // a readable/writable stream - transform stream

readable.pipe(writable).pipe(compressed);
```

### Method Chaining
A method returns an object so we can keep calling more methods.

# HTTP and being a Web Server in Node

## TCP/IP
A **Protocol** is a set of rules that two side agree on to use when communicating. Both the client and server are programmed to understand and use that particular set of rules. It is similar to two people from different countries agreeing on a language to speak in. There could be multiple protocols involved in the communication, but a single protocol is just a particular set of rules for how the information is structured.

**How does the client and server know each other?**
That is where TCP and IP comes in. Each computer is assigned an IP address. When we make connection between two computers, by identifying their IP address, the OS of both systems will establish a **socket** between them. A socket is a line where the information flows between the computers. The information is normally structured within its own type of protocol (HTTP, FTP, SMTP). These protocols just define the structure of the information but not how it will be sent. How it should be sent over the socket is being defined by **TCP (Transmission Control Protocol)**. TCP splits the information into pieces called **packets** and send those packets one at a time.

Your OS has this ability to communicate between two IP addresses using TCP, and Node provides the ability to access these features. Node treats the TCP packets as **streams**.

Sockets in internet are continously opened and closed. The idea of **Web Sockets** to keep that socket open between two computers for constant communication. Which allows the client and the server to send information to one another whenever they want.

## Addresses & Port

### Port
Once a computer receives a packet, how it knows what program to send the packet to.

When a program is setup on the OS to receive packets from a particular port, it is said that the program is listening to that port. NodeJS allows us to have a port address for itself, which it will listen to execute its program.

## HTTP
HTTP is the set of rules (format) for data that is being transferred on the web via TCP/IP. It is the core of how we send information on the World Wide Web (WWW). It has request and response headers.

### MIME type (Multipurpose Internet Mail Extensions)
A standard for specifying the type of data being sent. Examples: `application/json`, `text/html`, `image/jpeg`. The server and the client (browser) understands how to deal with the mime type. If you send an image MIME type, the browser will render an image and so forth.

### HTTP PARSER - `http_parser`
It parses HTTP requests and responses. It can look at the request and response and break it apart for us to have separate pieces of data (headers, body etc.). It is being written in C. It also gives us the ability to create a web server.

## Building a Web Server
`http_parser` provides us the method called `createServer`, which creates a server for us and executes the supplied callback with request and response objects passed as parameters. We then create our response headers. `createServer` will return the server object and which will then be passed to the `listen()` method which tells it about the port on which the server will start listening.

```
// server.js - creating a server at http://127.0.0.1:5253 or http://localhost:5253

var http = require('http');

http.createServer(function(req, res) {

	// building the response
	res.writeHead(200,
		// response headers
		{
			'Content-Type': 'text/plain' // return the plain text
		}
	);

	// res.end means this is the last piece of information we want to send
	res.end('Hello World\n');

}).listen(5253, '127.0.0.1');
```

## Outputting HTML and Templates

In the above code instead of the text, we the file and pass in the content.

```
// server.js

res.writeHead(200, { 'Content-Type': 'text/html' });
var html = fs.readFileSync(__dirname + '/index.html');
res.end(html);
```

### Template
Text designed to be the basis for final text or content after being processed. There is usually some specific template language, so the template system knows how to replace placeholders with real values.

```
// index.html

<h1>{message}</h1>
```

```
// server.js
var html = fs.readFileSync(__dirname + '/index.html', 'utf8'); // decoding the file content as string
var message = 'Hello World!';

html.replace('{message}', message);
res.end(html);
```

Usually there are template engines already written to handle this kind of templating. The above example is just understand the logic under the hood of those engines.

## Streams and Performance
In the above example we are reading `index.html` synchronously, which means if there are too many users requesting for it, the server may get slow. So let's rewrite the app to use Streams instead.


```
// replace this
// var html = fs.readFileSync(__dirname + '/index.html');

// with
fs.createReadStream(__dirname + '/index.html').pipe(res);
```

## APIs and Endpoints

### API - Application Progrmaming Interface
A set of tools for builing a software application. On the web the tools are made via a set of URLs which accept and send only data via HTTP and TCP/IP.

### Endpoint
One particular URL that is part of that API. Sometimes that endpoint does multiple things based on the HTTP request headers (GET, POST, DELETE etc.)

## Outputting JSON

```
res.writeHead(200, { 'Content-Type': 'application/json' });
var obj = {
	firstname: 'John',
	lastname: 'Doe'
};
res.end(JSON.stringify(obj));

```

`JSON.stringify` **serializes** the JavaScript object literal into string.

### Serialization
Translating an object into a format that can be stored or transferred. JSON, CSV, XML, and others are popular.

**Deserialize** is the opposite - converting the format back into the object.

We can serialize the data at the browser end before sending it to Node server, and then at the server's end (NodeJS) we can deserialize it into the JavaScript object.

## Routing
Mapping HTTP requests to content, weather actual files exist on the server or not.

In reference to our above `server.js`, if we make a request `http://localhost:5253/what/is/going/on/here.txt`, the server will still respond the same because the URL is just a part of HTTP request. It is upto the server to deal with it. Since we are not taking the URL into consideration the above URL will react as same as we saw in the previous example.

Let's play with `req.url` to get basic idea of routing.

```
// server.js

if (req.url === '/') {
	fs.createReadStream(__dirname + '/index.html').pipe(res);
}

if (req.url === '/api') {
	res.writeHead(200, { 'Content-Type': 'application/json' });
	var obj = {
		firstname: 'John',
		lastname: 'Doe'
	};
	res.end(JSON.stringify(obj));
}
```

# NPM - The Node Package Manager
The largest ecosystem of open source code in history.

### Package
A package is a collection of **code**, managed and maintained by a package management system.

### Package Management System
It is a software that automates installing and updating packages. Deals with what version you have or need, and manages dependencies.

### Dependencies
Code that another set of code depends on to work. If you use that code in your app, it is a depedency. Your app depends on it. Package management systems downloads this dependency for our code to use it.

### Semantic Versioning
*Versioning what version of a set of code this is*  so others can track if a new version has come out. This allows to watch for new features, or to watch for 'breaking changes'.

The word *Semantic* means that something has a meaning. So in this case, the version means something. Just looking at the version we get some kind of information about the package.

#### MAJOR.MINOR.PATCH
The basic format of Semantic Versioning.
Example: 1.7.2

**Third digit 1.7.3 (PATCH)** - If we have some bug fixes or patches to the above code then we add a new patch. But the code is still backward compitable.

**Second digit 1.8.0 (MINOR)** - If I increment the second number that means I have added some new features. But the code is still backward compatible.

**First digit 2.0.0 (MAJOR)** - If I increment the first number that means big changes, and code using it as a depedency may break.

For more information on symantic versioning check [semver.org]

### NPM vs NPM Registry
NPM is a program comes along with NodeJS, while NPM registry is a collection of other peoples' code.

## `init`, `nodemon` and `package.json`

### `npm init`
A command to initialize our code to be as a node package. It should be run on the root folder of the project/package. It creates a `package.json` with our npm configuration.

**`scripts`** in `package.json` helps us to run commands like `npm test`, `npm start` etc.

**`npm install moment --save`** - NPM the program on my computer will go to the registry and look for `moment` package and installs it in my app. **--save** will save it is a depedency in my `package.json`.

**^** in `^2.0.1` dependency versioning means npm is OK to install anything in version `2.x.x`. In other words install it if any minor or patch changes, but within that major version.

**~** in `~2.0.1` means that only update patches.

### Accessing node modules in our app
Node has a builtin feature in the `require` function to handle this.

```
var moment = require('moment');
```

NodeJS will first look for `moment` into its core. If it doesn't find it there then it looks into `node_modules` in your app.

### Development Dependencies
These are the dependencies that we only need during our development. It doesn't impact our our app. Example `npm install jasmine-node --save-dev`.

### Installing global depdencies
Install depedencies not in our package but globally somewhere on the computer where it can be accessed by any package.

### `npm update`
To update all the dependencies defined your `package.json`.

### Nodemon package - Node Monitor
It is a watcher for our node code during development. Install it globally.

```
> npm install nodemon -g
> nodemon server.js
```

# Express

## Installing Express

```
> npm install express --save
```

```
// app.js

var express = require('express');
var app = express();

// 'process' is a global object provided by node which has an 'env' variable
var port = process.env.PORT || 5253;

app.listen(port); // creates a server that listens to port 5253
```

### Environment Variables
Environment variables are global variables specific to the environment (server) our code is living in. Different servers have different variable settings, and we can access those values in our code.

Env. variables can be setup while setting up node on that server.

### HTTP Method
Specifies the type of action the request wishes to make. GET, POST, DELETE, and others. Also called *verbs*.

Express looks for the method requested and allow us perform the response.

```
// app.js

app.get('/', function(req, res) {
	res.send('Hello World!');
});
```

## Routes

```
// app.js

// example: /person/john
app.get('/person/:id', function(req, res) {
	res.send(res.params.id);
})
```

## Static Files and Middleware

### Middleware
Code that sits between two layers of software.

Express provides an easy way to plugin middleware in between the request and the response to handle certain requests and providing certain responses. It also allows to have multiple layers of middleware. It lets me build re-usable code for HTTP requests and responses.

### Static Files
Not dynamic - files that are not being generated by the code. For e.g. HTML, CSS and image files.

### Express Middleware
When the request comes for static files, we can use Express middleware to serve them `epxress.static(dir)`. This will serve the respective static file in the defined path based on the route.

```
// server.js

app.use('/assets', express.static(__dirname + '/public'));
```

#### Custom Middlewares in Express
```
// server.js

app.use('/assets', function(req, res, next) {
	console.log('Requested URL', req.url);
	next(); // move on to the next middleware
});
```

Express has a good collection of middlewares. `cookie-parser` and `passport` are the popular ones. List of all middlewares can be found on its website.

## Templates and Template Engines

Express is an unopinionated framework. It custom templating engines (e.g. handlebars, jade, ejs etc.). You just need to install the engine via npm and tell express to use it via `app.set('view engine', '<extension of the template file>')` command. By default Express looks for template files in the folder called **views**.

### Using EJS templating engine

```
// views/index.ejs

<html>
	<head>
		<link rel="stylesheet" href="style.css">
	</head>
	<body>
		Person: <%= ID %>
	</body>
</html>
```

Install `ejs` via npm.

```
> npm install ejs
```

In order to render the template in Express use `res.render()` instead of `res.send()`.

```
// app.js

app.set('view engine', 'ejs'); // use .ejs files as templates

app.get('/person/:id', function(req, res) {

	// renders index.ejs
	res.render('index', {
		ID: req.params.id
	});
})
```


## Querying and Post Parameters

In GET requests, the querystring is embedded in the URL. In POST requests it is being moved in the body.

Express provides support for querystring out of the box using `req.query.<parameter name>`. However it doesn't provides support for handling POST requests. So we need to get a middleware to do it.

There is a famous middleware to handle POST requests called `body-parser`.

```
> npm install body-parser --save
```

```
// index.ejs

<form method="post" action="/person">
	<label>First name: <input type="text" name="firstname"></label><br />
	<label>Last name: <input type="text" name="lastname"></label><br />
	<input type="submit" value="Submit">
</form>
```

```
// app.js

var bodyParser = require('body-parser');

// create application/x-www-form-urlencoded parser
var urlencodedParser = bodyParser.urlencoded({ extended: false })

app.post('/person', urlencodedParser, function(req, res) {
	res.send('Thank you!');
	console.log(req.body.firstname);
	console.log(req.body.lastname);
});
```

If the POST data is in JSON (may be from a jQuery form submission).

```
// app.js
var jsonParser = bodyParser.json();

app.post('/person', jsonParser, function(req, res) {
	res.send('Thank you for the JSON data');
	console.log(req.body.firstname);
	console.log(req.body.lastname);
});

```

## RESTful APIs and JSON

### REST
It is an architectural style for building APIs. We decide that HTTP verbs and URLs mean something.

```
app.get('/api/person/:id', function(req, res) {
	// get that data from the database
});

app.get('/api/person', jsonParser, function(req, res) {
	// save to the database
});

app.delete('/api/person/:id', function(req, res) {
	// delete from the database
});
```

## Structuring an Express app

Use `express-generator` to scaffhold your Express app.

`> npm install express-generator -g`

Go into your desired folder where you want to create the app and run `express-generator <name>`.

You can also modularalize your code easily yourself.

# JavaScript, JSON and databases

## Relational Databases and SQL
A relation database has tables, that has fields and columns. We normalize our data in relational databases in order avoid redundancy/repetition. SQL is a lanugage to query database.

In JS we store data as Objects. A table can be represented as array of objects. So we need someone to convert our tabular data into objects in order to be used in JS.

## Node and MySQL
There is a really good package named `mysql` on npm to use MySQL with Node. See its documentation for usage. It returns an array of JS Objects when we query our tabular data in MySQL. It even streams the rows so that we can pipe them to our response object if needed.


## NoSQL and Documents
**NoSQL** - A variety of technologies that are alternatives to tables and SQL. One of those types is a **document** database. MongoDB is one of those.

### Why NoSQL is powerful
In old days relational databases were great because they saved spaces by avoiding repeating information, but nowadays HDD spaces are cheaper and not a bigger concern. Instead we are more concern with how often we change software. Adding a field in a SQL databases can be cumbersome. But if the data is stored in documents (like JSON), then I can add a field in one object and wouldn't impact the software much, that field will simply be undefined for other objects. Structures can be changed on the fly. It is more flexible.

### Using MongoDB with Node
**Mongoose** is the most popular npm package for MongoDB.

```
// app.js
var mongoose = require('mongoose');

var Schema = mongoose.Schema;

// create a schema
var personSchema = new Schema({
	firstname: String,
	lastname: String,
	address: String
});

// create a model
var Person = mongoose.model('Person', personSchema);

// create a document
var john = Person({
	firstname: 'John',
	lastname: 'Doe',
	address: '555 Main St.'
});

// saving it in db
john.save(function(err) {
	if (err) {
		throw err;
	}

	console.log('person saved!');
});
```

The great thing about Mongo is that the structure it saves data is very similar to how JS stores data i.e. objects. Each object has its own structure. If one of the document has a different structure the code won't complain.

# The MEAN Stack (MongoDB + Express + AngularJS + NodeJS)
**Stack** is a combination of all technologies used to build a piece of software.

MEAN Stack is a very popular stack to build web applications. All these technologies embrases **JavaScript**. They work very naturally with each other.

Browsers are written in C++. They have JS engine embedded in them and give them access to extra features.

## DOM
The structure that browsers use to store and manage web pages. Browsers give the JS engine the ability to manipulate the DOM. The DOM doesn't live inside the JS engine of the browser. The browser uses the DOM to access the webpage. It changes the DOM and re-renders the webpage.

When the browsers gets HTML response from the server, it creates a DOM with a hierarchy of elements called **DOM Tree**. Then the browser renders the webpage using the DOM.

A JS engine is also embedded within the browser (V8 in Chrome). That engine receives the JS code that the server sends to the browser. If that JS code has some features to manipulate the DOM then JS engines does that manipulation and browser re-renders the webpage.

Now managing the code for different JS engines and browsers is cumbersome. So frameworks like AngularJS helps to deal with that, making our app managable.

## Note about Angular1, Angular2, ReactJS and other frameworks
They are just JavaScript. They are not adding anything extra to JavaScript. They are just using what the browser and the JS engine make available to JS.

## Full-Stack Developer
A developer who knows all the pieces of a software stack, and thus build software by themselves.
