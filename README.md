# js-tricks

A collection of ~~useful~~ *interesting* javascript tricks.

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
        return this[this.length-1];
    }
});

[1,2,3,4,5].last // -> 5
```

Any function can be called with a template literal without parentheses.
```javascript
console.log `look ma, no parentheses!`
// -> ["hello there", raw: Array(1)]
```
... but the output might not be what you expect.

## Proxies

Proxies let you send object property access through a handler.

You could use a recursive proxy like so:
```javacript
const o = {
    a: 1,
    b: 2
};

const proxy = new Proxy(o, {
    get: function(obj, prop) {
        return obj[prop] || prox;
    }
});

proxy.a // -> 1
proxy.b // -> 2
proxy.c // -> Proxy {a: 1, b: 2}

proxy.any.level.of.nested.properties // -> 1
proxy.any.level.of.nested.properties // -> 2
proxy.any.level.of.nested.properties // -> Proxy {a: 1, b: 2}
```
