## 1. ECMA Script: 
ECMAScript (/ˈɛkməskrɪpt/; ES) is a standard for scripting languages, including JavaScript, JScript, and ActionScript. It is also best 
known as a JavaScript standard intended to ensure the interoperability of web pages across different web browsers. It is standardized by Ecma 
International in the document ECMA-262.
	In the early days, for single websites developer needs to write code multiple times , for different browsers, so to avoid this , 
ECMA script in used.
	
	
## 2. JAVASCRIPT ENGINES:
Javascript code we write can not be understood by the computer.
So the javascript engine is the program that converts javascript code that developers write into machine code that allows computer
to perform specific task.
	
	
## 3. WHAT IS NODE JS:
Node js is open source, cross platform Javascript runtime environment.
	Open source - source code is publicly available for sharing and modification.
	cross platform- available on Mac, windows and Linux
	Javascript runtime environment - provides all the necessary components which allows to use javascript program outside the browser.
	
	

# ==================================================> MODULES <===================================================================================


## 4. MODULES IN NODE JS : 
it is an encapsulated and reusable chunk of code that has its own context.
In node js, each file is treated as a separate module.
	
Types : 	
	1. Local modules : Modules that we create in our application.
	2. Build in modules : Modules that node js ships with out of the box
	3. Third party modules : Modules written by other developers that we can use in our application.	
		

===================================================> LOCAL MODULES <=============================================================================
Before modules code is executed node js is wrapped it in IIFE to load module into another file we use require() function.
	Summary of MODULE SCOPE: 
		Each loaded module in node js is wrapped with an IIFE that provides private scoping of code.
		IIFE allows you to repeat variable or function names without any conflicts.
		
		
		
## . MODULE WRAPPER: 	
Every module in node js gets wrapped in IIFE before being loaded. 
IIFE helps keep top- level variables scoped to the module rather than the global object
The IIFE that wraps every module contains 5 parameters which are pretty important for the functioning of a module.
			
	
passing argument to IIFE: 
```jsx
(function(message){
	console.log(message);
})("hello")
```		
  o/p: hello
				
	
## Structure of MODULE WRAPPER: 
	
//these parameters are by default available in node IIFE function. 
```jsx	
(function(exports, require, module, __filename, __dirname){
	const superhero="superman";
	console.log(superhero);
})()
```
	
	
16
	
	
	
## . MODULE CACHING: 
e.g. 
super-hero.js
```jsx
	class SuperHero{
		constructor(name){
			this.name=name;
		}
		getName(){
			returnt this.name;
		}
				
		setName(name){
			this.name=name;
		}
	}
			
	module.exports=new SuperHero("Superman");
			
			
	NOW IN index.js
			 
	const superhero=require("./super-hero");
	console.log(superhero.getName());    // Superman    =>  this generates from superHero class  check exports function
	superhero.setName("Batman");
	console.log(superhero.getName());    // Batman
			
	const newSuperhero=require("./super-hero")
	console.log(newSuperhero.getName());      // Batman       => it still displays batman 
```
			
when we write require() two times for same file , it will cached only single time , second time it will not goes to that file 
			
			
if we want to change it then in super-hero.js when exporting export just class as SuperHero and not SuperHero("Superman") .
					note => no need to write new .
			
		i.e. =====>
		super-hero.js
```jsx			
	class SuperHero{
		constructor(name){
			this.name=name;
		}
		getName(){
			returnt this.name;
		}
		
		setName(name){
			this.name=name;
		}
	}
			
	module.exports=SuperHero;
	
	NOW IN index.js
			 
	const SuperHero=require("./super-hero");
	const s1=new SuperHero("Hello");    // Hello
	console.log(s1.getName());
	s1.setName("Hii")
	console.log(s1.getName());   // Hii
	const s2=new SuperHero("World")
	console.log(s2.getName());      // World           Here it change the name .
	
```			
			

