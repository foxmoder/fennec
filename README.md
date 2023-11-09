# Fennec
A tiny JCVM language for effortless Java Card programming.

## What is Fennec?

Fennec is a tiny, opinionated language targetting the Java Card Virtual Machine with the primary goal of getting out of your way and allowing you to test and iterate quickly.

### Easy interfacing

Java Card works at the APDU level, meaning Java Card programs work directly with an IO buffer, often adding unnecessary boilerplate and room for programmer error. 

Fennec instead allows the programmer to write functions for each ISO 7816 instruction as they would in a systems language, using [protocol buffers](https://protobuf.dev/) within the command and response APDUs' data fields for serialization. This ensures that data passed to the card is interpreted correctly in a manner transparent to the user.

### Better typing

Java Card provides fairly barebones support for ...


### First-class cryptography support

...

## Why's it called that?

Fennecs are tiny foxes. I like foxes.

## Why write it in Rust?

Rust is great for writing little compilers like this, especially when using the parser combinator framework [nom](https://github.com/rust-bakery/nom). I wanted to try Zig for this, especially since I've been trying to pick it up more recently, but I figured Rust would be a bit more stable in the short term and also would allow other devs to help easier.

## Why not write it in Python then?

I totally could have. I just didn't want to. I'll use the excuse that Rust will be faster for longer programs, and also something something better typing for large projects etc.

## Why compile directly to the JCVM and not to Java Card?

For one, the Java Card toolchain is somewhat annoying to install--I wanted the user experience to be slick. From a compiler design perspective, this also gives me a bit more expressivity, especially when trying to enforce constant time execution for functions operating on private key material. Lastly, I thought this would be a neat way to learn the ins and outs of the Java Card CAP format.
