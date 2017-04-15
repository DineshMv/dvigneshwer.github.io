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

For Windows,

* Go to https://win.rustup.rs/ .This will download rustup-init.exe
* Double click the executable and the start the installation

Type System
===========


Ownership & Borrowing Concepts
==============================



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

