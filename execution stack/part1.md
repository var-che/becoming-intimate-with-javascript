From the very beginning of the Javascript program, we start using the execution context. It is there from the start up to the very end of the program. Because of that fact, we are led to a conclusion that that part of the language is crucial to understand before we move on. The execution context is a fundamental part of the language. On the stack, we are going to pushing and popping execution contexts, the things that are created when the functions are called and destroyed when functions return.
One more important thing that exists from the very beginning of the program is 'global context', a context that possesses a global object, and that which possesses all built-in methods that come with the language (String, Number, Random...). One of the interesting facts is that when you run a JS file, even if its empty, the 'global context' along with global object will be made.

So, what kind of stack are we talking about?

It's LIFO stack, last in, first out. It functions in a way that the last element that made into the stack, is being processed first. In a more concrete way, when we call a function and put it into the 'execution stack', the current function execution is put on hold until the newly created function is done running. When the function is done, the context related to that function is being popped out from the stack and the program resumes. 

    function first(){
      console.log('Hey');
    }
    
    first();
I am going to take a case of this code. I have declared a function and called it after. By calling it, I have created a new line, a new execution context on the top of the stack, that also sits on 'global context'. Since it is called, we do all instructions in the body of 'first' function, by that I mean logging 'Hey' in console, and since that is the first and the last instruction in the body of the function, we are facing with '}' symbol, and that means that we are done with that function. Our function returns and the execution context for that function is being removed from the stack.

    function first(){
      second();
    }
    
    function second(){
      console.log('Hey');
    }
    first();

Here is another example. Beginning of the program, we get the 'global execution context' for gratis, as always, and with it, we are calling function 'first' and putting its 'execution context' on the stack. In the body of that function, we have instruction to call function 'second' and by doing that, we are putting 'second's execution context on the top of the stack. Because its the last context in the stack, and because of the LIFO mechanism, the body of function 'second' has been put as the priority in the program. And because of that, the function 'first' still has not completed and it is still there. 
We are logging 'Hey' in the console, and we are hittin the '}' symbol, which means that our function has returned. We don't need it anymore and the program resumes where it paused in the function 'first'. Because the very next line is the symbol '}', the function returns and the context is being what? Popped out the stack. 
After the 'first()' line in the code, we don't have anything more and the 'global context' is being popped off the stack. We have reached the end of our program.

Important!

JS program uses a mechanism called 'Synchronous execution', and that means that the program is being executed line by line. Finishes one line and then! comes to the next one. Every time when the function is called, execution of the program waits when the newly created function ends, and by ends, I mean hitting the 'return' statement or the '}'. Then, it just resumes where it paused. 
Another of the important characteristics of Javascript language is that it is 'Single-threaded', and that is the ability to process one command/instruction before it gets to another one. A simple example would be:

    console.log(2+2)
    console.log(4+2)

Here, we get the result of 4 and then 6, one after another. The top most instruction is being finished and then it comes to the next one. A counterexample would be when the both of instructions would execute at the same time, by 'Multithreading', and maybe the values would return at the same time. The bottom instruction does not depend on the first one. That would be a 'parallel execution', and visually it would look like we have two stacks, one next to another, and putting the topmost instruction on the left stack, and the bottom instruction on the right stack. 
