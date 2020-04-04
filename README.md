# JS_The_Weird_Parts

This my notes and I will keep updating this in future.

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
 
Conceptual Aside:-
Dynamically typed language:- the language in which variables can be assigned with out defining the type of the variable like int, float
.JS is Dynamically typed language where var a=1 and var a="arsalan" both are correct.


Primitive Data Type in JS:- 
1:-UNDEFINED
2:-NULL
3:-NUMBER
4:-STRING
5:-BOOLEAN
6:-SYMBOL


Operators are function in JS:-

  when you write 
                        let a=4+5;

 4+5 is a infix notation of expression for info +4 5 is prefix and 4 5+ is a post fix .
 since infix is more human readable infix expression gets converted in to a function call and that function returns the value and that 
 return value get assigned with a.
 
 For visualisation :-
 
     let a=4+5;
     let a=+(4,5)
     where + is function which do return a+b
 
 Operator presidence:-when there are different operators compiler have to pick which operation should I took first and so on.
 
 Every operator has its own precedence value higher the precedence value earlier it gets exicuted.
 Since every operator is a function call.The same happen in case of multiple operator case.
 
 let a=3+4*5
 
 Multiplication has more presidence than Add so 3+*(4,5) happen first
 *(4,5) will return 20
 3+20 again +(3,20) =====23
 
 Operator assiciativity:-
 How will the computer decide if there will same operator whom to pick first.
 There associativity comes
               
               a=1;b=2;c=4;

               a=b=c
               console.log(a)
               console.log(b)
               console.log(c)
               o/p:4,4,4
  Reason = has associativity from right to left.
  
  
  Type Coersion:- is same as internal type casting in jS.
  
                 0==false  //true
                 0==""      //true
                  1>2<3      //true  precidence of > is more than < . 1>2 false .false<3  .false coerse to 0. 0<3 thats true
                  1<2<2   //true      1<2 (true) coersed to 1 ,1<2(true) associativity of < is left to right.
                  
   The biggest asset to guess how things will coerse is Number() function .
              
              Number("")  //0
              
   Equality and Strict equality:=
    
   Equality(==)
                       
                       ""==false   //true     
                       // "" coerse to  0 and same goes with false which is not a string but a boolean value
   
   JS gives us Strict Equality(===) which do not coerse any thing but compare with out doing any type casting.
   
   Link will tell you the sameness chart with different operator.
   
   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness
  
 the auther says that coersion is not always bad and buggy but some time it helps you .
 
              
              var a 
              //do some web operation and return to a
              if(a){
              do some thing
              }
                                 
  here if a is not null or undefine then do some thing will happen but if result return zero it will coerse to zero and condition become false 
            
              if(a || a===0){
              }
              
here a===0 will give true and anything || true is true so do some thing will run even web operation will return 0 also.


