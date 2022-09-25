## Exceptions Handling with JavaScript

In a flawed world, there is no such thing as flawless code. Even if there was, there is odd to be a person who will find ways to break what seemed to be a flawless code. Is there a way we can prevent or control this? Let me introduce you to the `try/catch` block statements in JavaScript.

> When the code runs into an unexpected problem, the JavaScript idiomatic way to handle this situation is through exceptions.

There are errors that will occur during a program’s runtime and exceptions will be raised. If they’re not properly caught and handled, it might crash the program itself. Usually, this is something all developers want to avoid, as it provides a bad user experience to the users. The way to better handle those exceptions is with a `try/catch` block.

```javascript
try {
     // lines of code that might throw exceptions
} catch (error) {
     // here is where you handle those exceptions more gracefully
}
```

With this, any exceptions occur within the try block will be gracefully handled and catch by the catch block.  

We can take this one step further with a finally statement, which usually provides a way to close and clean up any remaining opened resources, like files or network requests. It runs regardless of whether an error occurs or it was handled or not. 

```javascript
try {
	// lines of code that might throw exceptions
} catch (error) {
	// here is where you handle those exceptions more gracefully
} finally {
    // code here runs regardless what happens previously
}
```

We can even use the finally statement without the catch block.

```javascript
try {
	// lines of code that might throw exceptions
} finally {
	// code here runs regardless what happens previously
}
```

Just like if-else statements, we can nest the `try/catch` block as well.

```javascript
try {
	// lines of code that might throw exceptions

	try {
		// other lines of code that might throw exceptions
	} finally {
		// code here runs regardless what happens previously
	}

} catch (error) {
	// here is where you handle those exceptions more gracefully
}
```
Hmm, you might be wondering, since there isn’t a catch statement in the inner `try/finally` block, how are the exceptions being handled? 

Any exceptions that occur in the inner try block, it will be handled in the outer catch block, that way we only need a catch statement at the outermost try/catch block. 

THAT’S IT 🥳

Now with the try/catch block, you can rest assured that your application will not crash ungracefully. It will provide a much better user experience overall. Do you use the `try/catch` block to handle errors more gracefully? Let me know in the comments below!





