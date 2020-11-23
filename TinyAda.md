# Case Study: 
## Initial Static Semantic Analysis of TinyAda
<ul>
  <li>Syntax analyzer for TinyAda
    <ul>
      <li>A simple parsing shell that pulled tokens from a
      </br>scanner until a syntax error was detected</li>
    </ul></li>
  <li>Here, we extend the parsing shell to perform some
  </br>semantic analysis
    <ul>
      <li>Focus will be on tools for scope analysis and for
      </br>restricting the use of identifiers</li>
    </ul></li>
  <li>Must focus on two attributes of an identifier:
    <ul>
      <li>Name</li>
      <li>Role it plays(constant, variable, type, or procedure)</li>
    </ul></li>
</ul>

## Scope Analysis
<ul>
  <li>TinyAda is lexically scoped, with these scope rules:
    <ul>
      <li>All identifiers must be declared before use</li>
      <li>At most, one declaration for a given identifier in a
      </br>single block</li>
      <li>A new block starts with formal parameter
      </br>specificiations of a procedure and extends to the
      </br>reserved word end</li>
      <li>Visibility of a declared identifier extends into nested
      </br>blocks unless it is redeclared in that block</li>
      <li>Identifiers are not case sensitive</li>
    </ul>
  </li>
</ul>

## Scope analysis (cont'd.)
<ul>
  <li>TinyAda has five built-in (predefined) identifiers:
    <ul>
      <li>Data type names <code>integer</code>, <code>char</code>, <code>boolean</code></li>
      <li>Boolean constants <code>true</code> and <code>false</code></li>
    </ul>
  </li>
  <li>These identifiers must be visible in a top-level
    </br>scope before a source program is parsed
    <ul>
      <li>Static nesting level of this scope is 0</li>
    </ul>
  </li>
  <li>Scope at nesting level 1 contains the procedure's
  </br>formal parameters(if any) and any identifiers
  </br>introduced in the procedures basic declarations</li>
  <li>Names in nested procedures follow this pattern</li>
</ul>

## (cont'd.)
<ul>
  <li>TinyAda's parser uses a stack of symbol tables
    <ul>
      <li>When each new scope is entered, a new table is
      </br>pushed onto the stack</li>
      <li>When a scope is exited, the table at the top of the
      </br>stack is popped off the stack</li>
    </ul></li>
  <li>Two classes are defined to support scope analysis:
    <ul>
      <li><code>SymbolEntry:</code> holds information about an identifier</li>
      <li><code>SymbolTable:</code> manages the stack of scopes</li>
    </ul>
  </li>
</ul>

<table>
  <thead>
    <caption>Table 7.1 The interface for the <code>SymbolTable</code> class</caption>
    <tr>
      <th><code>SymbolTable</code> Method</th>
      <th>What it does</th>
    </tr>
  </thead>
  
  <tbody>
  <tr>
    <td><code>SymbolTable(Chario c)</code></td>
    <td>Creates an empty stack of tables, with a reference to a
</br><code>Chario</code> object for the output of error messages.</td>
  </tr>
    <td><code>void enterScope()</code></td>
    <td>Pushes a new table onto the stack</td>
  <tr>
  </tr>
    <td><code>void exitScope();</code></td>
    <td>Pops a table from the stack and prints its contents.</td>
  <tr>
    <td><code>SymbolEntry enterSymbol(String name)</code></td>
  <td>If <code>name</code> is not already present, inserts an entry for it into the
    </br>table and returns that entry; otherwise, prints an error message
    </br>and returns an empty entry</td>
  </tr>
  <tr>
    <td><code>SymbolEntry findSymbol(String name);</code></td>
  <td>If <code>name</code> is already present, returns its entry; otherwise, prints
    </br>an error message and returns an empty entry.</td>
  </tr>
  </tbody>
</table>
