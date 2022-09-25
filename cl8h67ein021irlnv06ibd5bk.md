## == vs === in JavaScript

In JavaScript, there are two sets of equality operators, `===` and `!==`, and their wicked twins `==` and `!=`. At first glance, the only difference is an extra `=` sign. But there is more than that behind the scenes as both might yield different results depending on what is being compared. If two operands are of the same type and have the same value, the `===` will produce true, and `!==` will produce false. Using the wicked twins on the other hand will produce the same result when the operands are the same type. But when they are different types, things get interesting and the results might not be what is expected.  

Here are some interesting ones:  

```javascript
'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true

"abc" == new String("abc")    // true
"abc" === new String("abc")   // false
```

Confusing is it? This is due to the `==` operators doing type coercion, where it tries to implicitly convert the values before comparing. Whereas the `===` operators do not do type coercion, thus it matches only the exact same type and value, and it is also faster as it skips any conversions required.

If you have been using the wicked twin operators, my advice is to stay away from them. Always use `===` and `!==` instead of `==` and `!=`. The results produced by the `===` and `!==` are more consistent and less prone to making you scratch your head while figuring out what is causing the bug in your program.
