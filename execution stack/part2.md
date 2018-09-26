Programming is creating things from nothing, in digital format, and performing transformations on those things. Variables, as well as functions, are making our lives easier when doing that. Variable is a thing for what we can with a confidence tell that it will change. For computers, it is data that can be changed during the runtime of the program.

    var a = 4
    a = 5
    a = 'amsterdam'

We stated that the value of *a* is *4*, and later we changed that value to *5*, and after that, into the *amsterdam* string. *a* is a variable and its value changed during the program. 

Alright, but why do we use functions? We saw that we can transform the data even without functions, so why do we need them? 

That is a good question, and the reason why we are using functions is using the same code over and over again. Code reusability. Functions collaborate with variables very often in order to achieve some data transformation. With functions, we can replicate the same routine to transform the data on many places in our program. 

One more reason for using functions is the abstraction. We don't even have to know how the function works, as long as it returns what we want, it is all just fine.

    function oddOrEven(x) {
      return ( x & 1 ) ? "odd" : "even";
    }
    
    oddOrEven(10); // "even"
    oddOrEven(11); // "odd"
    oddOrEven(17); // "odd"

For us, that makes sense, but how is that mapped into computer sense? It has to find that data, perform some manipulation on them and eventually, give us some meaningful/desired result from that. What are those routines that it has to go through to achieve that? Well, that is the topic in this section.

What we have learned from the previous chapter is that variables belong to some context. They are located in some of the rows from our FILO stack.

    function first(){
      // local variable of 'first' function, bound to the 'first' execution context
      var one = 23;
    }
    
    // variable bound to the global execution kontext
    var e = 'b';

We have to be more systematic. Let me introduce you with a variable object. It is a domain of data that is bound to the execution context. It is a special object that is bound to the context, and it stores our data such as variables and function declarations. Because it is a special object, we can't access it directly. It is a concept, an abstraction. It is a routine that uses an optimal algorithm that will do those two things: store variables and function declarations. Let us use this example:

    function first(input){
      var z = 'one';
    }
    
    var b = '3';
    var y = 522;
    
    first(14)

In order to be more organized in presenting variables and functions, I am going to take a stack and make/draw a section that will serve me as a record. I am going to track and write the values of variables and function declarations. We said that it is the part of the execution context and because of that, I will draw that section on the right side, to be more organized. In the *global context*, I will put a function declaration (the name that points to a function), along with *b* and *y* variables and their values.

Then, calling the *first* function that has the number *14* as a formal parameter. By calling this function and entering into new *execution context*, we are creating activation object where we can get a new property that we don't have in variable object. That property is called *arguments*. We are making a new *execution context*, wherein the AO we have *input* that points to *14*, and *z* that points to a string *one*.

Now, wait a minute, slow down. I think that all of this was rushed up. I understand that VO stores the data, why all the sudden we have this AO? It has the same purpose as VO, to store data. So why two names for the same thing?

That is a great question. Since the algorithm for VO does not cover the case with formal parameters (things that we put in the functions), and because we were working in the *global context*, and it doesn't have formal parameters, simply because it is not a function. With AO we have covered the case with function arguments. In AO, as I sad, we got the property *arguments* that contains all the things that we have put into the function  when we called it. Here, I am going to show you data structure using JS object.

    globalExecutionContext = {
      VO: {
        first: points to some function in memory,
        b: points string 'b' somewhere in memory,
        y: points to number 522 somewhere in memory
      }
    }
    

Now, the difference is a bit more visible. In AO, the object that we get immediately upon the creation of the new *execution context* (called function), now has *arguments* object that contains information on formal parameters. And besides *arguments* property, we have identical things that VO contains, a mechanism that stores data, variables and function declarations.

    firstExecutionContext = {
      AO: {
        arguments: {
          0: 14,
          length: 1
        },
        input: points to a number 14 in memory,
        z: points to string 'one' in memory
      }
    }

