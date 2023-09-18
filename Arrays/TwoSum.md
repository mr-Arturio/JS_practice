Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

Example 3:
```
Input: nums = [3,3], target = 6
Output: [0,1]
```
___
### Solution 1: Brute Force
This solution has a time complexity of ```O(n^2)``` due to the nested loops.
```JavaScript
function twoSum(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
    
    return []; // If no solution is found, return an empty array
}
```
### Solution 2: Using a plain object
Here's the same solution using a plain object to store elements and their indices:  a time complexity of ```O(n)```<br>

```JavaScript
function twoSum(nums, target) {
    const numIndices = {}; // Create an object to store elements and their indices
    
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        
        if (numIndices[complement] !== undefined) {
            return [numIndices[complement], i];
        }
        
        numIndices[nums[i]] = i; // Store the current element and its index
    }
    
    return []; // If no solution is found, return an empty array
}

```

### Solution 3: Using a HashMap
same as Object but using Map<br>
This solution using a HashMap is the most efficient with a time complexity of ```O(n)```<br>

```JavaScript
function twoSum(nums, target) {
    const numIndices = new Map(); // Create a HashMap to store elements and their indices
    
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        
        if (numIndices.has(complement)) {
            return [numIndices.get(complement), i];
        }
        
        numIndices.set(nums[i], i); // Store the current element and its index
    }
    
    return []; // If no solution is found, return an empty array
}
```

- ```const numIndices = new Map();```: This line creates an empty Map called ```numIndices```. The Map will be used to store the elements from the ```nums``` array as keys and their corresponding indices as values.

- The function then enters a loop that iterates through the ```nums``` array using the variable ```i```.

- ```const complement = target - nums[i];```: Inside the loop, it calculates the complement, which is the difference between the target value and the current element ```nums[i]```. The complement represents the number that, when added to the current element, will result in the target sum.

- ```if (numIndices.has(complement)) { ... }```: This conditional statement checks if the complement (the number we're looking for) is already in the numIndices Map. If it is, that means we've found a pair of elements in the nums array whose sum equals the target.

- return [numIndices.get(complement), i];: If a complement exists in the numIndices Map, this line returns an array containing the indices of the two elements that add up to the target. numIndices.get(complement) retrieves the index of the complement, and i is the index of the current element.

- ```numIndices.set(nums[i], i);```: If the complement is not found in the Map, the code proceeds to this line. It adds the current element nums[i] as the key and its index i as the value to the numIndices Map. This step ensures that if we encounter the complement in future iterations, we can quickly find its index.

- The loop continues to iterate through the nums array, checking each element and its complement until a solution is found or until the loop finishes.

- If no solution is found within the loop (i.e., no pair of elements adds up to the target), the function returns an empty array [] as specified in the problem statement.