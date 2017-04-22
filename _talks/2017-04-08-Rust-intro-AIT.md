---
title: "Rust: Making System Programming Great again"
collection: talks
type: "Talk"
permalink: /talks/2017-04-07-Rust-AIT
venue: "Army Institute of Technology"
date: 2017-04-07
location: "Pune, India"
---

MozHack AITpune event happened at AIT college, Pune and it is one of the early TS-MozillaReps coordinated MozActivate Rust event. I gave a 1 hour talk about Rust Lang and its features followed by Q&A. This talk was completely focussed on covering all the functional units of Rust so that participants feel confident enough to go ahead and build their rust applications.

If you are looking for some pitch points or use case of Rust jump to the conclusion session where I have tried to cover all the uber level Rust aspects according to industries use cases.

Highlights
==========

Delivered a remote session on Rust Language to the members of AIT Mozilla club.

* There were around 60+ participants
* Covered all the major aspects of the Rust language
* Shared all the details about how to get started with Rust Community
* Mentioned the active projects build using Rust

Key Takeaways for the participants:

* Introduction to a new state of art programming language
* Notes on getting started with Rust
* Code samples and information about Rust community
* Understanding of reallife use cases

Demystifying Rust @AIT
======================

Among all my live remote sessions, this was the largest one in terms of participation. Initially there was some connectivity problems but we some how managed to overcome the hurdles and went ahead with the talk. The pdf version of my slides are available at the Resources section below.

Since majority of the participants were students, I started off with explanation of the basic terminologies which are as follows,

* Low and high level language - In very simple terms low languages are machine level codes which tell the processor what to do and the HLL are human understandable and provides the user an abstract commands to implement their tasks

* System programming - It is the process of building the platforms over which application are developed for example the rendering engine of a web browser are developed in system programming language

* Stack and heap - All the variables and functionality that we implement in our code gets saved in the memory, where stack is used for static memory allocation and heap for dynamic memory allocation, both stored in the computer's RAM. The objects are usually stored in Heap during runtime and the variable get stored in the Stack at compile time.

* Compile time - The source code must be compiled into machine code in order to become and executable program. This compilation process is referred to as compile time.

* Run time - A compiled program can be opened and run by a user. When an application is running, it is called runtime.

* Concurrency & Parallelism - The below quote explains it all :) 

>> "Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once." - Rob Pike

* Type system - These are rules which define the functional units of computer program such as variables, functions etc

* Garbage collector - These are automatic memory management software which cleans up memory used by units of the code

* Mutability - The ability to change the value of an entity in Runtime

* Scope - It talks about the life time of a particular entity in the code whose memory location will be destructed after it is no longer used in the code

## Common System programming bugs

Rust type system and the concepts on which it is designed helps you to overcome almost all the common system programming bugs. Lets try to understand a few before we deep dive into Rust concpets. On a wider range we can say that most of the system programming bugs occurs due to wrong memory managements, if we are able to get that part right we can fix a class of concurrency and memory bugs.

### Segmentation Fault 

Segmentation fault is a specific kind of error caused by accessing memory that “does not belong to you". Below are few reasons by which you will end up getting a segfault,

Have illustrated few C++ examples to understand them better,

* Dereference a null pointer (null pointer is points to end of memory ie it is allocated any memory location)

~~~~
int *p = NULL;
*p = 1;
~~~~

* Writing to read only memory

~~~~
// Compiler marks the constant string as read-only
char *str = "Foo"; 

// Which means this is illegal and results in a segfault
*str = 'b'; 
~~~~

* Dangling pointer cases

~~~~
char *p = NULL;
{
    char c;
    p = &c;
}
// Now p is dangling
~~~~

The c variable is local, it means that it have been pushed on the stack after { and pop-ed out of it after }. The dangling pointer is just a reference to an offset which is now out of the stack.

### Buffer Overflow

A buffer overflow is basically when a section (or buffer) of memory is written outside of its intended bounds. If an attacker can manage to make this happen from outside of a program it can cause security problems.

~~~~
char a[4];

// write past end of buffer (buffer overflow)
strcpy(a,"a string longer than 4 characters"); 

// read past end of buffer (also not a good idea)
printf("%s\n",a[6]); 
~~~~

Before I jump into Rust concepts, let first answer the below questions,

### Why should you learn Rust?

>> Coding is an art exploration. You start from nothing and learn as you go.

Well to put this question in another way why should you learn a new programming language.

* Improve your toolkit - interdisciplinary coding knowledge is always gonna help you 
* Rust solves a lot of common system programming bugs
* Its the most loved programming language in the year 2016 - 17 acc to stackoverflow developer survey
* Self learning
* Help in decentarization and promote open innovation

Now lets get our hands dirty with Rust :) 

Killer Features of Rust
=======================

Rust in short words is a system programming language which offers no trade-off between control and safety. It is designed to deliver low-level control like in C/C++ and high-level constructs which enable safety features like in python/JS. 

Best things about Rust are,

* Strong type system
  * Reduces a lot of common bugs
  
This is where most of the developers complain about Rust, the type system of Rust is really unique. People do complain its explicit nature but later appreciate the fact these factors contribute a lot to write good code