Setting default value :-


                 function greet(name){
                      name=name|| "  but you havent passed your name as argument"
                      console.log("hellow " +name)
                  }
                  greet("arsalan")
                  greet()
                  
                  o/p:-hellow arsalan
                       hellow   but you havent passed your name as argument
    
  So here we are not using ES6 function greet(name="default") but we are using || operator.
  || function will return the first argument which is true in nature

                        undefined || 1   //1
                        undefined || "hiii"   //"hii"
                        null || 100        //100
                        ""||"helllow"       //hellow
                        
  We are using the same logic that if user is not passing any thing at creation time compiler will assign local argument variable with
  undefine and when you dont give any argument and directly try to  exicute it JS exicute it with undefine.
  But undefined coerse to false or 0 so we are using that logic to initialise it.
  
  
  What happen when we add different liberaries or .JS file in our html page.
  
                                   <body>
                                      <h1 style="text-align: center">Project 0001</h1> 
                                      <button id="myButton">Call back</button> 

                                      <script src="./lib1.js"></script>
                                      <script src="./lib2.js"></script>
                                      <script src="./app.js"></script>
                                    </body>
                                    </html>
                                    
   so codes from lib1.js and lib2.js and app.js actually sits there and make a chunk of code .
   If I am defining variable var lib="arsalan" in lib1.js and same variable var lib ="some other developer" is assigned by some developer in lib2.js then my var lib="arsalan" get ovverride by var lib="some other developer" .
   
   Solution:-  we should assign global variable like
   
                    windows.lib=windows.log || "arsalan"
                                 
                      so if variable is already defined in some file globally dont override it .if not assigned with string "arsalan"
                      
                      
                      
 ////////////////////////SECTION  Object And Function//////////////////////////////////
 
 object can contain 2 things 
 1:-property(primitive or other object)
 2:-methods(methods are functions tied with object)
 
 object can be accessed in 2 ways:-
 1:-Computed member access operator (property accessor)
 2:-Dot operator (.)
 
 1:-Computed member access operator (property accessor):-
      
        var myObject={
                name:"arsalan",
                work:"explorer"
            }
            //computed member access operator(property accessor)

            console.log(myObject[name])  //undefined
            console.log(myObject["name"]) // arsalan      
      
   this operator basically looks for property name given as a string in [] of object .
   Why it is giving 
   
    console.log(myObject[name])  //undefined
    
  because it looks for variable "name" and that got initialise with undefine at creation time.
  now it is looking for undefined property in object(at exicution time) now that undefined property is assigned with value undefined (again at creation time).
  so it gives undefine.(thats a fuck I know see this)
  
  
                        var myObject={
                            name:"arsalan",
                            work:"explorer",
                            city:"varanasi",
                            undefined:"this is weird"
                        }
                    //computed member access operator(property accessor)
                    var cityPlaceHolder="city"

                    console.log(myObject[cityPlaceHolder])   //varanasi
                    console.log(myObject["name"])             //arsalan
                    console.log(myObject[name])                 //this is weird
                    console.log(myObject["randomVariableName"])     //undefined
                    console.log(myObject[name])                     //this is weired
                    console.log(myObject[randomVariableName])        //this will give error because JS will not assigne undefine to                           randomVariableName here because object keys will always be unique since it is a hash map..
                    
    
 2:-Dot Operator:-
 
        var myObject=new Object()
        myObject.name="userName"
        console.log(myObject.name) //userNAme
        myObject.skills=new Object()
        myObject.skills.programming="Good" // Good
        console.log(myObject.skills.programming)
        myObject.address.city="varanasi" //Uncaught TypeError: Cannot set property 'city' of undefined
Here we need to first create address key inside myobject then only we can create city key inside adress

Object Literals:-

When JS compiler reads {} and they are not part of block (if esle for or function) it creates a object.
  
              var Arsalan={
                        firstName:"Arsalan",
                        lastName:"Adeeb"
                          }
                          console.log(typeof(Arsalan))   //object
                          console.log(typeof(Arsalan)==="object")  //true
                          console.log(Arsalan)  
            
 The best part of object literals is you can create it on the fly like   greet({firstName:"Shahrukh",lastName:"Khan"})
   
                        function greet(object){
                    console.log("Hellow Mr "+ object.firstName+object.lastName)
                    }


                    greet(Arsalan)
                    greet({firstName:"Shahrukh",lastName:"Khan"})

  
                                 
 JSON and Object Literals:-
 
 JSON is a subset of JS object Literals .
 Object Literal can have keys both as string or value but json have a strict protocol that keys can only be strings.
 
 Global object window have a class JSON just type JSON there .
 That JSON class contain 2 method stringify() and parse() only.
                  var order={
                              "fruit": "Apple",
                              "size": "Large",
                              "color": "Red",
                              adrress:{
                                  Adress1:"111 bakers street",
                                  city:"Bareilly"
                              }
                          }
                          var orderString=JSON.stringify(order)
                          console.log(orderString)
                          console.log(JSON.parse(orderString))
                          
                          
                          
Functions:-


First Order Function :-Just like JS object and primitive JS functions are also a block of memory.
You can Imagine  a function like block in memory like below.

