# js-tricks

A collection of useful javascript tricks.

```javascript
let object = {
    a: 1,
    b: 2,
    c: 3
};
// Iterate over an object
Object.entries(object).forEach(([key, value]) => console.log(`${key} : ${value}`));
// -> a : 1
// -> b : 2
// -> c : 3

// Clone an object
let target;
Object.assign(target, source);
// console.log(target)
// -> {..same as source..}

// Selectively clone an object
const desiredKeys = ['a, 'c'];

let clone = Object.entries().reduce((obj, [key,value]) => {
    if (desiredKeys.includes(key)) {
        obj[key] = value;
    }
    return obj;
} ,{});

console.log(clone);
// -> {a: 1, c:3}
```
