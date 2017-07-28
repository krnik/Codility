### Lesson 1 - Iterations
#### Binary Gap
```javascript
    function solution (N) {
        const gaps = N.toString(2).match(/(0+)(?=1)/g);
        return gaps ? gaps.sort((a, b) => a.length - b.length )[0].length : 0;
    }
```

### Lesson 2 - Arrays
#### Cyclic Rotation
```javascript
    function solution (A, K) {
        if (!K || A.length < 2) return A;
        const ar = A.slice();
        for (let i = 0; i < K; i++) {
            let first = ar.pop();
            ar.push(first);
        }
        return ar;
    }
```
#### Odd Occurrences In Array
