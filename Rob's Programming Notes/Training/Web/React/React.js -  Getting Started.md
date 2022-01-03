# React.js: Getting Started

**Created**: Saturday, April 01, 2017 01:47:09 PM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


Samer Buna

[@samerbuna](https://twitter.com/samerbuna)

https://jscomplete.com

https://edgecoders.com

https://edgecoders.com/@samerbuna

# Course Link

[React.js: Getting Started](https://app.pluralsight.com/player?course=react-js-getting-started&amp;amp;author=samer-buna&amp;amp;name=80d0eca3-47cd-4461-a875-7b1c078659dd&amp;amp;clip=0)

# Section 1: Introduction

## Introduction

1. You need to know the basics of JavaScript.
    1. Define and user variables: const/let.
    2. Classes and functions
    3. Loops and conditionals
2. Interactive Labs
    1. https://jscomplete.com/learn-javascript
    2. Requested an invite on https://slack.jscomplete.com
    3. Watch all videos from ReactConf17 -&#160;https://www.youtube.com/playlist?list=PLb0IAmt7-GS3fZ46IGFirdqKTIxlws7e0
3. Home Page
    1. https://facebook.github.io/react/
4. React is a library, not a framework.
    1. React is small.
    2. It is not a complete solution.
    3. You often need to use other libraries with React in order to form a solution.
    4. React is really good at building user interfaces.
    5. React lets you **<span style="">describe</span>** a user interface.
    6. Declarative language.
    7. Essentially the &quot;V&quot; in MVC.
        1. He&#39;s not a fan of MVC anymore, so he doesn&#39;t like this analogy.
5. React is made up of:
    1. Components
        1. Like functions.
        2. Can manage private state.
    2. Reactive Updates
        1. React will react.
        2. Take updates to browser.
    3. Virtual views in memory
        1. Write HTML in JavaScript.
        2. Using JS to render HTML enables a virtual DOM.
            1. React only writes difference between old tree and new tree.
6. Babel.js: https://babeljs.io
    1. [Babel REPL](http://babeljs.io/repl/#?babili=false&amp;amp;evaluate=true&amp;amp;lineWrap=false&amp;amp;presets=react%2Cstage-2&amp;amp;targets=&amp;amp;browsers=&amp;amp;builtIns=false&amp;amp;experimental=false&amp;amp;loose=false&amp;amp;spec=false&amp;amp;code=%5B1%2C2%2C3%5D.map%28n%20%3D%3E%20n%20%2B%201%29%3B&amp;amp;playground=true)
    2. [Learn ES 2015](http://babeljs.io/learn-es2015/) from Babel.
7. [Getting Started with ReactJS, Typescript, and Webpack](https://medium.com/@fay_jai/getting-started-with-reactjs-typescript-and-webpack-95dcaa0ed33c)

## Your First Component

1. React Components
    1. Function Component
        1. Simplest form of a React component.
    2. Class Component
        1. More featured way to define a React component.
        2. Has private internal state.
            1. This internal state gives React its reactive nature.
        3. When this internal state changes, React will automatically re-render that component.
        4. Inputs
            1. State
                1. Can be changed.
            2. Props
                1. All fixed values.
            3. Class components can only change their internal state, not their properties.
        5. <mark style="background: #FFF3A3A6;">This is a core idea to understand in React.</mark>
2. JSX
    1. React can be used without it.
3. He is using jsComplete&#39;s REPL to work through this example.
    1. https://jscomplete.com/repl
    2. No need to install or configure anything.
    3. The editor tab is on the left.
        1. This is where we write JavaScript.
        2. The latest version of React and ReactDOM are already pre-loaded here.
        3. The editor understands JSX and all the modern features of JavaScript.
        4. This lets us focus on React rather than wasting time configuring and compiling.
    4. The preview tab is on the right.
        1. Predefined mountNode element.
        2. Anything you put in this element shows up in the preview tab.
            - <span style="">Render content here using the&amp;#160;</span>**<span style="">console.log()</span>**<span style="">&amp;#160;function</span>
            - <span style="">Use React/ReactDOM with the&amp;#160;</span>**<span style="">mountNode</span>**<span style="">&amp;#160;variable</span>
            - <span style="">Use this as a simple&amp;#160;</span>**<span style="">REPL</span>**
        3. Also shows any errors in the code.
        4. Also a simple JavaScript REPL.
    5. To execute the code, press Ctrl-Enter.
4. To create a new React component, simply define a new function.

# <span style="">You can</span>

## Reusable Components

1. <mark style="background: #FFF3A3A6;">Command+/ comments and uncomments code.</mark>
2. See http://bit.ly/psreact1
3. See http://bit.ly/psreact2

# Section 2: Working with Data

## Introduction

1. https://api.github.com
2. Install the React DevTools extension.
    1. https://github.com/facebook/react-devtools
    2. Not available for Safari.
    3. Installed Chrome for macOS.
    4. Installed the React DevTools into Chrome.

## Build a GitHub Card Component

1. Determine your component structure.
2. If a component is not going to have any interaction with the user, start that component as a Function Component.
3. http://placehold.it/75
4. Test your code as often as you can.
    1. Don&#39;t write a lot of code and test it all at once.
5. Styling React components.
    1. You can use a CSS file.
    2. React uses &quot;className&quot;, not just &quot;class&quot; as HTML does.
    3. React is all about writing HTML in JavaScript.
        1. So, you can also write CSS in JavaScript.
        2. Include a &quot;style&quot; property instead of &quot;className&quot;.
    4. This is different from using inline styles.
        1. We&#39;re using JavaScript, not strings.
6. See http://bit.ly/psreact3

## Taking Input from the User

1. Ref element
2. <mark style="background: #FFF3A3A6;">Stopped at 5:10</mark>
3.