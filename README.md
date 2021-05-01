# React Best Practices

The following best practices are driven by consensus among developers and direction driven by management. 

Pull Requests are encouraged to modify/add best practices.

## 1. Favor functional components over class components.

Functional components have multiple benefits over class components. 
- Hooks provide lifecycle functionality previously exclusive to classes
- Hooks can only be used by functional components.
- Less verbose to boost readability
- Provide a speed advantage over class components

[Components and Props](https://reactjs.org/docs/components-and-props.html)

## 2. Strive to write pure functions and components.

A pillar of functional programming is writing pure functions that have minimal side effects. Making functions pure allows for easier unit testing and predictable code. In the React API, React.memo() can be used to make a functional component pure by doing a shallow prop comparison. See the examples and links below for more on this. **Sometimes in React, we must alter parent state inside of a function.**

**Pure**
```
function createOutput(var1,var2) {
    return var1 + var2;
}
```
**Not Pure**
```
let foo = 1;
function doSomething(var1,var2) {
     foo = var1 + var2; //modifying variable outside function
     return "something happened!";
}
```

[JavaScript: What Are Pure Functions And Why Use Them?](https://medium.com/@jamesjefferyuk/javascript-what-are-pure-functions-4d4d5392d49c)<br/>
[React: Pure Component](https://reactjs.org/docs/react-api.html#reactpurecomponent)



## 3. Write unit tests.

It doesn't make sense to unit test 100% of React apps. As a basic rule, it's time to unit test whenever you've created something that should yield the same output given the same input. If you don't know what to test on a component, start with testing that it's rendering what's expected.
- Unit tests benefit long term maintenance. 
- Unit tests are usually easy to write.
- Integrate 'npm run test' into your CI/CD pipelines.
- Look to QA for integration testing and E2E testing (end to end).<br/>
[Jest](https://jestjs.io/)

## 4. Before using Redux, think twice.

Redux is a powerful state management tool. However there are many great alternatives to Redux. Carefully consider using Redux in your application as it's not uncommon to edit 3 or more files for a simple feature. If you choose Redux, think about using [Redux Toolkit](https://redux-toolkit.js.org/).<br/>
</br>
More Alternatives:
- [useReducer](https://reactjs.org/docs/hooks-reference.html)
- [ContextAPI](https://reactjs.org/docs/context.html)
- [React Apollo](https://www.apollographql.com/docs/react/)
- [React Relay](https://relay.dev/)

## 5. Use Prettier for cleaner code.

Prettier is a package available in most IDE's that enables auto code formatting on save. Using Prettier enhances readability and consistency within a codebase. Below is a .prettierrc config that can be put inside of a project folder.<br/>
```
{
"semi": false,
"trailingComma": "none",
"singleQuote": true,
"printWidth": 80
}
```
[Prettier](https://prettier.io/)

## 6. Sort imports at the top of each file.

Much like Prettier, sorting imports enhances readibility and consistency within a codebase. ESLint has a configurable option to automatically sort imports by alphabetical order. Alternatively, imports can also be sorted by type. See the two examples below.

**ESLint (ABC)**
```
import * as foo from "foo.js";
import a from "a.js";
import b from "b.js";
import c from "c.js";
```
**Type (Manual)**

```
import React from "react";
import { Button } from "@material-ui/core";

import Component from "../componentFolder";
import AnotherComponent from "../anotherFolder";

import { APP_STATE } from "../../constants";
import { Field_Types } from "../../constants/fieldTypes";

import "./index.css";
```


Both styles work, just make sure your team agrees upon one or the other.

## 7. Use npx create-react-app or a similar tool.

Using the create-react-app cli primes an environment for development. This is preferred as the DIY version is difficult to maintain. 
There are other tools like create-react-app that provide a great starting environment as well.
- [Next.js](https://nextjs.org/)
- [Gatsby](https://www.gatsbyjs.com/)
- [Create React App](https://reactjs.org/docs/create-a-new-react-app.html)

## 8. Keep libraries up to date.

Being a JavaScript Library, React is built on packages of multiple different origins. Failure to keep these packages up to date can result in too many updates to handle if they are put off. We encourage teams to update packages one at a time, test, and then rollback if needed.
```
npm update
npm audit
npm audit fix
```

## 9. Follow the design patterns native to the application.

As a general rule for development, it is a good idea to follow the design patterns already set in place in an application. For example, if Redux Sagas is being used in the React App, don't introduce Redux Thunk alongside it. If Material-UI is being used, don't introduce a new components library alongside it.


## 10. Make use of code-splitting.

Code splitting is a powerful tool that enables low TTI (Time to Interactive) for end-users. If your codebase has a large component that isn't needed on first-load, lift that component off of the initial load of the application. Loadable components and React.lazy() are easy ways to accomplish this. <br/><br/>
[Loadable Components](https://loadable-components.com/)<br/>
`const BigComponent = loadable(() => import("./someBigComponent");`<br/><br/>
[React Concurrent Mode (Experimental)](https://reactjs.org/docs/concurrent-mode-intro.html)<br/>
`const BigComponent = React.lazy(() => import("./someBigComponent");`<br/>
*React Concurrent Mode is not yet recommended for production release*


## 11. Use Typescript everywhere possible