16. ECMA Modules:
	 we can import modules without using require also, i.e. by using import .
	 we need to create files using mjs extension , not using js extension.
	 
	  e.g. 
	  	in math.mjs
	```jsx  	
	  	const add=(a,b)=>{
	  		return a+b;
	  	}
	  	
	  	const sub=(a,b)=>{
	  		return a-b;
	  	}
				
		export default{
			add, 
			sub,
		}
		
		
		
		in index.mjs
		
		import math from "./math.mjs"
		const {add, sub}=math;
		console.log(add(3,4));
		console.log(sub(5,1);
		
	```		

	
	
	NOTE :
		1. ES modules is the ECMAScript Standard for module.
		2. It was introduced with ES2015.
		3. Node 14 and above support ES modules.
		4. Instead of module.export, we use export keyword.
		5. The export an be default or named.
		6. If it is default export, we can assign any name while exporting.
		7. If it is named export, the import name must be same.
		
	SAME AS REACTJS 
	
	
	
NOTE: 
	node index.js command only compile code one time, if we made any changes in file then we need to again run our node application using 
node index.js command ,
    to avoid this we use watch ,
    	COMMAND: 	
    		node --watch index
    		
    		
    		
   
===================================================> BUILT-IN MODULES <===========================================================================
	
	
BUILT IN MODULES :
	Modules that node js ships with.
	They are also refered to as core modules.
	Import the module before you can use it.	

 Some important built-in modules are:
		1. path
		2. events 
		3. fs
		4. stream
		5. http
		
		

	
	
####. 1. PATH MODULE :
	path module provides utilities for working with file and directory path.
	

callback funcction: 
	Any function that passed as an argument to another function is called as callback function.
	Also a function which accepts a function or return another function is called as higher order function.
		e.g. 
```jsx
	 	function greet(name){                  //this is callback function
   		 console.log(`hello ${name}`)
		}

		function greetAkshay(greetFn){         // this is higher order function
  		  const name="Akshay";
  		  greetFn(name)
		}

		greetAkshay(greet)
```



Types of callback function :
		1. Synchronous 
		2. Asynchronous
			
		
1. Synchronous callback function:
		A callback which is executed immediately is called synchronous callback function.
		e.g. above greet function, sort, filter, map
		
		
2. Asynchronou callback function:
		A callback that is often used to continue or resume code execution after an asynchronous operation has completed.
		Callback used to delay the execution of a function until a perticular time or event has occurred. 
	e.g. click handler on some button , means the function is only invoked when someone click on the button.
		
		
		
		
####. 2. EVENTS MODULE: 
 	The events module allows us to work with events in Node.js.
 	An event is an action or occurence that has happened in our application that we can respond to.
 	Using the events module, we can dispatch our own custom events and respond to those custom events in a non-blocking manner.
 	
 	
 	e.g. 
 	 in index.js 
 	 
 	 const EventEmitter= require("events");
 	 const emitter=new EventEmitter();
 	 emitter.on("order-pizza", (h)=>{
 	 	console.log("Order received!! baking a pizza", h)
 	 })
	
	emitter.emit("order-pizza", "hello")
	
	
	
	
	
	Binary data:
		0's and 1's that computers can understand.
		
	Character sets:
		Predefined lists of characters represented by numbers.
		
	Character encoding:
		First it converts character to its ASCII code or UNICODE and then convert it into its binary code.
		
	Streams:
		e.g. Youtube, we dont wait for the entire video download, video will start playing when some of the data is downloaded.
		
		i.e. The contents arrive in chunks and you watch in chunks while the rest of the data arrives over time. 
		
		Process streams of data in chunks as they arrive instead of waiting for the entire data to be available before processing.
		
		
	Buffer:
		suppose in hall there is only 30 people seating arrangement, but remaining 70 out of 100 needs to wait, 
		So the area where people waits is nothing but the buffer.
		
		
		e.g.  streming a video online
			If your connection is fast enough, the speed of the stream will be fast enough to instantly fill up the buffer and send 
it out for processing.
			That will repeat till the stream is finished.
			If your connection is slow, after processing the first chunk of data that arrived, the video player will display a loading 
spinner which indicates it is waiting for more data to arrive.
			Once the buffer is filled up and data is processed, the video player shows the video.
			
			
	
