# Big O Notation and Algorithm Analysis

###What is an algorithm?

A set of instructions to find the solution to a problem.

Note: we use code to *implement* algoritms, but algorithms don't have to be expressed in code. It's usually better to talk through or write out the general strategy of an algorithm before trying to code it.

###What is efficiency?

Time efficiency helps us predict how long it could take a particular algorithm to run. Space efficiency helps us predict how much memory a particular algorithm could use up.

###Why study algorithms and efficiency?

* Understanding algorithms let us reuse knowledge from the field.

* Better-performing algorithms can enhance the user experience by decreasing wait times or improving results.

* Better-performing algorithms can save companies money by reducing equipment needs.

* Algorithms and algorithm analysis are an important part of the shared language developers use to talk about programs (especially in **INTERVIEWS!**).


##Big O notation

### Big O Intro 

Big O notation gives us a simplified way to talk about the  time and space requirements of an algorithm (often called time and space "complexity").  

1. Ask yourself: In the worst case scenario, about how many calculations does your algorithm do?
2. Phrase the answer in terms of the size of the input.  
3. Ignore constant multiples or smaller things added on.



If we tried to get a 100% accurate picture of how long an algorithm would take, the analysis required would be so complex it wouldn't be useful.  We'd basically have to use the algorithm, or run the function, and record how long it took.

So Big O notation makes step one above WAY easier by pretending computers are simpler than they actually are.   

Big O notation usually looks like this:  O(1), O(log(n)), O(n), O(n*log(n)), O(n<sup>2</sup>), O(2<sup>n</sup>)...  where `n` is the size or number of inputs.

Big O notation gives an upper limit for how long or how much space an algorithm could take. The idea is it's safer to overestimate how much time something could take than to underestimate. Still, we try to get estimates that are close to what time or space will actually be required.

Remember: Big O overestimates. An algorithm is O(n) if (and only if) the time it takes to complete the algorithm is **less than or equal to** some constant multiple of the number of inputs.  



### Big O Guidelines

#### O(1) operations

To say an algorithm takes O(1) time means no matter how big the input(s) are, the computer will do basically same amount of work to perform the algorithm on them.  

We will consider all mathematical operations on normal-size numbers or characters O(1).  In Big O notation, these are **O(1)** operations: `+`, `-`, `*`, `/`, and `%`.  

```js
function returnZero(){
    return 0;
}

function add(a,b){
    return a+b;
}
```

We also assume that comparisons ( `<` ) are constant time operations, and that handling for `function`s or `def`s, `if`s, and `return`s is usually constant time too.


Note that in the example below, we always subtract once, divide once, and return once. The same sequence of O(1) operations is carried out no matter what the problem size is, so you might think of the the total time as 3*O(1).  Big O ignores constant multiples, so this is still just expressed in big O noation as O(1).

```js
function average(a,b){
    return (a-b)/2;
}
```


#### O(n)

To say an algorithm takes O(n) time means that the computer will do more work to perform the algorithm if the inputs are larger or if there are more inputs -- *and* that the increase in work done mirrors the incresase in the size or number of inputs.

Algorithms that process each input at least once are generally implementing algorithms that will take at least **O(n)** time.  Functions containing loops that go through the whole input are a common example.  

```js
function addAll(numArray){
    var sum = 1;                             // O(1)
    for (var i=0; i<numArray.length; i++){   // n times:
        sum +=  numArray[i];                        // O(1)
    }
    return sum;                              // O(1)
}
```

The time complexity of `addAll` is `O(1) + n*O(1) + O(1)`, which simplifies to `O(n) + O(1)` and finally to `O(n)`.

See how the for loop acts like a multiplier for the O(1) operation(s) happening inside?  If the stuff inside the for loop required more time, like say if it were O(n), we'd still have to multiply. We'd get `O(1) + n*O(n) + O(1)` which would simplify to O(n<sup>2</sup>).


####O(log(n)) or O(n*log(n))

Logarithm terms in Big O notation usually come from recursive functions or scenarios where we use the "divide and conquer" approach. For interview prep purposes, some good rules of thumb are:

* searching through a sorted array takes O(log(n)) time  
* sorting an array takes O(n*log(n)) time



####Combinations

Almost everything else is composed of combinations of the times we've looked at so far. For example, if a for loop has more complex operations inside it, time complexity is usually higher.

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


**Graph: how the number of operations (time) grows with the number of input elements for various orders of complexity**

![time complexity graph from Yaacov Apelbaum, apelbaum.wordpress.com](https://apelbaum.files.wordpress.com/2011/10/yaacovapelbaumbigoplot.jpg)


**[Exercises](exercises.md)**
