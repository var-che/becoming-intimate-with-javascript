# Execution context

In this chapter, we are going to tackle the subject of execution contexts, how are they activated, how they behave on the stack and what is its purpose. This is not going to be a very heavy subject, especially because we are going to recycle the things that we have learned and put them into use. Functions will also come to play because creating a new execution context happens when some function is called. Luckily for us, that is only one line of code and you are probably used to using them every day in your developer life.

(pic 11)

First of all, we need to establish what global execution context is. 

It is a space reserved on the stack memory which has a collection of all variable and function declarations in the global scope of the code. That context has the longest life time, because it is there from the beginning of the program, up until the end of it. Meaning that if you create some variable in that context, it will be available for the whole life span of the program. 

(picture 12)

From this picture you can see that functions that return are getting popped off the stack, along with the things defined inside them. Like with the d function that had ‘x’ variable inside, the moment it returned the data inside on the memory address of <400> has been cleared. 

Also, take a look at the function that is currently executing, the function m. Previously, on the memory address <400> there was a different variable (x) with a different value (433) from a different context (d’s execution context). Since space has been cleared up, a new function is ready to take up the space that once was taken. And you can see that now, there is a variable d pointing on the address of <400> that has the value of ‘s is here’.  And of course, once m function returns, everything inside that will be cleared from the stack, and we will be left with only global execution context.

Please take a look at that context. I know that what I have drawn only variables ( e, and g), but in that context, there are also function declarations as well. The ones that I have been calling from the global scope, such are functions z, d, and m. So the more accurate representation would look something like this:
( picture 13 )

A thing to notice is that functions are stored on the heap, you can see the addresses that are stored on the stack but that’s nothing to worry about right now. I will be explaining that in depth later on in this book. 

## 5.1 Code representation of the execution stack

An array unitises the stack data structure and has push and pop method and we can write it like this:
```javascript
var execStack = []
```
and if we run the JS file, we get global execution context pushed into that list:
```javascript
var globalExecContext = {}
execStack.push( globalExeContext )
```
This is very straightforward and it represents the mechanism that I have mentioned above. I used object to represent the context, just like we have been using it in the previous chapter, so we can get key-value pair of memory-value in it. In every context that we define, we will have memory-value pairs in them, pushed into the execStack.

( pic 14 )

Using this picture, we can edit `globalExecContext` and after pushed into the stack will look like this:
```javascript
execStack = [{
  204: {type: 'primitive', value: 17},
  208: {type: 'reference', value: 5000}
}]
```
So, what is this? It is not a tricky question, just read what we have in the code there.
It is an array that as a first element have an object that contains memory-value keys inside it. That first element would always be global context. Is that clear? Of course it is. Now let us move on to the execution of the function k. 

Can you guess what are we going to do first when the function is called? Hint: it has to do with the stack. We are going to push a new object into the stack, and that object will contain what? 
```javascript
var kExecContext = {}
execStack.push( kExecContext )
```
( pic 15 )

Initially, we can set it just as an empty object sitting on top of the stack, and as soon as we start evaluating the code of that function body, yes, I mean the only line written in there, then we can start changing the object itself. In our code above, we are telling something like this:
```javascript
execStack[1][400] = {type: 'primitive', value: 55}
```
which translates into, get in that last object on the stack, set 400 as a key and that object as a value, and at this point we have this on our stack:
```javascript
execStack = [{
  204: {type: 'primitive', value: 17},
  208: {type: 'reference', value: 5000}
}, 
{
  400: {type: 'primitive', value: 55}
}]
```
( pic 16 )

Take a moment and look at what is out there. Two objects on the stack, occupying some memory space, and having values in them. That means that at this point of our program, if we would request a value from the memory 204, we could get it, because it is there, available for us. 

(picture 17)

We would be performing a stack lookup very soon, but for now, let us finish our program. We have reached the return statement of our k function and then what happens? Can you remember what happens when some function returns? What happens on the stack?

( picture 18 )

We are performing a pop function on the array, 
```javascript
execStack.pop()
```
that way we are resizing our stack that getting us back on the one element, the global context:
```javascript
execStack = [{
  204: {type: 'primitive', value: 17},
  208: {type: 'reference', value: 5000}
}]
```
Clearly, you can see that the memory space on the address is no longer there, that memory slot has been cleared and if some other function would get called, it would be using that memory section. Recycling. And we are back on the square one (pun intended), proving that the global context is there longer than the function one. Now we are left with the last step of our program, and that is to end it.

( pic 19 )

This would perform the 
```javascript
execStack.pop()
```
which leaves us with an empty stack, memory cleared stage, program has ended stage. 

## 5.2 Global execution context

I have briefly mentioned the global context, and we have seen one important feature that it has, and that is the longest life span of all contexts that will ever be created. But besides that, what else does it have? Let us address the stuff that you can get from it. What does it contain?

There are lots of stuff if there, not just the variables and function declarations that we make like you have seen on the stack related pictures.

In global context, there is a `global` (nodejs) or `window` (browsers) object, that contains all build in functions and objects that come with the language. 

Whenever you declare a variable or a function in that global scope / context, it will become a property of that `global` object. A property that gets a key the same as your declaration name, and the value, well, the one that you have assigned to that variable. That means that:
```javascript
var zet = '212'
```
Is the same as:
```javascript
window.zet = '212'
```
Now, this is not necessarily important to know at this point, but I figured out that I should start easing you up into the objects in JavaScript, I don’t want all of the sudden at some point of this book. And the thing to memorise at this point is that:

1. There is a global/window object in the global context
2. All built in methods can be found attached to that object

Question, how many built in functions do you know that come with JavaScript? Or, without using any libraries, what are the functions that you use the most in your coding? 

Alright, things to address since we are on the global object still. You know that we have said in the previous chapter that some objects can be found on the stack, and not on the heap? `global` is one of those cases. A good reasoning that this object should be on the stack is of the fact, that accessing the memory from the stack is much faster then from the heap. 

( to continue )

## 5.3 Back to data declarations

We have seen from the pictures with a stack memory that there are blocks bound to global and function contexts. In those, the data is stored with respect to where the data is declared. If we declare a variable in the global context, then it is stored in the global context block, and if some data is declared in some function, that data is stored in the block of that function context. 

There is a clear distinction where is data going to be stored, in which block on the stack, and ENTIRELY that depends on where the declarations are made in the code. 

If you remember, I have been using an object to encapsulate the data that is declared in the respected scope, and now I can follow up with a slight change and introduce you with a concept of Variable Object.

A Variable Object is a object that gets created with every execution context created during the run time of the program. It is a object that stores: 

1. function declarations
2. variable declarations
3. functions formal parameters

?> _TODO_ Note that documentation links begin with `#/`.