####. 3. FS MODULE: (File System module)
	e.g . 
	 in file.text 
	 
	 	Hello
	 	
	 in index.js
	 const fs=require("fs")
	 const content=fs.readFileSync("./file.txt", "utf-8")
	 console.log(content);
	 
	 O/p: hello 
	 	Note: if we do not write utf-8 then it will display ascii code of characters.
	
	
	//below is synchronous
	fs.writeFileSync("./greet.txt", "hellow world")   // it will create greet.txt file if not exist and add hellow world in it
	
	fs.writeFile("./greet.txt", "Hii",(err)=>{               //asynchronous 
		if(err){
			console.log(err);
		}
		else{
			console.log("data changed successfully");
		}
	})
	
	
	note it will add Hii in greet.txt and remove Hellow world from greeet.txt file, to append file we use
	
	fs.writeFileSync("./greet.txt"," Hii",{flag:"a"} ...and then rest of the things)  // a in the sense of append
	
	//op it adds text i.e. Hellow world Hii
	
	
	
	
	
	
	##############fs using promise###################
	
	index.js
	
	const fs=require("fs/promises")
	fs.readFile("./greet.txt","utf-8")
	.then((data)=>console.log(data))
	.catch((error)=>console.log(error))


	note=> 
		it will gives us a proper output. 
		it is also ASYNCHRONOUS that means other task are executed before it.
		
		const fs=require("fs/promises")
		console.log("first")
		
		fs.readFile("./greet.txt","utf-8")
		.then((data)=>console.log(data))
		.catch((error)=>console.log(error))

		console.log("second")
		
		
		Output:
			first
			second
			Hello 3.Akshay
			
	
	
########3. STREAMS :
		e.g. Youtube, we dont wait for the entire video download, video will start playing when some of the data is downloaded.
		
		i.e. The contents arrive in chunks and you watch in chunks while the rest of the data arrives over time. 
		
		Process streams of data in chunks as they arrive instead of waiting for the entire data to be available before processing.
		
		
		
##### 4. PIPES:
	used for chaining. i.e. for copying data from one file to another file .
	
	in index.js
	
	const fs=require("fs")
	const readableStream=fs.createReadStream("./file.txt",{
		encoding:"utf-8",
		highWaterMark:2,
	})
	
	const writableStream=fs.createWriteStream("./file2.txt")
	readableStream.pipe(writeableStrem)
	
	
	
	NOTE: 
		it will copy all data inside readableStream to writableStream
		
		
		
		
########5. HTTP MODULE:
		in web server there is a communication between client and server, but what type of request send by client is can not understand 
by server and also what kind of response send to the server can not understand by client.
		The client sends an HTTP requests and the server responds with a HTTP response.





==============================================================================================================================================================================================================


1. CREATING SERVER IN NODE JS :

	e.g.
		const http = require("http");
		const server = http.createServer((req, res) => {
  		
		res.writeHead(200, { "Content-Type": "text/plain" });
		res.end("Hello world");
		});

		server.listen(3000, () => console.log("server up and running"));



2. DISPLAY HTML IN RESPONSE OF REQUEST:
		const http = require("http");
		const server = http.createServer((req, res) => {
  		
		res.writeHead(200, { "Content-Type": "text/html" });
		res.end("Hello world");
		});

		server.listen(3000, () => console.log("server up and running"));
	
	
3. DISPLAY OBJECT IN RESPONSE:
		const http = require("http");
		const server = http.createServer((req, res) => {
  		const obj = {
    			fname: "Akshay",
			lname: "Gawade",
  		};
		res.writeHead(200, { "Content-Type": "application/json" });
		res.end(JSON.stringify(obj));
		});

		server.listen(3000, () => console.log("server up and running"));	
		


4.DISPLAY ANOTHER HTML FILE IN NODE JS AS RESPONSE : 
	in index.html 
	
	<html>
		<body>
			<h3>Hello another file</h3>
			
		</body>
	</html>
	
	
	in index.js 
	
	const http=require("http");
	const fs=require("fs")
	const server=http.createServer((req, res)=>{
		res.writeHead(200,{"Content-Type":"application/json"})
		
		const html=fs.readFileSync("./index.html","utf-8");
		res.end(html)
		//instead of above two lines we will write this single line 
		
		fs.createReadStream(__dirname+"./index.html").pipe(res)
	})
	
	
	server.listen(3000,()=>console.log("server up and running"))
	
	
	
	
	
	
	
	
