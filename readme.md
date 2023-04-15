# Type Assertion In TypeScript

Type assertion allows you to set the type of a value and tell the compiler not to infer it. This is when you, as a programmer, might have a better understanding of the type of a variable than what TypeScript can infer on its own. Such a situation can occur when you might be porting over code from JavaScript and you may know a more accurate type of the variable than what is currently assigned. It is similar to type casting in other languages like C# and Java. However, unlike C# and Java, there is no runtime effect of type assertion in TypeScript. It is merely a way to let the TypeScript compiler know the type of a variable.

```ts
let code: any = 123;
let employeeCode = <number>code;
console.log(typeof employeeCode); //Output: number
```

In the above example, we have a variable code of type any. We assign the value of this variable to another variable called employeeCode. However, we know that code is of type number, even though it has been declared as 'any'. So, while assigning code to employeeCode, we have asserted that code is of type number in this case, and we are certain about it. Now, the type of employeeCode is number.

Similarly, we might have a situation where we have an object that has been declared without any properties yet.

```ts
let employee = {};
employee.name = "John"; //Compiler Error: Property 'name' does not exist on type '{}'
employee.code = 123; //Compiler Error: Property 'code' does not exist on type '{}'
```

The above example will give a compiler error, because the compiler assumes that the type of employee is {} with no properties. But, we can avoid this situation by using type assertion, as shown below.

```ts
interface Employee {
  name: string;
  code: number;
}

let employee = <Employee>{};
employee.name = "John"; // OK
employee.code = 123; // OK
```

In the above example, we created an interface Employee with the properties name and code. We then used this type assertion on employee. Interfaces are used to define the structure of variables.

Be careful while using type assertion. The TypeScript compiler will autocomplete Employee properties, but it won't show any compile time error if you forgot to add the properties. For example:

```ts
interface Employee {
  name: string;
  code: number;
}

let employee = <Employee>{
  // Compiler will provide autocomplete properties,
  //but will not give an error if you forgot to add the properties
};
console.log(employee.name); // undefined;
```
