Q. When does Illegal shadowing happen? 
- While shadowing a variable, it should not cross the boundary of the scope, i.e. we can shadow var variable by let variable but cannot do the opposite. So, if we try to shadow let variable by var variable, it is known as Illegal Shadowing and it will give the error as “variable is already defined.”

Q. Some common things to know about Shadowing?
- Shadowing is based on lexical scoping rather than memory scope. 
- There is no hierarchy in memory scopes(global, script, block)


Q. Why is a new Lexical Environment for each iteration of for loop?
- In JavaScript, when you declare a variable with let inside a block, such as a for loop, a new lexical environment (scope) is created for each iteration of the loop. This behavior ensures that each iteration of the loop has its own distinct variable i, scoped only to that iteration.

- The reason for this behavior is to prevent a common issue known as "closure capture" or "variable capture" in JavaScript. Consider the following example: 

  ```
  let functions = [];
  for (let i = 0; i < 3; i++) {
      functions.push(function() {
          console.log(i);
      });
  }
  
  functions.forEach(func => func());
  ```


In this example, you might expect that each function pushed into the functions array would log the value of i at the time it was created in the loop. However, if i were bound to a single scope shared across all iterations, all the functions would log the final value of i, which is 3. This is because by the time any of the functions execute, the loop has already finished, and i has the final value of 3.

By creating a new lexical environment for each iteration of the loop when i is declared with let, each function captures a different i, preserving the value of i at the time the function was created. This ensures that each function in the functions array logs the value of i specific to its iteration.


Q. But the closures always preserve the reference to the variable not the value? Then how is the above true?
- You're correct that closures in JavaScript preserve references to variables, not their values at the time of creation. This is an important concept to understand when working with closures.

```
let functions = [];
for (let i = 0; i < 3; i++) {
    functions.push(function() {
        console.log(i);
    });
}

functions.forEach(func => func());
```

- In this example, each function pushed into the functions array captures a reference to the variable i, not its value. So, when each function executes during the forEach loop, it looks up the current value of i in its lexical scope. Since i was declared with let, each function has its own lexical scope for i corresponding to the iteration it was created in.

Therefore, each function, when executed, logs the value of i from its own lexical scope. In the first iteration, i is 0, in the second iteration, i is 1, and in the third iteration, i is 2.

So, while closures in JavaScript preserve references to variables, the behavior observed in the example is due to the fact that each closure captures a reference to a different lexical environment corresponding to each iteration of the loop. This creates the expected behavior of logging 0, 1, and 2 respectively.


Q. Is lexical scope same as execution context?

- Lexical scope and execution context are related concepts in JavaScript, but they are not the same thing.
- Lexical Scope: Lexical scope refers to the scope of variables defined in your code at the time of writing, determined by their location within the code's structure. In JavaScript, scope is defined by the placement of functions and blocks of code. When a function is defined within another function, it creates a nested scope where the inner function has access to variables in the outer function's scope. This access is based on where the variables are physically located in the code.
- Execution Context: Execution context, on the other hand, refers to the environment in which JavaScript code is executed. Every time JavaScript code is run, it is run within an execution context. This context includes information such as the scope chain (which determines variable access), the this keyword binding, and other execution-related details. There are different types of execution contexts in JavaScript, including the global context, function context, and eval context.
While lexical scope determines the accessibility of variables based on where they are written in the code, execution context manages the execution of code and provides the necessary environment for that execution. Lexical scope is static and determined by the structure of the code, whereas execution context is dynamic and changes as code is executed.

Q. Is Lexical scope and lexical environment same?

- Lexical scope and lexical environment are closely related concepts in JavaScript, but they are not the same thing.

- Lexical Scope: Lexical scope refers to the scope of variables defined in your code at the time of writing, determined by their location within the code's structure. It determines the visibility and accessibility of variables in a particular context. Lexical scope is based on where variables and functions are physically located within the code, and it is established statically at compile time.
- Lexical Environment: A lexical environment, on the other hand, is an internal JavaScript data structure that holds identifier-variable mapping (i.e., variable names and their associated values) created during the execution of a program. A lexical environment consists of two components:
Environment Record: This component stores identifier bindings and their values. It can be thought of as a table that maps variable names to their values.
- Outer Lexical Environment Reference: This component is a reference to the lexical environment in which the current lexical environment was created. This reference allows for nested scopes to access variables from outer scopes.
In simpler terms, lexical scope refers to the visibility and accessibility of variables based on their location in the code, while a lexical environment is the data structure that holds information about variables and their values during code execution. Lexical scope is a concept, while a lexical environment is a concrete data structure used by JavaScript engines to manage scope and variable access.