* Borrowing and Ownership
  * Memory safety without garbage collection
  * Concurrency without data races

These concepts make sure that the memory at any point of time is not exploited and compliment deterministic destruction, where an entity and its associated resources are cleaned, when its no longer used or has an owner.

* Zero Cost abstraction

>> C++ implementations obey the zero-overhead principle: What you don’t use, you don’t pay for [Stroustrup, 1994]. And further: What you do use, you couldn’t hand code any better. – Stroustrup

Traits in Rust helps us to achieve this abstraction where we have unique implementations for different types. Traits basically 

We will cover these topics in detail in the below sections.

Installation of Rust
====================

Rust compiler is very easy to install,

For Ubuntu / MacOS users,

* Open your terminal (cntrl + Alt +T) and run,

~~~~
curl -sSf https://static.rust-lang.org/rustup.sh | sh
~~~~

This will install rustc and cargo for you. Cross check your installation by,

~~~~
rustc --version
cargo --version
~~~~

Rust compiler comes with Cargo. Cargo is the package manager tool for Rust and its simply amazing it takes care of the following:

* Creating a new project
* Compilation and running Rust projects
* Testing the new project
* Downloading and installing dependencies
* Version management of the dependecies
* Pushing to crates.io - its the Rust community repository of open Rust crates/libraries
* Benchmarking Rust units 
* & more ... the list goes on

Its one of the biggest selling point of Rust as its something very new in the system programming space and helps in going to production faster as it is designed according to the needs of the different processes involved in taking an application to solve real life problems.

For Windows,

* Go to https://win.rustup.rs/ .This will download rustup-init.exe
* Double click the executable and the start the installation

Type System
===========

* Sample hello world code

~~~~
fn main() {
    println!("Hello, world!");
}
~~~~

Every programming language must start with hello world script, its like a rule when you are introducing programming languages (this is very debatable topic), but I am just following the crowd here.

