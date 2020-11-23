"#webdesign" 
<h1> Ch.7 Basic Semantics </h1>

<h2>Objectives</h2>
<ul>
  <li>Understand <b>attributes</b>, <b>binding</b>, and <b>semantics</b> functions</li>
  <li>Understand <b>declarations</b>, <b>blocks</b>, and <b>scope</b></li>
  <li>Learn how to construct a <b>symbol table</b></li>
  <li>Understand <i>name resolution</i> and <i>overloading</i></li>
  <li>Understand <i>allocation</i>, <i>lifetimes</i>, and the <i>environment</i></li>
</ul>

## Introduction
- **Syntax**: what the language *constructs* look like
- **Semantics**: what the language constructs actually do
- Specifying semantics is more difficult than specifying syntax

**Several ways** to specify semantics:
- Language reference manual
- Defining a translator
- Formal definition

<h2>Introduction (cont'd.)</h2>
<ul>
  <li><b>Language reference manual</b></li>
  <ul><li>Most common way to specify semantics</li>
    <li>Provides clearer and more precise reference manuals</li>
    <li>Suffers from a lack of precision inherent in natural language descriptions</li>
    <li>Maybe have omissions and ambiguities</li>
  </ul>
</ul>

<li>Defining a translator:
  <ul>
    <li>Questions about a language can be answered by
    </br>experimentation</li>
    <li>Questions about program behavior cannot be 
    </br>answered in advance</li>
    <li>Bugs and machine dependencies in the translator
    </br>may become part of the language semantics,
    </br>possibly unintentionally</li>
    <li>May not be protable to all machines</li>
    <li>May not be generally available</li>
  </ul>
</li>

<h2>Introduction (cont'd.)</h2>
<ul>
  <li>Formal definition:</li>
  <ul>
    <li>Formal mathematical methods: <b>precise</b>, but are also
      </br><i>complex</i> and <i>abstract</i></li>
    <li>Requires study to understand</li>
    <li><b>Denotational semantics</b>: probably the best <i>formal methods</i>
    </br>for the description of the translation and 
    </br>exection of programs
    <ul><li>Describes semantics using a series of functions</li>
  </ul>
  <li>This course will use a hybrid of informal description
  </br>with the simplified functions used in denotational
  </br>descriptions</li>
</ul>


<div class="abs">
<h1>Attributes, Binding,</br>and Semantic Functions</h1>
<ul>
  <li><b>Names</b>(or <b>identifiers</b>): a fundamental abstraction
    </br>mechanism used to denote <i>language entities</i> or contructs.</li>
  <li>Fundamental step in describing semantics is to
  </br>describe <i>naming conventions for identifiers</i></li>
  <li>Most languages also include concepts of location
  </br>and value
    <ul>
  <li><b>Value:</b> any storable quantities</li>
  <li><b>Location:</b> place where value can be stored; usually
    </br>a <i>relative location</i></li>
    </ul>
    </li>
</ul>

<ul>
  <li><b>Attributes:</b> properties that determine the meaning
    </br>of the name to which they are associated</li>
  <li>Example in C: <code>const int n = 5;</code>
  <ul>
    <li>Attribute for variables and constants include data
      </br>type and value</li>
      </ul>
  <li>Example in C:
  </br><code>double f(int n) {
  ...
  }
  </code></li>
  <li>Attributes include <code>function</code>, <code>number</code>, <code>names</code> and
  </br><code>data type</code> of parameters, return value data type, 
  </br>body of code to be executed</li>
</ul>


    <ul>
  <li>Assignment statements associate attributes to names</li>
  <li>Example <code>x = 2;</code>
    <ul>
      <li>Associates attribute "value 2" to variable <code>x</code></li>
    </ul></li>
  <li>Example in C++: <p>
    <code>int* y;</code>
    <code>y = new int;</code>
  </p><ul><li>Allocates memory (associates location to <code>y</code>)</li>
  <li>Associates value</li></ul></li>
  </ul>


  <ul>
  <li><b>Binding:</b> process of associating an attribute with a
    </br>name</li>
    <li><b>Binding time:</b> the time when an attribute is
  </br>computed and bound to a name</li>
  <li>Two categories of binding:
  <ul><li><b>Static binding:</b> occurs prior to execution</li>
    <li><b>Dynamic binding:</b> occurs during execution</li>
  </ul>
  <li>Static attribute: an attribute that is bound statically</li>
  <li>Dynamic attribute: an attribute that is bound
  </br>dynamically</li>
  </ul>


## Attributes, Binding, and Semantic Functions(cont'd.)
- Languages differ substantially in which attributes are bound **statically** or **dynamically**
  - Functional languages tend to have more *dynamic* binding than *imperative langauges*
- Static attributes can be bound during *translation*, during *linking*, or during *loading* of the program
- Dynamic attributes can be *bound* at *different times* during *execution*, such as *entry* or *exit* from a procedure or from the program

## (cont'd.)
<ul>
  <li>Some attributes are bound prior to translation time
    <ul>
      <li><b>Predefined identifiers:</b> specified by the language
      </br>definition</li>
  <li>Values <code>true/false</code> bound to data type <code>Boolean</code></li>
  <li><code>maxint</code> specified by language definition and</br>implementation</li>
  </ul></li>
  <li>All binding times <i>except execution time</i> are static
  </br>binding</li>
</ul>

## binding times for attributes of names
<ul>
  <li>Static binding
    <ul>
      <li>lang. definition time</li>
      <li>lang. implementation time</li>
      <li>translation time</li>
      <li>link time</li>
      <li>load time</li>
    </ul></li>
  <li>Dynamic binding execution time</li>
</ul>

## Attributes, Binding, and Semantic Functions(cont'd.)
<ul>
  <li>A <b>translator</b> creates a data structure to maintain
    </br>bindings
       <ul>
          <li>Can be thought of as a function that expresses the
            </br>binding of attributes to names
            </li>
            </ul></li>
  <li><b>Symbol table</b>: a function from names to attributes
     <ul>
       <li><i>Mapping names to attributes in a symbol table</i></li>
  </ul></ul>
  
 ## (cont'd.)
 <ul>
  <li><b>Parsing phase</b> of <i>translation</i> includes three types of
    </br>analysis:
    <ul><li><b>Lexical analysis</b>: determines whether a string of
  </br>characters represents a <i>token</i></li>
  <li><b>Syntax analysis:</b> determines whether a sequence of
  </br>tokens represents a phrase in the context-free
  </br>grammar</li>
  <li><b>Static semantic analysis:</b> establishes attributes of
  </br>names in declarations and ensures that the use of
  </br>these names conforms to their declared attributes</li></ul>
  <li>During execution, attributes are also mantained</li>
  </ul>
  
  ## declarations, blocks, and scope
  <ul>
  <li>Bindings can be <b>implicit</b> or <b>explicit</b><li>
  <li>Example: <code>int x;</code> 
    <ul>
      <li>Data type is bound explicityly; location of <code>x</code> is bound</br>implicitly</li></ul></li>
      <li>Entire declaration itself may be implicit in
  </br>languages where simply using the varaible name
  </br>causes it to be declared</li>
  <li><b>Definition:</b> in C and C++, a declaration that binds
  </br> all potential attributes</li>
  <li><b>Prototype:</b> function declaration that specifies the
  <?br>data type but not the code to implement it</li>
</ul>

## (cont'd.)
<ul>
  <li><b>Block:</b> a sequence of declarations followed by a
    </br>sequence of statements</li>
    <li><b>Compound statements:</b> blocks in C that appear
  </br>as the body of functions or anwhere an oridnary
  </br>program statement could appear</li>
  <li><b>Local declarations:</b> associated with a block</li>
  <li><b>Nonlocal declarations:</b> associated with
  </br>surrounding blocks</li>
  <li>Block-structured languages allow nesting of blocks
  </br>and redeclaration of names within nested blocks</li>
  </ul>
## (cont'd.)
<ul>
  <li>Each declared name has a <b>lexical address</b>
    </br>containing a <b>level number</b> and an <b>offset</b>
    <ul><li>Level number starts at 0 and increases into each
  </br>nested block</li></ul>
  <li>Other sources of declarations include:
  <ul>
    <li>A <code>struct</code> definition composed of local(member)
    </br>declarations</li>
    <li>A class in object-oriented languages</li>
  </ul>
  <li>Declarations can be collected into packages (Ada),
  </br>modules (ML, Haskell, Python), and namespaces
  </br>(C++)</li>
</ul>

## Declarations, Blocks, and Scope (cont'd.)
<ul>
  <li><b>Scope of a binding:</b> region of the program over
    </br>which the binding is maintained</li>
    <li><b>Lexical scope:</b> in block-structured languages,
  </br>scope is limited to the block in which its associated 
  </br>declaration appears (and other blocks contained
  </br>within it)</li>
  <li><b>Declaration before use rule:</b> in C, scope of a
  </br>declaration extends from the point of declaration to
  </br>the end of the block in which it is located</li>
</ul>

## Simple C program demonstrating scope
```C
int x;

void p() {
  char y;
  ...
} /* p */

void q() {
  double z;
  ...
} /* q */

main() {
  int w[10];
  ...
}
```

## Declarations, Blocks, and Scope (cont'd.)
<ul>
  <li>Declarations in nested blocks take precedence
    </br>over previous declarations</li>
    <li>A global variable is said to have a <b>scope hole</b> in a
  </br>block containing a local declaration with the same name
      <ul>
  <li>Use <b>scope resolution operator</b> <code>::</code> in C++ to
    </br>access the global variable</li></ul>
    <li>Local declaration is said to <b>shadow</b> its global
  </br>declaration</li>
  <li><b>Visibility:</b> includes only regions where the bindings
  </br>of a declaration apply</li>
  </ul>
  
## code example:
``` C
int x;

void p() {
char x;
   x = 'a'; // assigns to char x
   ::x = 42; // assigns to global int x
   ...
}

main() {
x = 2; // assigns to global x
...
}
```

## Declarations, Blocks, and Scope (cont'd.)
<ul>
  <li>Scope rules need to be constructed such that
    </br>recursive (<i>self-referential</i>) declarations are possible
    </br>when they make sense
    <ul>
  <li>Example: functions must be allowed to be recursive,
    </br>so function name must have scope beginning before
    </br>the block of the function body</li></ul>
    </ul>

``` C
int factorial (int n) {
  /* scope of factorial begins here */
  /* factorial can be called here */
  ...
}
```

## The Symbol Table
<ul>
  <li><b>Symbol table:</b></br>
  <ul>
  <li>Must support <i>insertion</i>, <i>lookup</i>, and <i>deletion</i> of
    </br>names with associated attributes, representing
    </br>bindings in declarations</li>
    <li>A lexically scoped, block-structured languages
  </br>requires a stack-like data structure to perform
  </br><b>scope analysis</b>
  <ul>
  <li>On block entry, all declarations of that block are
    </br>processed and bindings added to symbol table</li>
    <li>On block exit, bindings are removed, restoring any
  </br>previous bindings that mayt have existed</li></ul>
  </li>
  </ul>
  
## code example:
``` C
int x;
char y;

void p() {
  double x;
  ...
  { int y[10];
    ...
  }
  ...
}

void q() {
  int y;
  ...
 }
 
 main() {
  char x;
  ...
  }
```
<caption>C Program demonstrating symbol table structure</caption>


## The Symbol Table(cont'd.)
<ul>
  <li>The previous example assumes that declarations
    </br>are processed <i>statically(prior to execution)</i>
    <ul>
  <li>This is called <b>static scoping</b> or <b>lexical scoping</b></li>
  <li>Symbol table is managed by a <i>compiler</i></li>
  <li>Bindings of declarations are all <i>static</i></li>
  </ul>
  <li>If symbol table is managed <i>dynamically</i> (during
  </br>execution), declarations will be processed as they
  </br>are encountered along an execution path
  <ul>
  <li>This is called <b>dynamic scoping</b></li>
  </ul></li>
  </ul>
  
## code example:
``` C
#include <stdio.h>

int x = 1;
char y = 'a';

void p() {
  double x = 2.5;
  printf("%c\n", y);
  {
     int y[10];
  }
}

void q() {
  int y = 42;
  printf(%d\n", x);
  p();
}

main() {
   char x = 'b';
   q();
   return 0;
}
```

### Problems with dynamic scoping:
<ul>
  <li>The declaration of a nonlocal name cannot be
    </br>determined by simply reading the program: the
    </br>program must be executed to know the execution
    </br>path</li>
    <li>Since nonlocal variable references cannot be
  </br>predicted prior to execution, netiher can their data
  </br>types</li>
</ul>

<li>Dynamic scoping is a possible option for highly
  </br>dynamic, interpreted languages when programs
  </br>are not expected to be extremely large</li>
  
## The Symbol Table (cont'd.)
<ul>
  <li>Runtime environment is simpler with dynamic
    </br>scoping in an interpreter
    <ul>
      <li>APL, Snobol, Perl, and early dialects of Lisp were
        </br>dynamically scoped</li>
      <li>Scheme and Common Lisp use <b>static scoping</b></li>
    </ul>
  <li>There is additional complexity for symbol tables</li>
  <li><code>struct</code> declaration must contain further
  </br>declarations of the data fields within it
  <ul>
  <li>Those field must be accessible using dot member
    </br>notation whenever the <code>struct</code> variable is in scope</li>
    </ul></li>
</ul>

## (cont'd.)
<ul>
  <li>Two implications for struct variables:
    <ul>
      <li>A struct declaration actually contains a local symbol
      </br>table itself as an attribute</li>
  <li>This local symbol table cannot be deleted until the
    </br>struct variable itself is deleted from the global
    </br>symbol table of the program</li>
    </ul>
  </li>
</ul>

## code example:
``` C
struct {
  int a;
  char b;
  double c;
} x = {1, 'a', 2.5);

void p() {
  struct {
    double a;
    int b;
    char c;
  } y = { 1.2, 2, 'b' };
  printf("%d, %c, %g\n", x.a, x.b, x.c);
  printf("%f, %d, %c\n", y.a, y.b, y.c);
}

main () {
   p();
   return 0;
}
```

## The Symbol Table (cont'd.)
<ul>
  <li>Any scoping structure that can be referenced
  </br>directly must also have its own symbol table</li>
  <li>Examples:
    <ul>
      <li>Named scopes in Ada</li>
      <li>Classes, structs, and namespaces in C++</li>
      <li>Classes and packages in Java</li></ul>
  </li>
  <li>Typically, there will be a table for each scope in a
  </br>stack of symbol tables
    <ul>
      <li>When a reference to a name occurs, a search
  </br>begins in the current table and continues to the next
  </br>table if not found, and so on</li>
    </ul></li>
</ul>

## code example
``` Ada
with Text_IO; use Text_IO;
with Ada.Integer_Text_IO; use Ada.Integer_Text_IO;

procedure ex is
  x: integer := 1;
  y: character := 'a';
  
  procedure p is
  x: float := 2.5;
  begin
    put(y); new_line;
  A: declare
       y: array (1..10) of integer;
     begin
       y(1) := 2;
       put(y(1)); new_line;
       put(ex.y); new_line;
     end A;
  end p;
  
  procedure q is
     y: integer := 42;
  begin:
    put(x); new_line;
    p;
  end q;
  
   begin
   declare
      x: character := 'b';
   begin
      q;
      put(ex.x); new_line;
   end;
end ex;
  
```

## Name Resolution and Overloading
<ul>
  <li>Addition operator <code>+</code> actually indicates at least
    </br>two different operations: <i>integer addition</i> and <i>floating-point addition</i>
    <ul>
  <li><code>- +</code> operator is said to be <b>overloaded</b></li>
  </ul>
  <li>Translator must look at the data type of each
  </br>operand to determine which operation is indicated</li>
  <li><b>Overload resolution:</b> process of choosing a
  </br>unique function among many with the same name
  <ul>
    <li>Lookup operation of a symbol table must search on
  </br>name plus number and data type of parameters</li>
  </ul>
</ul>

## code example:

<h3> Three overloaded <code>max</code> functions in C++</h3>

``` C++
int max(int x, int y) { // max #1
    return x > y ? x : y;
}

double max(double x, double y) { // max #2
    return x > y ? x : y;
}

int max(int x, int y, int z) { // max #3
    return x > y ? (x > z ? x : z ) : (y > z ? y : z );
```

## Name Resolution and Overloading (cont'd.)
<ul>
  <li>Consider these function calls:
    <p><code>max(2, 3); // calls max #1 
      max(2.1, 3.2); // calls max #2
      max(1, 3, 2); // calls max #3</code></p>
    </li>
  <li>Symbol table can determine the appropriate
  </br>function based on number and type of parameters</li>
  <li><b>Calling context:</b> the information contained in each
</br>call</li>
  <li>But this <b>ambiguous</b> call depends on the language
</br>rules(if any) for converting between data types:
<p><code>max(2.1, 3); // which max?</code></p></li>
</ul>

## (cont'd.)
<li>Adding these definitions makes the function calls
  </br>legal in C++ and Ada but is unnecessary in Java</li>

``` C++
double max(int x, double y) { // max #4
    return x > y ? (double) x : y;
}

double max(double x, int y) { // max #5
    return x > y ? x : (double) y;
}
```
<li> Automatic conversions as they exist in C++ and
  </br>Java significantly complicate overload resolution</li>
  
## Name Resolution and Overloading (cont'd.)
<ul>
  <li>Additional information in a calling context may be
    </br>used for overload resolution:
    <ul>
      <li>Ada allows the return type and names of parameters
        </br>to be used for overhead resolution</li>
      <li>C++ and Java ignore the return type</li>
    </ul>
  <li>Both Ada and C++(but not Java) allow built-in
  </br>operators to be overloaded</li>
  <li>When overloading a built-in operator, we must
  </br>accept its syntactic properties
    <ul>
      <li>Example: cannot change the associativity or
        </br>precedence of the <code>+</code> operator</li>
    </ul></li>
</ul>

## (cont'd.)
<ul>
  <li>Note that there is no semantic difference between
    </br>operators and functions, only syntactic difference
    <ul>
      <li>Operators are written in infix form</li>
      <li>Function calls are always written in prefix form</li></ul>
  </li>
  <li>Names can also be overloaded</li>
  <li>Some languages use different symbol tables for
  </br>each of the major kinds of definitions to allow the
  </br>same name for a type, a function, and a variable
    <ul>
  <li>Example: Java</li></ul></li>
</ul>

## code example:
``` Java
class A
{ A A(A A)
  { A:
    for(;;)
    { if (A.A(A) == A) break A; }
  }
}
```
<p><emp>7.26</emp> Java class definition showing overloading of the same name for different language constructs</p>

## Allocation, Lifetimes, and the Environment
<ul>
  <li>Environment: maintains the bindings of names to
    </br>locations
    <ul>
      <li>May be constructed statically(at load time),
  </br>dynamically(at execution time), or with a mixture of
  </br>both</li></ul></li>
  <li>Not all names in a program are bound to locations
    <ul>
      <li>Examples: names of constants and data types may
      </br>represent purely compile-time quantites</li>
    </ul></li>
  <li>Declarations are also used in environment
  </br>construction
    <ul>
      <li>Indicate what allocation code must be generated</li>
   </ul></li>
</ul>

## (cont'd.)
<ul>
  <li>Typically, in a block-structured language:
    <ul>
      <li>Global variables are allocated statically</li>
      <li>Local variables are allocated dynamically when the
      </br>block is entered</li>
    </ul>
  </li>
  <li>When a block is entered, memory for variables
</br>declared in that block is allocated</li>
  <li>When a block is exited, this memory is deallocated</li>
</ul>

## code example
``` C
A: { int x;
     char y;
     ...
     
     B: { double x;
          int a;
          ...
        } /* end B */
        
     C: { char y;
          int b;
          ...
          
          D: { int x;
               double y;
               ...
             } /* end D */
             ...
           } /* end C */
           ...
         } /* end A */
```
<span><emp>Figure 7.27</emp> A C program with nested blocks to demonstrate
  </br>allocation by the environment</span>
  
## Allocation, Lifetimes, and the Environment (cont'd.)
<ul>
  <li>Memory for local variables within a function will not
  </br>be allocated until the function is called</li>
  <li><b>Activation:</b> a call to a function</li>
  <li><b>Activation record:</b> the corresponding region of
</br>allocated memory</li>
  <li>In a block-structured language with lexical scope,
</br>the same name can be associated with different
</br>locations, but only one of these can be accessed at 
</br>any one time</li>
  <li><b>Lifetime</b>(or <b>extent</b>) of an object is the duration of
</br>its allocation in the environment</li>
</ul>

## (cont'd.)
<ul>
  <li>Lifetime of an object can extend beyond the region
    </br>of a program in which it can be accessed
    <ul>
      <li>Lifetime extends through a scope hole</li>
    </ul></li>
  <li><b>Pointer:</b> an object whose stored value is a
</br>reference to another object</li>
  <li>C allows the initialization of pointers that do not
  </br>point to an allocated object: <code> int* x = NULL</code>
    <ul>
      <li>Objects must be manually allocated by use of an
  </br>allocation routine</li>
      <li>Variable can be dereferenced using the unary *
</br>operator</li>
    </ul></li>
</ul>

## Allocation, Lifetimes, and the Environment (cont'd.)
<li>C++ simplifies dynamic allocation with operators
</br><code>new</code> and <code>delete</code>:</li>

``` C++
int* x = new int; // C++
*x = 2;

cout << *x << endl; // output in C++
delete x;
```
<p>&emsp;&#8211; These are used as unary operators, not functions</p>
<li><b>Heap</b>: area in memory from which locations can be
</br>allocated in response to calls to <code>new</code></li>
<li><b>Dynamic allocation</b>: allocation on the heap</li>

## Allocation, Lifetimes, and the Environment (cont'd.)
<ul>
  <li>Many languages require that heap deallocation be
  </br>managed automatically</li>
  <li>Heap allocation/deallocation and explicit pointer
  </br>manipulation are inherently operations
    <ul>
      <li>Can introduce seriously faulty runtime behavior that
      </br>may even compromise the operating system</li>
    </ul>
  </li>
  <li><b>Storage class:</b> the type of allocation
    <ul>
      <li>Static(for global variables)</li>
      <li>Automatic(for local variables)</li>
      <li>Dynamic(for heap allocation)</li>
    </ul>
  </li>
</ul>

## Variables and Constants
<ul>
  <li>Although the references to variables and constants
  </br>look the same in many languages, their roles and
  </br>semantics are very different</li>
  <li>We will look at the basic semantics of both</li>
</ul>

## Variables
<ul>
  <li><b>Variable</b>: an object whose stored value can
    </br>change during exectuion
    <ul>
      <li>Is completely specified by its attributes (name,
      </br>location, value, data type, size of memory storage)</li>
    </ul></li>
  <li><b>Box and circle diagram:</b> focuses on name
  </br>and location</li>
</ul>

## Variables (cont'd.)
<ul>
  <li><b>Assignment</b> statement: principle way in which a
  </br>variable changes its value</li>
  <li>Example: <code>x = e</code>
    <ul>
      <li>Semantics: expression <code>e</code> is evaluated to a value,
      </br>then copied into the location of <code>x</code></li></ul>
  </li>
  <li>If <code>e</code> is a variable named <code>y</code>:</li>
</ul>
    
## Variables (cont'd.)
<ul>
  <li>Variable on right side of assignment statement
  </br>stands for a value (<b>r-value</b>); variable on left side
  </br>stands for a location (<b>l-value</b>)</li>
  <li><b>Address of operator</b>(&) in C: turns a reference
  </br>into a pointer to fetch the address of a variablee</li>
  <li><b>Assignment by sharing:</b> the location is 
</br>copied instead of the value</li></li>
  <li><b>Assignment by cloning:</b> allocates new location,
</br>copies value, and binds to the new location</li>
  <li>Both are sometimes called <b>pointer semantics</b> or <b>reference semantics</b></li>
</ul>

## (cont'd.)
<ul>
  <li><b>Storage semantics</b> or <b>value semantics</b> refer to
  </br>standard assignment</li>
  <li>Standard implementation of assignment by sharing
  </br>uses pointers and implicit dereferencing</li>
</ul>

## Constants
<ul>
  <li><b>Constant:</b> an entity with a fixed value for the
    </br>duration of its existence in a program
    <ul>
      <li>Like a variable, but has no location attribute</li>
  <li>Sometimes say that a constant has <b>value</b>
  </br><b>semantics</b></li>
    </ul>
  </li>
  <li><b>Literal:</b> a representation of characters or digits</li>
  <li><b>Compile-time constant:</b> its value can be
  </br>computed during compilation</li>
  <li><b>Static constant:</b> its value can be computed at load
  </br>time</li>
</ul>

## (cont'd.)
<ul>
  <li><b>Manifest constant:</b> a name for a literal</li>
  <li>Dynamic constant: its value must be computed
  </br>during execution</li>
  <li>Function definitions in virtually all languages are
  </br>definitions of constants whose values are functions
    <ul>
      <li>This differs from a function variable in C, which must
      </br>be defined as a pointer</li>
    </ul>
  </li>
</ul>

<div>
  <p>
  <ul>
    <li>a</li>
    <li>b</li>
    <li>c</li>
  </ul>
  </p>
  <aside><code>hello</code></aside>
</div>
