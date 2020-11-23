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
  
##
