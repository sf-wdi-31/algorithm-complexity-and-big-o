<!--
Creator:
Location: SF
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Big O Notation and Algorithm Complexity

### Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

- Understanding algorithms let us reuse knowledge from the field.
- Better-performing algorithms can enhance the user experience by decreasing wait times.
- Better-performing algorithms can save companies money by reducing equipment needs.
- Algorithms and algorithm analysis are an important part of the shared language developers use to talk about programs (especially in **INTERVIEWS!**).

### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

- Articulate a set of steps to determine Big O complexity.
- List the Big O complexities of some commonly-used patterns and algorithms.
- Estimate the time or space efficiency  of an algorithm using Big O notation.

### Where should we be now?
<!-- call out the skills that are prerequisites -->
*Before this workshop, developers should already be able to:*

* Write and interpret `for` loops.
* Write and interpret `if/else if/ else` structures.
* Compare and contrast linear or "brute force" search with binary search.

# Big O Notation and Algorithm Analysis

###What is an algorithm?

An algorithm is a set of instructions to find the solution to a problem.  It gives step-by-step operations to be performed that will take you from *any* valid input for the problem to an output.

We've been creating algorithms, in one form or another, throughout this class.

###What is efficiency?

Whenever we create algorithms, we need to be aware that they run on computers, and computers require time and space (memory) to process every instruction.

Even though most of the algorithms we've written seem to run instantaneously, "instant" algorithms can possibly take minutes or days to run if there's too much input data to process.  For scalability and large systems, it's important to take into account the time and space an algorithm will need to run with larger sizes of inputs.

**Developers need ways to predict how _efficient_ an algorithm is when we give it different sizes of inputs.** This is measured in terms of:

- Time or "runtime" (how much processing time does it use in the CPU)
- Space (how much memory does it take up)

If we tried to get a 100% accurate picture of how long an algorithm would take, the analysis required would be so hard it wouldn't be useful for predictions.  We'd basically have to use the algorithm, or run the function, and record how long it took.  

Instead of getting exact values, developers often estimate the efficiency of an algorithm.

The most common way to express these estimates is using what is called Big O Notation.

##Big O Notation

### Big O Intro

Big O notation gives us a simplified way to talk about the  time and space requirements of an algorithm (often called time and space "complexity").  To identify an algorithm's complexity, we focus on the "family" of scaling functions the algorithm belongs to. We don't care about exact values.


## Common Big O Values


| Input Size (N) |	O(1) |	O(log(N))	 |  O(N)	| O(Nlog(N))	| O(N<sup>2</sup>) |
| :-------------: |	:-------------: |	:-------------:	 | :-------------:	| :-------------:	| :-------------: |
| 1	| 1	 | 0 | 1 |	1 |	1 |
| 8	| 1	|  3	| 8 | 24 | 64  |
| 30	 | 1 | 	~5	 | 30 | 150 | 	900 |
| 500	 | 1 | 	~9	 | 500 | 4500 | 250,000 |
| 1000 | 	1 | 	~10	 | 1000	 | 10,000 | 	1,000,000 |
| 16,000	 | 1	 | ~14	 | 16,000	 | 224,000  | 	256,000,000 |
| 100,000	 | 1	 | ~17	 | 100,000	 | 1,700,000  | 	10,000,000,000 |


Observe how curves for different complexities compare to each other.
- O(1) is a totally flat line. It's constant no matter how much data is given to it.
- O(log(n)) goes up, then nearly flattens out.
- O(n) goes up and right in a straight line.
- O(n2) starts to spike up sharply as input size gets large.


**Graph: how the number of operations (time) grows with the number of input elements for various orders of complexity**

