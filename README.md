# js-tricks

A collection of useful javascript tricks.

## Cloning an object
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
let target = {};
Object.assign(target, source);

console.log(target)
// -> {..same as source..}


// Selectively clone an object
const desiredKeys = ['a', 'c'];

let clone = Object.entries().reduce((obj, [key,value]) => {
    if (desiredKeys.includes(key)) {
        obj[key] = value;
    }
    return obj;
} ,{});

console.log(clone);
// -> {a: 1, c:3}
```

## Call functions without parentheses
It should go without saying, but this is just for fun; you shouldn't use it for anything serious.

Let's say we want to have some Ruby-like syntactic sugar, like maybe array.first and array.last. Here's how to achieve that with js:

```javascript
Object.defineProperty(Array.prototype, 'first', {
    get: function() {
        return this[0];
    }
});

[1,2,3,4,5].first // -> 1

Object.defineProperty(Array.prototype, 'last', {
    get: function() {
        return this[0];
    }
});

[1,2,3,4,5].first // -> 5
```
