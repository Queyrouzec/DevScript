# DevScript
A superset of Javascript

This is an initial set of opinions on what a version of javascript made for developers would look like and is currently very tentative.

Because this is an initial opinion, outside input is strongly encouraged.
Much of this takes inspration from Dart, Rust, and other functional languages.
The syntax in this README is not the planned upon syntax, it is just what ever I thought would best convey my intent. It will be updated in the future to reflect the language.

## Goals
### Everything should be allowed to exist inline in one document

- HTML is glorified gui objects. That's not nessisarily a bad thing, but it should be better integrated with js.
- CSS is a glorified set of properties in a obscure way. This is potentially a bad thing.
- You should be allowed to write tests inline without them being compiled into the final file and you should be allowed to put them in your documentation.

### Be as close to the language as possible

- There should be no hidden compiler optimizations when reasonable. Compilation should be almost as preditcable as Typescript.
- The compiler should take no performance away from Javascript even if you can blow your foot off.
- This creates a problem with CSS because in order to make the most out of CSS you need to make use of the cascading part and give universal access to all - HTML objects. That option should still exist even if it is a massive foot gun. This makes choices with CSS very tenitive.

### Intent is built in

- The intent of the developer should be enforced by the language at every possible turn. This changes from topic to topic so we'll get into what this means further down.

### State is a first class citizen.

- State management should have it's own syntax for commen state management implementations.

### Types

- Strictly enforced. There should be no optional types, and it should be null safe.
- Types should be intimate with their declaration. Typedefs should not be seperate from their constructors.
- I have an affinity for how Dart handles null and types.
- Declairation of types will be local by default and can take the place of let.
```
Str something = "hi";
```
vs
```
let something: Str = "hi";
```
This is so that writing types will be as quick as declaration and make type declaration vs type inference a low cost choice.
- All basic types should be 3 letters in length unless there is an otherwise compelling reason.
- Types will be required for function parameters and returns. This is to keep your intent clear.

### Mutablility

- Rust style mutablility.
- Variables are immuntable by defualt; and if a function is going to change a variable, it should declare that change.

### Enums, switch statements, and match statements

- You should be able to match logical patterns.
- There should be context that require you to use all of your enums.
- Switch should be a JS switch statement while match compiles to `if(){} else if(){} else if(){} else{}`.
- You should be allowed to put exclusively classes, exclusively keywords or some other exclusive type as your enum.
- You should have to opt into matching multiple statements.
```
switch(expression) {
  case x:
    // something
  case y:
    // something
  default:
    // something
}
// vs
switch(expression) req break {
  case x:
    // something
    break;
  case y:
    // something
    break;
  default:
    // something
}
```
- Match statements shouldn't break. (tenative)

- A switch or match statement statement should be allowed to evaluate to it's value
```
String num = switch(2) eval {
  case 1:
    "one";
  case 2:
    "two";
  default:
    "three";
}
console.log(num);
// two
```

### Classes

- There should be abstract classes
- Developers should be allowed to limit the depth of classes or only allow classes to be formed from abstract classes. This should aliviate some of the - - head ache with deeply nested subclasses while giving the benifits of classes.
- You should be allowed to use Rust style traits or functions that are injected into a class.

### Code organization

- include modules
- include Elixir style aritable functions:
```
// different functions that can all be called based on what is passed to doSomething
doSomething() => 1;
doSomething(x) => x;
// named params (doSomething(x: "hi");)
doSomething(Int one: x) => x;
doSomething(Int two: y) => y;
```
- include the ability to call different functions based on parameter type like in Rust
```
doSomething(Int x) => console.log(x + 1);
doSomething(String y) => console.log(y);
doSomething("hi");
// "hi"
```
This helps discoverability, organization, and reduces the wordiness of functions in implimentation. It also allows you to seperate logic much easier.
```
searchDogByHairColor(String color) {
  // ...
}
searchDogByName(String name) {
  // ...
}
// or
searchDog((String|null) hairColor: color, (String|null) dogsName: name) {
  if (name != null) {
    // do something
  } else if(color != null) {
    // do something
  }
}
// turns into
searchDog(String hairColor: color) {
  // ...
}
searchDog(String name: name) {
  // ...
}
```

### Try Catch will stay but there will be other options to avoid hidden control flow

- There should be a built in way to propigate errors
- There will be a explicit style of error like in rust that doesn't crash the program.

## It will be written in Rust

Queue the memes, I want to rewrite JS in rust.

but why?

Rust is the low level language that most closely follows my philosophy of clear dev communication while being very fast.
There are faster low level languages but I probably won't significant use of any features outside of Rust and, it has the best developer communication out of any other low level language, meaning that for this project it'll probable end up being the fastest choice in development and speed. (bugs make things slow too!)

God bless
