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
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
  
