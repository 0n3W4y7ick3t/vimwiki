## function is value
In go, like many other languages, function is also a value whose type is `func(arg Type, ) Type`, which is also called the signature of this function. You can pass functions as paramaters and return them as well.

## closure
Closure is just a fancy word for a function inside another function, the inner function has access to all the variables in the outer function scope, no more.

## defer 
defer functions are called after the return statement, before the function where the defer is called actually exit.
There is one way to know what's a variable's value after the defer is executed, that is to use **named return values**, since they live inside the whole function, they can be accessed in the defer too.  So eventually after the outer func returned, the named return values carry the changes made in defer too. 

## blank returns 
Never use this along with named return values, it's terribly unreadable.