All the execution in Rust starts with the main function and here we use the **println!** macro to print the statement "hello world". Read more about [macros](https://doc.rust-lang.org/book/macros.html)

* Compiling and Running the code

~~~~
$ rustc main.rs
$ ./main
Hello, world!
~~~~

To compile and run the program, use the **rustc** compiler command line tool which has a lot of options.

* AVG Function

~~~~
fn avg(list: &[f64]) -> f64 {
    let mut total = 0;
    for el in list{
        total += *el
    }    
    total/list.len() as f64
}
~~~~

Let's deep dive into something more complex, here we have an average function (**fn** keyword denotes the function ) which takes in an array argument of float type and names it **list** , it also returns **f64** type.  

To create an variable in Rust we use the let keyword followed by the name of the entity for example:

~~~~
let rand_item = 10;
~~~~

This is the process of creating immutable variable, the value of the entity will not change through out its scope, but in the example above we have **total** variable which is suppose to be the cumulative sum of the iterations of the values of the array **list** when we run through each iterations in the for loop. 

The **&** symbol in the function argument defination is something to note down as it actually called **reference** we will cover more about this in the borrowing section, but in the avg function we only have the privilege of only dereferencing the values of the differnt elements of the array. 

Each type has various methods implemented for itself so here we the **list.len()** to find the total number of elements in the array and **as** help us with type casting of the result.

* HLL version

~~~~
fn avg(list: &[f64]) -> f64 {
    list.iter().sum::<f64>() / list.len() as f64
}
~~~~

* Parallel Version (Rayon)

~~~~
fn avg(list: &[f64]) -> f64 {
    list.par_iter().sum::<f64>() / list.len() as f64
}
~~~~

* Fold 

~~~~
fn avg(list: &[f64]) -> f64 {
    list.par_iter().fold(0., |a,b| a + b) / list.len() as f64
}
~~~~

**Primitive Types**

* bool

~~~~
let bool_val: bool = true;
println!("Bool value is {}", bool_val);
~~~~

* char

~~~~
let x_char: char = 'a';
 
// Printing the character
println!("x char is {}", x_char);
~~~~

* i8/i16/i32/i64/isize

~~~~
let num =10;
println!("Num is {}", num);

let age: i32 =40;
println!("Age is {}", age);
println!("Max i32 {}",i32::MAX);
println!("Max i32 {}",i32::MIN);
~~~~

* Tuples

~~~~
// Declaring a tuple
let rand_tuple = ("Mozilla Science Lab", 2016);
let rand_tuple2 : (&str, i8) = ("Viki",4);

// tuple operations
println!(" Name : {}", rand_tuple2.0);
println!(" Lucky no : {}", rand_tuple2.1);
~~~~

* Arrays

~~~~
let rand_array = [1,2,3]; // Defining an array 

println!("random array {:?}",rand_array );

println!("random array 1st element {}",rand_array[0] ); // indexing starts with 0

println!("random array length {}",rand_array.len() );

println!("random array {:?}",&rand_array[1..3] ); // last two elements
~~~~

* String

~~~~
let rand_string = "I love Mozilla "; // declaring a random string

println!("length of the string is {}",rand_string.len() ); // printing the length of the string

let (first,second) = rand_string.split_at(7); // Splits in string

let count = rand_string.chars().count();  // Count using iterator count
~~~~

**Complex Data Structures**

* struct

~~~~
// define your custom user datatype
struct Circle {
    x : f64,
    radius : f64,
}
~~~~

* Rust “Class”

~~~~
impl Circle {
    // pub makes this function public which makes it accessible outsite the scope {}
    pub fn get_x(&self) -> f64 {
    self.x
    }
}
~~~~

**Traits:**

* Interfaces
* Operator overloading
* Indicators of behaviour
* Bounds for generic
* Dynamic dispatch

~~~~
// create a functionality for the datatypes 
trait  HasArea {
    fn area(&self) -> f64;
}

// implement area for circle
impl HasArea for Circle {
    fn area(&self) -> f64 {
        3.14 * (self.r *self.r)
    }
}
~~~~

Ownership & Borrowing Concepts
==============================

**Ownership**

Example 1

~~~~
fn foo{
    let v = vec![1,2,3];
    let x = v;
    println!(“{:?}”,v); // ERROR : use of moved value: “v”
}
~~~~

Example 2

~~~~
fn print(v : Vec<u32>) {
    println!(“{:?}”, v);
}

fn make_vec() {
    let v = vec![1,2,3];
    print(v);
    print(v); // ERROR : use of moved value: “v” 
}
~~~~

**Borrowing**

If you have access to a value in Rust, you can lend out that access to the functions you call

**Types of Borrowing**

There is two type of borrowing in Rust, both the cases aliasing and mutation do not happen simultaneously

* Shared Borrowing (&T)
* Mutable Borrow (&mut T)

**Mutable Borrow**

~~~~
fn  add_one(v: &mut Vec<u32> ) {
    v.push(1)
}

fn foo() {
    let mut v = Vec![1,2,3];
    add_one(&mut v);
}
~~~~

**Rules of Borrowing**

* Mutable borrows are exclusive
* Cannot outlive the object being borrowed
* Cannot outlive the object being borrowed

~~~~
fn foo{
    let mut v = vec![1,2,3];
    let borrow1 = &v;
    let borrow2 = &v;
    add_one(&mut v): // ERROR : cannot borrow ‘v’ as mutuable because it is also borrowed as immutable
}                                
~~~~

**Lifetimes**

~~~~
let outer;
{
let v = 1;
outer = &v; 
// ERROR: ‘v’ doesn’t live long
}
println!(“{}”, outer);
~~~~

Getting started with Rust Communities 
=====================================

* Follow all the latest news & disussions about Rust features at [Reddit Rust Channel](https://www.reddit.com/r/rust/)

* Have doubts, post in [Rust users discourse](https://users.rust-lang.org) or ping in #rust IRC channel

People are really helpful, they will patiently help you with any kind of doubts

* Publish your crates at [crates.io](https://crates.io)

* Follow [@rustlang in twitter](https://twitter.com/rustlang)

Shout out your event and Rust activites, the team will love to know your updates

* Subscribe to [this week in Rust](https://this-week-in-rust.org/) newsletter

I always get some interesting reads from this corner

* Create your [rustaceans profile](https://github.com/nrc/rustaceans.org) and keep it updated with your Rust skills

Conclusion
==========

Rust as a programming language has a huge potential to be the core platform of many amazing futuristic projects across various domains and markets such as AI, IOT, Mobile Devices, Browser Engines etc where there is a lot of focus on optimized and safe usage of hardware capabilities to deliver high performant application which is production safe.

Properties of Rust help us think about few ideas,

* Deliering the same experience of the web in low cost hardware
* Compliments open innovation, most of the amazing crates available are open
* Reducing heat generated in mobile phones
* Reducing the battery consumption 
* Thinking about using GPU's & mutli processing for all common tasks safetly

For a person who is a product manager or business analyst these are the features that an Rust application delivers,

* Hack without fear - Can go to production fast
* Language which is supported by community and not dependant on a particular organisation - compliments decentralization
* Amazing community support channels
* deal for use cases where light overload and high control of hardware is required

On a personel note following Rust language paradigms has made me a better programmer and I do think a lot behind the scene hygeine of my code these days at my workplace, where I mostly code in Python. I just have one word for you **"Rust"**. 

>> Adopt Rust today :) 

Happy Rust Hacking !!! 

Resources
=========

* [Get the slides](/files/Deep_drive_into_Rust_programming_language.pdf)
* [Stack & Heap](http://net-informations.com/faq/net/stack-heap.htm)
* [Low & High level language](http://stackoverflow.com/questions/3468068/low-mid-high-level-language-whats-the-difference)
* [Segementation Fault](http://stackoverflow.com/questions/2346806/what-is-a-segmentation-fault)
* [Buffer Overflow](http://stackoverflow.com/questions/574159/what-is-a-buffer-overflow-and-how-do-i-cause-one)
* [Unraveling Rust Design](https://dvigneshwer.wordpress.com/2017/02/25/unraveling-rust-design/)
* [Zero Cost abstraction](https://blog.rust-lang.org/2015/05/11/traits.html)

