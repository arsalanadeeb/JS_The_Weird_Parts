# JS_The_Weird_Parts
//This work is under progress do not read it ....

20/01/2020.....

Auther's Philosophy:- "Do not immitate but understand" here auther says do not mimic or just know how thinks work but go under the hood                          and understand the basics that will make you able to write robust code and understand the framework written by                            smart people.

Conceptual Asides:-These are some concepts that are not directly used but very important to grasp other concept in depth .

Conceptual Aside 1:-

Syntax Parser:-Syntax parser is a part of interpreter or compiler(intermediate code) which takes code line by line and converts it into a               code that will be familier with computer or hardware and do some extra stuff which is necessary .

Lexical Environment:-Lexical means "having to do with words or grammer" 

                      function myVar(){
                      var a=10,
                      }

                    here the variable you have mentioned in function actually tells where it will reside in the memory this thing is taken                      care by the interpreter.
//my understanding:-Lexical Environment means the code that is surronded by {} is actually sitting in the memory together. 
                     basically these are the areas of your code which are having respective memory location.
                     
Exicution Context:-It is the the area of the code that is actually running or it is in exicution.

Name/Value Pairs and objects:-   Adress="13B Bakers Street" it is a name value pair.

                                 The auther explicitly says do not assume JS object other than the key value pairs.
                                 {
                                 Adress:{
                                          city:"London",
                                          friends:5,
                                          friendsAddress:{ city:"Delhi"
                                                            }
                                        }
                                 
                                 }
                                 in any exicution context only one Name can be there.
  
Global Environment and Global Object:- When You run your JS code many exicution context can form but there is one Exicution context that                                        will definetly form ie base exicution context or Global Environment .When this Global Exicution                                          Context or Global Environment is created it will create two things for you 
           
                                       1:-Global Object(just a collection of name value pairs)
                                       2:-'this' variable
                                       
Excercise:-In oreder to Explain Global Object base/Global context and Global object and this auther creates Project 0001. here the src file is empty but in browser console you can see 'this' is getting mapped to window object and window object got created automatically 
by JS engine .


Ecicution context and Hoisting:-

      Exicution Context consist of two phases 
      1:-Creation Phase(where memory allocation happen)
      2:-Exicution Phase(where actual line by line exicution happen)

                                  console.log(b)
                                    hoist()
                                    console.log(newHoist)
                                    
                                    var b="this will not hoist as it is"
                                    console.log(b)
                                    
                                  function hoist(){
                                       console.log("function as it is hoist but not variable")
                                   }
                                
                                var newHoist=  function (){
                                       console.log("function as it is hoist but not variable")
                                   }
                                   
                                   o/p:-  undefine
                                          function as it is hoist but not variable
                                          undefine
                                          "this will not hoist as it is"
                                   
This is because at the time of exicution(creation phase) Syntax parser will give memory to all functions and variable for functions it will allocate the memory and put function body in that memory,but for variable it will only allocate the memory but assign with a placeholder called "undefine" 

First time when we are doing console.log(b) its value is undefine because only creation phase of exicution have completed(in initial load) but when next time we are doing console.log(b) its giving the value because exicution context have been passed throug that statement.

,hoisting is not a recommended way to use in your code .As people say hoisting is that all definitions get bubble up in the code
that is not true if that happens variable use before variable definition do not give undefine.


Conceptual Aside 3:-  Undefine in JS
                      undefine is a keyword a special value that is assigned by js engine during exicution(creation phase).
                      
                      var a ,
                      console.log(a) //undefine
                      console.log(b) //Uncaught ReferenceError: b is not defined
 So if a value is declared but not assigned JS eng will assigne a placeholder value undefine .Usage of keyword undefine should not be done by programmer to avoid conflict while debugging.
 
 
 Conceptual Aside 4:-
 
 Single Threaded and Synchronous:-
 Java script is a single threaded and sinchronous language.
 
 Single Threaded:-
 Thread is a light weight process,a process is a peice of code in exicution cobtext.Single threaded means one statement of the code from a thread can get exicuted on a perticular time.
 
Synchronous:-
In an order means the flow in which exicution will occure is define or simply linear .You can predict which peice of code will get exicuted if current line in exicution is known.


Function Invocation and Exicution Stack:-


                                  function a(){
                                  console.log("a")
                                  }
                                  function b(){
                                  console.log("b")
                                  a()
                                  }
                                  var c=10;
                                  b();


When this peice of code loaded ,first global context get created (global object and 'this' get initialised) but where these memory get initialised answer is.... in Exicution stack 
In exicution stack all function and var c get loaded but when b() get exicuted it is a function invocation/call/run.
The moment a function invocation happen a new local exicution context get pushed in to exicution stack (with 'this' get initialised with local exicution context) and when function ends it again get popped even in case of IIFE.
The top pointer of exicution stack always pointing to context that is currently getting exicuted .


Function Context and Variable Enviroment:-

                              function second(){
                                var myVar     // what happen if you remove this line
                                console.log(myVar)
                              }

                              function first(){
                                  var myVar="first"
                                  console.log(myVar)
                                  second()
                              }

                              var myVar="global"
                              console.log(myVar)
                              first()
                              o/p: global
                                   first
                                   undefine
                            
 Here auther took myVar in global context and in functions local context also.
 When this code first gets loaded at creation time all function will get memory .at exicution time myVar ="global" get assigned,
 on the invocation of first() new local context get created in exicution stack and at exicution of that context myVar which is not in global but in the exicution context of first() create a seperate copy of myVar and set it to "first" during the exicution phase.
 Since second is only declaring myVar, at creation time 'undefine' get filled in myVar of second() context so it get printed.
 
 
The Scope Chain:-
Scope:-Is a area of code where your veriable and functions are awailable.

The auther says if you call a function or use variable in exicution context it searches its definition in its local lexical scope .
since every exicution context have Reference to outer lexical environment if the definition not found in local scope it will move one level up and search in its  parent's lexical scope.and if not found there one more level up and so on its a chain same prototype chain.
 
        var a=1;                                                                

        console.log(a)

        m1();

        function m1(){
            var a =2
            console.log(a)
            b();
        }

        function b(){
            var a;
            console.log(a)
        }
        
        o/p:-
        1
        2
        undefine
when we log a is present in local context so got printed
when we log a with in m1 its present in local context so got printed.
when we log a with in b here a got define during creation phase with undefine so undefine got printed.
        
Reference to outer lexical environment:-A pointer in every exicution context in exicution stack that points to lexical scope of its parent.
 
         var a=1;                                                                

        console.log(a)

        m1();

        function m1(){
            var a =2
            console.log(a)
            b();
        }

        function b(){
            console.log(a)
        }
        
        o/p:-
        1
        2
        1
when we log a is present in local context so got printed
when we log a with in m1 its present in local context so got printed.
when we log a with in b here a is not define during creation phase so it will look in to its parent lexical scope which is global.

        var a=1;
          console.log(a)

          m1();

          function m1(){
              function b(){
                  console.log(a)
              }
              var a =2
              console.log(a)
              b();
          }
          b();
          o/p:
           1
           2
           2
           Uncaught ReferenceError: b is not defined

           
when we log a is present in local context so got printed
when we log a with in m1 its present in local context so got printed.
when we log a with in b here a is not define during creation phase of b so it will look in to its parent lexical scope which is m1.
when we call b() from global context it gives b not define because b is not present lexically below the global it will get created 
at the time of exicution phase of m1().


 
 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
  
