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
