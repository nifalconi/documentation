# JavaScript/TypeScript Reference

This document provides examples for strings, arrays, objects, and asynchronous operations in one markdown file.

---

## Strings

```javascript
const str = "  Hello, World!  ";

// Trimming
console.log(str.trim());        // "Hello, World!" - Remove whitespace from both ends
console.log(str.trimStart());   // "Hello, World!  " - Remove whitespace from the start
console.log(str.trimEnd());     // "  Hello, World!" - Remove whitespace from the end

// Case Conversion
console.log(str.toLowerCase()); // "  hello, world!  " - Convert to lowercase
console.log(str.toUpperCase()); // "  HELLO, WORLD!  " - Convert to uppercase

// Substring Checking
console.log(str.includes("World"));      // true - Check if "World" exists
console.log(str.startsWith("  He"));     // true - Check if starts with "  He"
console.log(str.endsWith("!  "));        // true - Check if ends with "!  "

// Finding and Replacing
console.log(str.indexOf("o"));           // 4 - Find first occurrence of 'o'
console.log(str.lastIndexOf("o"));       // 8 - Find last occurrence of 'o'
console.log(str.replace("World", "JS")); // "  Hello, JS!  " - Replace "World" with "JS"
console.log(str.replaceAll(" ", "_"));   // "__Hello,_World!__" - Replace all spaces with "_"

// Splitting and Joining
console.log(str.split(","));             // ["  Hello", " World!  "] - Split by comma
console.log(["A", "B"].join("-"));       // "A-B" - Join elements with a hyphen

// Length
console.log(str.length);                 // 16 - Get the string length
```

## Arrays

```javascript
const arr = [1, 2, 3, 4, 5];

// Adding and Removing Elements
arr.push(6);        // [1, 2, 3, 4, 5, 6] - Add element at the end
arr.pop();          // 6; arr = [1, 2, 3, 4, 5] - Remove and return last element
arr.unshift(0);     // [0, 1, 2, 3, 4, 5] - Add element at the start
arr.shift();        // 0; arr = [1, 2, 3, 4, 5] - Remove and return first element

// Slicing and Splicing
console.log(arr.slice(1, 3));    // [2, 3] - Extract elements from index 1 to 2
arr.slice(-1) // array with the last element
arr.splice(2, 1, 99);            // [1, 2, 99, 4, 5] - Remove 1 element at index 2 and insert 99

// Mapping and Reducing
console.log(arr.map(x => x * 2));                // [2, 4, 198, 8, 10] - Double each element
console.log(arr.reduce((sum, x) => sum + x, 0)); // 111 - Sum all elements

// Filtering and Finding
console.log(arr.filter(x => x > 2)); // [99, 4, 5] - Filter elements greater than 2
console.log(arr.find(x => x === 99)); // 99 - Find first element that matches

// Sorting and Reversing
arr.sort((a, b) => a - b); // [1, 2, 4, 5, 99] - Sort in ascending order
arr.reverse();             // [99, 5, 4, 2, 1] - Reverse the array

// Copying and Combining
const copy = [...arr];              // Create a shallow copy
const combined = arr.concat([6, 7]); // [99, 5, 4, 2, 1, 6, 7]
const extended = [...arr, 6, 7];     // [99, 5, 4, 2, 1, 6, 7]

// Looping
arr.forEach((value, index) => {
  console.log(index, value);
});

for (const value of arr) {
  console.log(value);
}
```

## Objects
```javascript
const obj = { name: "Alice", age: 25 };

// Accessing and Updating
console.log(obj.name);    // "Alice" - Access property
obj.age = 26;             // Update property; obj = { name: "Alice", age: 26 }

// Keys, Values, and Entries
console.log(Object.keys(obj));    // ["name", "age"] - Get all keys
console.log(Object.values(obj));  // ["Alice", 26] - Get all values
console.log(Object.entries(obj)); // [["name", "Alice"], ["age", 26]] - Get key-value pairs

// Cloning and Merging
const clone = { ...obj };         // Create a shallow copy
const merged = { ...obj, city: "Paris" };
// { name: "Alice", age: 26, city: "Paris" } - Merge two objects
```

