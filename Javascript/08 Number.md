# Number
JavaScript only has two kinds of numbers:
- number: a numeric data type in the double-precision 64-bit floating-point format (IEEE 754). Examples are -6, -2.4, 0, 0.1, 1, 3.14, 16.984025, 25, 976, 1024.0 and 500000.
- bigint: a numeric data type that can represent integers in the arbitrary precision format. Examples are -12n, 0n, 4n, and 9007199254740991n.

## Math object
```js
let x = 4.1;
let y = 5;
let z = 9;

// Generate a pseudorandom floating-point number between 0 (inclusive), and 1 (exclusive).
x = Math.random();

// Round
x = Math.round(x);
console.log(x);
>>> 4

// Round to 2 decimals
const price = Math.round(totalPrice * 100) / 100

// down round
x = Math.floor(x);
console.log(x);
>>> 4

// up round
x = Math.ceil(x);
console.log(x);
>>> 5

// Max
let maximum = Math.max(x, y, z);

// Min
let minimum = Math.min(x, y, z);


// Exponentiation
x = Math.power(x, 2);

// Square root
x = Math.sqrt(x);

// Distance from 0 (absolute value)
x = Math.abs(x);

// Built-in constants
x = Math.PI;

```

## Arithmetic operators
```js
// exponentiation
4 ** 3; // => 64

// remainder
4 % 3; // => 1
```

## Number.isNaN()

```JS
value == NaN        // ❌ false
value === NaN       // ❌  false
value == "NaN"      // ❌ 
NaN === NaN         // false

Number.isNaN(value)  // ✅

```

## Number.isFinite()
Implement the isNumber function, that checks if a value is a finite number or bigint, ie. not NaN or Infinity.

```js
export function isNumber(value) {
  return (typeof value === "number" && Number.isFinite(value)) || (typeof value === "bigint") 
}
```