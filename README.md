### Lesson 1 Iterations
#### Binary Gap
```javascript
    function solution (N) {
        const gaps = N.toString(2).match(/(0+)(?=1)/g);
        return gaps ? gaps.sort((a, b) => b.length - a.length )[0].length : 0;
    }

    // OR

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

### Lesson 2 - Arrays
#### Cyclic Rotation
```javascript
    function solution (A, K) {
        if (!K || A.length < 2) return A;
        const ar = A.slice();
        for (let i = 0; i < K; i++) {
            let last = ar.pop();
            ar.unshift(last);
        }
        return ar;
    }
```
#### Odd Occurrences In Array
```javascript
    function solution (A) {
        const ar = A.slice().sort();
        for (let i = 0; i < A.length; i = i + 2) {
            if (ar[i] !== ar[i + 1]) return ar[i];
        }
    }
```
### Lesson 3 - Time Complexity
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

### Lesson 4 - Counting Elements
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

### Lesson 5 - Sorting
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
        const negativeMax = array[0] * array[1] * array[len - 1];
        const positiveMax = array[len - 1] * array[len - 2] * array[len - 3];
        return negativeMax > positieMax ? negativeMax : positiveMax;
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

### Stacks And Queues
#### Brackets
#### Fish
#### Stone Wall
#### Nesting

### Leader
#### Dominator
#### EquiLeader

### Maximum Slice Problem
#### Max Profit
#### Max Double Slice Sum
#### Max Slice Sum

### Prime and Composite Numbers
#### Min Perimeter Rectangle
#### Count Factors
#### Peaks
#### Flags

### Sieve of Eratosthenes
#### Count Semiprimes
#### Count NonDivisible

### Euclidean Algorithm
#### Chocolates By Numbers
#### Common Prime Divisors
