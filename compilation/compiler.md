# Compiler

Compiler is a software which converts a program written in high level language \(source language\) to low level language \(Object/Target/Machine Language\).

The Hardware\(Machine\) knows a language that is hard for us to grasp, consequently we tend to write programs in high-level language, that is much less complicated for us to comprehend and maintain in thoughts. Compiler's Job is to convert from a language we understand to the language the machine understands.

![Conversion from HLL to LLL](https://media.geeksforgeeks.org/wp-content/uploads/compilerP.jpg)

### Interpreter vs Compiler

An interpreter converts high level language into low level language, just like a compiler. But they are different in the way they read the input. The Compiler reads the input in one go, does the processing and executes the source code whereas the interpreter does the same line by line. Compiler scans the entire program and translates it as a while into machine code whereas an interpreter translates the program one statement at a time. Interpreted programs are usually slower than compiled ones.

## Phases of Compiler

There are two major phases of compilation, which in turn have many parts. Each of them take input from the output of the previous level and work in a coordinated way. The compiler has two modules namely front-end and back-end. Front-end constitutes of the [lexical analyzer](compiler.md#1-lexical-analyzer), syntax analyzer, semantic analyzer and intermediate Code generator. And the rest are assembled to form the back end.

![Phases of Compiler](https://media.geeksforgeeks.org/wp-content/uploads/compilerDesign.jpg)

### Symbol Table

It is a data structure being used and maintained by the compiler, consists all the Identifier's name along with their types. It helps the compiler to function smoothly by finding identifiers quickly.

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

A lexical token is a sequence of characters that can be treated as a unit in the grammar of the programming languages.

**Examples of Tokens:**

* Type token \(id, number, real, ...\)
* Punctuation token \(IF, void, return ...\)
* Alphabetic tokens \(keywords\)
* Keywords - for, while, if etc
* Identifier - Variable name, function name 
* Operators - '+', '++', '-'
* Separators: , ; etc

**Examples of Non-Tokens:**

* Comments, pre-processor directive, macros, blanks, tabs, newline etc

#### Lexeme

The sequence of characters matched by a pattern to form the corresponding token or a sequence of input characters that comprises a single token is called a lexeme. Eg., "float", "abs\_zero", "=", "-", "273".

#### How Lexical Analyzer functions

1. Tokenization i.e Dividing the program into valid tokens
2. Remove white space characters
3. Remove comments
4. It also provides help in generating error messages by providing row numbers and column numbers.

![](../.gitbook/assets/image%20%282%29.png)

The lexical analyzer identifies the error with the help of the automation machine and the grammar of the given language on which it is based like C, C++, and gives row number and col number of the error.

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

```text
  S -> cAd
  A -> bc|a
  And the input string is “cad”.
```

Now the parser attempts to construct syntax tree from this grammar for the given input string. It uses the given production rules and applies those as needed to generate the string. To generate string "cad" it uses the rules as shown in the given diagram:

![](../.gitbook/assets/image%20%283%29.png)

In Step \(iii\), the production rule A-&gt;bc was not a suitable one to apply, here the parser needs to backtrack, and apply the next production rule available with A which is shown in the step iv, and the string "cad" is produced.

But backtrack is really a complex process to implement. There is an easier way to solve this using [FIRST and FOLLOW ](first-and-follow-in-syntax-analysis.md)sets in compiler design.

### 3. Semantic Analyzer

It verifies the parse tree, whether it is meaningful or not. It furthermore produces a verified parse tree. It also does **type checking, Label checking and Flow control checking.**

![](../.gitbook/assets/image%20%284%29.png)

### **4. Intermediate Code Generator**

The front end of the compiler translates a source program into an independent intermediate code. The benefits of using machine independent intermediate code are:

* Portability will be enhanced. Eg., If a compiler translates the source language to its target machine language without having the option for generating intermediate code, then for each new machine, a full native compiler is required.
* Retargeting is faciliated
* It is easier to apply source code modification to improve the performannce of source code by optimising the intermediate code.

If we generate machine code directly from source code then for n target machine we will have n optimizers and n code generators but if we will have a machine independent intermediate code, we will have only one optimiser. Intermediate code can be either language specifiic \( Bytecode for Java\) or language independent \(three-address code\)

#### Intermediate Code Representation

The following are commonly used intermediate code representation:

#### 1. Postfix Notation

In postfix notation, the operator follows its operands. eg: ab+. No parentheses are needed in postfix notation because the position and number of arguments of the operators permit only one way to decode a postfix expression.

#### 2. Three-Address Code

A statement involving no more than three references \( two for operands and one for result\) is known as **three address statement.** A sequence of three address statements is known as three address code. Three address statement is of the form x = y op z, here x,y,z will have address. Sometimes a statement might contain less than three references but it is still called three address statement. 

```text
Expression : a + b*c + d;
Converted to
T1 = b * c
T2 = a + T1
T3 = T2 + d
T1,T2,T3 are temporary variables.
```

#### 3. Syntax Tree

It is nothing more than condensed form of a parse tree. The operator and keyword nodes of the parse tree are moved to their parents and a chain of single productions is replaced bby a single link. In syntax tree the internal nodes are operators and child nodes are operands. For eg., x = \(a + b\*c\) / \(a - b\*c\)

![Syntax Tree](../.gitbook/assets/image%20%285%29.png)

### Synthesis Phase

Equivalent target program is created from the intermediate representation. It has two parts:

1. Code Optimizer
2. Code Generator

### Code Optimizer

It is a program transformation techinque, which tries to improve the intermediate code by making it consume fewer resources \( CPU, memory\) so that faster-running machine code will result. Compiler optimizing process should meet the following objectives:

* Optimization must be correct, it must not in any way, change the meaning of the program.
* Should increase the speed and performance of the program
* Compilation time must be kept reasonable
* Should not delay the overall compiling process.

#### When to Optimize?

Optimization of the code is often performed at the end of the development stage since it reduces readability and adds code that is used to increase the performance.

#### Why Optimize?

Optimization helps us to

* Reduce the space consumed and increases the speed of compilation
* Manually analyzing datasets involves a lot of time. Hence we make use of software like Tableau for data analysis. Similarly mannually performing the optimization is also tedious and is better done using a code optimizer.
* An optimized code often promotes re-usability.

#### Types of Code Optimization

1. **Machine Independent Optimization** - Improves the intermediate code to get a better target code as the output. The part of the intermediate code which is transformed here does not involve any CPU registers or absolute memory locations.
2. **Machine Dependent Optimization** - It is done after the target code is generated and when the code is transformed according to the target machine architecture. It involves CPU registers and may have absolute memory references rather than relative references. Machine-dependent optimizers put efforts to take maximum advantage of the memory hierarchy.

#### Code Optimization Methods

#### 1. Compile Time Evaluation

```text
(i)  A = 2*(22.0/7.0)*r 
     Perform 2*(22.0/7.0)*r at compile time.
(ii)  x = 12.4
      y = x/2.3 
      Evaluate x/2.3 as 12.4/2.3 at compile time.
```

#### 2. Variable Propagation

```text
//Before Optimization 
c = a * b                                               
x = a                                                  
till                                                           
d = x * b + 4 
 
 
//After Optimization 
c = a * b  
x = a
till
d = a * b + 4
```

Hence, after variable propagation, a\*b amd x\*b will be identified as common sub-expression.

#### 3. Dead code elimination

Variable propagation often leads to making assignment statement into dead code.

```text
c = a * b												
x = a												
till														
d = a * b + 4

//After elimination :
c = a * b
till
d = a * b + 4
```

#### 4. Code Motion

* Reduce the evaluation frequency of expression.
* Bring loop invariant statements out of the loop.

```text
a = 200;
 while(a>0)
 {
     b = x + y;
     if (a % b == 0}
     printf(“%d”, a);
   }
 
 
//This code can be further optimized as
a = 200;
b = x + y;
while(a>0)
 {
     if (a % b == 0}
     printf(“%d”, a);
}
```

#### 5. Inducation Variable and Strength Reduction:

* An induction variable is used in loop for the following kind of assignment i = i + constant.
* Strength reduction means replacing the high strength operator by the low strength.

```text
i = 1;																	
while (i<10)														
{																			
	y = i * 4;
}


//After Reduction
i = 1
t = 4
{
while( t<40)
y = t;
t = t + 4;
}

```

#### Where to apply Optimization?

**Source program:** Optimizing the source program involves makinng changes to the algorithm or changing the loop structures. User is the actor here.

**Intermediate Code:** Optimizing the intermediate code involves changing the address calculations and transforming the procedure calls involved. Here compiler is the actor.

**Target Code:** Optimizing the target code is done by the compiler. Usage of registers, select and move inststructions is part of optimization involved in the target code.

#### Phases of Optimization

**Global Optimization:** Transformation are applied to large program segments that includes function, procedures and loops.

**Local Optimization:** Transformations are applied to small block of statements. This is done prior to global optimization.

### 6. Target Code Generator

The main purpose of the target code generator is to write a code that the machine can understand and also register allocationn, instruction selection etc. The output is dependent on the type of assembler. The optimized code is converted into relocatable machine code which then forms the input to the linker and loader.

### Cross Compiler

Runs on a machine 'A' and produces a code for another machine 'BB'. It is capable of creating code for a platform other than the one on which the compiler is running.

### Source-to-souce Compiler / Transcompiler/ Transpiler

Translates source code written in one programming language into source code of annother programming language.



