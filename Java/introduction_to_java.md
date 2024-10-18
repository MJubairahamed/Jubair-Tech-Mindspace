# Introduction
## What is JDK, JRE and JVM?
### JDK (Java Development Kit)
* Used for developing Java programs (writing and compiling).
* Contains JRE + development tools (compiler, debugger, etc.)  

### JRE (Java Runtime Environment)
* Used for running Java programs (executing the code).
* Contains JVM and libraries needed to run Java applications. 

### JVM (Java Virtual Machine)
* The JVM acts as an interpreter between your Java code and your computer. 

## How JVM Works?
* Compiler converts the ‘C-Language code in to Assembly code. Assembler converts the Assembly code in to Machine code.
* Machine code is the sequences of binary 1 & 0's that the processor understands. 
* Combination of OS and Processor is called Platform.
* Java is a programming language as well as a Platform.
* Compiler compiles the Java code (.java file) in to byte code (.class file). JVM only understands the byte code which is available in RAM of the OS.

## Components of JVM
* Class Loader - Compiled .class files are loaded without linking using Class Loader.
* Byte Code verifier – Verify the byte Code. (Reason for why Java is secure).
* Execution Engine – Converts the byte code in to machine code.

