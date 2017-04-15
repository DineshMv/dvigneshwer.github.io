---
title: 'Binding python to Rust'
date: 2017-04-15
permalink: /posts/2016/04/Rust-Python/
tags:
  - Rust
  - Python
---

The objective of the blog post is to implement the current state of binding python to Rust. The idea is to see whether rust turns out to be a great replacement for C/C++ whenever we go ahead looking for performance in python.

Python module
=============

In this section lets create a simple python function, lets build a fibonacci sequence calculator. Follow the steps below to implement this code,

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
name = "rust_python_example"
version = "0.1.0"
authors = []

[lib]
name = "rust_python_example"
crate-type = ["dylib"]

[dependencies]
interpolate_idents = "*"

[dependencies.cpython]
version = "*"
default-features = false
features = ["python3-sys"]
~~~~

* Go to ./src/lib.rs and edit the lib.rs file with the code below,

~~~~
#![feature(plugin)]
#![plugin(interpolate_idents)]

#[macro_use] extern crate cpython;

use cpython::{PyResult, Python, PyTuple, PyErr, exc, ToPyObject, PythonObject};

mod fib {

pub fn fib(n : u64) -> u64 {
    if n < 2 {
        return 1
    }
    let mut prev1 = 1;
    let mut prev2 = 1;
    for _ in 1..n {
        let new = prev1 + prev2;
        prev2 = prev1;
        prev1 = new;
    }
    prev1 
}
}

py_module_initializer!(librust_python_example, |_py, m| {
    try!(m.add("__doc__", "Module documentation string"));
    try!(m.add("fib", py_fn!(fib)));
    Ok(())
});

fn fib<'p>(py: Python<'p>, args: &PyTuple<'p>, kwargs: Option<&PyDict<'p>>) -> PyResult<'p, u64> {
    let arg0 = match args.get_item(0).extract::<u64>() {
        Ok(x) => x,
        Err(_) => {
            let msg = "Fib takes a number greater than 0";
            let pyerr = PyErr::new_lazy_init(py.get_type::<exc::ValueError>(), Some(msg.to_py_object(py).into_object()));
            return Err(pyerr);
        }
    };
    Ok(fib::fib(arg0))
}
~~~~

TBC ..

Conclusion
==========

Rust is great language to build python module and has sea of oppurtunities in terms of getting high performance. I am personally excited about building numpy functions in Rust and benchmark them.

**Ref:**

* [Teaching Rust to python programmer](http://lucumr.pocoo.org/2015/5/27/rust-for-pythonistas/)
* [Python modules in Rust](http://ehiggs.github.io/2015/07/Python-Modules-In-Rust/)


