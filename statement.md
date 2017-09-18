# Recursion in Javascript

This post goes through code samples utilizing recursion. We will state the problems and then provide runnable code snippets that show the answer. The answers will 

### Question 1: sum all numbers
Write a function called `sumRange`. It will take a number and return 
the sum of all numbers from 1 up to the number passed in. 

**Sample:**
sumRange(3) returns 6, since 1 + 2 + 3 = 6.


<details>
<summary>Answer 1</summary>
The most important thing we need for recursive solutions is a base case. There needs to be a way of exiting the loop or the function will go on forever. The base case in the below code code is that when the input is 1, return 1.

```javascript runnable
var output = sumRange(3)
console.log(output);

function sumRange(num){
	if(num == 1) return 1;

	return num + sumRange(num - 1);
}

```
</details>


