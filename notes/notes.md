# Parts of a Language


### 1. Scanning
Also known as **lexing** (lexical analysis). Turns stream of characters into **tokens**.

Example:
- `var average = (min + max);`
- Into "var", "average", "=", "(", "min", "+", "max", ")", ";"

### 2. Parsing
Provides a **grammar** for the syntax. It takes the tokens and builds a **tree** structure (Abstract Syntax Tree). It reports syntax errors.

### 3. Static Analysis
Performs **binding** or **resolution**.
- For each identifier find out where the name is defined and wire the two together. Scope comes into play.

If the language is statically typed, **type checking** is also performed to report type errors.

This is the highest point, a sweeping view of the program. Insights are stored in:
- Attributes on the syntax tree nodes
- A look up table also called a **symbol table**

<br>

---

### 4. Intermidiate Representations (IR)
Code stored in this form is not specific to the source or the destination. Interfaces between the front and the back end. 

Advantage: You can write one front end for each langugage to produce the IR, then just write the backend for each architecture to target.

### 5. Optimizations
Examples: 
- Constant folding
- Constant propagation
- Common subexpression elimination
- Loop invariant code motion
- Global value numbering
- Strength reduction
- Scalar replacement of aggregates
- Dead code elimination
- Loop unrolling

<br>

---
### 6. Code Generation
Converting to machine code. Machine code can be targetted to specific architectures (x86, arm) or be virtual machine code known as **bytecode**. 

### 7. Virtual Machine
If the compiler produces bytecode. There are two options:
1. Write a mini compiler for each architecture, using bytecode as IR.
2. Write a VM to emulate a chip at runtime, slower than translating to native code but offers more simplicity and portability.

### 8. Runtime
If compiled to machine code then just tell OS to load exe. If it is bytecode we will have to start up the VM and load the program into it. In both cases, there are services that the language provides when the program is executing. Example:
- Garbage collector
- "Instance of" tests

All of this is going at runtime. In a fully compiled language the runtime is inserted directly into the exe (think C, Go). If it is run inside an interpreter or VM, the runtime lives there (think JS, Java, Python).


<br>

# Shortcuts and Alternate Routes

### 1. Single Pass Compilers
Produce output code directly in the parser without ASTs or IRs. Examples: Pascal (Type declarations first in a block) and C (unable to call a function above the code that defines unless a forward declaration is used).

### 2. Tree Walk Interpreters
Begins executing code after parsing it into an AST (with slight static analysis). To run the program the interpreter traverses the syntax tree one branch and leaf at a time, evaluating each node. Tends to be slow.

### 3. Transpilers
Treating another source language as an IR. Write a front end for your language, and in the backend produce a string of valid source code of another language and use their compilation tools. Known as a **source to source compiler**.

### 4. Just-in-time Compilation
When the program is loaded, you compile it into the native code for the architecture the computer supports.

<br>

# Closures
Functions are **first class**: They are real values that you can get a reference to, store in variables, and pass around.

```
fun addPair(a, b) {
  return a + b;
}

fun identity(a) {
  return a;
}

print identity(addPair)(1, 2); // Prints "3".
```

Functions inside functions are allowed.

```
fun outerFunction() {
  fun localFunction() {
    print "I'm local!";
  }

  localFunction();
}
```

Combining local functions, first-class functions, and block scope:

```
fun returnFunction() {
  var outside = "outside";

  fun inner() {
    print outside;
  }

  return inner;
}

var fn = returnFunction();
fn();
```

<br>

# Classes vs Prototypes
Prototypes only have objects but no classes. Each object may contain its state and methods. 

![](<Screenshot 2024-12-05 192921-1.png>)



