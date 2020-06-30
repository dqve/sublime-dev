
To give some context, Big-O Notation or rather Big-O Time Complexity was one of the subjects I was taught back in school, but I slept through some of those classes 😅. Reading a book a while ago sparked my interest in the subject again, so I wrote this article hoping it sparks your interest in it too.

# Table of contents
1. What is time-complexity?
2. O(1) - Constant Time Complexity
3. O(N) - Linear Time Complexity
4. O(log(n)) - Logarithmic Time Complexity
5. O(N²) - Quadratic Time Complexity
6. O(2^N) - Exponential Time Complexity
7. Conclusion

# What is Time - Complexity?

**Why should I know about Big-O?**

Big-O is useful to determine the speed of your code, if you've ever thought that your code was running too slow, or maybe your code is working out great, but it’s not running as quickly as that other lengthier ones. The time complexity of your code can explain why it executes in the time it does.

[Big-O](https://en.wikipedia.org/wiki/Big_O_notation) notation is a typical method for depicting the performance or complex nature of an algorithm in Computer Science, notation, `n` represents the number of inputs. 
It is used as a gauge to test the efficiency of your code, and if it can be improved. In this article, I'd attempt to break down each Time-complexity and explain how they work in real life so that at the end of this article, you would be able to analyze pieces of code and indicate which one falls within what time complexity.

# O(1) - Constant Time Complexity:

CTC describes an algorithm that will always execute in the same time (or space) regardless of the size of the input data. In JavaScript, this can be as simple as accessing a specific index within an array:
```js
var array = [1, 2, 3];  
array[0] // This is a constant time look-up
```
It doesn’t matter whether the array has a length of 3 or 30,000, looking up a specific index in the array would take the same amount of time, therefore the function has a *constant time look-up*.
Consider another example.
```js
function ctcExample(n) {
    return n*n;
}
```
In this second example, the function `ctcExample` accepts one parameter and returns the square of it, regardless of the size of this parameter, this function will always take the same amount of time to execute.

The last example, if we wad pieces of paper with names written on them spread across a table, and I tell you to pick out any name from the table, you could simply grab the first name you see from the table, no stress, this is a constant time look-up.

# O(N) - Linear Time Complexity:

Linear Time Complexity describes an algorithm whose complexity will increase in direct proportion to the size of the input data. It applies to algorithms that must do `n` operations in the worst-case scenario. 
As a dependable guideline, it is ideal to attempt to keep your functions running below or within this range of time-complexity, but obviously, it won’t always be possible.
```js
function ltcExample(array) {  
  for (var i = 0; i < array.length; i++) {  
    console.log(array[i]);  
  }
}
```
The example above will have a linear time look-up since the function is looking at every index in the array once. 

In our example, the look-up time is related to the size of our input because we will be looping through every item within the array. Therefore the larger the input, the greater the amount of time it takes to execute the function. Do note that if the array had only one index, it would have a constant time look-up.

To further clarify, let's assume we still had pieces of paper on the table, and I asked you to pick piece of paper and call out the name written on it. You would have to look through every piece of paper calling out names. Now think about if this table was a very long one filled with lots of tiny pieces of paper, that could potentially take a lot of time. Your search is directly related to the number of pieces of paper on the table.

# O(log(n)) - Logarithmic Time Complexity:

Logarithmic Time Complexity describes an algorithm whose time of execution is proportional to the logarithm of the input size. Let's go over this one slowly. 
```js
function logtcExample(array) {  
  for (var i = 1; i < array.length; i = i * 2) {  
  //don't initialize i as zero, seriously don't!
	console.log(array[i]);  
  }
}
```
The example above will have a logarithmic time look-up since the function will only search through certain parts of the array.

From the example, we can see that in any given iteration, the value of `i` is equal to `2i` (i=2i), so in the nth iteration (where n = array.length), the value of `i` is equal to `2n` (i=2n). Also, we know that the value of `i` is always less than the size of the input itself (i<N).  
therefore we can deduce the following:  

**2n < N  
log(2n) < log(N)  
n < log(N)**

From the preceding code, we can see that the number of iterations would always be less than the log of the input size. Hence, the worst-case time complexity of such an algorithm would be O(log(n)).  
The efficiency of logarithmic time complexities is apparent with large inputs such as a million items.

And finally, let's consider our **pieces of paper on the table** example again, but this time all the pieces are arranged in alphabetical piles, if I told you to pick every piece where the name on it starts with a *D* and is followed by an *a*. This time around you do not need to search through all the pieces on the table, but it wasn't as easy as selecting one at random.

# O(N²) - Quadratic Time Complexity:

Quadratic Time Complexity describes an algorithm whose time of execution is directly proportional to the squared size of the input data  (think of Linear, but squared). Within our code, this time complexity will occur whenever we nest multiple iterations over the data.
```js
function qtcExample(array) {  
  for (var i = 0; i < array.length; i++) {  
	var item = array[i];  
    if (array.slice(i + 1).indexOf(item) !== -1) {  
	  return true;  
    }  
  }  
return false;  
};
```
In the example above we access our array twice (without using two for loops 😎). The for loop iterates over each item in the array and at each iteration the `if` statement checks the array to find the `indexOf` item. Therefore this produces a Quadratic Time Complexity.

From the example we can see for every iteration, the inner statement runs `n` times so at the end of the outer loop the number of iterations would equate `n²` Hence, the worst-case time complexity of such an algorithm would be O(n²).

Back to our **pieces of paper on the table** example. If this time around and the pieces are stacked, and I asked you to pick the first piece in the stack, then remove every piece whose first letter resembles the first letter of the one you picked. You would have to search through every piece of paper on the table removing the similar ones as you go. Once all the similar ones have been removed, you'd have to repeat the process for the next piece you pick and so on until you reach the end of the stack. I'm sure you get it now.

# O(2^N) - Exponential Time Complexity:

Exponential Time complexity denotes an algorithm whose growth doubles with each addition to the input data set. If you know of other exponential growth patterns, this works in much the same way. The time complexity starts very shallowly, rising at an ever-increasing rate until the end.
```js
function etcFibonacci(number) {
if(number <= 1) return number;  
return etcFibonacci(number - 2) + etcFibonacci(number - 1);  
}
```
This example implements recursion to explain how a function can be _Exponential time look-up_. Here the recursive instantiation will pass over every number from the `number` to zero. It will do this twice (once for each recursive call) until it reaches the base case if statement. Since the number of recursive calls is directly related to the `number` parameter, it is easy to see how this look-up time will quickly grow out of hand.

# Rules of  Big O Time Complexity
Rules come into place when you attempt to determine the complexity of an algorithm. In cases of large (modular) piece of code that possess different complexities at different intervals, you may have to go through each line of your code to establish if it is O(1), O(n) etc. then return the results. However it can be challenging to calculate these time complexities. Therefore we've been provided with a couple of rules that would make the calculation process easier.
Some of these rules include:

1.  Consider the worst case
2.  Coefficient rule (Remove constants)
3.  Sum rule
4.  Product rule
5.  Drop Non Dominants


## Consider The Worst Case
When calculating Big O, it's advisable to always consider the worst case scenario. For example when search through an array for an item "x" (refer to the O(n) paper example) "x" can be the first or last item. Since we aren't certain of "x"'s location we have to consider the size of the array and assume O(n) in this case.

## Coefficient Rule
This rule requires us to ignore any constant that is not related to the size of our input size. In cases where the there are more complex algorithm than the O(1) we are obligate to remove the constant.
For example, let us consider this block of code:
```js
function x(n){
    var counter =0;
    for (var i = 0; i < 5+n; i++){
        count += 1;
    }
    return count;
}
```

This example has a complexity of O(5 + n) because the loop has a linear complexity that runs from 0 to 5+n. In this case the constant "5" doesn't directly affect the size of the input and could prove to be insignificant. Therefore we can discard 5 in this case, making the Time complexity O(n).

## Sum Rule
This rule allows us to perform arithmetic additions on Time complexities.
If we have an algorithm that contains two steps (smaller internal algorithms). To get this algorithms time complexity, we simply sum the complexities of the internal algorithms.
For example, let us consider this block of code:
```js
function x(n){
    var counter =0;
    for (var i = 0; i < n; i++){
        count += 1;
    }
     for (var i = 0; i < 5*n; i++){
        count += 1;
    }
    return count;
}
```
In this example, the first loop has a time complexity of O(n) and the second loop has time complexity of O(5n).
Therefore Big O  of function x is O(n + 5n) and results to O(6n).
However, we should always apply the coefficient rule and using the sum, then the final complexity of function x is O(n) = n.

## Product Rule
This rule allows us to perform arithmetic multiplication on Time complexities.
This can be applied similarly to the Sum Rule but in different scenarios.
For example, let us consider this block of code:
```js
function x(n){
    var counter =0;
    for (var i = 0; i < n; i++){
        count += 1;
        for (var i = 0; i < 5*n; i++){
	        count += 1;
	    }
    }
    return count;
}
```
In this example, the first loop has a Quadratic Time Complexity of O(n) and the second loop has time complexity of O(5n).
Since 5n runs for total of n iterations, the Big O of function x is O(5n * n) and results to O(5n2).
Applying the coefficient rule, the final complexity of function x is O(n) = n2.

## Drop Non Dominants
This rule is similar to the coefficient rule, it requires us to the non-dominant term in cases were a definite Time Complexity cannot be concluded and there isn't a constant to drop.
For example, let us consider this block of code:
```js
function x(n){
    var counter =0;
	for (var i = 0; i < n; i++){
	        console.log(n);
	    }
	    
    for (var i = 0; i < n; i++){
        count += 1;
        for (var i = 0; i < 5*n; i++){
	        count += 1;
	    }
    }
    return count;
}
```
In this example there are two loops, a single and a nested loop, the single has a Time Complexity of O(n) while the second loop Time Complexity of O(n2).
Therefore the Big O of function x is O(n + n²). 
In this case we drop O(n) and keep O(n2) as this is more significant as it has a heavier impact on the functions performance compared to o(n).


# Conclusion
We've come to the end, that was intense (for me to write at least).
If you'd like to improve your understanding of the topic you can check out the [**_Big-O Cheat Sheet_**](http://bigocheatsheet.com/). Cheers.
