<br>
<p align="center">
<img src="https://github.com/foxmoder/fennec/assets/6652788/655f0c10-b807-4e92-b043-7a6b8da303fd" alt="The fennec logo: the word fennec in a sans serif font with an orange gradient" width="300">
</p>

## What is Fennec?

Fennec is a tiny, opinionated language targetting the Java Card Virtual Machine with the primary goal of getting out of your way and allowing you to test and iterate quickly.

### Easy interfacing

Java Card works at the APDU level, meaning Java Card programs work directly with an IO buffer, often adding unnecessary boilerplate and room for programmer error. 

Fennec instead allows the programmer to write functions for each ISO 7816 instruction as they would in a systems language, using [protocol buffers](https://protobuf.dev/) within the command and response APDUs' data fields for serialization. This ensures that data passed to the card is interpreted correctly in a manner transparent to the user.

### Better typing

Java Card provides fairly barebones support for various types: just `boolean`, `byte`, `short`, and `int`, as well as arrays of those.

On top of these, Fennec provides built-in support for wide integer types, option types, and result types.

### Simpler syntax

Java requires a lot of boilerplate, and Java Card adds to this with initialization and APDU-handling boilerplate.

Fennec handles state and persisted data in a "convention over configuration" manner, erring toward simplicity.

### First-class cryptography support

While the hardware accelerators on many Java Cards provide constant-time implementations, many have issues, including the [Minerva attack](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14318). Additionally, often the hardware accelerators on a Java Card will be used for unintended purposes, such as how [JCMathLib](https://github.com/OpenCryptoProject/JCMathLib) leverages the RSA accelerator on cards for fast modular exponentiation. This often leads to fast but (as the README for JCMathLib warns) non-constant time implementations that can leak private key material.

Fennec similarly leverages hardware accelerators on cards, but controls the output program at the bytecode level in order to ensure fast but constant time implementations.

### Inline unit testing

Java frequently puts unit far away from the actual code. Fennec puts them right next to the code, and lets you test them trivially with physical hardware or [jCardSim](https://github.com/licel/jcardsim). Eventually I'd like to write a Java Card simulator in Rust too, but for now that's out of scope.

## Why's it called that?

It's a tiny language for a tiny processor. Fennecs are tiny foxes. I like foxes.

## Why write it in Rust?

Rust is great for writing little compilers like this, especially when using the parser combinator framework [nom](https://github.com/rust-bakery/nom). I wanted to try Zig for this, especially since I've been trying to pick it up more recently, but I figured Rust would be a bit more stable in the short term and also would allow other devs to help easier.

## Why not write it in Python then?

I totally could have. I just didn't want to. I'll use the excuse that Rust will be faster for longer programs, and also Rust's typing is nice when working on larger projects.

## Isn't `$RELATED_PROJECT` good enough for this?

Probably. I haven't seen any alternate Java Card languages. At the moment, I'm mostly writing this for my personal Java Card experiments. Suggestions are always welcome though--feel free to add any issues/MRs.

## Why compile directly to the JCVM and not to Java Card?

For one, the Java Card toolchain is somewhat annoying to install--I wanted the user experience to be slick. From a compiler design perspective, this also gives me a bit more expressivity, especially when trying to enforce constant time execution for functions operating on private key material. Lastly, I thought this would be a neat way to learn the ins and outs of the Java Card CAP format.
