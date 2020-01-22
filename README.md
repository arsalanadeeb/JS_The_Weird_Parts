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

                                  console.log(b)
                                    hoist()
                                     var b="this will not hoist as it is"
                                   function hoist(){
                                       console.log("function as it is hoist but not variable")
                                   }
                                   
                                   o/p:-  undefine
                                          function as it is hoist but not variable
                                   
This is because at the time of exicution Syntax parser will give memory to all functions and variable for functions it will allocate the memory and put function body in that memory,but for variable it will only allocate the memory but assign with a placeholder called "undefine" 
,hoisting is not a recommended way to use in your code .As people say hoisting is that all definitions get bubble up in the code
that is not true if that happens variable use before declaration do not give undefine.


Conceptual Aside 3:-  Undefine in JS
                      undefine is a keyword a special value that is assigned by js engine .
                      
                      var a ,
                      console.log(a) //undefine
                      console.log(b) //Uncaught ReferenceError: b is not defined
 So if a value is declared but not assigned JS eng will assigne a placeholder value undefine .Usage of keyword undefine should not be done by programmer to avoid conflict while debugging.
 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
  
