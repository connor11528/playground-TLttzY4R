# Recursion in Javascript

This post goes through code samples utilizing recursion. We will state the problems and then provide runnable code snippets that show the answer. The answers will be hidden you can try them on your own and then peek.

Special thanks to the [Rithm School free computer science course](https://www.rithmschool.com/courses/javascript-computer-science-fundamentals) and their [exercises on github](https://github.com/rithmschool/javascript_computer_science_exercises/tree/master/recursion_exercise)

### Question 1: Sum all numbers

Write a function called `sumRange`. It will take a number and return 
the sum of all numbers from 1 up to the number passed in. 

**Sample:**
sumRange(3) returns 6, since 1 + 2 + 3 = 6.


<details>
<summary>Answer 1</summary>
The most important thing we need for recursive solutions is a base case. There needs to be a way of exiting the loop or the function will go on forever. The base case in the below code code is that when the input is 1, return 1. Eventually the function will return 6, the correct answer

Once you understand this code move on to the next problem

```javascript runnable
var output = sumRange(3)
console.log(output);

function sumRange(num){
	if(num == 1) return 1;

	return num + sumRange(num - 1);
}

```
</details>

### Question 2: Power function

Write a function called `power` which takes in a base and an exponent. If 
the exponent is 0, return 1. 

**Sample:**

console.log(power(2, 4)); // 16
console.log(power(2, 3)); // 8
console.log(power(2, 2)); // 4 
console.log(power(2, 1)); // 2
console.log(power(2, 0)); // 1

<details>
<summary>Answer 2</summary>

You can think of it in terms of this example:
2^4 = 2 * 2^3;
2^3 = 2 * 2^2;
2^2 = 2 * 2^1;
2^1 = 2 * 2^0; // once our exponent is 0 we KNOW that the value is always 1!

```javascript runnable
function power(base, exponent){
	if(exponent == 0) return 1;
	return base * power(base, exponent - 1);
}
```
</details>

### Question 3: Calculate factorial

Write a function that returns the `factorial` of a number. As a quick refresher, 
a factorial of a number is the result of that number multiplied by the number 
before it, and the number before that number, and so on, until you reach 1. 
The factorial of 1 is just 1.

**Sample:**

factorial(5); // 5 * 4 * 3 * 2 * 1 === 120

<details>
<summary>Answer 3</summary>

```javascript runnable
console.log(factorial(5));

function factorial(num){
	if(num == 1) return 1;

	return num * factorial(num - 1); // pending multiplier
}
```
</details>

### Question 4: Check all values in an array

Write a function called `all` which accepts an array and a callback and returns 
true if every value in the array returns true when passed as parameter to the 
callback function

**Sample:**
```
var allAreLessThanSeven = all([1,2,9], function(num){
	return num < 7;
});

console.log(allAreLessThanSeven); // false

```

<details>
<summary>Answer 4</summary>

```javascript runnable
var allAreLessThanSeven = all([1,2,9], function(num){
	return num < 7;
});

console.log(allAreLessThanSeven); // false

function all(array, callback){
	var copy = copy || array.slice(); // shallow copies array

	if(copy.length === 0) return true;

	if(callback(copy[0])){
		copy.shift(); // remove first element from array
		return all(copy, callback);
	} else {
		return false;
	}
}
```
</details>

### Question 5: Product of an array

Write a function called productOfArray which takes in an array of numbers 
and returns the product of them all

**Sample:**

```
var six = productOfArray([1,2,3]) // 6
var sixty = productOfArray([1,2,3,10]) // 60
```

<details>
<summary>Answer 5</summary>

```javascript runnable
var six = productOfArray([1,2,3]) // 6
var sixty = productOfArray([1,2,3,10]) // 60

console.log(six, sixty);

function productOfArray(array){
	if(array.length === 0) return 1;

	return array.shift() * productOfArray(array);
}
```
</details>

### Question 6: Search JS object

Write a function called `contains` that searches for a value in a nested object. 
It returns true if the object contains that value.

**Sample:**

```
var nestedObject = {
    data: {
        info: {
            stuff: {
                thing: {
                    moreStuff: {
                        magicNumber: 44,
                        something: 'foo2'
                    }
                }
            }
        }
    }
}

let hasIt = contains(nestedObject, 44); // true
let doesntHaveIt = contains(nestedObject, "foo"); // false
```

<details>
<summary>Answer 6</summary>

```javascript runnable
var nestedObject = {
    data: {
        info: {
            stuff: {
                thing: {
                    moreStuff: {
                        magicNumber: 44,
                        something: 'foo2'
                    }
                }
            }
        }
    }
}

let hasIt = contains(nestedObject, 44); // true
let doesntHaveIt = contains(nestedObject, "foo"); // false
console.log(hasIt, doesntHaveIt);

function contains(obj, value){
	for(var key in obj){
		if(typeof obj[key] === 'object'){
			return contains(obj[key], value);
		}

		if (obj[key] === value){
			return true;
		}
	}
	return false;
}

```
</details>


### Question 7: Parse a multi-dimensional array

Given a multi-dimensional integer array, return the total number of integers 
stored inside this array

**Sample:**
```
var seven = totalIntegers([[[5], 3], 0, 2, ['foo'], [], [4, [5, 6]]]); // 7
```

<details>
<summary>Answer 7</summary>

```javascript runnable
var seven = totalIntegers([[[5], 3], 0, 2, ['foo'], [], [4, [5, 6]]]); // 7
console.log(seven);

function totalIntegers(array){
	if(array.length === 0) return 0;

	let total = 0;
	let first = array.shift();

	if (Array.isArray(first)){
		total += totalIntegers(first); 
	} else if (Number.isInteger(first)) {
		total += 1;
	}

	return total + totalIntegers(array);
}
```
</details>

### Question 8:

Write a function that sums squares of numbers in list that may contain more lists

**Sample:**

```
var l = [1,2,3]; 
console.log(SumSquares(l)); // 1 + 4 + 9 = 14

l = [[1,2],3]; 
console.log(SumSquares(l)); // 1 + 4 + 9 = 14

l = [[[[[[[[[1]]]]]]]]] 
console.log(SumSquares(l)); // 1 = 1

l = [10,[[10],10],[10]] 
console.log(SumSquares(l)); // 100 + 100 + 100 + 100 = 400
```

<details>
<summary>Answer 8</summary>

```javascript runnable
var l = [1,2,3]; 
console.log(SumSquares(l)); // 14

l = [[1,2],3]; 
console.log(SumSquares(l)); // 14

l = [[[[[[[[[1]]]]]]]]] 
console.log(SumSquares(l)); // 1

l = [10,[[10],10],[10]] 
console.log(SumSquares(l)); // 400

function SumSquares(array){
	if(array.length === 0) return 0;
	let total = 0;

	for(let i = 0; i < array.length; i++){
		if(Array.isArray(array[i])){
			total += SumSquares(array[i]);
		} else {
			total += array[i] * array[i];
		}
		
	}
	return total;
}
```
</details>

### Question 9:

The function should return an array containing repetitions of the number argument. 
For instance, replicate(3, 5) should return [5,5,5]. 
If the times argument is negative, return an empty array.

**Sample:**
```
console.log(replicate(3, 5)) // [5, 5, 5]
console.log(replicate(1, 69)) // [69]
console.log(replicate(-2, 6)) // []
```

<details>
<summary>Answer 9</summary>

```javascript runnable
console.log(replicate(3, 5)) // [5, 5, 5]
console.log(replicate(1, 69)) // [69]
console.log(replicate(-2, 6)) // []

function replicate(times, number){
	if(times <= 0) return [];

	return [number].concat(replicate(times - 1, number));
}
```
</details>


