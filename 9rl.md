#  Readings: FUNCTIONAL PROGRAMMING

##  Reading

###  Functional Programming Concepts (https://medium.com/the-renaissance-developer/concepts-of-functional-programming-in-javascript-6bc84220d2aa)
1.  What is functional programming?
    -  Functional programming is a programming paradigm — a style of building the structure and elements of computer programs — that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data — Wikipedia
2.  What is a pure function and how do we know if something is a pure function?
    -  Here is a very strict definition of purity:
        -  It returns the same result if given the same arguments (it is also referred as deterministic)
        -  It does not cause any observable side effects
3.  What are the benefits of a pure function?
    -  Pure functions are stable, consistent, and predictable
    -  Given the same parameters, pure functions will always return the same result
    -  We don’t need to think of situations when the same parameter has different results — because it will never happen
    -  The code’s definitely easier to test. We don’t need to mock anything. 
4.  What is immutability?
    -  Unchanging over time or unable to be changed
        -  When data is immutable, its state cannot change after it’s created
            -  If you want to change an immutable object, you can’t
            -  Instead, you create a new object with the new value.
5.  What is Referential transparency?
    -  Basically, if a function consistently yields the same result for the same input, it is referentially transparent
    -  pure functions + immutable data = referential transparency

##  Videos

###  Node JS Tutorial for Beginners #6 - Modules and require()  (https://www.youtube.com/watch?v=xHLd36QoS4k)
1.  What is a module?
    -  Logical modules for different bits of code that has functionality in our application and then call upon the module when we need to use it
2.  What does the word ‘require’ do?
    -  It make sure that the module is available to access for our app
3.  How do we bring another module into the file the we are working in?
    -  A path to the module  Ex. var counter = require('./count');  
4.  What do we have to do to make a module available?
    -  Add to the bottom of the module the exports statement.  Ex.  module.exports = counter