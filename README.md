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


Asynchronous Call back:-
https://miro.medium.com/max/1050/1*zeKjWCjyAGZ9JN4fvnWsiA.png

Java Script(v8 engine) is pure syncronous language but JS runtime environment is Asyncronous in nature.

Why JS is synchronous


                               function waitThreeSeconds() {
                                        var ms = 5000 + new Date().getTime();
                                        while (new Date() < ms){}
                                        console.log("finished from async")
                                    }

                                    function clickHandler() {
                                        console.log('click event!');   
                                    }

                                    // listen for the click event
                                    document.getElementById("myButton").addEventListener('click', clickHandler);

                                    waitThreeSeconds();
                                    console.log('finished execution');
                                    
                                    o/p:-app.js:5 finished from async
                                         app.js:16 finished execution



 In this code waitThreeSeconds() is a blocking code it blocks the exicution for three seconds still the code is in sync because 
 in JS run time environment API,Timers,HTTP Request and Events goes to WEB API and after complition come to CallBackQueue
 from there event loop pics in FIFO fasion if exicution stack is empty .Since our waitThreeSecond function do not have any of the (
 API,Timers,HTTP Request and Events) so it was actually busy in exicuting while loop .
 
 By changing slightly in the code we can get no of time the while loop get exicuted 
 
                                 
                                 
                                 
                                  function waitThreeSeconds() {
                                      var ms = 5000 + new Date().getTime();
                                      let a=0;
                                      while (new Date() < ms){
                                         a++
                                      }
                                      console.log("exicution happend actually times: " ,a)
                                      console.log("finished from async")
                                  }

                                  function clickHandler() {
                                      console.log('click event!');   
                                  }

                                  // listen for the click event
                                  document.getElementById("myButton").addEventListener('click', clickHandler);

                                  waitThreeSeconds();
                                  console.log('finished execution');           
                                  
                                  o/p:-
                                  exicution happend actually times:  9387821
                                  app.js:9 finished from async
                                  app.js:20 finished execution
                                  
                                  
 So if we cange the function waitThreeSeconds from sync blocking to asyc non blocking we should add any of the (
 API,Timers,HTTP Request and Events) we will first start with timers.
 
 
                             function waitThreeSeconds() {
                                setTimeout(function(){ console.log("Hello sleep"); }, 4000);
                            }

                            function clickHandler() {
                                console.log('click event!');   
                            }

                            // listen for the click event
                            document.getElementById("myButton").addEventListener('click', clickHandler);

                            waitThreeSeconds();
                            console.log('finished execution');
                            
                            o/p:
                            app.js:14 finished execution
                            app.js:3 Hello sleep
This is a example of async nonblocking code waitThreeSeconds get called first because its a timer and comes in (
 API,Timers,HTTP Request and Events) it goes to web api then callback queue and thats why  console.log('finished execution')
 got exicuted first and its a typical example of async nature of JSRE.
 
 
 Now what if we do sleep for 0 sec will it be sync or async
 
                                                       function waitThreeSeconds() {
                                                          setTimeout(function(){ console.log("that was not good"); }, 0);
                                                      }

                                                      function clickHandler() {
                                                          console.log('click event!');   
                                                      }

                                                      // listen for the click event
                                                      document.getElementById("myButton").addEventListener('click', clickHandler);

                                                      waitThreeSeconds();
                                                      console.log('finished execution');
                                                      
                                                      o/p:-finished execution
                                                           app.js:3 that was not good
 The main key is wether the code will take the web API route or exicution stack will take care of it.
 Since it is a timer and it comes under  (API,Timers,HTTP Request and Events) JSRE will pull this function from  exicution stack.
 And put in to web api route now it will waite till exicution stack got empty.
 
 For fun you try by replacing timer code with http request
                                               fetch('https://jsonplaceholder.typicode.com/todos/1')
                                            .then(response => response.json())
                                            .then(json => console.log(json))
 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
                                 
  
