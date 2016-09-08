#Big O Drills Solutions


1. `compare`

    ```js
    function compare(a,b){
        if (a > b) {
            return 1;
        } else if (a === b){
            return 0;
        } else {
            return -1
        }
    }
    ```

    `compare` always does up to 2 calculations (comparisons), no matter what the size of  `a` and `b` are. So `compare` = O(1).

1. `mid`   

    ```js
    function mid(arr){
        var midIndex;                       // declaration is O(1)
        if(arr.length % 2 === 0){           // array length lookup and % are O(1)
            midIndex = arr.length/2;        // array length, division, assignment all O(1)
        }else {
            midIndex = (arr.length-1)/2;    // division and subtraction both O(1)
        }
        return arr[midIndex];               // array lookup O(1)
    }
    ```

    `mid` does
    * one lookup of `arr.length`
    * one calculation with `%`
    * another lookup of `arr.length`
    * one or two more calculations to find the middle index
    * a lookup to find the array element at the middle index

    Each of these 5-6 individual operations is O(1), so we have 5 * O(1) = O(1) or 6 * O(1) = O(1).

    Whether the array has 3 elements, or 8, or 10000000, or n, `mid` always does the same 5 or 6 operations.  

    Since the number of calculations/operations does **not** depend on the size of the input, `mid` is O(1).



1. `max`

    ```js
    function getMax(arr){
        var currentMax = 0;                     // assignment is O(1)

        for (var i=0; i<arr.length; i++){       // for loop runs arr.length times = n times
            if (arr[i] > currentMax){               // comparison and array lookup are O(1)
                currentMax = arr[i];                // assignment and lookup are O(1)
            }
        }
        return currentMax;
    }
    ```

    `getMax` does O(1) + n*O(1) = O(1) + O(n) = O(n)

1. `indexOf`

    ```js
    function indexOf(num, arr){                 
        var foundIndex = null;                  // O(1)
        for (var i=0; i<arr.length; i++){       // n times (worst case scenario)
            if (arr[i] === num){                    // O(1)
                foundIndex = i;                     // O(1)
            }
        }
        return foundIndex;
    }
    ```

    `indexOf` does O(1) + n*O(1) = O(1) + O(n) = O(n)


1. `countNums`

    ```js
    function countNums(arr){
        var output = {};                    // O(1)
        for (var i=0; i<arr.length; i++){   // n times:
            if (output[arr[i]] === undefined){      // O(1)
                output[arr[i]] = 1;                 // O(1)
            } else {
                output[arr[i]] += 1;                // O(1)
            }
        }

        // bonus section: printing the counts
        for (num in output){                            // n times or fewer
            if (output.hasOwnProperty(num)){                // O(1)
                console.log(num+": ", output[num]);         // O(1)
            }
        }
        return output;
    }
    ```

    `countNums` does O(1) + n*O(1) + (n or less)\*O(1) = O(1) + O(n) + O(n) = O(n)

    We can simplify (n or less) * O(1) to O(n) because big O notation overestimates. It gives us an UPPER limit on how long our algorithms take.  If we overestimate, this upper limit is still valid (though if we overestimate too much it's not helpful.)


1. `findShared`

    ```js
    function findShared(arr1, arr2){
        var shared = [];                    // O(1)
        for (var i=0; i<arr1.length; i++){  // arr1.length times (we'll say n)
            for (var j=0; j<arr2.length; j++){     // arr2.length times (we'll say m)
                if (arr1[i] === arr2[j]){                   // O(1)
                    if (shared.indexOf(arr1[i]) === -1){    // O(1)
                        shared.push(arr1[i]);
                    }
                }
            }
        }
        return shared;
    }
    ```

    If we call the length of `arr1` n and the length of `arr2` m, `findShared` does O(1) + n \*(m * O(1)) = O(1) + n * O(m) = O(1) + O(m * n) = O(m * n)

    Again, we can simplify by sacrificing some accuracy and overestimating. If we say n is the size of the bigger array, we can overestimate the time this algorithm needs as O(n * n) = O(n<sup>2</sup>).
    
