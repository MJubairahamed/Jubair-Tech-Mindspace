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

![Components of JDK!](/Java/Images/JDK_JRE_JVM_ss.png "Components of JDK")

## What is Class and Object in Java?
* A class is like a set of instructions or a blueprint.
* Ex: The class would describe things like the car’s features (color, model, speed) and what it can do (drive, honk). 
* An object is the actual thing created from those instructions. 
* An object would be an actual car made using that blueprint, with specific details (e.g., a red sports car that can go 200 km/h) .

### First Java Program
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("Hello, World!");
        }
    }

