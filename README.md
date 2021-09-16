# startToLearnTypeScript

## Main Content:
 * [Interface Type](https://github.com/IT-nhan326/startToLearnTypeScript/blob/main/README.md#interface-types)
 * [Generic Type](https://github.com/IT-nhan326/startToLearnTypeScript/blob/main/README.md#2-composing-type--create-complex-types-by-combining-simple-ones)
 * [Best Practice of TS](https://github.com/IT-nhan326/startToLearnTypeScript/blob/main/README.md#3-best-practice-of-typescript)
 * [Refferences](https://github.com/IT-nhan326/startToLearnTypeScript/blob/main/README.md#references)

## [TypeScript](https://www.typescriptlang.org) : 
 * TypeScript offers all of JS's features + TypeScript's type system
 * TypeScript check language primitives like `string` and `number` which will highlight unexpected behavior in the code => lowering the chance of bugs

### 1. Defining Types :
### Interface Types
  * Explicitly describe the object's shape using `interface` declaration : 
```
* interface User { 
     name : string ; 
     id : number; 
   }
=> declare a JS object have the shape of "interface" by using syntax " : TypeNane"

* const user: User = { 
     name: 'Newgate', 
     id: 0, 
   } 
=> if provided object that does not match the interface provided, Typescript will warn you
```

  * Interface declaration with classes : 
```
interface User {
   name: string;
   id: number;
 
class UserAccount {
   name: string;
   id: number;
   
   constructor(name: string, id: number) {
      this.name = name;
      this.id = id;
   }
 }
 
 const user: User = new UserAccount('Newgate', 1)
```

 * Use interfaces to annotate parameters and return value to functions : 
```
function getAdminUser(): {...}

function deleteUser(user: User){...}
```

 * Extending an interface
```
interface Animal { name: string }
interface Bear extends Animal { honey: boolean }
const bear = getBear()
bear.name
bear.honey
```

### 2. Composing Type : 
 #### 1. TypeScript Basic Types : 
* `string, number, undefined, null, boolean, void, bigint`
* `symbol` ???
* `unknown` : ensure to declare the type when it being used
* `never` : value will never occur or return from a function
* `any` : use when you want a particular value to cause typechecking errors
* `Array Types` : to specified the type of array, you can `number[]` == `Array<number>` or `string[]` ...
* `Function Types` :

_Add return type annotations : 
```
function getFavoriteNumber(): number { return 26 }
```

_Parameter Type Annotations :  
```
function greet(name: string) {
   console.log('Hello," + name.toUpperCase()+ " !!")
}
```
_Anonymous Functions : TypeScript can determine the type without your declaration

* `Object Types` : Prefer to any JS value with properties

_Function takes a point-lke object :
```
function printCoord(pt: { x: number; y: number}){
    console.log("The coordinate's x value is " + pt.x)
    console.log("The coordinate's y value is " + pt.y)
}
printCoord({ x : 3 , y : 7 })
```
=> The type part of each property is optional. If it is not specified, type will be `any`

_Optional Properties : Object types can also specify that properties are `optional`. To do this, add `?` after the property name
```
function printName(obj: { first: string; last?: string}){...}
=> both OK
printName({ first: Newgate })
printName({ first: Newgate, last: "Phan" })
```
***Note*** : remember to check for `optional` properties before using it because its value maybe `undefine`
```
to check for undefine val with JS mordern syntax : 
=> console.log(obj.last?.toUpperCase())
```


 #### 2. Composing Type : create complex types by combining simple ones
  1. Union Types : 
```
function printID( id: number | string){console.log("Your ID is " + id)}
=> These are ok options :
printID(101)
printID("202")
Not Ok : 
printID({ id: 2233 })
```

_TypeScript will only allow you to do things with the Union if that thins is valid for **every member** of the Union:
```
function printID( id: number | string){
    console.log(id.toUpperCase())
}
=> error because toUpperCase does not exist on type 'number'
=> Solution :
   Use if(typeof id ==="string") - else to wrap the executation of String method
```

  2. [Generic Types](https://www.typescriptlang.org/docs/handbook/2/generics.html) : one of the main tools in the toolbox for creating reusable components is generics, that is, being able to create a component that can work over a variety of types rather than a single one. This allows users to consume these components and use their own types.

_Don't ever use types `Number`, `String`, `Boolean`, `Symbol`, `Object`. These types prefer non-primitive boxed objects that are almost never used in JS code
_Use types `number`, `string`, `boolean`, `symbol`, `object` 




### 3. Best Practice of TypeScript
1. Use correct data type annotaion (void 'any')
2. Enable stick check on (configure `strict` in tsconfig file)
3. Use `let` instead of `var`
4. General types - prefer to use [primitive types](https://github.com/IT-nhan326/startToLearnTypeScript/blob/main/README.md#2-composing-type--create-complex-types-by-combining-simple-ones)
5. Callback types : using `void` for callback types instead of `any` to prevent unchecked
```
function cal(x: () => any/void ){
   var y = x()
   y.doAnything()  => ok but unchecked with any, this will throw error with void
}
```
6. Function parameters :  
* function with many parameters with the same type => change function to take object parameter
* calling object to prevent calling with wrong order
```
function cal(x: string, y: string, z: string){}
cal(x,y,z)
=>Replace with:
function cal(obj: {x: string, y: string, z: string})
cal({x,y,z}) will easier to spot mistake and review code
```
7. Don't use "bind" : `bind` returns `any`

8. Non exising value - prefer to use undefinded : 
* When a value on object or function parameter is missing, can use TypeScript optional `?` to say so
* TypeScript `?` operator doesn't handle null value

9. Use tuples for fixed length arrays
10. Use type aliases in repetitive data types : 
```
type Details = {name: string, age: number}
let man: Details = {name = 'Newgate', age = 25}
let woman: Details = {name = "Katy", age = 20}
```
11. Use access modifiers for class members : protected | private | default | public


## References:
  1. Practice with React. Section 27 from series
**React - The Complete Guide (incl Hooks, React Router, Redux)** of **Maximilian Schwarzmüller** on **Udemy**

  2. [typescriptlang.org](https://www.typescriptlang.org/)
  3. [TypeScript Best Practice](https://engineering.zalando.com/posts/2019/02/typescript-best-practices.html)