![time complexity graph from Yaacov Apelbaum, apelbaum.wordpress.com](https://apelbaum.files.wordpress.com/2011/10/yaacovapelbaumbigoplot.jpg)


Big O notation gives an upper limit for how long or how much space an algorithm could take. We try to get estimates that are close to what time or space will actually be required, but Big O is a guarantee that that the resources it takes to complete the algorithm, as inputs grow infinitely large, will be less than or equal to some constant multiple complexity of an algorithm.

> Note: Those constant multiples can get *really* large, meaning sometimes an O(n) algorithm will run faster than an O(log (n)) algorithm.



### Rules for Evaluating Complexity

How can you predict the complexity of a given algorithm? We can look for certain
features to help us characterize it.

-   Think of a name (often `n`) for the size of the input. If you have multiple inputs, like `arr1`, `arr2`, assign different names for each one (size of `arr1` is `n`; size of `arr2` is `m`).
-   For consecutive statements, add the complexities of each.  
-   For branching statements (`if/else`), use the complexity of the worse
    branch.
-   For loops, multiply the maximum number of times the loop can run by the complexity of the work inside the loop.
-   Simplify: eliminate constant multiples within parentheses (`O(2n)` -> `O(n)`), constant multiples of a single big-o family (`8*O(n)` -> `O(n)`), and entire smaller terms (`O(n) + 3*O(1)` -> `O(n)`).  Don't remove smaller terms that use a different name for the input size: `O(n) + O(log(m))` doesn't simplify.


#### O(1)

To say an algorithm takes constant (or `O(1)`) time means: no matter how big the input(s) are, the computer will do basically same amount of work to perform the algorithm on them.

Constant time steps are the building blocks of algorithms - they correspond to the most basic steps a computer can take.    

We'll consider most mathematical operations to be `O(1)`: `+`, `-`, `*`, `/`, `%`, `<`, `>`. `==`, `===`.  (This assumes that the numbers are all with some limited size like 32-bit numbers or 64-bit numbers.)

Assignment (`=`), `return`, and accessing a value in an array (`arr[4]`) or object (`obj['a']`) are other examples of steps that are considered `O(1)`.

```js
function isFirstUndefined(numArray){
  var first = numArray[0];
  return first === undefined;
}

function average(a,b){
    return (a-b)/2;
}
```

> Note that the algorithms above each perform more than one `O(1)` step. The key factor that makes the algorithms `O(1)` is that the amount of calculations doesn't depend on the size of the inputs `numArray`, `a`, or `b`.

> *Optional: Turn to a partner and convince each that the amount of calculations above doesn't depend on the size of the inputs.*

#### O(n)

To say an algorithm is linear or `O(n)` means the resources required grow proportionally to the size of the input.

Algorithms that process each input at least once will take at least **O(n)** time.  Loops are a common example.  

```js
function addAll(numArray){
    var sum = 1;                             // O(1)
    for (var i=0; i<numArray.length; i++){   // n times:
        sum = sum + numArray[i];                // O(1)
    }
    return sum;                              // O(1)
}
```

Following our [rules for evaluating complexity](#evaluating-complexity), the time complexity of `addAll` is `O(1) + n*O(1) + O(1)`. You might be tempted to call this `O(n) + 2*O(1)`, but don't forget to  simplify!  

<details><summary>*Optional: What would happen if the work going on inside the loop had been O(n<sup>2</sup>)?* </summary>

We still follow the exact same rules, so instead of the term from the loop being `n*O(1)`, we get `n` * O(n<sup>2</sup>), which yields O(n<sup>3</sup>).
</details>


####O(log(n))

Any algorithm which cuts the problem size in half each at each step is logarithmic or `O(log n)`.

These algorithms take longer for larger inputs, but the rate of increase is very slow compared to a lot of other possibilities.

<details><summary>*Optional: Can you think of an example of an `O(log n)` algorithm?*</summary>

An common example is finding an item in a sorted list with a balanced search tree or a binary search! Here's some pseudocode:

```ruby

def binary_search(array, value, low=0, high=array.size-1)
  # if high and low overlap, nothing was found.
  return false if high < low
  # Determine the middle element.
  mid = low + ((high - low) / 2)
  # Split the result in half and search again recursively until we succeed.
  if array[mid] > value
    return binary_search(array, value, low, mid-1)
  elsif array[mid] < value
    return binary_search(array, value, mid+1, high)
  else
    return mid # Found!
  end
end
```

> Just kidding; that "pseudocode" is Ruby!

</details>

> Note: The base of a logarithm doesn't matter (as long as it doesn't depend on n) because it can be changed with a constant multiplier. Check out the "change of base" formula for a review.


####O(n log(n))

You'll usually see `O(n log(n))` in "divide and conquer" algorithms that cut a problem into halves, *solve both halves*, and combine the results into a final solution.  This `O(n log(n))` complexity is famous for being the fastest possible time complexity of sorting algorithms on unrestricted inputs.

Of course, this would also be the time complexity of a loop that ran `n` times and did  `O(log(n))` work inside.

#### O(2<sup>n</sup>)

An O(2<sup>n</sup>) algorithm requires double the resources for each additional input. This is an example of exponential growth - and it gets out of hand very quickly.

```
function fibonacci(num) {
  if (num <= 1){
    return num;
  } else {
    return fibonacci(num - 1) + fibonacci (num - 2);
  }
}
```


####Combinations

There are a few other common Big O families (notably `O(n!)`), but many problems are composed of combinations of the times we've looked at so far. For example, if a for loop has more complex operations inside it, time complexity is usually higher.

```js
function addAllArrays(arrayOfArrays){
    var sum = 1;
    var oneArray;
    for (var i=0; i<arrayOfArrays.length; i++){
        oneArray = arrayOfArrays[i];
        for (var j=0; j<oneArray.length; j++){
            sum +=  numArray[j];
        }
    }
    return sum;
}
```

## Extra Practice

More **[Exercises](exercises.md)** and their **[Solutions](solutions.md)** are available for you to try.


## Additional Resources

-   [Big-O Algorithm Complexity Cheat Sheet](http://bigocheatsheet.com/)
-   [Sorting Algorithm Animations](http://www.sorting-algorithms.com/)
-   [A Beginner’s Guide to Big O Notation « Rob Bell](http://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/)
-   [Fibonacci sequence - Rosetta Code](http://rosettacode.org/wiki/Fibonacci_sequence#Recursive_51)
-   [Bubble-sort with Hungarian ("Csángó") folk dance - YouTube](https://www.youtube.com/watch?v=lyZQPjUT5B4)
-   [Quick-sort with Hungarian (Küküllőmenti legényes) folk dance - YouTube](https://www.youtube.com/watch?v=ywWBy6J5gz8)
