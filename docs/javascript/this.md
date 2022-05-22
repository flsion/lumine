# this 指针


this一般有几种调用场景

var obj = {a: 1, b: function(){console.log(this);}}

1. 作为对象调用时，指向该对象 obj.b(); // 指向obj
2. 作为函数调用, var b = obj.b; b(); // 指向全局window
3. 作为构造函数调用 var b = new Fun(); // this指向当前实例对象
4. 作为call与apply调用 obj.b.apply(object, []); // this指向当前的object

```js
var value = 1;
var obj = {
  value: 2,
  prop: {
    value: 3,
    getValue: function() {
      return this.value;
    }
  }
};

console.log(obj.prop.getValue()); // c
var foo = obj.prop.getValue;
console.log(foo());  // a
```

```js
var value = 1;
var obj = {
  value: 2,
  getValue: function () {
    return this.value;
  }
}

console.log(obj.getValue()); // 2
console.log((obj.getValue)()); // 2
console.log((obj.getValue = obj.getValue)()); // 1
console.log((false || obj.getValue)()); // 1
console.log((obj.getValue, obj.getValue)()); // 1
```

```js
function Foo() {
    getValue = function() {
        console.log(1);
    };
    return this;
}

Foo.prototype.getValue = function() {
    console.log(3);
};

function getValue() {
    console.log(5);
};

console.log(Foo().getName()) // 1
console.log(new Foo().getName()) // 3
```


```js
var foo = 'a';
let bar = 'b';

console.log(this.foo);  // a
console.log(this.bar);  // undefined
```