# Angular 2 Development with TypeScript

**Created**: Monday, January 16, 2017 09:06:37 PM -05:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


[https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle\_split\_008.html](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_008.html)

# Chapter 1.&#160;Introducing Angular 2

Angular 2 is an open source JavaScript framework maintained by Google. It’s a complete rewrite of its popular predecessor, AngularJS. Angular applications can be developed in:

1. JavaScript (using the syntax of ECMAScript 5 or 6),
2. Dart, or
3. TypeScript.

## Prerequisites

In this book, we don’t expect you to have any experience with AngularJS<span style="background-color:yellow">. We do expect you to know the syntax of JavaScript</span> and HTML and to understand what web applications consist of. We also assume that you know what CSS is and that you’re familiar with the role of the DOM object in a browser.

## Note

This book is about the Angular 2 framework, and for brevity we’ll call it Angular throughout. If we mention AngularJS, we’re talking about the 1.x versions of this framework.

Whereas AngularJS was MVC-based, Angular is not. This framework doesn’t include UI components.

<mark style="background: #FFF3A3A6;">Jasmine&amp;#160;is an open source framework for testing JavaScript code.</mark>
1. Jasmine doesn’t require a DOM object. It includes a set of functions that test whether certain parts of your application behave as expected.
2. <mark style="background: #FFF3A3A6;">Jasmine is often used with Karma, which is a test runner that allows you to run tests in different browsers.</mark>

Bootstrap&#160;is an open source library of UI components developed by Twitter. The components are built using the responsive web design principles, which makes this library extremely valuable if your web application needs to automatically adjust its layout depending on the screen size of the user’s device. In this book we’ll use Bootstrap while developing a sample online auction application.

## Note

