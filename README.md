### Lesson 1 - Iterations
#### Binary Gap
```javascript
    function solution (N) {
        const gaps = N.toString(2).match(/(0+)(?=1)/g);
        return gaps ? gaps.sort((a, b) => b.length - a.length )[0].length : 0;
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