5. PASSING DATA FROM INDEX.JS TO INDEX.HTML
	in index.html
	
	<html>
		<body>
			<h1>Hello {{name}}, WElcome to our page</h1>
		</body>
	</html>
	
	in index.js
	
	const http=require("http");
	const fs=require("fs");
	
	const server=http.createServer((req, res)=>{
		const name="Akshay";
		res.writeHead(200, {"Content-Type":"text/html"})
		let html=fs.readFileSync("./index.html", "utf-8");
		html=html-replace("{{name}}", name);
		res.end(html)
	})

	server.listen(3000,()=>console.log("Server up and running"))
	
	
6 NODE ROUTING :
	const server=http.createServer((req, res)=>{
		if(req.url==="/"){
			res.writeHead(200, {"Content-Type":"text/plain"})
			res.end("Home page");
		}
		else if(req.url==="/about"){
			res.writeHead(200, {"Content-Type":"text/plain"})
			res.end("about page");
		}
		else{
			res.writeHead(400)
			res.end("Page not found");
		}
	})
	
	
	NOTE : 
		HERE ALSO WE HAVE req.method 



==============================================================================================================================================================================================================

libuv:
	libuv is a cross platform open source library written in C language.
	it handles asynchronous non-blocking oprations in node js by using Thread pool, Event loop
	
	in index.js 
	
		const crypto = require("crypto")
		const MAX_CALLS=5;
		const start=Date.now();
		for(let i=0;i<MAX_CALLS;i++){
			crypto.pbkdf2("password", "salt", 1000000, 512, "sha512", ()=>{
				console.log(`Hash: ${i+1}`, Date.now()-start)
			})
		}
		
		OUTPUT:
			Hash: 4 270
			Hash: 3 297
			Hash: 2 297
			Hash: 1 314
			Hash: 5 531
			
		NOTE : it takes about double time for 5th execution , so libuv has by default 4 threads.
			if we set 
			process.env.UV_THREADPOOL_SIZE=5;
			
			THEN 5TH THREAD WILL TAKE SAME TIME, ALSO WE CAN INCREASE THIS NUMBER .
			
			
			
		
		
		
USING HTTPS REQUEST:
	in index.js 
	
	const https=require("https");
	const MAX_CALLS=12;
	const start=Date.now();
	for(let i=0;i<MAX_CALLS;i++){
		https.request("https://www.google.com", (res)=>{
			res.on("data",()=>{});
			res.on("end",()=>{
				console.log(`Request ${i+1}`, Date.now()-start)
			})
		})
		.end()
	}
	
	
	OUTPUT : 
		 Request: 5 202
		 Request: 6 206
		 Request: 1 209
		 Request: 3 207
		 Request: 2 204
		 Request: 4 206
		 Request: 7 205
		 Request: 8 206
		 Request: 9 201
		 Request: 10 206
		 Request: 12 203
		 Request: 11 206
		 
		 
		THIS MEANS THAT  : 
			1. https.request is a network input/output operation and not a CPU bound operation 
			2. It does not use the thread pool.
			
			
	
CALL STACK : 
	function greeting(){
		//some code
		sayhi();
		//some code;
	}	
	function sayhi(){
		return "hello";
	}
	greeting();
	
	NOTE :
		first it will push greeting to the stack , and then it pushes sayhi function to the stack , after execution of sayhi, 
it will push sayhi to outside of the stack, all the variables inside sayhi function are destroyed, still greeting function is inside the stack,
again after complete execution of greeting , this also push greeting function outside the stack.
		
		this is called as call stack.
		
		
TASK QUEUE:
	1. Javascript can do one thing at a time.
	2. The rest are queued to the task queue waiting to be executed.
	3. When we run setTimeout, webapis will run a timer and push the function provided to setTimeout to the task queue once the timer ends.
	4. These tasks will be pushed to the stack where they can executed.
	