Function
   ----------------
   |    Name      |
   ----------------
   |      Code    |
   ----------------
   |   argument   |
   ----------------
   |     caller   |
   ----------------
   |  call apply  |
   ----------------                              
  Note:-Function instances inherit methods from Function.prototype.      
  
  The code section contains code which is invokable.
  
                  function add (a,b){

                if(arguments.length){  //here argument is coming from prototype
                    return a+b
                }
                else{
                    console.log("plaese pass args")

                }
                }


                console.log(add(1,2))  
                add() 
 same code wit es6 rest operator
                 function add (...args){
                    console.log(arguments.length)
                 if(arguments.length){
                     return args[0]+args[1]
                 }
                 else{
                     console.log("plaese pass args")

                 }
                 }


                 console.log(add(1,2))
                 add() 
             
Function is a object or a box in a memory function name is a special box in function box that contains its name .
function add(a,b){} here add is a refrence that points to add box we can achive it explicitly also by making anonimous function and take refrence or function object in that


                      var anonimousGreet =function  (a,b){
                          console.log(arguments)
                          console.log("Hellow from anynomous")
                      }
                      anonimousGreet(2,3)
                      
  Here anonimousGreet is a variable points to function since it is dynamically typed language we can have it var other wise it would have been a pointer to function type variable.

                      var anonimousGreet =function add(a,b){
                          console.log(arguments)
                          console.log("Hellow from anynomous")
                      }


                      anonimousGreet(2,3)
                      
add() will give error here why because ........add is no longer pointing the code   anonimousGreet overrides add.
() will exicutes the code part of the code.

How functions can also be passed as an argument like primitive and objectLiterals(on the fly)

                        var exicute=function (a){
                        a()
                        }


                        exicute(function(){console.log("annonimous got exicuted")})
                        
                        
 Concept of pass by value and pass by refrence and mutation
 
 for premitive assignment operator actually create a new memory and populate it with the value of rhs refrence value
 but for object and function this is not the case only reference got created .
 
                        var a =2
                        var b=a
                        b++
                        console.log(a,b)   //o/p = 2,3

                        var greet={
                            word:"Hellow"
                        }
                        var greetIndia=greet

                        greetIndia.word="Namaste"

                        console.log(greet,greetIndia) //o/p {word: "Namaste"} {word: "Namaste"}
                      

The concept of 'this'


                                                        var count =0
                                                        let c={
                                                            name:"the c object",
                                                            log:function(){
                                                                console.log(count)
                                                                count++
                                                                if(count<100){
                                                                    this.log()
                                                                }
                                                            }
                                                        }
                                                        c.log()

                                                        var myFunction =function(){
                                                            console.log(this)
                                                            this.username="Arsalan"
                                                        }
                                                        myFunction()
                                                        console.log(username)


                                                        var count =0
                                                        let c={
                                                            name:"the c object",
                                                            log:function(){
                                                                console.log(count)
                                                                count++
                                                                    this.log()
                                                            }
                                                        }
                                                        c.log()
                                                        
                                                        
               let myFunction= {
                          name:"arsalan",
                          method:function(){
                              this.name="Adeeb"

                          }

              }
              console.log(myFunction.name) //"arsalan"
              myFunction.method()
              console.log(myFunction.name) //"Adeeb"

Interesting example

                  let myFunction= {
                              name:"arsalan",
                              method:function(){

                                  let newMethod=function(value){
                                      this.name=value
                                  }
                                  newMethod("Arsalan Adeeb")
                              }

                  }
                  console.log(myFunction.name)
                  myFunction.method()
                  console.log(myFunction.name)
                  
     
     Very very Confused with these need to do more work.
     
              let myFunction= {
                          name:"arsalan",
                          method:function(){

                              let newMethod=function(value){
                                  this.name=value  //why the context is global
                                  console.log(this)
                              }
                              newMethod("Arsalan Adeeb")
                              console.log(this)
                          }

              }
              console.log(myFunction.name)
              myFunction.method()
              console.log(myFunction.name)
              console.log(myFunction.method)
              
              
              
Array is a collection of anything:-


                      var array=[
                          1,
                          true,
                          "Arsalan",
                          function (name){
                              console.log("Hellow my friend "+name)
                          }
                      ]


                      array[3](array[2])


 Spread operator:-
                        var myFunction =function(name,isStudent,amount,...others){
                        console.log("explictArgs",name,isStudent,amount)
                        console.log("spread",others)
                        }

                        myFunction("Arsalan",true,2500,"Varanasi","Up")
                        
 You can achive the same with argument array also.
 
 
 Automatic Semicolon Insertion:-
 "Enter" buttons put a invisible character in the code Syntax parser decides what to do when see Enter Character in the code.
 
 
                      function obj(){
                      
                          return                     //Automatic syntax injection after return on seeing invisible enterChar\|/
                           {
                              firstname:"arsalan"
                          }
                      }

                      console.log(obj())   //o/p:-Undefined
                                 
                                 
