Before 2024-03-11 Monday
- I learned web development through the Anacle's Framework, which is based on .NET webforms. 
- ASP.NET Web Forms is part of the ASP.NET web application framework. 
	- Web Forms are pages that your users request using their browser. These pages can be written using a combination of HTML, client-script, server controls, and server code. 
	- When users request a page, it is compiled and executed on the server by the framework, and then the framework generates the HTML markup that the browser can render.
	- I used C# to write server code/application logic (including server scripts and ORM objects). 
	- Instead of ASP.NET controls, we used customized controls under Anacle's UI Framework.
- The web development used here is very traditional: HTML + CSS with server-side scripts. 
	- Web Forms have no state, hence I had to save the state in the ORM object.
	- Event-driven programming model: when an event happens on client-side, each control can fire events which are handled by event-handlers on server-side. The underlying mechanism of capturing an event on the client, transmitting it to the server, and calling the appropriate method is all automatic and invisible to you.

2024-03-11 Monday
- React props: passing "attributes" from parent component to children component. Allows parent component to use children components independently without thinking about how the children components use the props ⇒ abstraction
- React `useEffect(setupFunction, dependencies)`: useEffect is called whenever the component is (re)connected to some external system (e.g. web APIs). 
- DOM: Document Object Model, programming interface for web documents. Allow programs to manipulate structure, content and style of web documents dynamically.
- Virtual DOM: only in React, optimize the process of updating actual DOM. It is a **in-memory*** light weight representation of the actual DOM. It is used to calculate the changes between different version of the DOM and make only the necessary changes to the real DOM.
- Component: traditionally, we pages have mostly Markups, sprinkled with JavaScript. React components are JS functions sprinkled with Markups.

2024-03-12 Tuesday
- **People often use default exports if the file exports only one component, and use named exports if it exports multiple components and values**. 
	- `export default function Button() {}` ⇒ `import Button from './Button.js';`. You can name the imported component anyway you want (e.g. `import Banana from './BUtton.js'`)
	- `export function Button() {}` ⇒ `import { Button } from './Button.js';`
- React components use a syntax extension called JSX to represent that markup. JSX looks a lot like HTML, but it is a bit stricter and can display dynamic information. ⇒ JSX is a syntax extension, while React is a JavaScript library.

2024-03-14 Thursday
- Been reading a bunch of React documentations. But it wont stick with me unless I use them in a project or write them down.
- Learn how React manages States through arrays: [link](https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e). 
	- The first time the component is rendered, all the states and its setState functions are appended to 2 arrays. 
	- The next time they are rendered, the states and corresponding setState functions are simply being read from the arrays. 
	- The setState functions hold a "pointer" to where the  corresponding state is in the array, allowing the state to be updated.
	- States behave like snapshots. setState does not change the state variable in the current render, but only in the next render. setState also ~~triggers~~ enqueues/schedules a re-render.
- Dont change objects that you hold in the React state directly. Instead, when you want to update an object, you need to create a new one (or make a copy of an existing one), and then set the state to use that copy. ⇒ immutability. **Treat state as read-only**. 
	- use spread syntax `newStudent = { ...oldStudent, id: 69 }` to shallow-copy objects.
	- useImmer is an alternative to useState, but it allows objects to be mutated directly (the library takes care of creating a new object for us)
- Render and Commit: 3 steps to modifying a component dynamically:
	1. **Triggering** a render 
	2. **Rendering** the component (create a new virtual DOM and diff it with the previous virtual DOM)
	3. **Committing** to the actual DOM  (efficiently, if there are any changes)
- A render of a parent component trigger re-renders of children component recursively ⇒ performance.

2024-03-20 Wednesday
- I have got a hang of the react framework, and gain more understanding of the useEffect, useState and rendering cycles.
- Learned about `React.memo(component)`, which prevent the child component from being re-rendered whenever the parent re-render (unless the child component itself changes state/props)
	- React normally re-renders a component whenever its parent re-renders. With `memo`, you can create a component that React will not re-render when its parent re-renders so long as its new props are the same as the old props. Such a component is said to be _memoized_.
- I really need to overcome lazyness when i debug. Just try whatever you suspect is the problem, instead of sitting there thinking aimlessly. 

2024-04-01 Monday
- I am writing my March monthly report today. Here is the reflection of what I learned:
- I was tasked with developing an autocomplete feature for my 