EVENT LOOP: 
	1. Javascript has a runtime model based on an event loop, which is responsible for executing code, collecting and processing events and
executing queued sub-tasks .
	2. The event loop pushes the task from the task queue to the call stack.
	3. setTimeout(func1, 0) can be used to defer (stop) a function until all the pending task have been executed.
	 
	 
	 
======================================><===============================================================
MICROTASK QUEUE: 
	console.log("first");
	process.nextTick(()=>console.log("this is process.nextTick 1"))
	console.log("second")
	
	O/P. : first	
	       second
	       this is process.nextTick 1
	       
	       
	 e.g. 2 
	 
	 Promise.resolve().then(()=>console.log("this is Promise.resole 1"))
	 process.nextTick(()=>console.log("this is process.nextTick 1 "))
	 
	 OP : this is process.nextTick 1
	      this is process.nextTick 1
	      
	      
	      NOTE : 
	      	ALL CALLBACKS IN nextTick queue are executed before callbacks in promise queue.
	      	
	    
	    
	  e.g. 3 
	        process.nextTick(()=>console.log("next tick 1"))
		process.nextTick(()=>console.log("next tick 2"))
		Promise.resolve().then(()=>console.log("promise 1"))
		Promise.resolve().then(()=>console.log("promise 2"))
		Promise.resolve().then(()=>{
		    console.log("promise 2")
		    process.nextTick(()=>console.log("next tick in promise 2"))
		})
		Promise.resolve().then(()=>console.log("promise 3"))
		
		
		O/P: 
			next tick 1
			next tick 2
			promise 1
			promise 2
			promise 2
			promise 3
			next tick in promise 2

	    
TIMER QUEUE: 
		setTimeout(()=>console.log("first timeout"),0)
		setTimeout(()=>console.log("second timeout"),0)
		process.nextTick(()=>console.log("next tick 1"))
		process.nextTick(()=>console.log("next tick 2"))
		Promise.resolve().then(()=>console.log("promise 1"))
		Promise.resolve().then(()=>console.log("promise 2"))
		Promise.resolve().then(()=>{
		    console.log("promise 2")
		    process.nextTick(()=>console.log("next tick in promise 2"))
		})
		Promise.resolve().then(()=>console.log("promise 3"))
		
		
		O/P: 
			next tick 1
			next tick 2
			promise 1
			promise 2
			promise 2
			promise 3
			next tick in promise 2
			first timeout 
			second timeout
			
			
	NOTE :
		IF WE PASS 0 IN setTimeout then this call back function will execute after all code executed.
		
		
		
	      	
IO QUEUE: 
	 Callbakcs in the microtask queue are executed before callback in the IO Queue.
	 
	 const fs=require("fs");

	 fs.readFile(__filename, ()=>{
	 	console.log("this is readfile 1")
	 })
	 
	 process.nextTick(()=>console.log("nextTick 1"))
	 Promise.resolve.then(()=>console.log("this is promise resolve 1"))
	 
	 
	 O/P: 
	 	nextTick 1
	 	this is promise resolve 1
	 	this is readfile 1




  ==============================================================================================================================================================================================================

WHAT IS NPM  : (node package manager)
	it is the worlds largest software library.
	it is the software package manager.
	
	npm is a library which contains code packages written by various developers. 
	

	 
WHAT IS package.json: 
	package.json is npm's configuration file.
	It is a json file that typically lives in the root directory of your package and holds various metadata releavant to the package.
	
	why we need package.json
		package.json is the central place to configure and describe how to interact with and run your package. 
		
	it is primarily used by npm CLI.
	
 	in dependencies of package.json we have all the packages which are installed in our project.
 	
 	
 
 PUBLISHING NODE PACKAGE: 
 	visit npmjs.com and click on sign up , after that go to your project directory, and type 
 		npm adduser __username__
 		
 		after that enter what terminal asks.
 		
 		
 		after that enter command : npm publish 
 		
 		then it will publish your application . 
 		
 		NOTE: 
 			for checking of published package, visit site: https://npmjs.com/package/package_name
 			
 			