Immidiately Invoked Function Expression(IIFE):-

                                    //function statement

                                    function print(){
                                        console.log("printing")
                                    }
                                    //function expression

                                    var ePrint=function (name){
                                    console.log(name)
                                    }

                                    //IIFE

                                    var iife=function (name){
                                    console.log(name)
                                    return "return"+name
                                    }("IIFE");

                                    console.log(iife)

                                    //IIFE without any refernce to return object
                                    (function (name){
                                        console.log(name)
                                        return "return"+name
                                        }("AIIFE"));

                                    //O/p
                                    // IIFE
                                    // app.js
                                    // app.js
                                    

CLOSURES:-
Since functions are objects it can be returned from a function or can be passed as a argument in other function.

Function returning function

                function one(){
                    return function (){
                        console.log("function returning function")
                    }
                }

                one()()
                
 passing function as a argument.
 
                 var argFun =function (){
                    console.log("function as a argument")
                }


                function exicuter (args){
                    args()
                }

                exicuter(argFun)
                
  Closures Example:-
  
                function closure (args){
                  let myVAr=args   //In closures this called free variable
                  return function (cArgs){
                   console.log(args,cArgs)
                  }
               }

               let retFun=closure("hellow")
               //In exicution context will remove after closure() exicution but not everything got wiped out 
               //myVAr=args will be there even after the exicution of closure()
               retFun("Closure")

               //o/p :- hellow Closure

One Example to understand the whole game


                      function funGenerator(){
                          var arr=[]

                          for (var i=0;i<3;i++){
                              arr.push(function(){
                                  console.log(i)
                              })
                          }
                          return arr
                      }

                      var functionArray=funGenerator()
                      functionArray[0]()
                      functionArray[1]()
                      functionArray[2]()

                      //o/p  3,3,3
                      
 var provides block level scope so after funGenerator() exicution context got poped out but except i because it is a free variable (used in closure function) since the scope of i is at block level so after 2 increment i become 2 and one i++ before coming out so i =3 and all internal function are pointing to i which is after exicution of funGenerator is 3 .
 This problem can be fixed by replacing var to let since let is having block level scoping even at function and if level.
 
 One more possible solution is to create a context for each function using IIFE.
 
                               function funGenerator(){
                                  var arr=[]

                                  for (var i=0;i<3;i++){
                                      arr.push((function(j){
                                          console.log(j)
                                      })(i))
                                  }
                                  return arr
                              }

                              var functionArray=funGenerator()
                              functionArray[0]()
                              functionArray[1]()
                              functionArray[2]()

                              //o/p  0,1,2

  TakeAway:-IIFE  can be used to create scopes .
  
  Using Closures to create function factory.
  
                                                            function functionGenerator(operator){
                                                          return function(a,b){
                                                              if(operator==="+"){
                                                                  return a+b
                                                              }
                                                              if(operator==="-"){
                                                                  return a-b
                                                              }
                                                              if(operator==="*"){
                                                                  return a*b
                                                              }

                                                          }
                                                          }

                                                          var add=functionGenerator("+")
                                                          console.log(add(2,3))
                                                          
  Difference between callback and closures.
                                 
  Callback defination :-
                              \|/
            function name(functionExpression){
            work;
            work;
            functionExpression()
            }
            
   A function you have given to another function as args to exicute after some code.
   
   Example:-
   
                                  function print(){
                                      console.log("Hellow Call Back")
                                  }


                                  setTimeout(print,3000)
                                 
