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
