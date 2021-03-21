# THIS keyword and how to fix losing context

## THIS keyword

**This**

 This keyword refers to an object, that object which is executing the current bit of javascript code.

 In other words, every javascript function while executing has a reference to its current execution context, called this. Execution context means here is how the function is called.

 Important when and from where the function is called, does not matter how and where function is declared or defined.

**Example**

```js
function bike() {
 console.log(this.name);
}

var name = "Ninja";
var obj1 = { name: "Pulsar", bike: bike };
var obj2 = { name: "Gixxer", bike: bike };

bike();           // "Ninja" the same as window.name
obj1.bike();      // "Pulsar"
obj2.bike();      // "Gixxer"
```

- The job of bike() function is printing the this.name which means it’s trying to print the value of name property of the current execution context(i.e.this object).
- When function bike() gets called it prints “Ninja” because the context of execution is not specified so by default its global context and there is a variable name is present at global context whose value is “Ninja”.
- In case of obj1().bike(), “Pulsar” gets printed and the reason behind this is function bike() gets called with the execution context as obj1 so this.name became obj1.name . Same with obj2.bike() where the execution context of function bike() is obj2..

### Default THIS
If we are in strict mode then the default value of this keyword is undefined otherwise this keyword act as global object, it’s called default binding of this keyword. (default is window object in case of browser).

When there is an object property which we are calling as a method then that object becomes this object or execution context object for that method, it is implicit binding of this keyword

## Losing THIS


 When passing object methods as callbacks, for instance to setTimeout, there’s a known problem: "losing this". Or once a method is passed somewhere separately from the object – this is lost.


```js
const obj3 = {

 numbers: [1,2,3,4],

 doSomething() {

   console.log(this);

   setTimeout(function doAnotherThing(){
     console.log(this)

     this.numbers.forEach(function log(number){ //Cannot read property 'forEach' of undefined

         console.log(number); // Undefined

     });

 }, 100); }

}
```


### Solution 1: Bind()

```js
const obj3 = {

 numbers: [1,2,3,4],

 doSomething() {

   setTimeout(function doAnotherThing(){

     this.numbers.forEach(function log(number){

         console.log(number);

     });

 }.bind(this), 100); }

}
```


The result of doAnotherThing.bind(context) is a special function-like “exotic object”, that is callable as function and transparently passes the call to "doAnotherThing" setting this=context.

In other words, calling boundFunc is like 'doAnotherThing' with fixed this.

For instance, here funcUser passes a call to 'doAnotherThing' with this=obj3


### Solution 2: Save context
```js
const obj3 = {

 numbers: [1,2,3,4],

 doSomething() {

   const self = this;

   setTimeout(function doAnotherThing(){

     self.numbers.forEach(function log(number){

     //Cannot read property 'forEach' of undefined

         console.log(number);

     });

 });

}

}
```

We can save this in new variable self, and use SELF instead THIS in callback.


### Solution 3: Using arrow function

While other callback functions lose This and refer to window, arrows functions are special. They don’t have own THIS and always see on outer context(parent’s this).

```js
const obj3 = {

 numbers: [1,2,3,4],

 doSomething: () => {

   console.log(this) //window

 }

}
```

So we can use this feature to prevent losing context:

```js
const obj3 = {

 numbers: [1,2,3,4],

 doSomething() {

   const self = this;

   setTimeout(() => {

     self.numbers.forEach(function log(number){

         console.log(number);

     });

   });

}

}
```