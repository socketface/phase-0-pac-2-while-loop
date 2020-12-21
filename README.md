# Repetition: the `while` Loop

## Learning Goals

* Define the basic `while` structure
* Write an infinite loop
* Use Control-C to break out of an infinite loop
* Terminate a `while` loop naturally
* Learn about operators used to increment/decrement
* Use a `do...while` loop

## Introduction

The final piece of using _statements_ to control the flow of JavaScript execution is
**repetition**.

![Repetition Graphic](https://curriculum-content.s3.amazonaws.com/programming-univbasics-2/sequence-and-comments/Repetition_thick.png)

While the **default sequence** requires JavaScript to execute top-down, left to
right, we've seen that we can skip chunks of code using _selection_ statements
(`if` or `switch`). In some ways the reverse of _selection_ is _repetition_:
"Don't move on," we tell JavaScript. "Instead do something else until I say it's
OK to move on." The most fundamental _repetition_ construct, present in pretty
much every programming language, is the `while` loop.

## Define the Basic `while` Structure

A basic `while` loop looks like:

```js
while (condition expression) {
 // stuff to do
}
```

As long as the condition expression is `true` (or truthy), the code inside the
code block will run. Keep in mind the condition expression can be quite rich,
using `&&`, `||`, `()`, etc.

## Write an Infinite Loop

Given this definition of `while`, any truthy expression will make the loop run
forever.

```js
while (true) {
  console.log("say this forever...");
}
```

This will output:

```text
say this forever...
say this forever...
say this forever...
say this forever...
say this forever...
...
```

Note that the condition expression doesn't need to be the literal value `true`
&mdash; any truthy value will have the same effect:

```js
while (-1) { // -1 is truthy....
  console.log("say this forever...");
}
```

By contrast, a `false` (or falsey) condition expression will keep the code block
from executing at all:

```js
while (null) {
  console.log("I will never run");
}
```

## Use Control-C to Break Out of an Infinitely Looping Program

When you start writing code and creating loops yourself, you will almost
certainly inadvertently create infinite loops from time to time. If you try to
run the code and it either logs over and over without end **or** never seems to
finish, you're probably stuck in an infinite loop.

In most programming environments (including repl.it), you can break out of an
infinite loop by typing Control-C. That's an old-school UNIX key combination
that means INTERRUPT. In order for this to work, you first need to make the
terminal portion of the programming environment (where the results of running
the code are displayed) the active window by clicking inside it.

Give it a try here:

<iframe height="400px" width="100%" src="https://repl.it/@LizBurton/QuietNervousRotation?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Don't forget to click in the terminal (the window on the bottom) before typing
Control-C!

## Terminate a `while` Loop Naturally

Most loops aren't meant to run infinitely. There's some condition that they
cross, captured in the _condition expression_, that tells JavaScript that it's
time to return to the **default sequence** and execute the code after the while
loop.

So, somehow we need to create an expression that's true when the `while` begins
(so that the code in the `{}` runs), but that eventually becomes false.

Here's a simple example:

```js
let count = 0; // A bit of data defined outside the loop; note that we need to use `let` here
while (count < 3) { //A Boolean expression using the bit of data
  console.log(`I am the ${count}, I love to count!`); // The work the loop does
  count = count + 1; // A bit of work that moves the bit of data closer to being false
}
```

In the line `count = count + 1`, we are _assigning_ a new value to the `count`
variable, where the new value is equal to its current value plus 1.

The code above produces:

```text
I am the 0, I love to count!
I am the 1, I love to count!
I am the 2, I love to count!
```

Let's say we forgot the line `count = count + 1`. Our _condition expression_
would then _always_ be `true` and we'd have an infinite loop.

## Learn About Operators Used to Increment/Decrement

Let's look back at that previous example to notice how we're moving from a
true or truthy statement to a false or falsey statement. Within each loop, the
following code is executed:

```js
count = count + 1
```

which slowly moves `count` to a place where it is no longer less than 3, thus
ending the loop.

But writing `count = count + 1` is a bit long-winded (although very explicit;
sometimes a few extra keystrokes can save you headaches with debugging,
especially when you're first learning to code). This pattern of "incrementing" a
variable is very common, so JavaScript includes a couple of shorthand operators
you can use. It's like a contraction in conversation: very few English speakers
say "can not," "have not," or "would not" **all** the time. You're likely to
hear them use _contractions_ (from the Latin: "pulling together") like "can't,"
"haven't," and "wouldn't." In the code below, we are combining the addition and
assignment with the `addition assignment operator`, `+=`:

```js
count += 1 // take the value of count, add one to it and then assign that result to count
```

Unsurprisingly `-=` does the reverse of `+=`: it "decrements" the variable's
value and re-assigns the new value to the variable. JavaScript has a number of
other [assignment
operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#Assignment_operators)
that allow you to use multiplication (`*=`), division (`/=`), and a number of
other operations.

The assignment operators will work with any _number_. If you want to add 10 or
3.14 instead of 1, the assignment operators will do that for you. For the
special (but common) case where you want to add (or subtract) 1, however, there
is another option: the [increment and decrement
operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#Increment_and_decrement),
`++` and `--`. For a case such as the above, where we're using a counter
variable to keep track of where we are in our loop, the `increment operator` is
frequently used:

<iframe height="400px" width="100%" src="https://repl.it/@LizBurton/EuphoricNoteworthyMuse?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Try out the different options and experiment with writing some loops of your own.

## Use a `do...while` Loop

The `do...while` loop is similar to `while`, in that it will execute a block of
code based on a condition or set of conditions. The difference, however, is that
**it will always execute at least once**. The reason is that the condition isn't
evaluated until **after** the code block executes the first time:

```js
do { 
  console.log(`I will execute once`); 
} while (false);
```

The JavaScript engine will enter the loop, execute the console.log, then evalute
the condition. Because the condition returns `false` the loop will stop
executing there.

This construction is helpful any time you want to make sure that the loop
executes at least once. As an example, this might be useful for asking a user to
create a password. The `do while` loop will always ask them to enter their
password the first time, and can continue to ask as long as (`while`) the value
they enter doesn't meet the password requirements.

## Conclusion

In this lesson, we have learned how to use a _repetition_ statement, the `while`
loop. JavaScript includes some other looping mechanisms that you'll learn about
later in the course. But for now, with an understanding of _sequence_,
_selection_ and now _repetition_ on top of your experience with expressions, you
can write powerful programs! Be sure to experiment with writing your own loops
and don't forget, if your code is not responding, you can use Control-C to
interrupt the program!
