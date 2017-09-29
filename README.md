### Table Of Content
- [1. Iterations](#lesson-1.-iterations)
    - [1.1. Binary Gap](#binary-gap)
- [2. Arrays](#lesson-2.-arrays)
    - [2.1. Cyclic Rotation](#cyclic-rotation)
    - [2.2. Odd Occurrences In Array](#odd-occurrences-in-array)
- [3. Time Complexity](#3-time-complexity)
    - [3.1. Perm Missing Element](#perm-missing-element)
    - [3.2. Frog Jump](#frog-jump)
    - [3.3 Tape Equilibrium](#tape-equilibrium)
- [4. Counting Elements](#4-counting-elements)
    - [4.1. Missing Integer](#missing-integer)
    - [4.2. Frog River One](#frog-river-one)
    - [4.3. Perm Check](#perm-check)
    - [4.4. Max Counters](#max-counters)
- [5. Prefix Sums](#5-prefix-sums)
    - [5.1](#count-div)
    - [5.2](#passing-cars)
    - [5.3](#genomic-range-query)
    - [5.4](#min-avg-two-slice)
- [6. Sorting](#6-sorting)
    - [6.1. Distinct](#distinct)
    - [6.2. Max Product Of Three](#max-product-of-three)
    - [6.3. Triangle](#triangle)
    - [6.4. Number Of Disc Intersections](#number-of-disc-intersections)
- [7. Stacks And Queues](#7-stacks-and-queues)
- [8. Leader](#8-leader)
- [9. Maximum Slice Problem](#9-maximum-slice-problem)
- [10. Prime And Composite Numbers](#10-prime-and-composite-numbers)
- [11. Sieve Of Eratosthenes](#11-sieve-of-eratosthenes)
- [12. Euclidean Algorithm](#12-euclidean-algorithm)

### [Lesson 1. Iterations](https://codility.com/programmers/lessons/1-iterations/)
#### [Binary Gap](https://codility.com/programmers/lessons/1-iterations/binary_gap/)
> Solution: Either use String method - Match [(see MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Match) or simply iterate through binary representation of a given number as shown in second solution function.
```javascript
function solution (N) {
    const gaps = N.toString(2).match(/(0+)(?=1)/g);
    return gaps ? gaps.sort((a, b) => b.length - a.length )[0].length : 0;
}
```

```javascript
function solution (N) {
    const num = N.toString(2);
    let longestGap = 0;
    let currentGap = 0;
    for (let i = 0; i < num.length; i++) {
        if (num[i] === '1') {
            if (longestGap < currentGap) {
                longestGap = currentGap;
            }
            currentGap = 0;
        } else {
            currentGap = currentGap + 1;
        }
    }
}
```

### [Lesson 2. Arrays](https://codility.com/programmers/lessons/2-arrays/)
#### [Cyclic Rotation](https://codility.com/programmers/lessons/2-arrays/cyclic_rotation/)

> Solution: Iterate K times while removing last element of given array and adding it to the beginning of an array.
```javascript
function solution (A, K) {
    if (!K || A.length < 2) return A;
    const array = A.slice();
    let lastElem;
    for (let i = 0; i < K; i++) {
        let lastElem = array.pop();
        array.unshift(lastElem);
    }
    return array;
}
```
> Solution: Find index of an element that will be first element of an array after rotation.
> **(K modulo A.len)** will return index of slice.
> Elements with index bigger than slice index are first part of answer array.
> Elements with index smaller than slice index are second part of answer array.
```javascript
function solution (A, K) {
    const len = A.length;
    if ( !K || !(K % len) || len < 2 ) return A;
    const beginIndex = (K % len) * -1;
    const answer = A.slice(beginIndex).concat(A.slice(0, len + beginIndex));
    return answer;
}
```

#### [Odd Occurrences In Array](https://codility.com/programmers/lessons/2-arrays/odd_occurrences_in_array/)
> Solution: Use XOR [(see MDN)](https://developer.mozilla.org/pl/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_XOR)
```javascript
function solution (A) {
    let answer = 0;
    for (let i = 0; i < A.length; i++) {
        answer = answer ^ A[i];
    }
    return answer;
}
```

> Worst-case time complexity probably is O(N * log(N)) - evaluated as 100%
```javascript
function solution (A) {
    const ar = A.slice().sort( (a, b) => a - b );
    for (let i = 0; i < ar.length; i = i + 2) {
        if (ar[i] !== ar[i + 1]) return ar[i];
    }
}
```

### 3 Time Complexity
#### Perm Missing Element
```javascript
function solution (A) {
    let sum = 0;
    for (let i = 0; i < A.length; i++) {
        sum = sum + A[i];
    }
    return ((A.length + 1) * (A.length + 2)) / 2 - sum;
}
```
> Hint - see Sum of Arithmetic Progression

#### Frog Jump
```javascript
function solution (X, Y, D) {
    return Math.ceil((Y - X) /D);
}
```

#### Tape Equilibrium
```javascript
function solution (A) {
    let left = 0;
    let right = A.reduce((s, elem) => s + elem);
    let answer = false;
    for (let i = 0; i < A.length - 1; i++) {
        left = left + A[i];
        right = right - A[i];
        const diff = Math.abs(left - right);
        if (answer === false) {
            answer = diff;
        } else {
            answer = diff < answer ? diff : answer;
        }
    }
    return answer;
}
```

### 4 Counting Elements
#### Missing Integer
```javascript
function solution (A) {
    const results = [0];
    for (let i = 0; i < A.length; i++) {
        if (A[i] > 0 && !results[A[i]]) {
            results[A[i]] = A[i];
        }
    }
    for (let i = 0; i < results.length; i++) {
        if (results[i] === undefined) return i;
    }
    return results.length;
}
```

#### Frog River One
```javascript
function solution (X, A) {
    const leaves = new Array(X + 1).fill(false);
    let riverCovered = X;
    for (let i = 0; i < A.length; i++) {
        if (!leaves[A[i]]) {
            leaves[A[i]] = true;
            riverCovered = riverCovered - 1;
        }
        if (!riverCovered) {
            return i;
        }
    }
    return -1;
}
```

#### Perm Check
```javascript
function solution (A) {
    const nums = [0];
    for (let i = 0; i < A.length; i++) {
        nums[A[i]] = A[i];
    }
    for (let i = 1; i <= A.length; i++) {
        if (nums[i] !== i) {
            return 0;
        }
    }
    return 1;
}
```

#### Max Counters
```javascript
function solution (N, A) {
    const counters = new Array(N).fill(0);
    let min = 0;
    let max = 0;
    for (let i = 0; i < A.length; i++) {
        if (A[i] > N) {
            min = max;
        } else {
            if (min <= counters[A[i] - 1]) {
                counters[A[i] - 1] = counters[A[i] - 1] + 1;
            } else {
                counters[A[i] - 1] = min + 1;
            }
            max = max < counters[A[i]- 1] ? counters[A[i] - 1] : max;
        }
    }
    for (let i = 0; i < counters.length; i++) {
        if (counters[i] < min) {
            counters[i] = min;
        }
    }
    return counters;
}
```

### 5 Prefix Sums
#### Count Div
```javascript
function solution (A, B, K) {
    return Math.floor(B / K) - Math.floor((A - 1) - K);
}
```
#### Passing Cars
```javascript
function solution (A) {
    let eastCars = 0;
    let passingCars = 0;
    for (let i = 0; i < A.length; i++) {
        if (A[i] === 0) {
            eastCars = eastCars + 1;
        } else {
            passingCars = pasingCars + eastCars;
        }
        // Check condition
        if (passingCars > 1000000000) {
            return -1;
        }
    }
    return passingCars;
}
```
#### Genomic Range Query
#### Min Avg Two Slice


### 6 Sorting
#### Distinct
```javascript
function solution (A) {
    const array = A.slice();
    array.sort((a, b) => a - b);
    let distinct = 0;
    let currentNumber = null;
    for (let i = 0; i < array.length; i++) {
        if (array[i] !== currentNumber) {
            currentNumber = array[i];
            distinct = distinct + 1;
        }
    }
    return distinct;
}
```

#### Max Product Of Three
```javascript
function solution (A) {
    const array = A.slice();
    array.sort((a, b) => a - b);
    const len = array.length;
    const negMax = array[0] * array[1] * array[len - 1];
    const posMax = array[len - 1] * array[len - 2] * array[len - 3];
    return negMax > posMax ? negMax : posMax;
}
```

#### Triangle
```javascript
function solution (A) {
    if (A.length < 3) return 0;
    const array = A.slice();
    array.sort((a, b) => a - b);
    let answer = 0;
    for (let i = 0; i < array.length - 2; i++) {
        const a = array[i];
        const b = array[i + 1];
        const c = array[i + 2];
        if (a + b > c && a + c > b && b + c > a) ans = 1;
    }
}
```

#### Number Of Disc Intersections
```javascript
function solution (A) {
    const discPoints = [];
    for (let i = 0; i < A.length; i++) {
        discPoints.push([i - A[i], 0], [i + A[i], 0]);
    }
    discPoints.sort((a, b) => {
        if (a[0] === b[0]) {
            return a[1] - b[1];
        } else {
            return a[0] - b[0]
        }
    });
    let answer = 0;
    let openDiscs = 0;
    let closedDiscs = 0;
    for (let i = 0; i < discPoints.length; i++) {
        if (!discPoints[i][1]) {
            openDiscs = openDiscs + 1;
        } else {
            closedDiscs = closedDiscs + 1;
            openDiscs = openDiscs - 1;
            answer = answer + openDiscs;
        }
    }
    return answer > 10000000 ? -1 : answer;
}
```

### 7 Stacks And Queues
#### Brackets
#### Fish
#### Stone Wall
#### Nesting

### 8 Leader
#### Dominator
#### EquiLeader

### 9 Maximum Slice Problem
#### Max Profit
#### Max Double Slice Sum
#### Max Slice Sum

### 10 Prime And Composite Numbers
#### Min Perimeter Rectangle
#### Count Factors
#### Peaks
#### Flags

### 11 Sieve Of Eratosthenes
#### Count Semiprimes
#### Count NonDivisible

### 12 Euclidean Algorithm
#### Chocolates By Numbers
#### Common Prime Divisors
