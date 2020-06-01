
Have you ever had to write a series of if-else statements and wondered if it could be shorter? Like the code block below, maybe you figured out how to use a shorthand statement but don't fully grasp the context of using them? Well, no need to fear, David is here!

```js
if (score >= 80 && score <= 100) {
 rating = "Expert level"
}
else if (score >= 70 && score <= 79) {
 rating = "Expert"
}
else if (score >= 60 && score <= 69) {
 rating = "Professional"
}
else if (score >= 50 && score <= 59) {
 rating = "Semi-Pro"
}
else if (score >= 40 && score <= 49) {
 rating = "Normal"
}
else if (score >= 30 && score <= 39) {
 rating = "Novice"
}
else if (score >= 20 && score <= 29) {
 rating = "Beginner"
}
else{
 throw new Error('Score is too low to rate');
}
```
I am going to show you how to take code blocks like the one above, and implement them in much less lines of code.

*What exactly is wrong with if-else statements?*

**Nothing! **
To be clear, an if-else statement executes a statement if a specific condition is [truthy](https://developer.mozilla.org/en-US/docs/Glossary/truthy), if it is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/falsy), another statement can be executed.
This has been the standard for conditionally executing statements for a long time, but writing code this way can quickly become tedious and cumbersome. Thankfully, Javascript provides other ways of determining if a condition is truthy or not and we can harness these abilities to write shorter and more concise conditional statements.

The Alternatives
--
Here's a list of the shorthand coding techniques and scenarios I will be discussing, I will also cover how and when to use them as well as their advantages.
1. If Checks
2. Multiple If checks
3. Short-circuit evaluation
4. Logical operators
5. Lookup tables
6. Ternary operators
7. Ternary Function calls

If Checks
==

This technique is a bit trifling but will come in handy in certain situations. When doing "if checks" assignments, operators can sometimes be omitted.

**Longhand statement**
```js
if(a == true){
 console.log(//something)
}
```
**Shorthand statement**
```js
if(a)console.log(//something)
```
Here's an example of logging something to the console if the variable `a` is true, the long hand statement checks that `a` has been defined and is truthy, but since in Javascript all values are truthy unless they are defined as falsy the shorthand statement will still execute.

Multiple If Checks
==
Consider a scenario where there are multiple conditions in your if statement, this technique provides a simple way to make it shorter and less verbose.

**Longhand statement**
```js
if(x == 1 || x == 5 || x == 7) {
 console.log('X has some value');
}
```
**Shorthand statement**
```js
if([1, 5, 7].includes(x)) {'X has some value'}
```
In this example, we implement the technique by creating an array from the values used for the conditions and then checking through them until one of the conditions passes. It gets the same job done in less time😉. Find out more about the includes array method here:  [Includes array method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes).


Short-circuit Evaluation
==
This technique comes in handy when you want to assign a variable to another one and need to check that it is defined.

**Longhand statement**
```js
if (a !== null || a !== undefined || a !== "") {
 var something = a;
} else {
 var something = 'default';
}
```

**Shorthand statement**
```js
var something = a || 'default';
```
Instead of writing a statement with multiple conditions to ensure that the variable is defined, we can use a short-circuit evaluation as seen in the example. 
Here 'something' is assigned `a` if `a` is truthy (as I mentioned earlier, all declared values & variables are truthy unless declared otherwise), if it is not it, is assigned the value 'default'. 
This technique makes use of logical operators while assigning, I will discuss using logical operators next.
Short-circuit expressions allow you to validate the source variable while assigning it to a new variable, with fewer words, as opposed to writing an if statement to perform this validation. It makes the process easier and will ensure less clutter in your code.

Logical operators
==
As I earlier mentioned the if-else statement executes a statement if a specific condition is truthy and if it is not, it executes another, here's how MDN describes the `&&` logical operator.

> … when used with Boolean values, && returns true if both operands are true; otherwise, returns false.
> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Logical) 
 
The `&&` operator, during execution, checks the first expression to see if it is truthy, if it is, it returns the second expression, if it is not, it returns `false`.
For example: 
```js
true && true //# since exp 1 is true, true (exp 2) will be returned
false && true //# since exp 1 is false, false will be returned regardless of the 'truthiness' of exp2
```
Putting this in mind, we can use the `&&` operator to validate expressions. Copy and paste the example below in your console and see the output
```js
(false) && console.log("I am true")
```
switch `false` for `true` and see the result.

The `&&` operator can be merged with other logical operators like the `||` operator. Here is how MDN describes the `||` logical operator.

> … when used with Boolean values, || returns true if either operand is true; if both are false, returns false. 
> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Logical)

The `||` operator during execution, behaves slightly different from `&&`, it returns the first operator if it is truthy and if it is not it returns the second.
For example:
```js
true || true //# since exp 1 is true, true (exp 1) will be returned
false || true //# since exp 1 is false, true (exp 2) will be returned
false || false //# since exp 1 is false, false (exp 2) will be returned
```
Copy and paste the example below in your console and see the output
```js
(false) || console.log("I am true")
```
switch `false` for `true` and see the result.
Finally, let's see the logical operators in action.

**Longhand Statement**
```js
var knowledge = 10, status
if (knowledge > 50){
status = "You are smart, keep it up"
 }else{
status = "You are not dumb, keep pushing"
}
console.log("Based on your knowledge, "+status)
```