CLI (COMMAND LINE INTERFACE) : BUILDING CLI:
	CLI stands for Command Line Interface. 
	A program that you can run from the terminal.
	
	e.g. npm and git
	
	
	=====above need to learn====



=====================================><==========================================================================================================


CLUSTER MODULE:
	we know that node is a single threaded application.
	No matter how many cores you have, node only uses single core of your CPU.
	This is fine for I/O operations but if the code has long running and CPU intensive operations, your application might struggle from a 
perfomance point of view.
	
	for avoid this issue node introduce cluster module.
	
	
	The cluster module enables the creation of child processes (also called workers) that run simultaneously.
	All created worker share the same worker port.	
 
 	e.g. WITHOUT cluster module .
 		suppose our applications have two routes , first route is taken 3 ms for fetching data and second route is taking 4 seconds for
fetching data , then if we again refreshh first route then first route also takes 4 to 5 secondds or fetching data , so to avoid this we use 
cluster model .
 		
 		e.g. without cluster module 
 			const http=require("http");
 			const {Worker}=require("worker_threads");
 			const server=http.createServer((req, res)=>{
 				if(req.url==="/"){
 					res.writeHead(200,{"Content-Type":"text/plain"})
 					res.end("Home page")
 				}
 				else if(req.url==="/slow-page"){
 					let j=0;
 					for(let i=0;i<200000;i++){
 						j++;
 					}
 					res.writeHead(200,{"Content-Type":"text/plain"})
 					res.end(`slow page ${j}`)
 					
 				}
 			})
 			server.listen(8000, ()=>console.log("server listen on port 8000"))
 		
 		
 		
 		
 		
 		e.g. with cluster 
 		
 		
 		const cluster=require("cluster");
 		if(cluster.isMaster){
 			console.log(`Master process ${process.pid} is running`);
 			cluster.fork();
 			cluster.fork();
 		}
 		else{
 			console.log(`Worker ${process.pid} started`);
 			const server=http.createServer((req, res)=>{
 				if(req.url==="/"){
 					res.writeHead(200, {"Content-Type":"text/plain"});
 					res.end("Home page");
 				}else if(req.url==="/slow-page"){
 					for(let i=0;i<1000000;i++){}
 					res.writeHead(200, {"Content-Type":"text/plailn"})
 					res.end("slow page")
 				}
 			})
 			
 			server.listen(8000, ()=>console.log("server up and running "))
 		}
 		
 		
 		
 		O/P: 
 			Master process 3242 is running
 			Worker 3244 started
 			Worker 3243 started
 			server up and running 
 			
 			
 			NOTE : HERE IT WILL NOT AFFECT ON / route as we use cluster.
 			
 		
 =============================================================================================================================================
 
 WORKER THREAD MODULE: 
 	The worker thread module enables the use of threads that execute the Javascript in parallel.
 	Code executed in worker thread runs in a seperate child process, preventing it from blocking your main application.
 	
 	
 	difference between cluster and worker module : 
 		The cluster module can be used to run multiple instances of node js that can distribute workloads.
 		worker thread module allows running multiple application threads within a single Node.js instance.
 		
 	
 	
 	e.g. 
 	
 		in index.js 
 			
 			const http=require("http");
 			const {Worker}=require("worker_threads");
 			const server=http.createServer((req, res)=>{
 				if(req.url==="/"){
 					res.writeHead(200,{"Content-Type":"text/plain"})
 					res.end("Home page")
 				}
 				else if(req.url==="/slow-page"){
 					const worker = new Worker("./worker-threads.js");
 					worker.on("message", (j)=>{                          //for getting message in index.js from worker-threads.js
 						res.writeHead(200,{"Content-Type":"text/plain"})
 						res.end(`slow page ${j}`)
 					})
 				}
 			})
 			server.listen(8000, ()=>console.log("server listen on port 8000"))
 			
 			
 			
 			in worker-threads.js
 			
 			const { parentPort }=require("worker-threads");
 			let j=0;
 			for(let i=0;i<200000;i++){
 				j++;
 			}
 			
 			parentPort.postMessage(j); 						
 		
	 
  
