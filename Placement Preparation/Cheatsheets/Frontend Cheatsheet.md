## Contents:
1. [[#Section 1 UI/UX and Accessibility]]
2. [[#Section 2 CSS Fundamentals]]
3. [[#Section 3 JavaScript Fundamentals]]
4. [[#Section 4 TypeScript JS but better]]
5. [[#Section 5 ReactJS Fundamentals]]
6. [[#Section 6 NextJS React on Steroids]]
7. [[#Section 7 High-Performance Frontend Architecture]]
8. [[#Section 8 SEO Fundamentals]]

## Section 1: UI/UX and Accessibility
Senior developers are expected to be product-minded and build inclusive applications. This section covers essential UI/UX and accessibility principles from an implementation perspective.

### Key UI/UX Principles for Implementation
1. **Visual Hierarchy:** This principle involves arranging elements to guide the user's eye and communicate importance. Developers implement this through the correct use of heading tags (`<h1>` to `<h6>`), font weights, color contrast, and layout structures created with CSS Grid or Flexbox.

2. **Consistency:** UI elements should look and behave predictably throughout an application. This builds user trust and reduces cognitive load. Developers achieve consistency by creating and using reusable component libraries and adhering to a design system.

3. **Usability:** The UI should be intuitive. That means predictable layouts, clear labels, and feedback on interactions. Nielsen’s heuristics (visibility of system status, matching real world language, consistency, error prevention and recovery) are good guidelines. For example, always show loading indicators on async actions, and confirm destructive actions with modals or undo options.

4. **Feedback:** The interface should provide immediate and clear feedback in response to user actions. This is a core responsibility of the frontend, implemented through loading indicators, success/error messages, and form validation states.

5. **Mobile-first & responsive UX:** Design for the smallest screens first, then progressively enhance for larger displays. Buttons and form fields should be easy to tap (fingertip-friendly). Text should be legible (use relative font sizes). Keep navigation reachable (e.g., thumb zone on mobile). Conduct usability testing on actual devices.

### Web Content Accessibility Guidelines (WCAG)
WCAG provides a framework for creating accessible web content. The guidelines are organized around four core principles, known as **POUR**.

1. **Perceivable:** Users must be able to perceive the information being presented.
    - **Action:** Provide `alt` text for all meaningful images. Use captions and transcripts for multimedia. Ensure sufficient color contrast between text and background (WCAG AA requires a ratio of at least 4.5:1 for normal text).

2. **Operable:** User interface components and navigation must be operable.
    - **Action:** Ensure all functionality is accessible via a keyboard. The tab order must be logical, and focus indicators must be clearly visible. Avoid "keyboard traps" where a user cannot tab out of a component.

3. **Understandable:** Information and the operation of the user interface must be understandable.
    - **Action:** Use clear and simple language. Ensure navigation is consistent across pages. Provide helpful error messages and clear instructions for forms. Declare the page's primary language using the `lang` attribute on the `<html>` tag.

4. **Robust:** Content must be robust enough that it can be interpreted reliably by a wide variety of user agents, including assistive technologies.
    - **Action:** Write valid, semantic HTML. For custom components (e.g., a custom dropdown), use ARIA (Accessible Rich Internet Applications) attributes to define their role, state, and properties (e.g., `role="button"`, `aria-expanded="true"`).

### The Importance of Semantic HTML
Using HTML tags according to their intended meaning (`<header>`, `<nav>`, `<main>`, `<article>`, `<footer>`, etc.) has a dual benefit :
1. **Accessibility (A11y):** Ensure your UI works for users with disabilities. Use semantic HTML (e.g., `<button>` for buttons), provide `alt` text on images, ensure sufficient color contrast, and enable keyboard navigation (e.g., focus states, `tabindex`, ARIA roles). MDN emphasizes that accessibility means making sites usable “no matter an individual’s physical and cognitive abilities”. Accessible design often aligns with SEO best practices too.

2. **SEO:** Search engine crawlers use semantic tags to parse the content, identify its structure, and determine the importance of different sections. A well-structured, semantic page is easier for search engines to index and can lead to better rankings.

### Tips & Questions

> [!tip] Tips & Best Practices:
> - Regularly use browser devtools accessibility audits (e.g., Lighthouse) to catch color contrast or missing labels.
> - Structure HTML so that assistive technologies (screen readers) correctly announce content. For example, use `<label>` with `for` for form inputs.
> - Provide fallback text or status for non-text content (images, icons).
> - Ensure focus state is visible (don’t override default outlines without alternative).
> - Plan flows and wireframes before coding. Always consider “What is the user’s goal on this page?”
> - Use design systems or component libraries for consistency (e.g., Material UI, Ant Design).

> [!question] Interview Questions:
> - What is the purpose of ARIA roles and when should you use them?
> - How do you ensure a website is accessible? Name some tools or guidelines.
> - Explain the concept of responsive design and mobile-first UX?
> - Describe a time you had to optimize a UI for better usability or accessibility.
> - How would you design a feature to be intuitive for first-time users?


## Section 2: CSS Fundamentals
CSS has evolved into a powerful layout engine. A deep understanding of modern layout models like Flexbox and Grid, along with the ability to create performant animations, is a core competency for any frontend developer.

### CSS Layouts
Modern CSS provides powerful layout tools:
#### Flexbox
The Flexible Box Layout Module, or Flexbox, is a one-dimensional layout model designed for distributing space and aligning items within a container. It is considered "content-first," meaning the size of the items can influence the final layout as they flex to fill available space or shrink to fit.

- **Axes:** The core concept of Flexbox revolves around two axes:
    - **Main Axis:** The primary axis along which flex items are laid out. Its direction is controlled by the `flex-direction` property.
    - **Cross Axis:** The axis perpendicular to the main axis.

- **Key Properties:**
    - `display: flex`: Applied to the parent container to initiate a flex context.
    - `flex-direction`: Defines the **main axis**. Values can be `row` (default), `column`, `row-reverse`, or `column-reverse`.
    - `justify-content`: Aligns items along the **main axis** (e.g., `flex-start`, `center`, `space-between`).
    - `align-items`: Aligns items along the **cross axis** (e.g., `stretch`, `center`, `flex-start`).
    - `flex`: A shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`, which control the flexibility of items.

**Simple Code Example:**
```html
<div class="flex-container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

```css
.flex-container {
  display: flex;
  justify-content: space-around; /* Distributes space around items on the main (horizontal) axis */
  align-items: center; /* Centers items on the cross (vertical) axis */
  height: 100px;
  background-color: lightgray;
}
```

#### Grid
CSS Grid Layout is a two-dimensional system, designed for laying out items in both rows and columns simultaneously. It is "layout-first," meaning you define a grid structure and then place items within it. You define rows/columns and place items in cells. CSS Grid excels at complex layouts, it excels at dividing a page into major regions.

- **Terminology:**
    - **Tracks:** The space between two grid lines, creating a column or a row.
    - **Lines:** The horizontal and vertical dividing lines that make up the grid structure.
    - **Cells:** The space formed by the intersection of a row and a column track.
    - **Areas:** A rectangular space composed of one or more cells.

- **Key Properties:**
    - `display: grid`: Applied to the parent container.
    - `grid-template-columns` & `grid-template-rows`: Define the columns and rows of the grid. The `fr` unit is introduced here, representing a fraction of the available space in the container.
    - `gap`: A shorthand for `row-gap` and `column-gap`, used to create space between tracks.
    - `grid-column` & `grid-row`: Used to place items on the grid by specifying start and end lines, or by using the `span` keyword.

**Simple Code Example:**
```html
<div class="grid-container">
  <div class="item1">Header</div>
  <div class="item2">Menu</div>
  <div class="item3">Main</div>
  <div class="item4">Footer</div>
</div>
```

```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 3fr; /* Two columns, second is 3x wider */
  grid-template-rows: auto auto;
  gap: 10px;
}
.item1 { grid-column: 1 / 3; } /* Header spans both columns */
.item4 { grid-column: 1 / 3; } /* Footer spans both columns */
```

#### Flexbox & Grid: A Practical Decision Guide
The choice between Flexbox and Grid is not about which is superior, but which is the right tool for the job, a distinction that hinges on dimensionality.

|Criterion|Flexbox|Grid|
|---|---|---|
|**Dimensionality**|One-dimensional (row or column)|Two-dimensional (rows and columns)|
|**Primary Use**|Aligning items and distributing space within a container (UI components)|Overall page layout and complex, structured designs|
|**Design Approach**|Content-first (item sizes can influence the layout)|Layout-first (a grid is defined, and items are placed into it)|
|**Alignment Control**|Aligns items as a group or individually along main/cross axes|Aligns items within their grid cell/area|
|**Item Wrapping**|Items wrap onto new lines, each line acting as a new flex container|Items are placed into the next available cell in a strict grid structure|

#### **Positioning:** 
CSS provides `static` (default), `relative`, `absolute`, `fixed`, and `sticky`. Absolute positioning removes elements from normal flow relative to the nearest positioned ancestor. Fixed positions relative to viewport (good for navbars). Sticky toggles between relative and fixed based on scroll. Avoid excessive absolute positioning for main layout (it complicates responsiveness).

#### **Responsive Design:** 
Use _relative units_ (%, `vw`, `vh`, `em`, `rem`) and **media queries** to adapt to screen sizes. MDN defines responsive design as making layouts “flexible and work well across different device screen sizes”[developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design#:~:text=Responsive%20web%20design%20,be%20used%20to%20master%20it). Common pattern: Mobile-first CSS (styles for small screens by default, then `@media (min-width: ...)` for larger). Always include `<meta name="viewport" content="width=device-width, initial-scale=1">` for proper scaling on mobile. Use Flexbox/Grid’s inherent flexibility (e.g., `flex-wrap`, `minmax` in Grid) to adjust layout. CSS frameworks (like Bootstrap) or utilities (like flex containers) help build responsive components quickly.

### CSS Animations & Transitions
Both transitions and animations can bring a UI to life, but understanding their performance implications is key. CSS and JavaScript both allow for animations. In CSS, the `transition` and `animation` properties handle it:

1. **Transitions:** Simpler, designed to animate a property change between two states (e.g., a `:hover` state). They are defined with properties like `transition-property` and `transition-duration`. Example:
   ```css
	button { transition: background 0.3s; } button:hover { background: blue; }
	```

2. **Animations:** More powerful and complex, allowing for multi-step sequences defined by `@keyframes`. They offer greater control with properties like `animation-iteration-count` and `animation-direction`. Example:
   ```css
	@keyframes fadeIn {
	  from { opacity: 0; }
	  to { opacity: 1; }
	}
	.fade-in {
	  animation: fadeIn 1s ease-in-out;
	}
	```

#### Optimizations
1. **Animation Performance:** The most performant properties to animate are `transform` and `opacity`. This is because these properties can be handled by the browser's **compositor thread**, which runs separately from the main thread where layout and paint operations occur. Animating these properties does not trigger a browser **reflow** (recalculating layout) or **repaint** (redrawing pixels), resulting in smoother, hardware-accelerated animations. Animating properties like `width`, `height`, `top`, or `left` is less performant as it forces the browser to perform these expensive layout and paint calculations on every frame.

2. **JavaScript Animations**: For complex sequences or physics-based animations, you can use JS (manipulating styles or using libraries). Examples include `requestAnimationFrame` loops or libraries like GSAP, or React libraries like Framer Motion or React Transition Group. Use JS when you need fine-grained control or dynamic timing (but be mindful: JS-based animations can drop frames if main thread is busy).

3. **Accessibility – prefers-reduced-motion**: Respect user preferences. Many users disable animations. Use the `prefers-reduced-motion` media query to tone down or eliminate non-essential animations. Example:
   ```
	@media (prefers-reduced-motion: reduce) {
	  .animation { animation: none; }
	}
	```

### Tips & Questions

> [!tip] Tips & Best Practices:
> - Use Flexbox for simple 1D layouts (bars, menus, lists); use Grid for complex 2D layouts (entire page grid, image galleries).
> - Use consistent box-sizing (`box-sizing: border-box;`) so padding/borders don’t break layouts.
> - In responsive design, set images/media to be fluid (`max-width: 100%`) and use `object-fit: cover` if needed.
> - Define `alt` on images and use semantic sizes; if using CSS background images, ensure additional context for SEO.
> - When using fixed or sticky positioning, test on various devices (sticky needs appropriate parent height).
> - Use `transform` and `opacity` for animations, as they typically don’t trigger layout and are GPU-accelerated.
> - Use `will-change` sparingly (only on elements you know will animate) to hint the browser to prepare compositing.
> - Test animations at different frame rates; a smooth 60fps animation is ideal.
> - On loading states, use subtle CSS spinners or skeleton loaders to indicate progress rather than blank screens.

> [!question] Interview Questions:
> - How do `flex-direction`, `justify-content`, and `align-items` work in Flexbox?
> - How do you create a responsive two-column layout using CSS Grid?
> - What is the difference between `position: relative` and `position: absolute`?
> - When would you use Flexbox vs Grid vs Floats for layout?
> - How does the CSS `order` property work in Flexbox?
> - How do CSS transitions differ from CSS animations?
> - Give an example of creating a keyframe animation in CSS.
> - How can you animate React components on mount/unmount?
> - What does `prefers-reduced-motion` do and why use it?
> - When should you use `transform: translate()` instead of `left/top` in animations?


## Section 3: JavaScript Fundamentals
A profound understanding of JavaScript's core runtime environment is a non-negotiable prerequisite for senior frontend roles. Interviewers at leading companies frequently test these fundamentals to gauge a candidate's depth of knowledge beyond the frameworks they use. This section deconstructs the essential mechanics of the JavaScript engine.

### The Event Loop: A Visual and Conceptual Deep Dive
JavaScript operates on a single-threaded model, meaning it can only execute one piece of code at a time. The event loop is the fundamental mechanism that enables this single thread to perform non-blocking, asynchronous operations, which is the cornerstone of a responsive user interface. It is the heart of JavaScript's concurrency model.

![[Pasted image 20250818130821.png]]

#### Core Components
The event loop orchestrates the interaction between several key components of the JavaScript runtime environment:

1. **Call Stack:** This is a LIFO data structure that tracks function execution. When a script calls a function, it's pushed to the top of the stack. When the function returns, it's popped from the stack. Whatever is at the top of the stack is the currently executing function.
    ```js
    function third() {
      console.log('Third');
    }
    function second() {
      third();
    }
    function first() {
      second();
    }
    first();
    
    // Execution Order:
    // 1. first() is pushed to the stack.
    // 2. second() is pushed to the stack.
    // 3. third() is pushed to the stack.
    // 4. 'Third' is logged. third() returns and is popped.
    // 5. second() returns and is popped.
    // 6. first() returns and is popped. The stack is now empty.
    ```

2. **Web APIs / Browser APIs:** Asynchronous operations like `setTimeout`, DOM events (e.g., clicks), and network requests (`fetch`) are not handled by the JavaScript engine itself. Instead, they are passed to the browser's Web APIs, which can handle them concurrently in the background without blocking the main thread.![[Pasted image 20250818131135.png]]

3. **Callback Queue (Task Queue / Macrotask Queue):** This is a FIFO queue. When an asynchronous operation handled by a Web API completes (e.g., a timer expires or a file finishes downloading), its associated callback function is placed in the Callback Queue. These callbacks wait here until the Call Stack is empty.

4. **Microtask Queue:** This is a separate, higher-priority queue. It holds callbacks for **promises** (`.then()`, `.catch()`, `.finally()`) and other microtasks like `queueMicrotask()` and `MutationObserver`. The key distinction is that the Microtask Queue is processed after the currently executing script finishes and _before_ the event loop processes the next task from the Callback Queue (task Queue).

#### Execution Order Illustrated
The interaction between these components determines the precise order of execution, a common and critical interview topic.
```js
console.log('Start'); // 1. Synchronous

setTimeout(() => {
  console.log('Timeout Callback'); // 4. Macrotask
}, 0);

Promise.resolve().then(() => {
  console.log('Promise Resolved'); // 3. Microtask
});

console.log('End'); // 2. Synchronous
```

**Execution Walkthrough:**
1. `console.log('Start')` is pushed to the call stack, executed, and popped. Output: `Start`.
2. `setTimeout` is pushed to the stack. Its callback is handed off to the Web APIs. The timer is set for 0ms. `setTimeout` is popped from the stack.
3. `Promise.resolve().then()` is pushed to the stack. The promise resolves immediately, and its `.then()` callback is placed in the Microtask Queue. The promise handler is popped.
4. `console.log('End')` is pushed to the stack, executed, and popped. Output: `End`.
5. The main script has finished. The call stack is now empty.
6. The event loop checks the Microtask Queue. It finds the promise callback, pushes it to the call stack, executes it, and pops it. Output: `Promise Resolved`.
7. The Microtask Queue is now empty. The event loop checks the Callback Queue (Macrotask Queue). The `setTimeout` timer has already expired, so its callback is waiting.
8. The event loop takes the `setTimeout` callback, pushes it to the call stack, executes it, and pops it. Output: `Timeout Callback`.

**Final Output:**
```js
Start
End
Promise Resolved
Timeout Callback
```

The distinction between the Microtask and Macrotask queues is a deliberate design choice that ensures the logical consistency of asynchronous operations. Microtasks, such as promise resolutions, are considered part of the current task's continuation and must be completed before any new, unrelated task (like a timer or a user click) is processed. This prioritization allows promise chains to resolve predictably and as quickly as possible, which is essential for managing state updates in modern applications that rely heavily on asynchronous data flow.

### Closures in JS
A closure is a function that remembers the environment in which it was created. More formally, it's a function bundled with its **lexical environment**, giving it access to its outer scope's variables even after the outer function has finished executing. A closure is just a function object with a reference to a retained environment property which is then part of the scope when it is invoked.

**Example**
```js
function outer() {
  const secret = 42;
  function inner() {
    console.log(secret);  // inner “closes over” secret
  }
  return inner;
}
const fn = outer();
fn();  // Logs 42
```

JavaScript's scoping is **lexical** (or static), meaning a function's scope is determined by its physical placement in the source code, not by where it is called. A nested function has access to the variables of its parent function, its parent's parent, and so on, up to the global scope.

![[IMG-20250818-WA0002~2.jpg]]

#### Practical Use Cases
- **Data Encapsulation & Private State (Module Pattern):** Closures can be used to create private variables that are not accessible from the global scope, a pattern often implemented with an Immediately Invoked Function Expression (IIFE). This is a classic interview question to test a candidate's understanding of scope and privacy.
    ```js
    const counter = (function() {
      let privateCount = 0; // This variable is private to the closure
    
      function changeBy(val) {
        privateCount += val;
      }
    
      return {
        increment: function() {
          changeBy(1);
        },
        decrement: function() {
          changeBy(-1);
        },
        value: function() {
          return privateCount;
        }
      };
    })();
    
    console.log(counter.value()); // 0
    counter.increment();
    console.log(counter.value()); // 1
    console.log(counter.privateCount); // undefined (cannot be accessed directly)
    ```

- **Function Factories:** Closures allow you to create functions that are pre-configured with certain data.
    ```js
    function makeAdder(x) {
      // x is part of the closure's lexical environment
      return function(y) {
        return x + y;
      };
    }
    
    const add5 = makeAdder(5);
    const add10 = makeAdder(10);
    
    console.log(add5(2));  // 7
    console.log(add10(2)); // 12
    ```
    Here, `add5` and `add10` are closures. They share the same function body but have different lexical environments, "remembering" the value of `x` they were created with.

- **Event Handlers & Callbacks:** Closures are essential for event listeners to maintain access to variables from the scope in which they were defined, which is crucial for creating interactive UIs.

#### Memory Implications
Because closures maintain a reference to their outer scope, they can potentially lead to memory leaks if not managed carefully. If a closure holds a reference to a large object that is no longer needed, the garbage collector will not be able to reclaim that memory. This is a key consideration in long-running Single Page Applications (SPAs).

The concept of closures is fundamental to how modern React Hooks operate. When `useState` is called within a functional component, it must "remember" its state across multiple renders. A normal variable would be lost when the component function finishes executing. React's internal machinery leverages closures to solve this. The setter function returned by `useState` (e.g., `setCount`) is a closure. It "closes over" an internal state store managed by React that is specific to that component instance. When this setter is called, it's not just a simple function invocation; it's an invocation of a closure that has a persistent reference to the component's state, allowing it to schedule an update. A candidate who can draw this line from the abstract concept of closures to the practical implementation of React Hooks demonstrates a superior level of understanding.

### The "this" Keyword Demystified
The `this` keyword is one of JavaScript's most frequently misunderstood concepts. It is not a variable but a keyword whose value is determined by the **invocation context** of the function it is in, a concept known as runtime binding.

#### Contexts Explained
1. **Global Context:** When used outside of any function, `this` refers to the global object, which is `window` in browsers.
2. **Function Context (Simple Call):** When a regular function is called directly (e.g., `myFunction()`), `this` defaults to the global object in non-strict mode. In strict mode, it is `undefined`.
3. **Method Context:** When a function is called as a method of an object (e.g., `obj.myMethod()`), `this` is bound to the object the method was called on.
4. **Constructor Context:** When a function is used as a constructor with the `new` keyword, `this` is bound to the newly created object instance.
5. **Arrow Functions:** Arrow functions are unique because they do not have their own `this` binding. Instead, they lexically inherit `this` from their surrounding (parent) scope. This behavior makes them predictable and useful for callbacks.

#### Explicit Binding
You can explicitly set the `this` context for a function using the `call()`, `apply()`, or `bind()` methods.
- `func.call(thisArg, arg1, arg2)`: Invokes the function with a specific `this` context and arguments provided individually.
- `func.apply(thisArg, [argsArray])`: Similar to `call`, but arguments are provided as an array.
- `func.bind(thisArg)`: Returns a _new_ function that, when called, will have its `this` context permanently set to `thisArg`.

#### Common Pitfalls
- **Losing `this` in Callbacks:** A classic pitfall is passing an object method as a callback, which detaches it from its object context.
    ```js
    const user = {
      name: 'Alex',
      greet: function() {
        console.log(`Hello, ${this.name}`);
      }
    };
    
    setTimeout(user.greet, 1000); // Outputs "Hello, undefined" (or "Hello, " in non-strict mode)
    ```

	**Solution:** Use `.bind()` or an arrow function to preserve the context.
    ```js
    setTimeout(user.greet.bind(user), 1000); // Works correctly
    // OR
    setTimeout(() => user.greet(), 1000); // Also works correctly
    ```

- **Arrow Functions as Object Methods:** Using an arrow function for an object method is usually a mistake if that method needs to access the object's properties via `this`, because it will inherit `this` from the global scope.
    ```JS
    const counter = {
      count: 0,
      increment: () => {
        // 'this' here is not 'counter', it's the global object (window)
        this.count++;
        console.log(this.count);
      }
    };
    counter.increment(); // Will likely result in NaN or an error
    ```

### Prototypal Inheritance and the Prototype Chain
JavaScript implements inheritance through a mechanism known as **prototypal inheritance**. Instead of classes inheriting from other classes, objects inherit directly from other objects. Every object has an internal property, `[[Prototype]]`, which is a link to another object.

#### The Prototype Chain
When you try to access a property on an object, the JavaScript engine first looks for it on the object itself. If it's not found, it follows the `[[Prototype]]` link to the next object in the chain and looks there. This process continues up the chain until the property is found or the end of the chain is reached. The end of the chain is `Object.prototype`, whose own `[[Prototype]]` is `null`.

**Code Example:**
```js
const animal = {
  eats: true,
  walk() {
    console.log("Animal walks");
  }
};

const rabbit = {
  jumps: true,
  __proto__: animal // Sets the prototype of rabbit to animal (legacy syntax)
};

// Modern way to set the prototype
// const rabbit = Object.create(animal);
// rabbit.jumps = true;

console.log(rabbit.eats); // true (inherited from animal)
rabbit.walk(); // "Animal walks" (inherited from animal)
console.log(rabbit.jumps); // true (own property)
```

In this example, `rabbit` inherits properties from `animal`. When `rabbit.eats` is accessed, JavaScript doesn't find it on `rabbit` itself, so it follows the prototype link to `animal` and finds it there.

#### Interacting with the Prototype Chain
- **`Object.create(proto)`:** The modern and recommended way to create an object with a specified prototype.
- **`Object.getPrototypeOf(obj)`:** The standard way to get an object's prototype.
- **`__proto__`:** A legacy property for accessing the prototype, now discouraged in favor of the `Object` methods.

### Asynchronous JS: Promises & Async/Await
Asynchronous operations are essential for a non-blocking UI. Promises and the `async/await` syntax are the modern standards for managing them.

#### 1. Promises
A **Promise** is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. It allows you to associate handlers with an asynchronous action's eventual success or failure reason.

A Promise can be in one of three states:
1. **pending**: The initial state; the operation has not completed yet.
2. **fulfilled**: The operation completed successfully, and the promise has a resulting value.
3. **rejected**: The operation failed, and the promise has a reason for the failure.

Promises are consumed using the `.then()` and `.catch()` methods. A key feature is **promise chaining**, which allows for sequential asynchronous operations without nesting callbacks (avoiding "callback hell").
```js
fetch('https://api.example.com/data')
 .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // returns another promise
  })
 .then(data => {
    console.log('Success:', data);
  })
 .catch(error => {
    console.error('Error:', error);
  });
```

#### 2. Async/Await
`async/await` is syntactic sugar built on top of Promises, making asynchronous code look and feel more like synchronous code. It improves readability and simplifies error handling.
- **`async` function:** A function declared with the `async` keyword automatically returns a promise.
- **`await` operator:** Used inside an `async` function, it pauses the function's execution and waits for a promise to settle. If the promise is fulfilled, `await` returns the fulfilled value. If it's rejected, it throws the rejection reason.

The previous `fetch` example can be rewritten with `async/await`:
```js
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    console.log('Success:', data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchData();
```
This version is often considered more readable, especially for complex sequences of asynchronous steps, as it uses standard `try...catch` blocks for error handling.

### Tips & Questions

> [!tip] Tips & Best Practices
> - Always declare variables (`let`/`const`) at the top of their scope to avoid confusion from hoisting.
> - Use `const` by default, and `let` when reassignment is needed. Avoid `var` in modern code.
> - For async code, use `async/await` for readability, but remember to catch errors (e.g. try/catch or `.catch()`).
> - Avoid deeply nested callbacks (callback hell); instead chain Promises or use `async` functions.
> - Prefer pure functions and avoid unnecessary global variables.
> - Use `Object.create` or ES6 `class` syntax to manage prototypes in a clear way, and be aware of the `instanceof` and `hasOwnProperty` behaviors.

> [!question] Interview Questions
> - How does the JavaScript event loop work? What are the microtask and task queues?
> - What is a closure? Give an example of where a closure is useful.
> - Differences between `var`, `let`, and `const` in terms of scope and hoisting?
> - What is prototypal inheritance? How do objects inherit in JavaScript?
> - How do Promises, async/await, and callbacks differ? How does `await` work internally?
> - What are common pitfalls in asynchronous JavaScript (e.g., promise chaining errors)?


## Section 4: TypeScript: JS but better
TypeScript has become the industry standard for large-scale frontend development. It is a superset of JavaScript that adds _static typing_ and compile-time checks. In essence, any valid JavaScript is valid TypeScript, but TS allows you to annotate variables, function parameters, and return types with explicit types. This static type system can catch errors like passing the wrong type to a function or accessing a property that might not exist, _before_ you run the code. 

### Static vs. Dynamic Typing: The Core Trade-off
- **JavaScript (Dynamic Typing):** Types are checked at **runtime**. This offers great flexibility and is fast for prototyping, but can lead to runtime errors that are difficult to debug in large applications.

- **TypeScript (Static Typing):** Types are checked at **compile time**, allowing developers to catch a whole class of errors before the code is ever run in a browser. This leads to more robust and maintainable code, especially in large, collaborative projects.

### Key Features of TypeScript
1. **Static Typing:** The core feature of TypeScript. It allows you to explicitly define the types of variables, function parameters, and return values.
    ```ts
    // TypeScript
    function greet(name: string): string {
      return `Hello, ${name}`;
    }
    
    greet("World"); // OK
    // greet(123); // Compile-time error: Argument of type 'number' is not assignable to parameter of type 'string'.
    ```

2. **Interfaces and Types:** Both are used to define the "shape" or structure of an object.
    - `interface`: Can be extended by other interfaces (`extends`) and supports **declaration merging**, where multiple declarations with the same name are merged into one. This is useful for extending third-party types.
    - `type`: A type alias is more versatile. It can represent not only object shapes but also unions, tuples, primitives, and more complex mapped or conditional types. It cannot be re-opened to add new properties.

    ```ts
    // Interface for an object shape
    interface User {
      id: number;
      name: string;
    }
    
    // Type for a union of possible values
    type Status = 'success' | 'error' | 'loading';
    ```

> [!info] Best Practice:
> A common convention is to use `interface` for defining the shape of objects and for public APIs, as they are extendable. Use `type` for unions, tuples, or when you need more advanced type manipulation features.

3. **Generics:** Generics allow you to create reusable, type-safe components (functions, classes, interfaces) that can work with a variety of types without sacrificing type safety. They act as placeholders for types that are specified when the component is used.
    ```ts
    function identity<T>(arg: T): T {
      return arg;
    }
    
    let outputString = identity<string>("myString"); // Type of outputString is 'string'
    let outputNumber = identity<number>(100);      // Type of outputNumber is 'number'
    ```

### Use in Large Scale Apps

> [!success] Advantages:
> - **Type Safety:** Catch type errors early, reducing runtime bugs.
> - **Improved Readability:** Explicit types serve as documentation.
> - **Tooling:** Excellent IDE/editor support, refactoring and code navigation.
> - **Modern JS Features:** TS supports new ECMAScript features and down-compiles for older environments.
> - **Large Codebases:** Better maintainability for big projects with many contributors.

> [!missing] Drawbacks:
> - **Learning Curve:** Developers must learn type annotations, interfaces, generics.
> - **Build Step:** Code must be compiled (`tsc` or bundler), adding build complexity.
> - **Overhead:** Some projects find strict typing verbose, though it often pays off.

Use TypeScript when building large-scale applications or libraries where maintainability and type safety are priorities, especially in teams. For small scripts or prototyping, plain JavaScript may be faster. But many modern frameworks (React, Angular, Vue) and companies favor TypeScript for its safety net. Importantly, TypeScript compiles to JavaScript, so it remains widely compatible.

### Tips & Questions

> [!tip] Tips & Best Practices:
> - Start with `"strict": true` in `tsconfig.json` to enforce strong typing.
> - Use `interface` or `type` aliases to define object shapes and function signatures.
> - Leverage TS’s built-in utility types (e.g., `Partial`, `Pick`).
> - Annotate functions and public APIs with types; use `any` sparingly.

> [!question] Interview Questions:
> - Explain static typing. What are the benefits of TypeScript’s type system?
> - What is type inference? When must you explicitly annotate types?
> - How do interfaces and type aliases work? Can you give an example?
> - How does TypeScript compile to JavaScript? Are there runtime performance differences?
> - What are some common pitfalls (e.g., `any` usage, declaration merging, null/undefined checks)?


## Section 5: ReactJS Fundamentals
This section transitions from JavaScript fundamentals to their application within the React paradigm. Senior-level interviews will rigorously test a candidate's ability to write clean, performant, and maintainable React code. This requires a deep understanding of React's core rendering mechanism and its modern state management and optimization tools.

### The Virtual DOM and Reconciliation
The **Virtual DOM (VDOM)** is a programming concept where a virtual representation of the UI is kept in memory and synchronized with the "real" DOM. It is a lightweight, in-memory copy of the actual DOM elements, existing as a JavaScript object.

- **Reconciliation:** This is the process through which React updates the UI. When a component's state or props change, React creates a new VDOM tree. This new tree represents the updated UI.

- **The "Diffing" Algorithm:** Instead of re-rendering the entire page, React compares the new VDOM tree with the previous one. This comparison process, known as "diffing," identifies the minimal set of changes required to update the real DOM. React's diffing algorithm is a heuristic with a time complexity of O(n), based on two key assumptions:
    1. **Different Element Types Produce Different Trees:** If the root elements have different types (e.g., a `<div>` is replaced by a `<p>`), React will tear down the old tree and build a new one from scratch.
    2. **The `key` Prop:** When rendering a list of elements, developers can provide a unique and stable `key` prop to each item. This `key` helps React identify which items have changed, been added, or been removed, preventing it from unnecessarily re-rendering or losing the state of unchanged components.

- **Commit Phase:** After the diffing algorithm identifies the changes, React applies these updates to the real DOM in a single, batched operation. This batching is crucial for performance, as it minimizes direct and costly manipulations of the real DOM, which can trigger multiple browser reflows and repaints.

### Core React Concepts
It's crucial to understand the foundational principles of React. These concepts are the "why" behind React's architecture and are frequently tested in interviews to distinguish candidates who understand the framework from those who only know the syntax.

#### 1. Declarative vs Imperative UI
One of React's most defining features is its **declarative** nature. This is a fundamental paradigm shift from the traditional **imperative** approach to DOM manipulation.
- **Imperative (The "How"):** In traditional JavaScript or with libraries like jQuery, you write step-by-step instructions to manipulate the DOM. You explicitly tell the browser _how_ to change the UI in response to an event. You select an element, change its style, create a new element, and append it. This approach can become complex and error-prone as the application grows, because you are responsible for managing every state transition. 
  **Example (Vanilla JS):**
    ```js
    // Goal: Show a message when a button is clicked.
    const button = document.getElementById('myButton');
    const container = document.getElementById('messageContainer');
    
    button.addEventListener('click', () => {
      // We manually create and append the element.
      const message = document.createElement('p');
      message.textContent = 'Hello, World!';
      container.appendChild(message);
    });
    ```

- **Declarative (The "What"):** In React, you describe _what_ the UI should look like for any given state. You don't write the step-by-step DOM manipulation. Instead, you declare the UI as a function of the current state. When the state changes, React takes on the responsibility of figuring out the most efficient way to update the DOM to match the new state.
  **Example (React):**
    ```jsx
    import React, { useState } from 'react';
    
    function App() {
      const = useState(false);
    
      return (
        <div>
          <button onClick={() => setShowMessage(true)}>Show Message</button>
          {/* We declare that the message should appear if showMessage is true. */}
          {showMessage && <p>Hello, World!</p>}
        </div>
      );
    }
    ```

This declarative approach simplifies development by abstracting away the complexities of direct DOM manipulation, leading to more predictable and maintainable code.

#### 2. Components: The Building Blocks
Components are the core unit of a React application. They are independent, reusable pieces of code that encapsulate both the UI (JSX) and the logic that controls it.

- **Functional Components:** These are simple JavaScript functions that accept an object of properties (props) and return a React element (JSX). With the introduction of Hooks, functional components can now manage state and handle side effects, making them the modern standard for most use cases.
    ```jsx
    // A simple functional component
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    ```

- **Class Components:** These are ES6 classes that extend `React.Component`. They use a `render()` method to return JSX and manage state and lifecycle events with built-in methods. While still supported, they are **less common** in new codebases but are prevalent in legacy projects.
    ```jsx
    import React, { Component } from 'react';
    
    // A simple class component
    class Welcome extends Component {
      render() {
        return <h1>Hello, {this.props.name}</h1>;
      }
    }
    ```

#### 3. State & Props: Managing Data Flow
Understanding the distinction between state and props is fundamental to managing data in React.

1. **Props (Properties):**
    - **Purpose:** Props are used to pass data from a parent component down to a child component. This is the primary mechanism for component communication.
    - **Mutability:** Props are **read-only** (immutable). A child component must never modify its own props. If a child needs to change a value, it must ask its parent to pass down new props. This enforces a unidirectional data flow, which makes applications more predictable.
    ```jsx
    // Parent component passes a 'name' prop
    function App() {
      return <Greeting name="Alice" />;
    }
    
    // Child component receives and displays the 'name' prop
    function Greeting(props) {
      return <p>Hello, {props.name}!</p>;
    }
    ```

2. **State:**
    - **Purpose:** State is data that is managed _within_ a component. It represents information that can change over time, typically in response to user interaction.
    - **Mutability:** State is **mutable**, but it should only be updated using its designated setter function (e.g., `setState` or the function returned by `useState`). Modifying state directly will not trigger a re-render. When state is updated correctly, React automatically re-renders the component to reflect the change.
    ```jsx
    import React, { useState } from 'react';
    
    function Counter() {
      // 'count' is a state variable local to this component
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
      );
    }
    ```

#### 4. Controlled & Uncontrolled Components
This distinction primarily applies to form elements like `<input>`, `<textarea>`, and `<select>`.

1. **Controlled Components:** In a controlled component, the form element's value is controlled by React state. The component's state is the "single source of truth." Every change to the input updates the state via an `onChange` handler, and the input's `value` prop is bound to that state variable. This provides predictability and allows for real-time validation and conditional logic.
    ```jsx
    function ControlledForm() {
      const [name, setName] = useState('');
    
      const handleChange = (event) => {
        setName(event.target.value.toUpperCase()); // Example: enforce uppercase
      };
    
      return <input type="text" value={name} onChange={handleChange} />;
    }
    ```

2. **Uncontrolled Components:** In an uncontrolled component, the form data is handled by the DOM itself, just like in traditional HTML. Instead of managing the value in React state, you use a **ref** to "pull" the value from the DOM when you need it (e.g., on form submission). This approach can be simpler for basic forms but offers less control.
    ```jsx
    import React, { useRef } from 'react';
    
    function UncontrolledForm() {
      const inputRef = useRef(null);
    
      const handleSubmit = (event) => {
        alert('A name was submitted: ' + inputRef.current.value);
        event.preventDefault();
      };
    
      return (
        <form onSubmit={handleSubmit}>
          <input type="text" ref={inputRef} />
          <button type="submit">Submit</button>
        </form>
      );
    }
    ```

#### 5. Higher-Order Components (HOCs)
A Higher-Order Component is an advanced React pattern for reusing component logic. It is not a feature in the React API but a pattern that emerges from React's compositional nature.
- **Definition:** An HOC is a function that takes a component as an argument and returns a new, enhanced component.
- **Use Case:** HOCs are used for cross-cutting concerns that can be applied to multiple components, such as authentication, logging, or data fetching. The HOC wraps the original component, injecting additional props or logic.
    ```jsx
    // This is a Higher-Order Component
    function withLogger(WrappedComponent) {
      // It returns a new component...
      return function(props) {
        useEffect(() => {
          console.log(`Component ${WrappedComponent.name} mounted with props:`, props);
        },);
    
        //...that renders the original component with its props.
        return <WrappedComponent {...props} />;
      };
    }
    
    // A simple component to be enhanced
    function MyComponent({ message }) {
      return <div>{message}</div>;
    }
    
    // Enhance the component with the HOC
    const MyComponentWithLogger = withLogger(MyComponent);
    
    // Usage
    <MyComponentWithLogger message="Hello World" />
    ```

### React Hooks
Hooks are functions that allow you to "hook into" React's state and lifecycle features from functional components. They were introduced in React 16.8 to enable stateful logic in functional components, making them a powerful alternative to class components.

**Rules of Hooks:** 
1. **Only call Hooks at the top level:** Do not call Hooks inside loops, conditions, or nested functions.
2. **Only call Hooks from React functions:** Call them from React functional components or custom Hooks, not from regular JavaScript functions.

#### 1. useState
This hook is used to add state variables to functional components.
- **Syntax:** `const = useState(initialState);` 
- **Use Cases:** It can manage simple state like numbers, strings, or booleans, as well as complex state like objects and arrays.
- **Key Concepts:**
    - **Functional Updates:** When the new state depends on the previous state, it's best practice to use a functional update to avoid issues with stale state from closures. For example: `setCount(prevCount => prevCount + 1);`.
    - **Batching:** React batches state updates that occur within the same event handler to prevent multiple re-renders.
- **Example:**
```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

#### 2. useEffect
This hook lets you perform side effects in functional components. It serves the combined purpose of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` from class components.

- **The Dependency Array:** This is the most crucial part of `useEffect` as it controls when the effect runs.
    - `(empty array)`: The effect runs only once, after the initial render. This is equivalent to `componentDidMount`.
    - `[dep1, dep2]`: The effect runs after the initial render and any subsequent render where the value of `dep1` or `dep2` has changed. This is equivalent to `componentDidUpdate`.
    - No array: The effect runs after _every_ render. This should be used with caution as it can lead to infinite loops if the effect itself triggers a state update.

- **The Cleanup Function:** The function returned from `useEffect` is the cleanup function. It runs before the component unmounts and also before the effect runs again due to a dependency change. It's used for cleanup tasks like unsubscribing from an API or clearing a timer.

- **Example:**
```js
import React, { useState, useEffect } from 'react';

function Timer() {
  const = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);

    // Cleanup function
    return () => {
      clearInterval(intervalId);
      console.log('Timer cleaned up');
    };
  },); // Empty dependency array means this effect runs only once on mount

  return <h1>Timer: {seconds}s</h1>;
}
```

#### 3. useContext
This hook provides a way to pass data through the component tree without having to pass props down manually at every level, thus solving the "prop drilling" problem.

- **How it Works:**
    1. Create a context using `React.createContext()`.
    2. Wrap a parent component in the context's `Provider` and pass the shared data via the `value` prop.
    3. Any descendant component can then consume this data using the `useContext()` hook.

- **Example:**
```js
// 1. Create Context
const ThemeContext = React.createContext('light');

// 2. Provide Context
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// 3. Consume Context
function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>I am a {theme} button</button>;
}
```

#### 4. useRef
The `useRef` hook is an "escape hatch" that allows you to create a mutable reference that persists across renders without causing the component to re-render when its value changes.

- **Use Cases:**
    1. **Accessing DOM nodes:** The most common use case is to get direct access to a DOM element, for tasks like managing focus, media playback, or measuring its dimensions.
    2. **Storing a mutable value:** It can be used to store any mutable value that you want to persist across renders without triggering a re-render, such as a timer ID or a previous state value.

- **Example:**
```js
import React, { useRef, useEffect } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

#### 5. Performance Hooks: useMemo & useCallback
These hooks are used for optimization by memoizing values and functions, respectively. The core problem they solve is related to **referential equality**. In JavaScript, functions and objects are re-created on every render, getting a new reference in memory. This causes child components that are optimized with `React.memo` to re-render unnecessarily, as they receive "new" props on each render.
1. **useMemo:** Memoizes a **value**. It re-executes an expensive calculation only when one of its dependencies has changed. This is useful for avoiding costly computations on every render.
    ```js
    const expensiveValue = useMemo(() => {
      // perform expensive calculation using 'a' and 'b'
      return compute(a, b);
    }, [a, b]); // Only recomputes if 'a' or 'b' changes
    ```

2. **useCallback:** Memoizes a **function**. It returns the same function instance between renders as long as its dependencies have not changed. This is crucial when passing callbacks to optimized child components to prevent unnecessary re-renders.
    ```js
    const memoizedCallback = useCallback(() => {
      doSomething(a, b);
    }, [a, b]); // Only creates a new function if 'a' or 'b' changes
    ```

#### Hooks At A Glance:

| Hook          | Primary Use Case                                                           | Returns                                          | Key Consideration                                                                                    |
| ------------- | -------------------------------------------------------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| `useState`    | Managing component state that triggers re-renders.                         | ``                                               | Use functional updates (`setState(prev =>...)`) for state based on previous state.                   |
| `useEffect`   | Handling side effects (data fetching, subscriptions, DOM manipulation).    | `undefined`                                      | The dependency array is critical for controlling when the effect runs and preventing infinite loops. |
| `useContext`  | Accessing global state or data without prop drilling.                      | `contextValue`                                   | Re-renders all consuming components when the provider's value changes.                               |
| `useMemo`     | Memoizing the result of an expensive calculation.                          | A memoized value.                                | Use for computationally heavy functions to avoid re-calculation on every render.                     |
| `useCallback` | Memoizing a callback function.                                             | A memoized function.                             | Use when passing callbacks to optimized child components to maintain referential equality.           |
| `useRef`      | Accessing DOM nodes or storing mutable values that don't cause re-renders. | A mutable ref object with a `.current` property. | Changing `.current` does not trigger a re-render.                                                    |

### React State Management
Components often need to change what is on the screen as a result of user interaction. Typing into a form should update the input field, clicking "next" on an image carousel should display a new image, and adding an item to a shopping cart should reflect that change in the cart's contents. To achieve this, components must "remember" information between renders. In React, this kind of component-specific memory is called **state**.

Conceptually, state is a JavaScript object that holds data pertinent to a component's current situation. When a React function component renders, it is essentially just a JavaScript function being called. Any local variables declared inside it are discarded once the function completes its execution. State variables, however, are preserved by React itself, persisting across multiple render cycles. This preservation mechanism is what allows a component to maintain its "memory."

#### Local State Management
Local state refers to data that is scoped directly to a single component or a small, co-located group of its descendants. It is the most common and fundamental type of state in any React application. 

React provides two primary hooks for managing local state in functional components:
1. **useState:** this hook has been covered above in detail please refer to [[#React Hooks]] section for its working and example usage.

2. **useReducer:** While `useState` is perfect for simple state, it can become cumbersome when managing more complex state logic, especially when the state is an object with multiple properties or when the next state depends on the previous one in intricate ways. For these scenarios, React provides a more powerful and structured alternative. The `useReducer` hook is called with a reducer function and an initial state:
   ```jsx
	const [state, dispatch] = useReducer(reducer, initialState);
	```
	It returns the current `state` and a `dispatch` function. Let's break down the key components:
	1. **The Reducer Function:** This is a pure function that you write. It accepts the current `state` and an `action` object as arguments and must return the _next_ state.12 All of your state update logic is consolidated within this single function, typically using a `switch` statement to handle different types of actions.
	2. **The Action Object:** A plain JavaScript object that describes a state change. By convention, it has a `type` property (a string that identifies the action) and an optional `payload` property containing any data needed to compute the next state.
	3. **The Dispatch Function:** Instead of calling a setter function with the new state, you call `dispatch` with an action object. This signals your intent to update the state. React then passes the current state and your action to your reducer function, which computes the new state and triggers a re-render.

**Example Usage of useReducer:**
```jsx
import { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </>
  );
}
```

> [!important] 
>  `useState` is more direct, providing a setter that says, "Set the state to this new value." The logic for determining that value resides within the component's event handlers. In contrast, `useReducer` provides a `dispatch` function that says, "An event of this type happened." The logic for how that event translates into a new state is encapsulated outside the component, within the reducer. This decouples the "what happened" (the action) from the "how the state changes" (the reducer logic), leading to cleaner components and more predictable, testable, and reusable state logic.
> 
> **When to Choose `useReducer` over `useState`?**
> 1. **Complex State Shape:** When your state is an object or array with multiple interdependent values, `useReducer` can make updates more manageable.
> 2. **Performance Optimization:** When passing update logic down to child components, passing a stable `dispatch` function can prevent the child components from re-rendering unnecessarily, whereas passing new callback functions from `useState` on each render can break memoization.

#### Managing State Across Components
While local state is sufficient for many components, applications often require multiple components to access and manipulate the same piece of data. This introduces the challenge of shared state. React's architecture, with its unidirectional data flow, provides clear patterns for managing these scenarios, from the fundamental technique of "lifting state up" to the more advanced Context API for solving the issues that arise at scale.

##### Concept of "Lifting State Up"
In React, data flows downwards from parent to child through props. This means there is no direct way for sibling components to communicate or share state. When two or more components need to be synchronized with the same data, the canonical solution is to **lift the state up** to their closest common ancestor.

The process involves three key steps:
1. **Identify the Common Ancestor:** Find the single parent component in the component tree that is an ancestor to all the components that need to share the state.
2. **Move the State:** Remove the local state from the child components and declare it in the common ancestor component using `useState` or `useReducer`. This parent now becomes the "single source of truth" for this piece of state.
3. **Pass Data and Callbacks Down:**
    - Pass the state value from the parent down to the relevant child components as props.
    - If a child component needs to modify the state, the parent must define a callback function that updates its own state and pass that function down to the child as a prop. The child then calls this prop function when an event occurs.

##### Prop Drilling Problem
While "lifting state up" is an effective pattern, it can lead to a new problem in large and deeply nested component trees: **prop drilling**, (also known as "threading"), is the process of passing props down through multiple layers of intermediary components that do not actually need or use the props themselves. Their only role is to forward the props to a child component further down the tree.

Prop drilling introduces several significant drawbacks:
- **Code Clutter and Boilerplate:** Components become cluttered with props that are irrelevant to their own logic, making the code harder to read and understand.
- **Tight Coupling and Maintenance Issues:** It creates a tight coupling between layers of components. If a prop needs to be renamed or its shape changes, every single component in the chain must be updated, making refactoring a tedious and error-prone process.
- **Reduced Reusability:** Components are less reusable because they are burdened with the responsibility of passing down specific props.
- **Scalability Problems:** In a large application, prop drilling can become completely unmanageable, obscuring the flow of data.

##### The Context API: Built-In
To solve the problem of prop drilling, React provides a built-in mechanism called the **Context API**. Context offers a way to pass data through the component tree without having to pass props down manually at every level. It is designed specifically for sharing data that can be considered "global" for a subtree of components, such as the current authenticated user, UI theme, or preferred language.

The Context API consists of **three** main parts:
1. **`React.createContext(defaultValue)`:** This function creates a Context object. It should be exported so other components can use it. The `defaultValue` argument is a fallback that is only used when a component tries to consume the context but does not have a matching Provider above it in the tree.

2. **`<MyContext.Provider value={...}>`:** Every Context object comes with a Provider component. You wrap a part of your component tree with this Provider to make the context value available to all components inside it. The `value` prop is where you pass the data you want to share.

3. **`useContext(MyContext)`:** This is the hook that allows a functional component to subscribe to context changes. It accepts the Context object as an argument and returns the current context `value` from the closest matching Provider up the tree. More details about this hook can be found in [[#React Hooks]]

##### Combining useReducer with Context
By combining the `useReducer` and `useContext` hooks, developers can create a powerful, scalable, and centralized state management solution using only React's built-in APIs. This pattern effectively mimics the core principles of libraries like Redux without adding any external dependencies, making it an excellent choice for small to medium-sized applications.

The implementation follows a clear pattern:
1. **Define the Reducer and Initial State:** Create a reducer function that encapsulates all the state transition logic and define the initial shape of your global state.
2. **Create a Context:** Use `React.createContext` to create a context that will provide the state and the dispatch function to the rest of the application.
3. **Create a Provider Component:** Build a custom component (e.g., `StateProvider`) that will manage the state. Inside this component, call `useReducer` to get the current `state` and the `dispatch` function.
4. **Provide the Value:** In the Provider component's return statement, wrap its `children` prop with the `Context.Provider`. Pass an object containing both the `state` and the `dispatch` function as the `value` prop.
5. **Wrap the Application:** Wrap your root application component (or the relevant subtree) with your custom Provider component.
6. **Consume the Context:** In any child component that needs to access or update the global state, use the `useContext` hook to pull out the `state` and `dispatch` function.

##### Redux: Better than Built-In
While React's built-in tools can manage global state, dedicated libraries often become necessary for large, complex applications. They offer benefits like advanced developer tools (such as time-travel debugging), middleware for handling side effects, fine-grained performance optimizations, and established conventions that can help large teams work together effectively.

The most established and battle-tested solution. Redux is built on the principles of the Flux architecture, enforcing a strict unidirectional data flow with a single, centralized, immutable store. While historically known for its significant boilerplate, the official **Redux Toolkit** package has drastically simplified its usage. It remains the standard for large-scale enterprise applications where predictability, maintainability, and a robust ecosystem of devtools are paramount.

#### A Decision-Making Framework for State Management
To choose the appropriate state management strategy, a developer can follow a logical progression of questions, starting with the simplest solution and escalating only when necessary. This "start local, grow global" philosophy prevents premature optimization and unnecessary complexity.

1. **Is the state truly necessary?** Can this value be derived from existing props or state on every render? If so, no state is needed at all. Compute it directly in the render body.

2. **Where is the state used?**
    - **A single component?** Start with `useState`.
    - **Is the update logic complex or are there many related state transitions?** If `useState` is becoming unwieldy, refactor to `useReducer` for better organization.

3. **Do multiple components need this state?**
    - **A few, co-located sibling components?** Use the **Lifting State Up** pattern. Move the state to their closest common ancestor and pass it down via props.
    - **Many components, scattered across different parts of the tree?** This is a sign of prop drilling. Use the **Context API** to make the state available to the entire subtree.
    - **Is the context value complex and updated from many different places?** Combine `useReducer` with `Context` for a robust, Redux-like pattern without external libraries.

4. **What kind of state is it?**
    - **Is the data being fetched from an API?** This is server state. Use a dedicated **server state library** like TanStack Query or SWR. Do not manage this data in your global client store.
    - **Is it complex, synchronous, client-only state that many disconnected components need to access and modify?** This is the use case for a **global client state library** like Zustand or Redux Toolkit.


### Tips & Questions

> [!tip] Tips & Best Practices:
> - Prefer functional components and hooks over class components unless legacy code requires it.
> - Use `useState` and `useEffect` for component state and side effects, keeping dependencies arrays correct.
> - Use Context or Redux for global state; avoid excessive prop drilling.
> - Leverage error boundaries (in class components) or try/catch in effects to handle UI errors gracefully.
> - Keep CSS and styling modular (CSS Modules, styled-components, or CSS-in-JS) to avoid style clashes.
> - Write pure components: no side-effects in render; derive UI only from props/state.

> [!question] Interview Questions:
> - What are React hooks? How do `useState` and `useEffect` work?
> - Explain the virtual DOM and how React updates the real DOM.
> - How do you manage global state or pass data deeply (hint: Context API)?
> - Difference between controlled and uncontrolled components?
> - What are pure components and how does `React.memo` help performance?
> - How would you optimize a slow React application?


## Section 6: NextJS: React on Steroids
A common high-level interview question for senior roles involves comparing frameworks to assess architectural awareness. The key is to frame the discussion around the trade-offs related to performance, SEO, and developer experience. 

### Core Distinction: Library & Framework
- **React:** Is a UI library for building user interfaces. It uses _Client-Side Rendering_ (CSR), the browser downloads a JS bundle and renders the UI in the client. It is unopinionated about routing, data fetching, and state management, giving the developer complete flexibility but also the responsibility to choose and configure these aspects of the application architecture. 
- **Next.js:** A full-stack React framework created by Vercel. It provides a structured, opinionated solution for building production-ready applications, with features like file-system-based routing, various rendering strategies, and API routes integrated out-of-the-box. It adds features like _Server-Side Rendering_ (SSR), _Static Site Generation_ (SSG), and file-based routing. Next.js can pre-render pages on the server or at build time, improving load times and SEO. Next.js supports SSR so that “requests are processed and generated from the server with HTML returned.

### Rendering Strategies Compared
The choice of rendering strategy is a fundamental architectural decision that impacts performance, SEO, and user experience.

|Strategy|How it Works|Initial Load Time|SEO Friendliness|Server Load|Ideal Use Case|
|---|---|---|---|---|---|
|**CSR (Client-Side Rendering)**|Browser receives minimal HTML and a JS bundle. React renders the app in the browser.|Slow (blank page initially, high Time to Interactive).|Poor (crawlers may not see content).|Low|Internal dashboards, applications behind a login.|
|**SSR (Server-Side Rendering)**|Server generates full HTML for each request and sends it to the browser.|Fast perceived load (fast Time to First Byte).|Excellent (crawlers see full content).|High|Dynamic, personalized content that needs SEO.|
|**SSG (Static Site Generation)**|All HTML pages are generated at build time and served as static files from a CDN.|Blazing Fast (served directly from CDN).|Excellent|Very Low|Blogs, marketing sites, documentation (content rarely changes).|
|**ISR (Incremental Static Regeneration)**|A hybrid of SSG and SSR. Pages are static but can be re-generated periodically or on-demand.|Blazing Fast (like SSG).|Excellent|Low|E-commerce sites, news sites (content updates frequently but not on every request).|


### Routing: React Router vs NextJS Routing
1. **React Router:** The de facto standard library for routing in React applications. It requires developers to explicitly define routes within their code, offering a high degree of flexibility and control over the routing logic.

2. **Next.js Routing:** Next.js uses a file-system-based routing system. Creating a file within the `pages` or `app` directory automatically generates a corresponding route. This approach is intuitive and requires zero configuration but is more opinionated than React Router.

### Tips & Questions

> [!important] When to Choose Which?
> - **Choose React for:**
> 	1. Highly interactive Single Page Applications (SPAs) where SEO is not a primary concern (e.g., internal dashboards, complex editors).
> 	2. Mobile applications, where it serves as the foundation for React Native.
> 	3. Projects where maximum architectural flexibility and control over the tech stack are desired.
> 
> - **Choose Next.js for:**
> 	1. SEO-critical applications such as e-commerce sites, blogs, and marketing websites.
> 	2. Applications where a fast initial page load is crucial for user experience.
> 	3. Projects that require both a frontend and a backend, as Next.js's API routes provide an integrated full-stack solution.

> [!question] Interview Questions:
> - What is SSR and CSR? How does Next.js implement SSR?
> - How does Next.js’s static generation differ from React’s CSR?
> - What are the SEO benefits of server-side rendering?
> - How does file-based routing work in Next.js?
> - What is Incremental Static Regeneration (ISR) in Next.js, and when would you use it?
> - Explain differences between `getStaticProps`, `getServerSideProps`, and client-side data fetching.


## Section 7: Performance Optimizations
Performance is a recurring and critical theme in senior frontend interviews. This section covers the key pillars of a performant web application, from core metrics to specific optimization techniques. Improving frontend performance involves reducing load times and efficient resource usage. Key techniques include **code splitting**, **lazy loading**, and **caching**.

### Core Web Vitals and Their Impact
Core Web Vitals are a set of metrics defined by Google to measure real-world user experience for loading performance, interactivity, and visual stability. They are a significant factor in SEO rankings.

1. **LCP (Largest Contentful Paint):** Measures **loading performance**. It marks the point in the page load timeline when the main content has likely loaded. A good LCP is **< 2.5s**. It is often impacted by slow server response times, render-blocking JavaScript and CSS, and large, unoptimized images or videos.

2. **INP (Interaction to Next Paint):** Measures **responsiveness**. It assesses a page's overall responsiveness to user interactions by observing the latency of all clicks, taps, and keyboard interactions that occur throughout the lifespan of a user's visit to a page. A good INP is **< 200ms**. It is primarily impacted by heavy JavaScript execution that blocks the main thread.

3. **CLS (Cumulative Layout Shift):** Measures **visual stability**. It quantifies how much unexpected layout shift occurs during the entire lifespan of the page. A good CLS score is **< 0.1**. It is commonly caused by images or ads without defined dimensions, dynamically injected content, and web fonts that cause a flash of unstyled or invisible text (FOUT/FOIT).

### Page Loading Optimization Techniques
1. **Code Splitting:** This technique involves breaking up the main JavaScript bundle into smaller chunks that can be loaded on demand. For example, code for a specific route or a feature that is only activated by user interaction can be loaded only when needed. Modern bundlers like Webpack and frameworks like Next.js support code splitting out of the box, significantly reducing the initial JavaScript payload.
  
2. **Minification & Tree Shaking:**
    - **Minification:** The process of removing all unnecessary characters (whitespace, comments, shortening variable names) from source code without changing its functionality. This reduces the file size of CSS and JavaScript assets.
    - **Tree Shaking:** A form of dead code elimination. During the build process, the bundler analyzes the import and export statements to detect which code is not being used and excludes it from the final bundle.

3. **Critical CSS:** This is a technique where the minimal CSS required to render the "above-the-fold" content of a page is inlined directly into the `<head>` of the HTML document. The rest of the CSS is then loaded asynchronously. This allows the browser to start rendering the visible part of the page immediately, improving the perceived load time and LCP.

### Asset Optimization: Image & Font Loading Strategies
1. **Image Optimization:**
    - **Compression:** Using tools to reduce the file size of images. **Lossy** compression permanently removes some data, resulting in smaller files but a potential loss of quality. **Lossless** compression reduces file size without any loss of quality.
    - **Modern Formats:** Serving images in next-gen formats like **WebP** or **AVIF**. These formats provide superior compression and quality compared to traditional formats like JPEG and PNG.
    - **Responsive Images:** Using the `<picture>` element and the `srcset` attribute on `<img>` tags allows the browser to select the most appropriate image file based on the device's screen size, resolution, and orientation, preventing the download of unnecessarily large images on mobile devices.

2. **Lazy Loading:** Deferring the loading of off-screen images and iframes until they are about to scroll into the viewport. Modern browsers support native lazy loading via the `loading="lazy"` attribute, which is a simple and effective optimization.

3. **Font Optimization:** Web fonts can be a performance bottleneck. Strategies to optimize them include:
    - **Preloading critical fonts:** Using `<link rel="preload">` to tell the browser to download key font files early.
    - **Using `font-display: swap`:** This CSS property ensures that text remains visible with a fallback font while the custom font is loading, preventing a flash of invisible text (FOIT).

### The Role of a Content Delivery Network (CDN)
- **Concept:** A CDN is a geographically distributed network of proxy servers and their data centers. The goal is to provide high availability and performance by distributing the service spatially relative to end-users.

- **How it Works:** A CDN caches static assets (like images, CSS, and JS files) on its **edge servers** located around the world. When a user requests an asset, the request is routed to the nearest edge server instead of the **origin server**. This significantly reduces latency, as the physical distance the data has to travel is much shorter.

- **Benefits:**
    1. **Improved Performance:** Drastically reduces latency and speeds up content delivery.
    2. **Higher Availability and Scalability:** Distributes traffic across many servers, reducing the load on the origin server and protecting against traffic spikes.
    3. **Enhanced Security:** Many CDNs offer protection against DDoS attacks and other security threats.

### Tips & Questions

> [!tip] Tips & Best Practices:
> - Split vendor and app code into separate bundles to take advantage of caching (changing app code doesn’t invalidate vendor bundle).
> - Use dynamic imports for routes or heavy components (chunk per route is common).
> - Implement lazy loading for images and components to defer offscreen work.
> - Leverage the browser cache and CDN for static assets. Set appropriate `Cache-Control` headers as recommended by MDN.
> - Pre-compress assets or enable on-the-fly compression on the server (gzip/Brotli).
> - Use HTTP/2 (multiplexing) if available, to reduce overhead of multiple file requests.

> [!question] Key Interview Questions:
> - What is code splitting? How do you implement it in React?
> - How does lazy loading differ from code splitting? Give examples.
> - Explain the critical rendering path and how to optimize it.
> - What are common HTTP cache headers and how do they improve performance?
> - How do you measure and improve First Contentful Paint (FCP) or Largest Contentful Paint (LCP)?
> - What is tree shaking and how does it work with ES modules?
> - Describe browser caching and how it benefits repeated visits?


## Section 8: SEO Fundamentals
Frontend development choices have a direct impact on a site's Search Engine Optimization (SEO). It involves ensuring search engines can crawl and index your content, and that your site meets best practices.

### Techniques
1. **Semantic HTML:** Using HTML tags according to their semantic meaning (e.g., `<header>`, `<nav>`, `<main>`, `<article>`, `<footer>`) is crucial. It helps search engine crawlers understand the structure, hierarchy, and importance of the content on a page, which can improve indexing and ranking. It is also fundamental for accessibility.

2. **Meta Tags:**
    - `<title>`: The title of the page, displayed in the browser tab and as the main headline in search results. It is a strong SEO signal.
    - `<meta name="description">`: A brief summary of the page's content. While not a direct ranking factor, a compelling description can significantly improve the click-through rate (CTR) from search results.

3. **Structured Data (Schema Markup):** This is a standardized format (often using JSON-LD) for providing information about a page and classifying its content. For example, you can mark up a recipe with its ingredients and cooking time, or a product with its price and rating. Search engines use this data to understand the content better and can display it as **rich results** (or rich snippets) in search, which can increase visibility and CTR.

4. **Accessibility:** Accessible sites (good contrast, alt text, ARIA roles) indirectly help SEO by improving content clarity. For example, `<img src="..." alt="Descriptive text">` both aids visually impaired users and gives crawlers context.

5. **Structure & Performance:** Use clean, descriptive URLs and a logical site hierarchy. Include a sitemap or robots.txt when appropriate. Page speed is a ranking factor. Fast load (via the optimizations above) also boosts SEO.

### Tips & Questions:

> [!tip] Tips & Best Practices:
> - Regularly run tools like Google’s PageSpeed Insights or Lighthouse to catch SEO issues (e.g., missing `lang` attribute on `<html>`, inadequate link text).
> - Use `<h1>` for the page title, and don’t skip heading levels.
> - Always include descriptive `alt` text for images.
> - For SPAs, ensure routing updates the `<title>` and that crawlers can see content (React Helmet or Next.js’s Head component).
> - Provide a `<link rel="canonical">` if multiple URLs show same content.
> - Monitor and fix broken links.
> - Test on search consoles (e.g., Google Search Console) to ensure pages are indexed correctly.

> [!question] Interview Questions:
> - How does server-side rendering affect SEO compared to client-side rendering?
> - What are key meta tags you should include on a webpage for SEO?
> - How do you ensure search engines can crawl your single-page application?
> - Explain how `robots.txt` or `sitemap.xml` files are used in SEO.
> - Describe how you would use Google Search Console or SEO auditing tools.
