# Angular Tutorial for Beginners: Learn Angular & TypeScript
This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 14.0.5.

## Benefits os using Angular
- Gives out applications a clean structure
- Includes a lot or re-usable code
- Makes our application more testable

**Angular is not mandatory, but makes your life a lot easier.**

#

## Architecture of Angular applications

### <u>Front-end</u> - **Client**
- Runs in a web browser;
- Includes the User Interface (UI):
  - HTML;
  - CSS;
  - TypeScript;
  - Angular.
- HTML Templates
- Presentation Logic: displaying data and responding to user actions likes what should happen when the user clicks on a button.

### <u>Back-end</u> - **Server**
- Runs in a web server;
- Responsable for data processing and store; 
- Business Logic;
- Connections with APIs and Databases.


### API - application Programming Interface 
Endpoints that are accessible via HTTP Protocol.


#

## Webpack - Compiled bundles 


- ### **polyfills.bundle.js**: All the scripts to fill the gap between the version of javascript than angular needs and the version of javascript supported by most browsers out there. 

- ### **main.bundle.js** : All the source code of the application.

- ### **styles.bundle.js**: All stylesheets stored in a javascript bundle.
- ### **vendor.bundle.js**: All the 3rt party libraries.
- ### **inline.bundle.js**

> **_NOTE:_** this is for uptomization. All this bundles are injected into the index.html javascript code.

## What is TypeScript
Is not an entire programming language. Its a **super set of javascript**. That means that every javascript code is also valid TypeScript code, but TypeScript has additional features that not exist in Javascript and are not supported by most browsers.
In TypeScript we have:
- Strong typing (is opptional, but using this feature makes the more more predictable);
- Object-oriented features like:
  - Classes
  - Interface
  - Constructor
  - Access modifiers
  - etc
- Compile-time errors;
- Great tooling

**Browser doesn't understand TypeScript** so we need to transpile the code. This a part of building the application. By default tsc transpile the TypeScript into JavaScript ES5.
> **_NOTE:_** You don't need to actual call a compiler because all the building can do it by itslef 'under the hood'. When you run your application using `ng serve`, angular CLI call tsc under the hood to transpile all out TypeScript code.

#

## TypeScript
### **Types** 
```
let a: number;
let b: boolean;
let c: string;
let d: any; 
let f: number[] = [1, 2, 3]
let g: any[] = [1, true, 'a', false]

const colorRed = 0;
const colorGreen = 0;
const colorBlue = 0;

enum Color {
    Red = 0, Green = 1, Blue = 2
};

let backgroundColor = Color.Green;

```

### **Type Assertations**
If you don't declare a var as any type, the tsc will get confused about that variable. It's always a better way (and even to read your code) that you decalre the type, but if you don't do it, you can make a call to tell at your tsc what type of the var you are using. This is a good choise to development because IntelliSense understand the info it needs to show to you.

```
let message;
message = 'abc';
let endsWithC = (<string>message).endsWith('c');
let alternativeWay = (message as string).endsWith('c');

// best way
let message: string = 'abc';
let endsWithC = message.endsWith('c');
```

### **Arrow Functions**
In c# we call this a lambda expression. In TypeScript we call it as arrow function.
```
// Old Fashing way
let log = function message(message) {
    console.log(message);
}

// Functions with more than 1 line
let doLog = (message) => { 
    console.log(message)
    console.log(message + "second Line")
};

// Functions with 1 line
let doLog = (message) => console.log(message)-;

// Function without brackets - IMO it's more unreadable for another coders
let doLog = message => console.log(message);

// Function without parameters
let doLog = () => console.log();
```

### **Interfaces**
When you have a function with a few parameters, you should declare that parameters directly on the function, but when you have many parameters, the best way to do it is using an entire Object to don't confuse the developer with a lot of properties that are passing to that specific function.
So, instead of doing something like this: 

```
let drawPoint = (x, y, a, b ,c, d, e)=> {
    // ... an implementation that uses x and y properties
}
```

You sould do something like this:

```
let drawPoint = (point)=> {
    // ... an implementation that uses x and y properties
}

drawPoint ({
    x: 1,
    y: 2
})
```

Now our function as a cleaner sintax.
However, there is a problem with this implementation. Instead of a point object, we can pass an Object without x, or y property. For example we can pass a Person object with the *name* property like this:

```
let drawPoint = (point)=> {
    // ... an implementation that uses x and y properties
}

drawPoint ({
    name : 'Guillermo'
})
```

At this moment, nowhere here we're getting a compile time error, but we know that our drawPoint implementation methods required the x and y properties, so our code will break at run time sometime. So, there are 2 solution to solve this problem. 

The first one is for simple cases and we can use what is called **inline anotation**, just like annotating the parameter with the type of the Object that you are passing by, like this:

``` 
let drawPoint = (point: {x: number, y: number})=> {
    // ... an implementation that use _x_ and _y_ properties
}
``` 
but the problem with this, as you can see, that's a little bit of verbose. Also, chances are to need this implementation in another place of your code and for that you will need to wrote the same declaration in multiple places. So in those case a better approach is to use **Interface**.

```
interface Point {
    x: number,
    y: number
}

let drawPoint = (point: Point)=> {
    // ... an implementation that use _x_ and _y_ properties
}

drawPoint ({
    x: 1,
    y: 2
})
```


### **Classes**
When you have methods and properties that have some relation with each other, you should use a class for coupling all the information about it.
With classes you can agroupate methods, properties and even interfaces.
```
class Point {
    x: number;
    y: number;
    draw() {
        console.log('X: '+ this.x + ", Y: " + this.y);
    } 
}

let point = new Point();
point.x = 1;
point.y = 2;
point.draw();
```