**Shorthand Statement**
```js
console.log("Based on your knowledge, ",(knowledge > 50) && "You are smart, keep it up" || "You are not dumb, keep pushing" )
```
Logical operators can be used to replace single if statements and perform checks in one line, it also allows you to conditionally output/execute certain statements based on a condition inline, without breaking your output.

Lookup tables
===
Consider a scenario where there are multiple if-else conditions and the behaviour of each condition is different, to shorten this we can use a lookup table. A similar implementation can be gotten from using a switch statement, however, using the lookup approach is cleaner.
The example below is good to go, so you can try it out in your console.

**Longhand Statement**
```js
var tribe = "Yoruba", stereoType
if (tribe == 'Yoruba') {
 stereoType = "be romantic and intelligent"
}
else if (tribe == 'Igbo') {
 stereoType = "be very entrepreneurial"
}
else if (tribe == 'Hausa') {
 stereoType = "be very generous"
}
else if (tribe == 'Ijaw') {
 stereoType = "live life to the fullest"
}
else if (tribe == 'Urhobo') {
 stereoType = "be beautiful people"
}
else if (tribe == 'Efik') {
 stereoType = "appreciate entertainment"
}
else{
 throw new Error("No stereotype available")
}
console.log(`They tend to ${stereoType}`)
```
**Shorthand Statement**
```js
var tribe = "Efikf"
var stereoType = {
 Yoruba: "be romantic and intelligent",
 Igbo: "be very entrepreneurial",
 Hausa: "be very generous",
 Urhobo: "be beautiful people",
 Ijaw: "live life to the fullest",
 Efik: "appreciate entertainment"
};
var check = function(){
console.log('They tend to '+stereoType[tribe])
}
stereoType[tribe]? check() : console.log('Stereotype for '+tribe+' not available ')
```
This look-up table example consists of an object that holds our statements, a function that houses the execution and a ternary if-else expression to handle errors. The look-up table can be written in different manners and may not even need the function, but this would most definitely save you time instead of writing a 16 line long if-else statement.

Ternary operators
===
This is a great code saver when you intend to write an if-else statement in one line.
These are the advantages of using ternary operators, these also apply to most of the other short-hand statements, so I would say this once, for all.
1. Makes writing code simple, and the if-else statement quicker
2. Allows you to perform a conditional execution inline with your output
3. Shortens the lines of code you have to write
4. Makes code maintenance easier

**Longhand Statement**
```js
const a = 60;
let position;
if (a >= 50) {
 position = "you are more than halfway there";
} else {
 position = "you are not up to halfway there";
}
```
**Shorthand Statement**
```js
const position = a >= 50 ? "you are more than halfway there": "you are not up to halfway there";
```
The major syntax for the ternary operators is the `?` and `:`, your conditions come before the `?` sign, if the condition passes the statement to the left of the `:` sign executes, else the statement to the right of `:` gets executed.
You can nest the statements as such:
```js
const position = a == 50 ? "you are halfway there" : a > 50 ? "you are more than halfway there" : "you are not up to halfway there yet";
```
Another important use case of ternary operators is during output (while logging a value to the console) 
```js
console.log(`Based on your score, you are `,position == 50 ? 'close to' : 'far from', `your destination`); 
```

Ternary Function calls
=== 
The ternary operator can also be used to call a function conditionally, 
```js
# consider these functions
function printA () { console.log('A')}
function printB () {console.log('B')}
```

**Longhand Statement**
```js
var isTrue = true;
if (isTrue) {
 printA();
} else {
 printB();
}
```
**Shorthand Statement**
```js
(isTrue ? printA : printB)();
```
This can easily save us 6 lines of code 😊.

Here are a few tips to consider when using ternary operators, some of these also apply to some of the other short-hand statements.
1. Do not overuse these shorthand statements, making them too complicated can make your code hard to maintain.
2. Avoid stacking ternary operators, it can cause unexpected behaviours, if the statement is becoming complicated, make use of a standard if-else statement.
3. If you aren't experienced with using shorthand statements, write your code using if/else first, then translate the code into a shorthand statement.
4. Use parentheses as much as possible, to separate parts of your code, and to keep your code organized, but not so many that you create "code soup."
5. If you work in a team setting, make sure the other programmers understand your code.

Finally
--

Using shorthand statements is awesome, but sometimes the good old if-else statement may be best to use. One thing you should consider before using a shorthand statement is the condition, most shorthand statements with single value conditions would work as long as the value is truthy which is an unstrict way of performing conditional checks.
```js
var loveJavascript = "true"
if (loveJavascript === true){console.log("I love Javascript")}
```
The example above wouldn't work because `loveJavascript` is assigned a string and not `true`, but using a single value condition in a ternary/logical statement would work regardless, as long as `loveJavascript` was defined (is truthy)
```js
(loveJavaScript) && console.log("I love Javascript")
```
You can research more about this in MDN's documentation of [truthy](https://developer.mozilla.org/en-US/docs/Glossary/truthy), [falsy](https://developer.mozilla.org/en-US/docs/Glossary/falsy) and [conditional statements](https://developer.mozilla.org/en-US/docs/Glossary/Boolean).


Hey, this is my first article here, so if you like it,  kindly leave an encouraging comment below. Constructive criticism is also expected and appreciated. Cheers.

