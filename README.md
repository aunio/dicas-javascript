# javascript-tips

1. [Multiple Conditions](#multiple-conditions)
2. [Ternary](#ternary)

## **Multiple Conditions**

**Bad:**

```javascript
if(x === 'abc' || x === 'def' || x === 'ghi' || x === 'jkl') {
    // code
}
```

**Good:**

```javascript
if(['abc', 'def', 'ghi', 'jkl'].includes(x)) {
    // code
}
```

**[⬆ Back to the top](#javascript-tips)**

## **Ternary**

**Bad:**

```javascript
let test: boolean;
if( x > 10 ) {
    test = true;
} else {
    test = false;
}
```

**Good:**

```javascript
// Option 1
let test = (x > 10) ? true : false;

// Option 2
let test = x > 10;

console.log(test);
// log: true
```

**[⬆ Back to the top](#javascript-tips)**