Q. Is execution context same as lexical environment.
- No, execution context and lexical environment are not the same thing, although they are closely related concepts in JavaScript.

- Execution Context: An execution context is an abstract concept that encompasses all the necessary information for the JavaScript engine to execute a piece of code. This includes details like the scope chain, the value of the this keyword, the reference to the outer lexical environment (for nested scopes), and other execution-related details. Execution contexts are created and managed by the JavaScript engine during the execution of code.

- Lexical Environment: A lexical environment is a data structure used by JavaScript engines to keep track of variable declarations and their values during the execution of code. It consists of two components:
	- Environment Record: This component stores identifier-variable bindings and their values. It's like a table that maps variable names to their values.
	- Outer Lexical Environment Reference: This component is a reference to the lexical environment in which the current lexical environment was created. It allows for nested scopes to access variables from outer scopes.

- While every execution context has a corresponding lexical environment, they are not the same thing. An execution context is broader in scope, encompassing all the details necessary for code execution, while a lexical environment is a specific data structure used to manage variable access and scope during execution.

Q. Graphical Representation of GEC for let-based for-loop?
```
Global Execution Context
│
└─── Lexical Environment: global
     │
     ├─── Environment Record: 
     │    ├─── i: undefined
     │    └─── (Other global variables)
     │
     └─── Outer Lexical Environment Reference: null
     
     Loop Execution Context (single context, but multiple lexical environments)
     │
     ├─── Lexical Environment: loop #1
     │    │
     │    ├─── Environment Record: 
     │    │    ├─── i: 0
     │    │    └─── (Other variables in the loop block)
     │    │
     │    └─── Outer Lexical Environment Reference: Reference to global lexical environment
     │
     ├─── Lexical Environment: loop #2
     │    │
     │    ├─── Environment Record: 
     │    │    ├─── i: 1
     │    │    └─── (Other variables in the loop block)
     │    │
     │    └─── Outer Lexical Environment Reference: Reference to global lexical environment
     │
     ├─── Lexical Environment: loop #3
     │    │
     │    ├─── Environment Record: 
     │    │    ├─── i: 2
     │    │    └─── (Other variables in the loop block)
     │    │
     │    └─── Outer Lexical Environment Reference: Reference to global lexical environment
```
At the beginning, we have the Global Execution Context, which includes the global lexical environment. This environment contains all global variables and functions.
Inside the loop, a new Execution Context (lexical environment) is created for each iteration of the loop. Let's call it "loop #1". This lexical environment has its own Environment Record, which holds the variable i initialized to 0.
Each iteration of the loop has its own lexical environment with a fresh copy of the loop variable i, scoped only to that iteration.
The "Outer Lexical Environment Reference" in the loop's lexical environment points to the global lexical environment, allowing access to global variables from within the loop.

Q. Global Execution Context Diagram for var based for looping
```
Global Execution Context
│
└─── Lexical Environment: global
     │
     ├─── Environment Record: 
     │    ├─── (Global variables)
     │    └─── i: undefined
     │
     └─── Outer Lexical Environment Reference: null
     
     Loop Execution Context (single context, but shared lexical environment)
     │
     └─── Lexical Environment: loop
          │
          ├─── Environment Record: 
          │    ├─── (Variables declared inside the loop block)
          │    └─── i: <current value>
          │
          └─── Outer Lexical Environment Reference: Reference to global lexical environment
```
Explanation:

The Global Execution Context remains the same as before.
Inside the loop, there's only one lexical environment shared across all iterations, as variables declared with var are function-scoped (or globally scoped if declared in the global scope). This lexical environment is part of the same execution context as the global environment.
The loop's lexical environment contains the loop variable i, whose value changes with each iteration.
Since var declarations are hoisted to the top of their enclosing function or global scope, the variable i is effectively declared once and shared across all iterations of the loop within the same lexical environment.
The outer lexical environment reference in the loop's lexical environment still points to the global lexical environment, allowing access to global variables from within the loop.
