# Pumping up python modules using Rust 

Lightning talk on how one can speed up their Python modules/lib/frameworks using Rust at Pycon Indonesia 2017.

This repository consists of all the code, instruction to execute the project & other reading materials used for curating the talk. 

## Running Projects

python to Rust
==============

Calling Rust operations from Python

~~~~
cd python-to-rust

sudo apt-get update
sudo apt-get -y upgrade

make -f Makefile
~~~~

python-rust-library
===================

Writing a Python module in Rust

~~~~
cd python-rust-library

sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get install python-pip python-dev build-essential

make -f Makefile
~~~~

Fibonacci Benchmarking Exp
==========================

~~~~
cd rust_python_fib
cargo build --release
cp ./target/release/libexample.so ./example.so

python
>>import example
>>print(example.fibo(4)

python bench_python.py

sudo pip install pytest-benchmark
pytest bench_python.py
~~~~

Counting Pairs Exp
===================

Refer to this [repo](https://github.com/rochacbruno/rust-python-example)

## Reading & Resource List 

Rust-Python FFi 
===============

* Rust-Python FFI blogs:
	* https://developers.redhat.com/blog/2017/11/16/speed-python-using-rust/
	* https://dvigneshwer.github.io/posts/2016/04/Rust-Python/
	* https://bheisler.github.io/post/calling-rust-in-python/

* Talks: 
	* https://www.youtube.com/watch?v=3CwJ0MH-4MA
	* https://www.youtube.com/watch?v=-ylbuEzkG4M

* Libraries/Crates:
	* https://github.com/mitsuhiko/snaek
	* https://github.com/PyO3/pyo3
	* https://pypi.python.org/pypi/setuptools-rust
	* https://github.com/mckaymatt/cookiecutter-pypackage-rust-cross-platform-publish
	* http://jakegoulding.com/rust-ffi-omnibus/
	* https://github.com/urschrei/polylabel-rs/blob/master/src/ffi.rs
	* https://github.com/saethlin/rust-lather

General Python list
====================

* Regex
	* https://regexone.com/lesson/letters_and_digits
	* https://regexone.com/references/python

* map zip lambda
	* https://bradmontgomery.net/blog/pythons-zip-map-and-lambda/

* GIL
	* https://stackoverflow.com/questions/1294382/what-is-a-global-interpreter-lock-gil
	* https://wiki.python.org/moin/GlobalInterpreterLock


## Setting up Rust compiler & projects

Follow the instruction below:  

### Step 1. Installation of Rust compiler:

MacOS/ Ubuntu (Debian based OS)
===============================

1. Open the terminal (Ctrl + Alt + T)
2. Make sure you have internet connection 
3. Type or copy paste the following command 

~~~~
curl https://sh.rustup.rs -sSf | sh
~~~~

4. Press 1 which is the default installation
5. To check if rust is installed properly or not type the following command rustc --version 
6. Try also cargo --version 


Windows Os
==========

1. Go to https://win.rustup.rs/ 
This will download rustup-init.exe
2. Double click and start the installation
3. Follow from step 4 of the installation instruction of Debian distribution instruction set

### Step 2. Clone the project content

If you have git installed in your system, fire your terminal and clone the repo with this following command:

~~~~
git clone https://github.com/vigneshwerd/DevfestYangon.git
~~~~

else you can download the zip version of the project

### Step 3. Installing necessary tools: 

* rustup features:

~~~~
rustup update stable
rustup self update
rustup install nightly
rustup run nightly rustc --version
rustup default nightly
rustup update
~~~~

* rustfmy installation:

~~~~
rustup install nightly
cargo new --bin sample_rust_project
cd sample_rust_project
cargo install rustfmt-nightly

// Magic
cargo fmt
~~~~

* rust-clippy tool

~~~~
rustup default nightly

// changes in cargo.toml

[dependencies]
clippy = {version = "*", optional = true}
[features]
default = []

cargo install clippy

// main.rs or code

#![feature(plugin)]
#![plugin(clippy)]

#![cfg_attr(feature="clippy", feature(plugin))]
#![cfg_attr(feature="clippy", plugin(clippy))]

~~~~

### Step 4. Running the examples:

To run standalone rust scripts:

~~~~
rustc -A warnings code_script_name.rs
~~~~

To run Cargo projects:

~~~~
cd /path_to_repo/cargo_projects/
cargo run
~~~~

FAQ's:
======

1. Why are macros useful?

	Macro is a useful way to avoid repeating code.
	Macros allow you to define special syntax for a specific purpose.

2. What's this some(T)?

	None and Some are the variants of the enum, that is, a value with type Option<T> can either be a None, or it can be a Some containing a value of type T.

3. What's the difference between &str and &'static str? 

	String is the dynamic heap string type, like Vec: use it when you need to own or modify your string data.

	str is an immutable1 sequence of UTF-8 bytes of dynamic length somewhere in memory. 

	A &str is made up of two components: a pointer to some bytes, and a length, this reference is normally called a 'string slice'

	Making a string literal which has type: &'static str, where 'static lifetime is the longest possible lifetime, and lasts for the lifetime of the running program. 

4. What is varible shadowing?

	when the first variable is shadowed by the second, which means that the second variable’s value is what we’ll see when we use the variable. 

5. How is a closure different from a function?
	
	You can create the closure in one place, and then call the closure to evaluate it in a different context. Unlike functions, closures are able to capture values from the scope in which they are called. 

6. Difference between static & const?

	They’re similar to constants, but static items aren’t inlined upon use. This means that there is only one instance for each value, and it’s at a fixed location in memory.

7. What is a hashmap?

	In computing, a hash table (hash map) is a data structure which implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

8. Inheritance in Rust?

	Rust does not have multiple inheritance, or even inheritance. However, it does have traits. If the people who implemented structs A and B were considerate enough to describe their interfaces with traits TraitA and TraitB, then you can describe the isomorphism each way with impl TraitA for B and impl TraitB for A, then any variable of type A or type B can be treated as implementing both TraitA and TraitB.


Rust References:
================

* [Rust by example](https://rustbyexample.com)
* [FAQ's](https://www.rust-lang.org/en-US/faq.html)
* [Rust official book](https://doc.rust-lang.org/book/second-edition/)
* [Online Rust playground](https://play.rust-lang.org/)
* [Awesome crates for different verticals](https://github.com/rust-unofficial/awesome-rust#gui)
* [Constructor in Rust](http://words.steveklabnik.com/structure-literals-vs-constructors-in-rust)

Stuck anywhere? 
===============

Feel free to raise an ticket in the issue section of the repository 
