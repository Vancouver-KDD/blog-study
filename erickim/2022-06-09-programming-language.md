# What is a programming language?

[Read Korean Version](./2022-06-09-programming-language-kr.md)

Many people know that Java is a programming language, but what about HTML or English?

In order to understand the meaning of programming language, let's first try to understand what is a program.

Program, in essense, is a set of instructions for a computer to perform certain tasks.

For example, one can write a program for a computer to calculate trajectory of a missile, or play an alarm clock at 8 o'clock in the monring.

Now that we have some understanding of what a program can do, programming language is a language that a computer can understand perform tasks. If a programming language is capable of writing all possible programs, it is called a tourning complete.

## What it takes to be a programming language

There are only 3 properties you should look for when determining if a programming language is tourning complete.

1. Conditional Loop. This allows the code to execute same piece of code 0 to infinite times.
2. Variables / Storage. We need to be able to store computed values and used in other parts of the program.
3. Function / Goto. We need to be able to break normal sequential execution and go to other specific line.

With these, we can safely say HTML and English is not a tourning complete programming language.

## Low Level vs High Level programming language.

Imagine a computer at the lowest level and human at the highest level. Low level programming language is what a computer can understand directly without much translation/abstraction. For example C and C++ will be considered low level, and JavaScript and Python being high level programming language.

There are trade-offs of low level and high level programming languages.

### Low-Level

Has more control over hardware and memory management.
More lines of code to write.
Faster execution

### High-Level

Less control over hardware and memory management.
Less lines of code to write.
Slower execution.

High level programming languages has been getting more popular as more people are looking to find ways to learn programming with lower barrier to entry.
JavaScript and Python is now the most popular languages due to its usefulness in web and data science respectively.

## Static vs dynamic typing

Languages such as C,C++, Java, and C# is considered static typing as type of a variable such as integer or String must be defined statically, before it can be compiled.

On the other hand, dynamic typing languages such as JavaScript, Python, and PHP, does not require variable to declare types and is determiend dynamically during runtime. This makes the language shorter, and typically faster to develop, but causes more runtime error that could have been caught during compile time. There are special languages such as TypeScript which is a static typed language which compiles to JavaScript. Although TypeScript requires more lines of code, it allows incremental static type adaption, but does not have benefit of fast execution such as Java.

There are many more classifications of a programming language and each will have trade-offs. The reason why there is trade-offs for everything is because ones without trade-offs is no longer a choice.

As a person who has experience in many programming languages, the best advice I can give is, use the programming language best suited to get the job done. Remember, programming language is simply a tool to make the ends meet.