### **Constructor**
Constructor is a special type of subroutine called to create an object. Usually you use underscore (_) befor the name of your property so you can better understand the code when using setters and/or getters.

```
class Point {
    constructor(private _x: number, private _y: number){
    }
    
    draw() {
        console.log('X: '+ this._x + ", Y: " + this._y);
    }
}
```
Contrary to what happens in C#, that you can have various constructors, in JavaScript is only possible to have one signature of constructor. So, if you want to add some required and another optional properties, you can do it by adding a question mark (?) after the name of the property like this:
```
constructor(private _x?: number, private _y?: number){}
```

### **Access modifiers**
- _public_ - accessible from everywhere;
- _private_ - accessible within the same class only;
- _protected_ - accessible by the classes of the same package and the subclasses residing in any package;
- _default_ (no modifier specified): accessible by the classes of the same package.

#

## Angular Fundamentals

### **Components**
A component incapsulate the Data, HTML Template and the logic for a view. Allow us to **work on smaller and more mantinable pieces** that can be reused in diff places.
When you're working with a big application, you maybe need to be more carefull when design your structure, because you need to organize the components that are logically connected with each other. For that, you need to create **modules**. A module is a container for a group of related components. Evey angular app has at least one module, witch it called **app.module**. As your application grows, we need to break our **app.module** to more smaller and more mantinable modules. Each module has its responsability and its created to secure some funcionality/area in the application.

The steps to use a component:
- **Create** a component
- **Register** it in a module
- Add an element in an **HTML markup**

You can also run a command in the base folder `ng g c name_of_component`. This command will generate all the files required to create a component and also register it in a module.

> **_NOTE:_** A component should NOT include any logic other than the presentation logic. Details of how data is retrieve should be delegated to somewhere else on the application. 

### **Templates**
To binding the data in the view, we mostly use some a method called **Interpolation**.

**Interpolation** refers to embedding expressions into marked up text. By default, interpolation uses the double curly braces {{ and }} as delimiters. Something like this:

```
import { Component } from '@angular/core';

@Component({
    selector: 'courses',
    template: '<h2>{{ getTitle() }}</h2>' // <--- here we are calling a method from the class
})
export class CoursesComponent {
    title = "List of courses";

    getTitle(){
        return this.title;
    }
}
```
In this curly braces you can also write directly the var `{{ title }}`, or you can call an existing method `{{ getTitle() }}`, or even an JavaScript expression like `{{ "Title: " + getTitle() }}`. With this you can render something in our template dinamically, and then the expression will be evaluating in run-time and the value of the title field with be placeed in our DOM. If the value of this field changes at sometime in the future, Angular will automatically update the DOM. This is the concept of **data binding**, so we're binding a view to a field in this component. Whenever the value of that field changes, the view is automatically notified and updated.

### **Directives**
We use directives to manipulate the DOM:
- Add a DOM element
- Remove an existing DOM element
- Change a class or style of a DOM element

Whenever we use a directive that modifies the structure of the DOM you should prefix that directive with an * like this:

```
@Component({
    selector: 'courses',
    template: `
        <h2>{{ getTitle() }}</h2>
        <ul>
            <li *ngFor="let course of courses"></li> // <--- prefix the directive with an *
        </ul>
    `
})
```

### **Services**
Whenever you need to get **data from a server** or something outside of your application you need to use another building block of Angular called **Service**.
The convention used to name a Service is: `name_of_component.service.ts`.
Inside of this class we will add the next code:
```
export class CoursesService {
    getCourses(){
        return ["course1", "course2", "course3"];
    } 
}
```
and then replace the `courses.component.ts`:
```
import { CoursesService } from './course/courses.service'; // <--- import the service
export class CoursesComponent {
    title = "List of courses";
    courses;

    constructor(){
        let service = new CoursesService(); // <--- create the instance
        this.courses = service.getCourses(); // <--- call the method
    }
}
```

This implementation works, but it gives to the code a high coupling and that's not good.
So for us to improve this implementation we can use **Dependency Injection**, because if we in sometime change the CoursesService constructor to now recieve a parameter, we will need to change in all the places that we are using this service. 
> **_NOTE:_** High coupling means that a change in one place can have unknown effects in unknown other places. It means that your code is harder to understand because complex, intertwined relationships are difficult to understand.
Angular has Dependency Injection built to it. In order that to work we need to change a litle bit our code. So, in `courses.component.ts` we need to change the constructor to recieve the service by param, like this:

```
constructor(service: CoursesService){ // <--- recieve the service by parameter
    this.courses = service.getCourses();
}
```
After that we need to register this dependencies somewhere in our module, so now we need to go to app.module.ts and add to all the dependencies that components in this module are depending upon.
In this case the `courses.component.ts` are depending of the `courses.service.ts`, so we need to register it in the providers like this:

``` 
...
providers: [
    CoursesService
],
...
``` 
> **_NOTE:_** If you forget this step, Angular will thrown an error like "No provider for CoursesService".
When you register a dependency as a provider in a module, Angular will create a single instance of that class in that entire module. So, imagine in this modules contains 100 components, and 50 of them need the CoursesService, in the memory we're gonna have only a single instance of CoursesServices and Angular will pass the same instance to all of that components. This is what we call a **Singleton pattern**.

You can also run a command in the base folder `ng g s name_of_service`. This command will generate all the files required to create a service and but, contrary to creating an component, this command does not register it in a module.


 
# Development Server Information

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

#