## Objects Promises and Async/Await

```javascript
// Creating a Promise
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done!"), 1000);
});

// Using Then/Catch
myPromise
  .then((val) => console.log(val)) // "Done!" - Log resolved value
  .catch((err) => console.error(err)); // Log error if rejected

// Async/Await
async function fetchData() {
  try {
    const data = await myPromise;
    console.log(data); // "Done!" - Await promise resolution
  } catch (error) {
    console.error(error);
  }
}
fetchData();
```


## Advanced Array Methods

### Flattening
```javascript
const nested = [[1, 2], [3, 4], [5]];
console.log(nested.flat()); // [1, 2, 3, 4, 5] - Flatten one level deep

const deeplyNested = [1, [2, [3, [4]]]];
console.log(deeplyNested.flat(Infinity)); // [1, 2, 3, 4] - Flatten all levels
```

### FlatMap
```javascript
const arr = [1, 2, 3];
console.log(arr.flatMap(x => [x, x * 2]));
// [1, 2, 2, 4, 3, 6] - Map and flatten the result
```

### Removing Duplicates
```javascript
const duplicates = [1, 2, 2, 3, 4, 4];
console.log([...new Set(duplicates)]); // [1, 2, 3, 4] - Remove duplicates
```

### Transposing a Matrix
```javascript
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];
const transposed = matrix[0].map((_, i) => matrix.map(row => row[i]));
console.log(transposed);
// [
//   [1, 4, 7],
//   [2, 5, 8],
//   [3, 6, 9]
// ]
```

### Cartesian Product
```javascript
const arr1 = [1, 2];
const arr2 = ['a', 'b'];
const product = arr1.flatMap(x => arr2.map(y => [x, y]));
console.log(product);
// [
//   [1, "a"], [1, "b"],
//   [2, "a"], [2, "b"]
// ]
```

---

## Loops

### For Loop
```javascript
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}
```

### For…Of Loop
```javascript
const arr = [10, 20, 30];
for (const num of arr) {
  console.log(num); // 10, 20, 30
}
```

### For…In Loop
```javascript
const obj = { name: "Alice", age: 25 };
for (const key in obj) {
  console.log(`${key}: ${obj[key]}`); // name: Alice, age: 25
}
```

### While Loop
```javascript
let count = 0;
while (count < 3) {
  console.log(count); // 0, 1, 2
  count++;
}
```

### Do…While Loop
```javascript
let count = 0;
do {
  console.log(count); // 0, 1, 2
  count++;
} while (count < 3);
```

---

## Function Utilities

### Default Parameters
```javascript
function greet(name = "Guest") {
  return `Hello, ${name}!`;
}
console.log(greet());       // Hello, Guest!
console.log(greet("Alice")); // Hello, Alice!
```

### Rest Parameters
```javascript
function sum(...numbers) {
  return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

### Arrow Functions
```javascript
const add = (a, b) => a + b;
console.log(add(5, 3)); // 8
```

### Immediately Invoked Function Expressions (IIFE)
```javascript
(() => {
  console.log("This runs immediately!");
})(); // This runs immediately!
```

---

## Error Handling

### Try…Catch
```javascript
try {
  const result = JSON.parse('{"key": "value"}');
  console.log(result.key); // value
} catch (error) {
  console.error("Invalid JSON!");
}
```

### Throwing Errors
```javascript
function validateAge(age) {
  if (age < 0) throw new Error("Age cannot be negative!");
  return "Valid age";
}
try {
  console.log(validateAge(-5));
} catch (error) {
  console.error(error.message); // Age cannot be negative!
}
```

---

## Modules

### Exporting
```javascript
// utils.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Default export
export default function multiply(a, b) {
  return a * b;
}
```

### Importing
```javascript
// main.js
import multiply, { add, subtract } from "./utils.js";

console.log(add(2, 3));        // 5
console.log(subtract(5, 2));   // 3
console.log(multiply(3, 4));   // 12
```
