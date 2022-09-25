## How To Sort Array in JavaScript

Recently I have been doing a lot of interview assessments and the ones that I usually find a joy to do is all those small data structures problems, like how do you sort a set of random numbers in ascending order. So let's try to do that in JavaScript.

Given an array of random numbers:
```javascript
let numbers = [5,2,3,7,8]
```

We have to sort the numbers in ascending order. Straight at the top of my mind was to loop through the array of numbers and do comparison between numbers and sort it accordingly.
```javascript
for (let i = 0; i < numbers.length; i++) {
  for (let index = 1; index < numbers.length; index++) {
    
    // check for smaller next
    if (numbers[index] < numbers[index - 1]) {
      swap(index, index - 1);
    }
  }
}
```
This was an easy solution, but not an effective one. 2 problems here, one is too much of a hassle to do this and the solution is slow. Like O(n2) slow. A good head start but an inefficient one. Especially if the dataset size is about thousands and millions. We will need to go through the numbers double from its original size 🤯

> NEVER REINVENT THE WHEEL, JUST REALIGN IT

Instead of creating our own solution to a problem I believe many developers like you and I will come across, we shall use existing solutions available.

Lets try and use `Array.prototype.sort()`

```javascript
// before: [5, 2, 3, 7, 8]

numbers.sort();

// after: [2, 3, 5, 7, 8]
```

See how elegant and simple by not reinventing the wheel? We squashed everything to one line of code and just a glance I know the numbers will be sorted by then. All looks good, but further reading on the docs shows that the sort functions by default does this

> If compareFunction is not supplied, all non-undefined array elements are sorted by converting them to strings and comparing strings in UTF-16 code units order. For example, “banana” comes before “cherry”. In a numeric sort, 9 comes before 80, but because numbers are converted to strings, “80” comes before “9” in the Unicode order. All undefined elements are sorted to the end of the array.

In our previous example, the numbers sort accordingly as expected. But let's try a different example:

```javascript
// before: [1, 30, 80, 21, 9]

numbers.sort();

// after: [1, 21, 30, 80, 9]
```

Hmm looks like something is wrong now, exactly as the docs stated, it was sorted in Unicode order instead of the number’s value. Let's try to add a comparison function into sort() to solve this.

```javascript
// before: [1, 30, 80, 21, 9]

numbers.sort((a, b) => {
  return a - b;
});

// before: [1, 9, 21, 30, 80]
```
By specifying how we would like to sort the array with a compare function, now it is being sorted accordingly as expected. Because a universal algorithm to solve all problems does not exist, the `sort()` uses different algorithms, including quicksort, merge sort, insertion sort, and so on to best sort the array in the most efficient way possible. What algorithm it uses depends on many factors, including the size of the array, type of array, and the type of browser the client is using.  

I know. I know. The question now is should we even use the library to solve interview problems? Yes and no.  

Yes, because I believe a developer that knows their language well will know what existing library they can utilize to solve a problem. I personally rather work with a developer who focuses on implementing the solution than waste their time in solving a problem someone else has helped them solve.

No, because I did face some interviewers that insist on rewriting the function to solve it. But this could be for many reasons including testing a developer’s in-depth knowledge. You be surprised how many developers don’t know how does a bubble-sort works.  

Is good to know how does sorting algorithm works and which one works best for which scenarios and datasets. Have you been recently faced with a tough interview assessment? Comment below and tell me about it 🙆🏻‍♂️