Remember call back should always be passed as a refrence do not exicute there unless it is necessary.


                      function print(){
                        console.log("Hellow Call Back")
                    }


                    setTimeout(print,3000)
  or in case of closure
                      function print(){
                       return function(){
                           console.log("there from closure")
                       }
                    }


                    setTimeout(print(),3000)
                                 
  Inheritence in JS:-
  
 Every Single object in js can use other objects methods and property .
 
                      //for demo only never ever use this in your code.
                              var person ={
                                  firstName:"Default",
                                  lastName:"Default",
                                  getDetail:function(){
                                      console.log(this.firstName,this.lastName)
                                  }
                              }   

                              var arsalan={
                                  firstName:"Arsalan",

                              }

                              var adeeb={
                                  firstName:"ad",
                                  lastName:"eeb"
                              }
                              arsalan.__proto__=person
                              adeeb.__proto__=arsalan

                              adeeb.getDetail()
                              o/p:-ad eeb
 Here adeeb is taking prototype of arsalan and arsalan is taking from person .Ultimatly this property should never be used in practice 
 
 
 New keyword /constructore function/prototype property:-
 
                        //class structure designing with this pointing to local context
                            function Student (firstName,lastName,roll){
                            this.firstName=firstName;
                            this.lastName=lastName;
                            this.roll=roll;
                            this.getFullName=function(){
                                console.log(this.firstName,this.lastName)
                            }
                            }

                        //creating object by running function in constructor mode (If you dont put new function got invoked ret undef)
                            var Arsalan= new Student("Arsalan","Adeeb",101)
                        //adding proerty or methos even after creation of cunstructor function
                            Student.prototype.getRollNo=function(){
                                console.log(this.roll)
                            }
                            
                        //properties added in cunstructor function will reflect in all of its instance
                            Arsalan.getRollNo()
                            console.log(Arsalan)
                         //even object literal can also acces to newly added property in prototype(Not recommended)
                            let yash={
                                firstName:"Yash",
                                lastName:"Pandey",
                            }

                            yeshi.__proto__=Arsalan

                            yeshi.getFullName() 
 
 There is two problem with creation of object with constructor function 
 1:-if user didnt assign anything during creation time undefined get assigned instead of default value (ofcourse it can be fixed)
 
                                  function Student (firstName,lastName,roll){
                                  this.firstName=firstName;
                                  this.lastName=lastName;
                                  this.roll=roll;
                                  this.getFullName=function(){
                                      console.log(this.firstName,this.lastName)
                                  }
                                  }


                                  var Arsalan= new Student()

                                  Student.prototype.getRollNo=function(){
                                      console.log(this.roll)
                                  }
                                  Arsalan.getRollNo()

2:-cunstructor mode function can also be written in invokable syntax  Student() which will return undefined might create a problem.


There are two problem in creating object with object literals 
1:-When you create a object var a={} its dunder proto .__proto__ points to Object object so basically it inherits only root level logics methods loke hasOwnProperty and valueOf etc
2:-Remember this prototype chaining is very slow and have performance issue.

                        let a ={}
                        let b={
                        name:"kalia",
                        getName:function(){
                        console.log(this.name)
                        }
                        }
                        a.__proto__=b
                        console.log(a.name)  //kalia
                        
  Extra Reminder point :-if I do   a.__proto__.name="bale" that will be reflected to b also because refrence sharing.
  
  The 100% proper inheritence way of creating object is 
  
                  var student={
                    name:"Default",
                    class:"Default",
                    getDetail:function(){
                        console.log(`Name${this.name} and calss ${this.class}`)
                    }
                }

                var arsalan=Object.create(student)
                console.log(arsalan)  //{}
                arsalan.getDetail()   //NameDefault and calss Default here these values are coming from prototype
 
 1:-get default value without assigning.
 2:-no need of manual dunder proto assignment
 3:-Not all browser support this.
 A polyfill is a piece of code (usually JavaScript on the Web) used to provide modern functionality on older browsers that do not natively support it.
 
 
 
 The instanceof operator tests whether the prototype property of a constructor appears anywhere in the prototype chain of an object.
                   function Car(make, model, year) {
                    this.make = make;
                    this.model = model;
                    this.year = year;
                  }
                  const auto = new Car('Honda', 'Accord', 1998);

                  console.log(auto instanceof Car);
                  // expected output: true

                  console.log(auto instanceof Object);
                  // expected output: true
 since it checks for prototype object in prototype chain so it will not literal obtects and and create .
 
 
 

  
  