Google developed a library of UI components based on the set of guidelines called Material Design, which may become an alternative to Bootstrap. Material Design is optimized for cross-device use and comes with a set of nice-looking UI components. At the time of writing, only the AngularJS version of Material Design is ready. The Angular version of this library is called [Angular Material](https://github.com/angular/material2), and it should be released shortly after this book is published.

1. npm install @angular/material

Node.js&#160;(or&#160;Node) isn’t just a framework or a library, but a runtime environment as well. In most of this book, we’ll use the Node runtime&#160;for running various utilities like Node Package Manager (npm). For example, to install TypeScript, you can use npm from a command line:

npm install typescript

The Node.js framework can be used to develop JavaScript programs that run outside the browser. You can develop the server-side layer of a web application in JavaScript or Typescript; you’ll write a web server using Node in&#160;[chapter 8](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_015.html#ch08). Google developed a high-performance V8 JavaScript engine for the Chrome browser, and it can be used to run code written using the Node.js API. The Node.js framework includes an API to work with the filesystem, access databases, listen to HTTP requests, and more.

Members of the JavaScript community have built lots of utilities that are useful for developing web applications, and with the help of Node’s JavaScript engine, you can run them from a command line.

## Glossary

| Directives | custom HTML tags and attributes |
| --- | --- |
| Controllers | Defines the application&#39;s data flow.  JavaScript objects containing properties and functions. |
| Component | The centerpiece of the new Angular 2 architecture, often a class written in TypeScript prepended with a&#160;@Component&#160;metadata annotation (a.k.a. decorator), which also contains the&#160;template&#160;property that declares an HTML fragment to be rendered by the browser. |
| Service | <br /> |
| Module | A TypeScript class&#160;prepended with a&#160;@NgModule&#160;metadata annotation&#160;represents a module. |

The Angular framework is better performing than AngularJS. It’s easier to learn, the application architecture has been simplified, and the code is simpler to write and read. This section contains a high-level overview of Angular, highlighting the improvements made since AngularJS. For a more detailed architectural overview of Angular, see the product documentation at&#160;https://angular.io/docs/ts/latest/guide/architecture.html.

First of all, an Angular application consists of standard modules in ECMAScript 6 (ES6), <span style="background-color:yellow">Asynchronous Module Definition</span> (AMD), and CommonJS formats. Typically, one module is one file. There’s no need to use a framework-specific syntax for loading and using modules. Use the universal module loader&#160;SystemJS&#160;(covered in&#160;[chapter 2](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_009.html#ch02)), and add&#160;import&#160;statements to use functionality implemented in the loaded modules. You don’t need to worry about the proper order of the&#160;&lt;script&gt;tags in your HTML files. If module A needs the functionality from module B, just import module B into module A.

To summarize, Angular is simpler than AngularJS for several reasons:

- Each building block of your app is a component with the well-encapsulated functionality of a view, controller, and auto-generated change detector.
- Components can be programmed as annotated classes.
- You don’t have to deal with scope hierarchies.
- Dependent components are injected via the component’s constructor.
- Two-way binding is turned off by default.
- The change-detection mechanism was rewritten and works faster.

## Note

Although Angular is a complete redesign of AngularJS, <span style="background-color:yellow">if you use AngularJS you can start writing code in Angular style by using&amp;#160;ng-forward&amp;#160;(see&amp;#160;</span>https://github.com/ngUpgraders/ng-forward<span style="background-color:yellow">)</span>. The other approach (ng-upgrade) is to gradually switch to a newer version of this framework by running Angular and AngularJS in the same application (see&#160;https://angular.io/docs/ts/latest/guide/upgrade.html), but this will increase the size of the application.

## 1.4. AN ANGULAR&#160;DEVELOPER’S&#160;TOOLBOX

The following rather long list identifies languages and tools that professional Angular developers use. Not all of them are needed for developing and deploying any given application. We’ll use only half of them in this book:

1. <span style="background-color:yellow">JavaScript</span> is a de facto standard programming language for the front end of web applications. ES6 is the latest standardized specification for scripting languages, and JavaScript is its most popular implementation.
2. <span style="background-color:yellow">TypeScript</span> is a superset of JavaScript that makes developers more productive. TypeScript supports most of the features of ES6 and adds optional types, interfaces, metadata annotations, and more.
3. The <span style="background-color:yellow">TypeScript code analyzer</span> uses type-definition files for code that’s not originally written in TypeScript. DefinitelyTyped is a popular collection of such files describing the APIs of hundreds of JavaScript libraries and frameworks. Using type-definition files allows the IDEs to provide context-sensitive help and highlight errors. You’ll be installing type-definition files from the @types organization of npmjs.org (see&#160;[appendix B](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_019.html#app02)).
4. Because most web browsers support only ECMAScript 5 (ES5) syntax, you’ll need to&#160;<span style="background-color:yellow">transpile</span> (convert from one language to another) the code written in TypeScript or ES6 to ES5 for deployment. Angular developers may use Babel, Traceur, and <span style="background-color:yellow">the TypeScript compiler</span> for code transpiling (see&#160;[appendixes A](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_018.html#app01)&#160;and&#160;[B](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_019.html#app02)&#160;for details).
5. <span style="background-color:yellow">SystemJS</span> is a universal module loader that loads modules created in ES6, AMD, and CommonJS standards.
6. <span style="background-color:yellow">Angular CLI</span> is a code generator that allows you to generate new Angular projects, components, services, and routes, as well as build the application for deployment.
7. <span style="background-color:yellow">Node.js</span> is a platform built on Chrome’s JavaScript engine. Node includes both a framework and a runtime environment for running JavaScript code outside of the browser. You won’t be using the Node.js framework in this book, but you’ll use its runtime to install the required tools for developing Angular applications.
8. <span style="background-color:yellow">npm</span> is a package manager that allows you to download tools as well as JavaScript libraries and frameworks. This package manager has a repository of thousands of items, and you’ll use it for installing pretty much everything from developer tools (such as the TypeScript compiler) to application dependencies (such as Angular 2, jQuery, and others). npm can also be used for running scripts, and you’ll use this feature to start HTTP servers as well as for build automation.
9. <span style="background-color:yellow">Bower</span> used to be a popular package manager for resolving application dependencies (such as for Angular 2 and jQuery).&#160;<span style="background-color:lime">We don’t use Bower any longer because everything we need can be downloaded using npm.</span>
    1. <mark style="background: #FFF3A3A6;">Go read this post: <a href="http://stackoverflow.com/questions/21198977/difference-between-grunt-npm-and-bower-package-json-vs-bower-json">http://stackoverflow.com/questions/21198977/difference-between-grunt-npm-and-bower-package-json-vs-bower-json</a></mark>
    2. <mark style="background: #FFF3A3A6;">You can start with Angular 2 project here&amp;#160;<a href="https://github.com/AngularClass/angular2-webpack-starter" style="font-family:Arial;font-size:9.5pt">github.com/AngularClass/angular2-webpack-starter</a></mark>
10. <span style="background-color:yellow">jspm</span> is yet another package manager. Why do we need another one if npm can take care of all dependencies? <span style="background-color:yellow">Modern web applications consist of loadable modules, and jspm integrates SystemJS, which makes loading modules a breeze.</span> In&#160;[chapter 2](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_009.html#ch02), we’ll give you a brief comparison of npm and jspm.
11. <span style="background-color:yellow">Grunt</span> is a task runner. Lots of steps need to be performed between developing and deploying the code, and all these steps must be automated. You may need to transpile code written in TypeScript or ES6 into widely supported ES5 syntax, and the code, images, and CSS files need to be minimized. You may also want to include the tasks that will check the code quality and unit-test your application. With Grunt, you can configure all the tasks and their dependencies in a JSON file so the process is 100% automated.
12. <span style="background-color:yellow">Gulp</span> is yet another task runner. It can automate tasks just as Grunt does, but instead of configuring the process in JSON, <span style="background-color:yellow">you program it in JavaScript. This allows you to debug it if need be.</span>
13. <span style="background-color:yellow">JSLint</span> and <span style="background-color:yellow">ESLint</span> are code analyzers that look for problematic patterns in JavaScript programs or <span style="background-color:yellow">JSON-formatted documents</span>. These are code-quality tools. Running a JavaScript program through JSLint or ESLint results in a number of warning messages suggesting how you can improve the code quality of the program.
14. <span style="background-color:yellow">TSLint</span> is a code-quality tool for TypeScript. It has a collection of extendable rules to enforce the recommended coding style and patterns.
15. <span style="background-color:yellow">Minifiers</span>, like <span style="background-color:yellow">UglifyJS</span>, make files smaller. In JavaScript they remove code comments and line breaks, and they make variable names shorter. Minification can also be applied to HTML, CSS, and image files.
16. <span style="background-color:yellow">Bundlers</span>, such as <span style="background-color:yellow">Webpack</span>,&#160;combine&#160;multiple files and their dependencies into a single file.
17. Because JavaScript syntax is very forgiving, the application code requires testing, so you’ll need to pick one of the testing frameworks. In this book, you’ll use the [Jasmine](https://jasmine.github.io/) <span style="background-color:yellow">framework</span> and the <span style="background-color:yellow">test runner called</span> [Karma](https://karma-runner.github.io/1.0/index.html).
18. Both JavaScript and TypeScript are well supported by modern IDEs and text editors such as WebStorm, <span style="background-color:yellow">Visual Studio</span>, <span style="background-color:yellow">Visual Studio Code</span>, Sublime Text, Atom, and others.
19. All major web browsers come with developer tools that allow you to debug your programs right inside the browser. Even if the program was written in TypeScript and deployed in JavaScript, you can debug the original source code using source maps. We use <span style="background-color:yellow">Chrome Developer Tools</span>.

## Note

Programming in Angular is much simpler than in AngularJS, but the initial setup of the application is more involved because you’ll be using transpilers and module loaders, which were not required for developing with JavaScript and AngularJS. In general, the introduction of ES6 modules changes the way applications will be loaded to the browser in the future, and we’ll use the new approach in this book.

[Figure 1.5](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_008.html#ch01fig05)&#160;illustrates how tools can be applied at different stages of the development and deployment processes. The tools you’ll use in this book are shown in bold.

![Modules: &#xA;System JS, &#xA;ES6 Module Loader &#xA;Test frameworks: &#xA;Jasmine, &#xA;Angular app &#xA;Is written in &#xA;Loads &#xA;Typescript/ES6 &#xA;Is transpibed to &#xA;Uses &#xA;Code q tools: &#xA;TSLint, ESLint &#xA;Packages: &#xA;npm, JSPM &#xA;JavaScript (ES5): &#xA;tsc, Babel, &#xA;Traceur &#xA;uses &#xA;Bundled and &#xA;optimized app: &#xA;Webpac k &#xA;References &#xA;Builds and deploys &#xA;Deployed app: &#xA;npm scripts, &#xA;Grunt, Gulp ](/Attachments/1-5fe1b75f985ab440ba1f626c37fbf947.png)

Programming in Angular is easier than in AngularJS, but the initial environment setup must be done right so you can really enjoy the development process. In the next chapter, we’ll discuss the initial project setup and tooling in greater detail.

To give you a taste of how things are done in Angular, we came up with&#160;[table 1.1](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_008.html#ch01table01), which lists the tasks that you may want to do (the left column) and what the Angular/TypeScript combo offers to accomplish each task (the right column). This is not a complete list of tasks that you can do, and we show you just fragments of the syntax, but it gives you the general idea. All these features will be explained in the book.

**<span style="">Table 1.1.&amp;#160;How things are done in Angular</span>**

| **<span style="">Task</span>** | **<span style="">How</span>** |
| --- | --- |
| Implement business logic. | Create a class, and Angular will instantiate and inject it into your component. You can also use the new operator. |
| Implement a component with UI. | Create a class annotated with @Component. |
| Specify the HTML template to be rendered by a component. | Either inline the HTML code in the @Component annotation using its template property, or specify the name of the HTML file in templateUrl. |
| Manipulate HTML. | Use one of the structural directives (\*ngIf, \*ngFor), or create a custom class annotated with @Directive. |
| Refer to the class variable on the current object. | Use the this keyword: this.userName=&quot;Mary&quot;;. |
| Arrange navigation on a single-page app. | Configure the component-based router, mapping components to URL segments, and add the &lt;router-outlet&gt; tag to the template where you want the component to be rendered. |
| Display a value of a component’s property on the UI. | Place the variables inside double curly brackets on the template: {{customerName}}. |
| Bind a component property to the UI. | Use property binding with square brackets: &lt;input [value]= &quot;greeting&quot; &gt;. |
| Handle UI events. | Surround the event name with parentheses, and specify the handler: &lt;button (click)=&quot;onClickEvent()&quot;&gt;Get Products &lt;/button&gt;. |
| Use two-way binding. | Use the [()] notation: &lt;input [(ngModel)] = &quot;myComponentProperty&quot;&gt;. |
| Pass data to a component. | Annotate component properties as @Input, and bind the values to it. |
| Pass data from a component. | Annotate component properties as @Output, and use EventEmitter to emit events. |
| Make an HTTP request. | Inject the Http object into a component, and invoke one of the HTTP methods: this.http.get(&#39;/products&#39;). |
| Handle HTTP responses. | Use the subscribe() method on the result that arrives as an observable stream: this.http.get(&#39;/products&#39;).subscribe(...);. |
| Pass an HTML fragment to a child component. | Use &lt;ng-content&gt; in the child’s template. |
| Intercept modifications of components. | Use the component’s lifecycle hooks. |
| Deploy. | Use third-party bundlers like Webpack to package the application files and frameworks into JavaScript bundles. |

# Chapter 2.&#160;Getting&#160;started&#160;with Angular

Code Samples: https://github.com/Farata/angular2typescript

## Tip

If you’re not familiar with the syntax of TypeScript and ECMAScript 6, we suggest you read&#160;[appendixes A](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_018.html#app01)&#160;and&#160;[B](https://www.safaribooksonline.com/library/view/angular-2-development/9781617293122/kindle_split_019.html#app02)&#160;first, and then start reading from this chapter on.

## 2.1.1.&#160;Hello&#160;World&#160;in TypeScript

This first application will be quite minimalistic to get you quickly started programming with Angular. This application will consist of two files:
![](/Attachments/1-c2060755b95b6c46ab4e6ca4ea8b0c03.jpeg)

The code of the Angular framework consists of modules (one file per module), which are combined into libraries, which are logically grouped into packages, such as&#160;@angular/core,&#160;@angular/common, and so on. Your application has to load required packages before the application code.

Stopped at 9:35 pm (1 1/2 hours).