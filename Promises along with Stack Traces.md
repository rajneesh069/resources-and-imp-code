Promises along with it’s stack tracing:

**What is a caller?**

The "caller" in this context refers to the part of your code that initiates the function call. When you call a function, the code that triggers the function call is considered the "caller."

In the case of Promises, the `Promise` constructor creates and returns a new Promise object immediately when the function is called. The caller, in this scenario, is the part of your code that invokes the function containing the `new Promise()` constructor.

Here's an example to illustrate the concept:

**```javascript**

**function myFunction() {**

**return new Promise((resolve, reject) => {**

**// ...**

**});**

**}**

**// The caller is this part of the code: const myPromise = myFunction(); ```**

In this example, the caller is the line `const myPromise = myFunction();`, which invokes the `myFunction()` and receives the returned Promise.

When the Promise is returned, the control returns to the caller, allowing the rest of the code to continue executing while the asynchronous operation initiated by the Promise is in progress. This is one of the key features of asynchronous programming and allows for non- blocking behavior, enabling your code to efficiently handle multiple tasks concurrently.

**Promises Version with Console Log:**

**```javascript**

**function placeOrder(dish) {**

**return new Promise((resolve, reject) => {**

**setTimeout(() => {**

**const isDishAvailable = Math.random() < 0.8; if (isDishAvailable) {**

**resolve(`Your ${dish} is ready!`);**

**} else {**

**reject(`Sorry, we're out of ${dish} today.`); }**

**}, 2000);**

**});**

**}**

**placeOrder("Pasta")**

**.then((message) => {**

**console.log(message); })**

**.catch((error) => {**

**console.error(error); });**

**console.log("Waiting for the order"); ```**

**Stack Tracing, Callback Queues, and APIs (Promises Version):**

1. `placeOrder("Pasta")` is called.
1. A new Promise is created and returned immediately.
1. Inside the Promise constructor, `setTimeout()` schedules a Web API timer with a delay of 2000 ms (2 seconds).
1. The Promise is returned immediately, and control returns to the caller.
1. `console.log("Waiting for the order")` is executed.
1. The timer in the Web API starts counting down.
1. During the 2-second delay, the JavaScript engine continues executing other code or Promises if available.
1. Once the timer expires, the callback (resolve or reject) is put into the callback queue.
1. The callback queue is checked when the call stack is empty.
1. The callback function is moved from the queue to the call stack for execution.
1. If `resolve()` is called, the `.then()` handler is executed.
1. If `reject()` is called, the `.catch()` handler is executed.

**\*\*Async/Await Version with Console Log:\*\***

**```javascript**

**async function placeOrder(dish) {**

**return new Promise((resolve, reject) => {**

**setTimeout(() => {**

**const isDishAvailable = Math.random() < 0.8; if (isDishAvailable) {**

**resolve(`Your ${dish} is ready!`);**

**} else {**

**reject(`Sorry, we're out of ${dish} today.`); }**

**}, 2000);**

**});**

**}**

**async function main() {**

**try {**

**const message = await placeOrder("Pasta"); console.log(message);**

**} catch (error) {**

**console.error(error);**

**}**

**}**

**main();**

**console.log("Waiting for the order"); ```**

**Stack Tracing, Callback Queues, and APIs (Async/Await Version):**

1. `main()` is called.
1. Inside `main()`, `await placeOrder("Pasta")` is encountered.
1. `await` pauses the execution of `main()` and returns control to the caller.
1. The rest of the main program continues executing.
1. `console.log("Waiting for the order")` is executed.
1. A new Promise is created and returned from `placeOrder()`.
1. `setTimeout()` schedules a Web API timer.
1. The timer counts down while other code or Promises may execute.
1. When the timer expires, the appropriate callback is put into the callback queue.
1. The callback queue is checked when the call stack is empty.
1. The callback function is moved from the queue to the call stack for execution.
1. If `resolve()` is called, the value is assigned to `message`, and `console.log()` is executed.
1. If `reject()` is called, an error is thrown and can be caught using the `catch` block in the nearest enclosing scope (`try` and `catch`).

In both versions, the order of execution and the interaction between the call stack, callback queue, and Web APIs remain consistent. The added `console.log("Waiting for the order")` statement is executed after the asynchronous operation is initiated, highlighting that the main program continues while awaiting the asynchronous task.
