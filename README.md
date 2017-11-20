### Table Of Content
- [1. Iterations](#1-iterations)
    - [1.1. Binary Gap](#binary-gap)
- [2. Arrays](#2-arrays)
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
    - [5.1. Count Div](#count-div)
    - [5.2. Passing Cars](#passing-cars)
    - [5.3. Genomic Range Query](#genomic-range-query)
    - [5.4. Min Avg Two Slice](#min-avg-two-slice)
- [6. Sorting](#6-sorting)
    - [6.1. Distinct](#distinct)
    - [6.2. Max Product Of Three](#max-product-of-three)
    - [6.3. Triangle](#triangle)
    - [6.4. Number Of Disc Intersections](#number-of-disc-intersections)
- [7. Stacks And Queues](#7-stacks-and-queues)
    - [7.1. Brackets](#brackets)
    - [7.2. Fish](#fish)
    - [7.3. Stone Wall](#stone-wall)
    - [7.4. Nesting](#nesting)
- [8. Leader](#8-leader)
    - [8.1. Dominator](#dominator)
    - [8.2. EquiLeader](#equileader)
- [9. Maximum Slice Problem](#9-maximum-slice-problem)
    - [9.1. Max Profit](#max-profit)
    - [9.2. Max Double Slice Sum](#max-double-slice-sum)
    - [9.3. Max Slice Sum](#max-slice-sum)
- [10. Prime And Composite Numbers](#10-prime-and-composite-numbers)
    - [10.1. Max Perimeter Rectangle](#max-perimeter-rectangle)
    - [10.2. Count Factors](#count-factors)
    - [10.3. Peaks](#peaks)
    - [10.4. Flags](#flags)
- [11. Sieve Of Eratosthenes](#11-sieve-of-eratosthenes)
    - [11.1. Count Semiprimes](#count-semiprimes)
    - [11.2. Count Non Divisible](#count-non-divisible)
- [12. Euclidean Algorithm](#12-euclidean-algorithm)
    - [12.1. Chocolates By Numbers](#chocolates-by-numbers)
    - [12.2. Common Prime Divisors](#common-prime-divisors)
- [13. Fibonacci numbers](#13-fibonacci-numbers)
    - [13.1. Ladder](#ladder)
    - [13.2. FibFrog](#fibfrog)
- [14. Binary Seach Algorithm](#14-binary-search-algorithm)
    - [14.1. Min Max Division](#min-max-division)
    - [14.2. Nailing Planks](#nailing-planks)

### [1 Iterations](https://codility.com/programmers/lessons/1-iterations/)
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
    const len = num.length;
    for (let i = 0; i < len; i++) {
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

### [2 Arrays](https://codility.com/programmers/lessons/2-arrays/)
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
    const len = A.length;
    for (let i = 0; i < len; i++) {
        answer = answer ^ A[i];
    }
    return answer;
}
```

> Worst-case time complexity probably is O(N * log(N)) - evaluated as 100%
```javascript
function solution (A) {
    const ar = A.slice().sort( (a, b) => a - b );
    const len = ar.length;
    for (let i = 0; i < len; i = i + 2) {
        if (ar[i] !== ar[i + 1]) return ar[i];
    }
}
```

### [3 Time Complexity](https://codility.com/programmers/lessons/3-time_complexity/)
#### [Perm Missing Element](https://codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/)
```javascript
function solution (A) {
    let sum = 0;
    const len = A.length;
    for (let i = 0; i < len; i++) {
        sum = sum + A[i];
    }
    return ((len + 1) * (len + 2)) / 2 - sum;
}
```
> Hint - see Sum of Arithmetic Progression

#### [Frog Jump](https://codility.com/programmers/lessons/3-time_complexity/frog_jmp/)
```javascript
function solution (X, Y, D) {
    return Math.ceil((Y - X) /D);
}
```

#### [Tape Equilibrium](https://codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/)
```javascript
function solution (A) {
    let left = 0;
    let right = A.reduce((s, elem) => s + elem);
    let answer = false;
    const len = A.length;
    for (let i = 0; i < len - 1; i++) {
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

### [4 Counting Elements](https://codility.com/programmers/lessons/4-counting_elements/)
#### [Missing Integer](https://codility.com/programmers/lessons/4-counting_elements/missing_integer/)
```javascript
function solution (A) {
    const results = [0];
    const len = A.length;
    for (let i = 0; i < len; i++) {
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

#### [Frog River One](https://codility.com/programmers/lessons/4-counting_elements/frog_river_one/)
```javascript
function solution (X, A) {
    const leaves = new Array(X + 1).fill(false);
    let riverCovered = X;
    const len = A.length;
    for (let i = 0; i < len; i++) {
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

#### [Perm Check](https://codility.com/programmers/lessons/4-counting_elements/perm_check/)
```javascript
function solution (A) {
    const nums = [0];
    const len = A.length;
    for (let i = 0; i < len; i++) {
        nums[A[i]] = A[i];
    }
    for (let i = 1; i <= len; i++) {
        if (nums[i] !== i) {
            return 0;
        }
    }
    return 1;
}
```

#### [Max Counters](https://codility.com/programmers/lessons/4-counting_elements/max_counters/)
```javascript
function solution (N, A) {
    const counters = new Array(N).fill(0);
    let min = 0;
    let max = 0;
    const len = A.length;
    for (let i = 0; i < len; i++) {
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
    const cntLen = counters.length;
    for (let i = 0; i < cntLen; i++) {
        if (counters[i] < min) {
            counters[i] = min;
        }
    }
    return counters;
}
```

### [5 Prefix Sums](https://codility.com/programmers/lessons/5-prefix_sums/)
#### [Count Div](https://codility.com/programmers/lessons/5-prefix_sums/count_div/)
```javascript
function solution (A, B, K) {
    return Math.floor(B / K) - Math.floor((A - 1) - K);
}
```
#### [Passing Cars](https://codility.com/programmers/lessons/5-prefix_sums/passing_cars/)
```javascript
function solution (A) {
    let eastCars = 0;
    let passingCars = 0;
    const len = A.length;
    for (let i = 0; i < len; i++) {
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
#### [Genomic Range Query](https://codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/)
```javascript
function solution (S, P, Q) {
    const answer = [];
    const prefixSums = [];
    const len = S.length;
    // Map nucleotides into prefixSums array
    for (let i = 0; i < len; i++) {
        const char = S.charAt(i);
        switch (char) {
            case 'A':
                prefixSums.push([1, 0, 0, 0]);
                break;
            case 'C':
                prefixSums.push([0, 1, 0, 0]);
                break;
            case 'G':
                prefixSums.push([0, 0, 1, 0]);
                break;
            default:
                prefixSums.push([0, 0, 0, 1]);
        }
    }
    // create prefix sum from mapped nucleotides
    for (let i = 1; i < len; i++) {
        for (let j = 0; j < 4; j++) {
            prefixSums[i][j] = prefixSums[i][j] + prefixSums[i - 1][j];
        }
    }
    const pLen = P.length;
    for (let i = 0; i < pLen; i++) {
        const x = P[i];
        const y = Q[i];
        for (let j = 0; j < 4; j++) {
            // Check if prefix sum at index preceding query start exists
            // if yes take it's value, if no assign 0
            const prefSum = x - 1 >= 0 ? prefixSums[x - 1][j] : 0;
            if (prefixSums[y][j] - prefSum > 0) {
                answer.push(j + 1);
                break;
            }
        }
    }
    return answer;
}
```
#### [Min Avg Two Slice](https://codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/)
```javascript
function solution (A) {
    let minAvgSlice = (A[0] + A[1]) / 2; // minimal slice average
    if (A.length === 2) {
        return 0;
    }
    let answer = 0;
    const len = A.length;
    for (let i = 0; i < len - 1; i++) {
        // Check slice containing 2 elements
        let currentSliceAvg = (A[i] + A[i + 1]) / 2;
        if (currentSliceAvg < minAvgSlice) {
            minAvgSlice = currentSliceAvg;
            answer = i;
        }
        // Check slice containing 3 elements
        if (i + 2 < len) {
            currentSliceAvg = (A[i] + A[i + 1] + A[i + 2]) / 3;
            if (currentSliceAvg < minAvgSlice) {
                minAvgSlice = currentSliceAvg;
                answer = i;
            }
        }
    }
    return answer;
}
```


### [6 Sorting](https://codility.com/programmers/lessons/6-sorting/)
#### [Distinct](https://codility.com/programmers/lessons/6-sorting/distinct/)
```javascript
function solution (A) {
    const array = A.slice();
    array.sort((a, b) => a - b);
    let distinct = 0;
    let currentNumber = null;
    const len = array.length;
    for (let i = 0; i < len; i++) {
        if (array[i] !== currentNumber) {
            currentNumber = array[i];
            distinct = distinct + 1;
        }
    }
    return distinct;
}
```

#### [Max Product Of Three](https://codility.com/programmers/lessons/6-sorting/max_product_of_three/)
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

#### [Triangle](https://codility.com/programmers/lessons/6-sorting/triangle/)
```javascript
function solution (A) {
    if (A.length < 3) return 0;
    const array = A.slice();
    array.sort((a, b) => a - b);
    let answer = 0;
    const len = A.length;
    for (let i = 0; i < len - 2; i++) {
        const a = array[i];
        const b = array[i + 1];
        const c = array[i + 2];
        if (a + b > c && a + c > b && b + c > a) ans = 1;
    }
}
```

#### [Number Of Disc Intersections](https://codility.com/programmers/lessons/6-sorting/number_of_disc_intersections/)
```javascript
function solution (A) {
    const discPoints = [];
    const len = A.length;
    for (let i = 0; i < len; i++) {
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
    const discLen = discPoints.length;
    for (let i = 0; i < discLen; i++) {
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

### [7 Stacks And Queues](https://codility.com/programmers/lessons/7-stacks_and_queues)
#### [Brackets](https://codility.com/programmers/lessons/7-stacks_and_queues/brackets/)
```javascript
function solution (S) {
    let stack = '';
    const len = S.length;
    for (let i = 0; i < len; i++) {
        if (/[\{\[\(]/.test(S[i])) {
            stack = stack + S[i];
            continue;
        }
        const lastChar = stack.length ? stack[stack.length - 1] : '';
        let lastOpposite = '';
        switch (S[i]) {
            case '}':
                lastOpposite = '{';
                break;
            case ']':
                lastOpposite = '[';
                break;
            case ')':
                lastOpposite = '(';
                break;
        }
        if (lastChar === lastOpposite) {
            stack = stack.slice(0, stack.length - 1);
        } else {
            stack = stack + S[i];
        }
    }
    return stack.length === 0 ? 1 : 0;
}
```
#### [Fish](https://codility.com/programmers/lessons/7-stacks_and_queues/fish/)
```javascript
function solution (A, B) {
    let alive = [];
    const len = A.length;
    for (let i = 0; i < len; i++) {
        let last = alive.length - 1;
        while (
            alive.length && // There are fish alive
            alive[last][0] < A[i] && // Current fish is bigger than last one
            alive[last][1] !== B[i] && // Current fish swims in different direction than last one
            B[i] === 0 // Current fish swims upstream
        ) {
            // Then current Fish eats last fish
            alive.pop();
            last = alive.length - 1;
        }
        if (!alive.length || B[i] === alive[last][1] || B[i] === 1) {
            alive.push([A[i], B[i]]);
        }
    }
    return alive.length;
}
```
#### [Stone Wall](https://codility.com/programmers/lessons/7-stacks_and_queues/stone_wall/)
```javascript
function solution (H) {
    const stack = [];
    let answer = 0;
    const len = H.length;
    for (let i = 0; i < len; i++) {
        while (stack.length && H[i] < stack[stack.length - 1]) {
            stack.pop();
        }
        if (stack.length && stack[stack.length - 1] === H[i]) {
            continue;
        }
        stack.push(H[i]);
        answer = answer + 1;
    }
    return answer;
}
```
#### [Nesting](https://codility.com/programmers/lessons/7-stacks_and_queues/nesting/)
```javascript
function solution (S) {
    const stack = [];
    const len = S.length;
    for (let i = 0; i < len; i++) {
        if (S[i] === '(') {
            stack.push(S[i]);
        } else {
            if (stack.length && stack[stack.length - 1] === '(') {
                stack.pop();
            } else {
                stack.push(S[i]);
            }
        }
    }
    return stack.length ? 0 : 1;
}
```

### [8 Leader](https://codility.com/programmers/lessons/8-leader/)
#### [Dominator](https://codility.com/programmers/lessons/8-leader/dominator/)
```javascript
function solution (A) {
    const dom = [];
    const len = A.length;
    for (let i = 0; i < len; i++) {
        if (!dom.length || dom[dom.length - 1] === A[i]) {
            dom.push(A[i]);
        } else {
            dom.pop();
        }
    }
    const first = dom[0];
    let count = 0;
    for (let i = 0; i < len; i++) {
        if (A[i] === first) {
            count = count + 1;
        }
    }
    return count > (A.length / 2) ? A.indexOf(first) : -1;
}
```
#### [EquiLeader](https://codility.com/programmers/lessons/8-leader/equi_leader/)
```javascript
function solution (A) {
    const dom = [];
    const len = A.length;
    for (let i = 0; i < len; i++) {
        if (!dom.length || dom[dom.length - 1] === A[i]) {
            dom.push(A[i]);
        } else {
            dom.pop();
        }
    }
    const candidate = dom[0];
    let count = 0;
    for (let i = 0; i < len; i++) {
        if (A[i] === candidate) {
            count = count + 1;
        }
    }
    const leader = count > (len / 2) ? candidate : false;
    if (leader === false) {
        return 0;
    }
    const equi = [];
    let eCount = 0;
    for (let i = 0; i < len; i++) {
        if (A[i] === leader) {
         eCount = eCount + 1;
        }
        equi.push(eCount);
    }
    let answer = 0;
    for (let i = 0; i < len - 1; i++) {
        if (equi[i] > ((i + 1) / 2) && (eCount - equi[i]) > ((len - i - 1) / 2)) {
            answer = answer + 1;
        }
    }
    return answer;
}
```

### [9 Maximum Slice Problem](https://codility.com/programmers/lessons/9-maximum_slice_problem/)
#### [Max Profit](https://codility.com/programmers/lessons/9-maximum_slice_problem/max_profit/)
```javascript
function solution (A) {
    let min = A[0];
    let max = A[1];
    let answer = 0;
    const len = A.length;
    for (let i = 0; i < len; i++) {
        if (min > A[i]) {
            min = A[i];
            max = min;
        } else {
            if (max < A[i]) max = A[u];
        }
        if (answer < max - min) answer = max - min;
    }
    return answer;
}
```
#### [Max Double Slice Sum](https://codility.com/programmers/lessons/9-maximum_slice_problem/max_double_slice_sum/)
```javascript
function solution (A) {
    const len = A.length;
    const left = new Array(len).fill(0);
    const right = new Array(len).fill(0);
    let ans = 0;
    for (let i = 1; i < len - 1; i++) {
        left[i] = Math.max(0, l[i - 1] + A[i]);
        right[i] = Math.max(0, r[i - 1] + A[len - i - 1]);
    }
    for (let i = 1; i < n - 1; i++) {
        ans = Math.max(ans, left[i - 1] + right[len - i - 2]);
    }
    return ans;
}
```
#### [Max Slice Sum](https://codility.com/programmers/lessons/9-maximum_slice_problem/max_slice_sum/)
```javascript
function solution (A) {
    let max = A[i];
    let m = A[i];
    const len = A.length;
    for (let i = 0; i < len; i++) {
        m = Math.max(A[i], m + A[i]);
        max = Math.max(max, m);
    }
    return max;
}
```

### [10 Prime And Composite Numbers](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/)
#### [Min Perimeter Rectangle](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/min_perimeter_rectangle/)
```javascript
function solution(N) {
    let i = 1;
    let A;
    let B;
    let answer = N * 5;
    while (i * i < N) {
        if (N % i === 0) {
            A = i * 2;
            B = (N / i) * 2;
            if (answer > A + B) {
                answer = A + B;
            }
        }
        i = i + 1;
    }
    if (i * i === N) {
        A = i * 2;
        B = i * 2;
        if (answer > A + B) {
            answer = A + B;
        }
    }
    return answer;
}
```
#### [Count Factors](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/count_factors/)
```javascript
function solution (N) {
    let ans = 0;
    let i = 1;
    while (i * i < N) {
        if (!(n % i)) ans = ans + 2;
        i = i + 1;
    }
    if (i * i === N) ans = ans + 1;
    return ans;
}
```
#### [Peaks](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/peaks/)
```javascript
function solution (A) {
    const peakIndexes = [];
    const Alen = A.length;
    for (let i = 1; i < Alen - 1; i++) {
        if (A[i] > A[i - 1] && A[i] > A[i + 1]) {
            peakIndexes.push(i);
        }
    }
    const pLen = peakIndexes.length;
    if (pLen <= 1) {
        return pLen;
    }
    const divisors = [];
    let i = 1;
    while (i <= pLen) {
        if (Alen % i === 0) {
            divisors.push(i);
        }
        i = i + 1;
    }
    i = divisors.length - 1;
    let answer;
    let filled;
    let len;
    let cnt;
    while (i > 0) {
        answer = divisors[i];
        len = A.length / answer;
        cnt = 0;
        filled = 0;
        while (cnt < pLen) {
            if (filled * len <= peakIndexes[cnt] && peakIndexes[cnt] < (filled + 1) * len) {
                filled = filled + 1;
            }
            cnt = cnt + 1;
        }
        if (answer === filled) {
            return answer;
        }
        i = i - 1;
    }
    return divisors[i];
}
```
#### [Flags](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/flags/)
```javascript
function solution (A) {
    if (A.length < 3) {
        return 0;
    }
    const peaks = [];
    const len = A.length;
    for (let i = 0; i < len; i++) {
        if (A[i] > A[i - 1] && A[i] > A[i + 1]) {
            peaks.push(i);
        }
    }
    if (peaks.length < 2) {
        return peaks.length;
    }
    let flagLimit = Math.floor(Math.sqrt(peaks[peaks.length - 1] - peaks[0])) + 1;
    let canPlaceAtLeast = 0;
    while (canPlaceAtLeast < flagLimit - 1) {
        const half = Math.floor((flagLimit + canPlaceAtLeast) / 2);
        if (canPlace(half)) {
            canPlaceAtLeast = half;
        } else {
            flagLimit = half;
        }
    }
    return canPlace(flagLimit) ? flagLimit : canPlaceAtLeast;

    function canPlace (numberOfFlags) {
        let last = peaks[0];
        let count = 1;
        let i = 1;
        while (i < peaks.length && count < numberOfFlags) {
            if (peaks[i] - last >= numberOfFlags) {
                last = peaks[i];
                count = count + 1;
            }
            i = i + 1;
        }
        return count >= numberOfFlags;
    }
}
```

### [11 Sieve Of Eratosthenes](https://codility.com/programmers/lessons/11-sieve_of_eratosthenes/)
#### [Count Semiprimes](https://codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_semiprimes/)
```javascript
function solution (N, P, Q) {

}
```

#### [Count Non Divisible](https://codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_non_divisible/)

### [12 Euclidean Algorithm](https://codility.com/programmers/lessons/12-euclidean_algorithm/)
#### [Chocolates By Numbers](https://codility.com/programmers/lessons/12-euclidean_algorithm/chocolates_by_numbers/)
```javascript
function solution (N, M) {
    const gcp = (a, b) => {
        if (!(a % b)) {
            return b;
        } else {
            return gcp(b, a % b);
        }
    };
    return N / gcp(N, M);
}
```

#### [Common Prime Divisors](https://codility.com/programmers/lessons/12-euclidean_algorithm/common_prime_divisors/)
```javascript
function solution(A, B) {
    const len = A.length;
    let ans = 0;
	for (let i = 0; i < len; i++) {
        let first = A[i];
        let second = B[i];
        let gcdA = gcd(first, second);
        let gcdB = gcd(first, second);
        while (gcdA !== 1) {
            first = Math.floor(first / gcdA);
            gcdA = gcd(first, gcdA);
        }
        while (gcdB !== 1) {
            second = Math.floor(second / gcdB);
            gcdB = gcd(second, gcdB);
        }
        if (first === second) {
            ans = ans + 1;
        }
    }
	return ans;
}
function gcd (a, b) {
	if (a % b == 0) {
		return b;
	} else {
		return gcd(b, a % b);
	}
}
```
### [13 Common Prime Divisors](https://codility.com/programmers/lessons/13-fibonacci_numbers/)
#### [Ladder](https://codility.com/programmers/lessons/13-fibonacci_numbers/ladder/)
```javascript
function solution(A, B) {
    const maxOfA = Math.max(...A);
    const fibNumbers = [1, 1];
    for (let i = 2; i <= maxOfA; i++) {
        const safeInt = (fibNumbers[i - 1] + fibNumbers[i - 2]) % (1 << 30);
        fibNumbers.push(safeInt);
    }
    const answer = A.slice();
    const len = A.length;
    for (let i = 0; i < len; i++) {
        answer[i] = fibNumbers[A[i]] % (1 << B[i]);
    }
    return answer;
}
```

#### [FibFrog](https://codility.com/programmers/lessons/13-fibonacci_numbers/fib_frog/)
```javascript
function solution(A) {
    const leaves = [...A, 1];
    const len = leaves.length;
    const fibNumbers = getFibNumsUpTo(len);
    const fNumsLen = fibNumbers.length;
    const reachableIn = new Array(len).fill(-1);
    for (let i of fibNumbers) {
        if (leaves[i - 1] === 1) {
            reachableIn[i - 1] = 1;
        }
    }
    for (let i = 0; i < len; i++) {
        if (!leaves[i] || reachableIn[i] > 0) {
            continue;
        }
        let minIndex = -1;
        let minValue = 100000;
        for (let j = 0; j < fNumsLen; j++) {
            const prevIndex = i - fibNumbers[j];
            if (prevIndex < 0) {
                break;
            }
            if (reachableIn[prevIndex] > 0 && minValue > reachableIn[prevIndex]) {
                minValue = reachableIn[prevIndex];
                minIndex = prevIndex;
            }
            if (minIndex !== -1) {
                reachableIn[i] = minValue + 1;
            }
        }
    }
    return reachableIn[len - 1];
}

function getFibNumsUpTo (N) {
    const fib = new Array(N + 2).fill(0);
    fib[1] = 1;
    const len = fib.length;
    let i = 2;
    for (i; i <= len; i++) {
        fib[i] = fib[i - 1] + fib[i - 2];
        if (fib[i] >= N) {
            break;
        }
    }
    return fib.slice(2, i + 1);
}
```
### [13 Binary Seach Algorithm](https://codility.com/programmers/lessons/14-binary_search_algorithm/)
#### [Min Max Division](https://codility.com/programmers/lessons/14-binary_search_algorithm/min_max_division/)
```javascript

```
#### [Nailing Planks](https://codility.com/programmers/lessons/14-binary_search_algorithm/nailing_planks/)
```javascript
```
