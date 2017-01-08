---
layout: post
title:  "JavaScript Object Instances"
date:   2016-12-05 03:39:33 +0100
categories: JavaScript
---
You need to create object instances, and after the initialization you need to set some function for all the instnaces.

```javascript
var op = function(){};
op.prototype.add = function() {
    var i, s = 0;
    for (i = 0; i < arguments.length; i++) {
        s += arguments[i];
    }
    return s;
}
var i = new op;
console.log(i.add(1, 2, 3, 4));
op.prototype.mul = function() {
    var i, m = 1;
    for (i = 0; i < arguments.length; i++) {
        m *= arguments[i];
    }
    return m;
}
console.log(i.mul(1, 2, 3, 4));
```

This will return **10, 24**.

Any other instance we create with the `new` will have the `add` and `mul` functions.

Even if we create new instance `i2` and add the `quad` to the instance prototype we will see all instances share the same prototype.


```javascript
var i2 = new op;
Object.getPrototypeOf(i2).quad = function(){
	var i, qs = 0;
    for (i = 0; i < arguments.length; i++) {
        qs += (arguments[i]*arguments[i]);
    }
    return qs;
}

console.log(i2.quad(1, 2, 3, 4));
console.log(i.quad(1, 2, 3, 4));
```

Returns **30,30**
