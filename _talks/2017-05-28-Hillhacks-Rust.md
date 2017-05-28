---
title: "Benchmarking Rust units"
collection: talks
type: "Talk"
permalink: /talks/2017-05-28-Rust-Hillhacks
venue: "Surya Homestay"
date: 2017-05-28
location: "Bir, India"
---

I was at hillhacks this year delivering a talk about [high performance computing in Rust](https://osem.hillhacks.in/conferences/hillhacks2017/program/proposals/94), it was a great great experience talking to a bunch of really cool hackers.

The while concept of hillhacks is to do innovative work in an informal way going against the odd. 

Highlights
==========

* Discussed all the topics of my [Rust presentation](https://dvigneshwer.github.io/files/Deep_drive_into_Rust_programming_language.pdf)
* Showcased bench mark experiment
* There were aroung 15 people in my session

Topics
======

The following topics were discussed

* Rust installation
* Rust type system
* Ownership and borrowing
* Showcased benchmarking experiment

Implementation
==============

* Create a new project:

~~~~
cargo new --bin bench_rust
~~~~

* To run benchmark feature in Rust, we require the nightly version

~~~~
rustup default nightly
~~~~

* Setup the dependencies by edting the Cargo.toml file:

~~~~
[package]
name = "bench_rust"
version = "0.1.0"
authors = ["Vigneshwer.D <dvigneshwer@gmail.com>"]

[dependencies]
rayon="*"
~~~~

* Copy and paste the following code in the src/main.rs file:

~~~~
//-- #########################
//-- Task: Benchmarking experiments
//-- Author: Vigneshwer.D
//-- Version: 1.0.0
//-- Date: 22 May 17
//-- #########################
// Importing external crates

#![feature(test)] 

extern crate test;
extern crate rayon;
use rayon::prelude::*;

// ordinary average function in Rust - Imperative style
pub fn ordavg(list: &[f64]) -> f64{
	let mut total = 0.;
	
	for el in list{
		total += *el
	}

	total/list.len() as f64
}	

// HLL version of the average function in Rust
pub fn hllavg(list: &[f64]) -> f64{

	list.iter().sum::<f64>() / list.len() as f64

}

// parallel version (Rayon)
pub fn rayavg(list:&[f64]) -> f64{

	list.par_iter().sum::<f64>() / list.len() as f64

}

// fold version - Reduce
pub fn foldavg(list: &[f64]) -> f64{

	list.iter().fold(0.,|a, b| a + b) / list.len() as f64

}

// Testing and benchmarking the functions
#[cfg(test)]
mod tests {
	use super::*; 
	use test::Bencher;

	#[test]
	fn check_results() {
		let rand_list = [1.0,1.0,1.0,1.0,1.0,1.0];
		assert_eq!(1.0, ordavg(&rand_list));
		assert_eq!(1.0, hllavg(&rand_list));
		assert_eq!(1.0, rayavg(&rand_list));
		assert_eq!(1.0, foldavg(&rand_list));
	}

	#[bench]
    fn bench_ordavg(b: &mut Bencher) {
        b.iter(|| {
        	let rand_list = [1.0,2.0,3.0,5.0,4.0,6.0];
        	ordavg(&rand_list)
        });
    }

    #[bench]
    fn bench_hllavg(b: &mut Bencher) {
        b.iter(|| {
        	let rand_list = [1.0,2.0,3.0,5.0,4.0,6.0];
        	hllavg(&rand_list)
        } );
    }

    #[bench]
    fn bench_rayavg(b: &mut Bencher) {
        b.iter(|| {
        	let rand_list = [1.0,2.0,3.0,5.0,4.0,6.0];
        	rayavg(&rand_list)
        });
    }

   	#[bench]
    fn bench_foldavg(b: &mut Bencher) {
        b.iter(|| {
        	let rand_list = [1.0,2.0,3.0,5.0,4.0,6.0];
        	foldavg(&rand_list)
        });
    }

}

// Main execution place
fn main() {
	let rand_list = [1.0,1.0,1.0,1.0,1.0,1.0];
	println!("{:?}", ordavg(&rand_list)); 
	println!("{:?}",hllavg(&rand_list));
	println!("{:?}", rayavg(&rand_list));
	println!("{:?}", foldavg(&rand_list));
}
~~~~

* To run benchmarks

~~~~
cargo bench
~~~~

* To run test cases

~~~~
cargo test
~~~~

* To execute the code:

~~~~
cargo run
~~~~

We should the following [output](https://github.com/MozillaIndia/RustIndia/blob/master/RainOfRust/Readme.md#output--1) on successfull execution of the code.
