# Compiler

Compiler is a software which converts a program written in high level language \(source language\) to low level language \(Object/Target/Machine Language\).

The Hardware\(Machine\) knows a language that is hard for us to grasp, consequently we tend to write programs in high-level language, that is much less complicated for us to comprehend and maintain in thoughts. Compiler's Job is to convert from a language we understand to the language the machine understands.

![Conversion from HLL to LLL](https://media.geeksforgeeks.org/wp-content/uploads/compilerP.jpg)

### Interpreter vs Compiler

An interpreter converts high level language into low level language, just like a compiler. But they are different in the way they read the input. The Compiler reads the input in one go, does the processing and executes the source code whereas the interpreter does the same line by line. Compiler scans the entire program and translates it as a while into machine code whereas an interpreter translates the program one statement at a time. Interpreted programs are usually slower than compiled ones.

## Phases of Compiler

There are two major phases of compilation, which in turn have many parts. Each of them take input from the output of the previous level and work in a coordinated way. The compiler has two modules namely front-end and back-end. Front-end constitutes of the lexical analyzer, semantic analyzer, syntax analyzer and intermediate Code generator. And the rest are assembled to form the back end.

![Phases of Compiler](https://media.geeksforgeeks.org/wp-content/uploads/compilerDesign.jpg)

### Symbol Table

It is a data structure being used and maintained by the compiler, consists all the identifier's name along with their types. It helps the compiler to function smoothly by finding identifiers quickly.

### Analysis Phase

An intermediate representation is created for the given source code. The analysis is done in three phases

#### 1. Linear Analysis

This involves scanning phase where the stream of characters are read from left to right. It is then grouped into various tokens having a collective meaning.

#### 2. Hierarchical Analysis

In this analysis phase, based on a collective meaning, the tokens are categorized hierarchically into nested groups.

#### 3. Semantic Analysis

This phase is used to check whether the components of the source program are meaningful or not.

### 1. Lexical Analyzer

First phase of compiler also known as **scanner.** It converts the high level input program into a sequence of Tokens. Lexical Analysis can be implemented with the deterministic finite Automata. The output is a sequence of tokens that is sent to the parser for syntax analysis.

![](https://media.geeksforgeeks.org/wp-content/uploads/20190301115936/lexical.png)

#### What is a token?

A lexical token is a sequence of characters that can be treated as a unit in the grammer of the programming languages.

Examples of Tokens:

* Type token \(id, number, real, ...\)
* Punctuation token \(IF, void, return ...\)
* Alphabetic tokens \(keywords\)
* Keywords - for, while, if etc
* Identifier - Variable name, function name 
* Operators - '+', '++', '-'
* Separators: , ; etc

Examples of Non-Tokens:

* Comments, preprocessor directive, macros, blanks, tabs, newline etc

#### Lexeme

The sequence of characters matched by a pattern to form the corresponding token or a sequence of input characters that comprises a single token is called a lexeme. eg: "float", "abs\_zero", "=", "-", "273".

#### How Lexical Analyzer functions

1. Tokenization i.e Dividing the program into valid tokens
2. Remove white space characters
3. Remove comments
4. It also provides help in generating error messages by providing row numbers and column numbers.

![](.gitbook/assets/image%20%282%29.png)

The lexical analyzer identifies the error with the help of the automation machine and the grammar of the given language onn which it is based like C, C++, and gives row number and col number of the error.

**a = b + c** ;                It will generate token sequence like this:

**id=id+id**;                 Where each id refers to it’s variable in the symbol table referencing all details

```text
Program Code:

int main()
{
  // 2 variables
  int a, b;
  a = 10;
 return 0;
}
Valid Tokens:

'int'  'main'  '('  ')'  '{'  'int'  'a' ','  'b'  ';'
 'a'  '='  '10'  ';' 'return'  '0'  ';'  '}' 
```

```text
 Program Code:
 
 printf("GeeksQuiz");
 
 Valid Tokens:  (5)
 'printf'  '(' '"GeeksQuiz"' ')' ';'
 
 Eg 1:
int main()
{
  int a = 10, b = 20;
  printf("sum is :%d",a+b);
  return 0;
}
Answer: Total number of token: 27.
```

### 2. Syntax Analyzer

Syntax Analysis or Parsing checks the syntactical structure of the given input i.e whether the given input is in correct syntax or not. It does so by building a data structure, called a **Parse tree or Syntax tree**. The parse tree is constructed by using the pre-defined Grammar of the language and the input string. If the given input string can be produced with the help of the syntax tree \(in the derivation process\), the input string is found to be in the correct syntax. If not, error is reported by syntax analyzer.

The Grammar for a Language consists of Production rules.





### Synthesis Phase

Equivalent target program is created from the intermediate representation. It has two parts:

1. Code Optimizer
2. Code Generator

Code Optimizer optimizes the abstract code

Code Generator translates abstract intermediate code into specific machine instructions.

### Cross Compiler

Runs on a machine 'A' and produces a code for another machine 'BB'. It is capable of creating code for a platform other than the one on which the compiler is running.

### Source-to-souce Compiler / Transcompiler/ Transpiler

Translates source code written in one programming language into source code of annother programming language.



