---
title: 'Creating python module in Rust'
date: 2017-04-15
permalink: /posts/2016/04/Rust-Python/
tags:
  - Rust
  - Python
---

The objective of the blog post is to implement a python module using the state of art programming language Rust. The idea is to create an python module in Rust.

We will be using the rust-cpython project which makes it possible to execute Python code from Rust and vice-versa build a module in Rust for Python.

Python module
=============

In this section lets create a simple python function for example fibonacci sequence calculator. Follow the steps below to implement this code,

* Create a file named sample_fib.py and copy paste the content below. 

~~~~
#Define a function in python
def fib(n):
  
  #If input is less than 2 return one
  if n < 2:
    return 1
  
  #Assign the first two values of the series to be one
  prev1 = 1
  prev2 = 1
  
  #Between the values 1 to the final input
  for i in range(1, n):
  
    next = prev1 + prev2
    prev2 = prev1
    prev1 = next
    
  return prev1

#Execution starts here
if __name__ == '__main__':
  print fib(3)
~~~~

* To run the code,

~~~~
python sample_fib.py
~~~~

Rust Implementation
===================

Now lets implement the same python module in Rust and for this we would be using Rust-cpython library, which seamlessly allows the developer to build for Python 2 & 3 with few manipulation in the Cargo.toml file to download the crate.

* Create a new rust projects

~~~~
cargo new rust_python_fib
~~~~

We are creating a library in Rust here.

*  Edit the Cargo.toml file for downloading the cpython dependency.

~~~~
nano Cargo.toml
~~~~

The Cargo.toml should look something like this,

~~~~
[package]
name = "python-rust-example"
version = "0.1.0"
authors = ["Vigneshwer <daniele.esposti@gmail.com>"]

[lib]
name = "example"
crate-type = ["dylib"]

[dependencies.cpython]
git = "https://github.com/dgrunwald/rust-cpython.git"
default-features = false
features = ["python27-sys"]

~~~~

* Go to ./src/lib.rs and edit the lib.rs file with the code below,

~~~~
#[macro_use] extern crate cpython;

use cpython::{PyString, Python, PyResult};

// 
fn fibo(py: Python, n : u64) -> PyResult<u64> {
    if n < 2 {
        return Ok(1)
    }
    let mut prev1 = 1;
    let mut prev2 = 1;
    for _ in 1..n {
        let new = prev1 + prev2;
        prev2 = prev1;
        prev1 = new;
    }
    Ok(prev1) 
}

// To build a Python compatible module we need an intialiser which expose the public interface
py_module_initializer!(example, initexample, PyInit_example, |py, m| {
    // Expose our function fibo as `extern "C"`
    try!(m.add(py, "fibo", py_fn!(py, fibo(rand_int: u64))));

    // Initialiser s macro needs a Result<> as return value
    Ok(())
});

~~~~

* Compile the project

~~~~
 cargo build --release
~~~~

* Use the project in Python

~~~~
cp ./target/release/lib_project_name.so ./rust_function.so

import rust_function
print(rust_function.fibo(4))
~~~~

Conclusion
==========

Rust is great language to build python module and has sea of oppurtunities in terms of getting high performance. I am personally excited about building numpy functions in Rust and benchmark them.

**Ref:**

* [rust-cpython](https://github.com/dgrunwald/rust-cpython)
* [Python-rust binding](http://www.expobrain.net/2016/09/18/create-python-module-in-rust/)
* [Teaching Rust to python programmer](http://lucumr.pocoo.org/2015/5/27/rust-for-pythonistas/)
* [Python modules in Rust](http://ehiggs.github.io/2015/07/Python-Modules-In-Rust/)


