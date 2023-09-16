Given an integer array ```nums```, return true if any value appears at *least twice* in the array, and return ```false``` if every element is distinct.

#### Example 1:
```
Input: nums = [1,2,3,1]
Output: true
```

#### Example 2:
```
Input: nums = [1,2,3,4]
Output: false
```
#### Example 3:
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### Solution 1: Using a Set*
**the most efficient**<br>
this code creates a Set from the input array, and it checks if the size of the Set is different from the length of the input array. If they are not equal, it returns true, indicating that there are duplicates. Otherwise, it returns false, indicating that all elements in the array are distinct.
**Set will automatically remove any duplicate elements, as Sets only store unique values**
```JavaScript
function containsDuplicate(nums) {
  const seen = new Set(nums); 
    
    // Compare the size of the Set to the length of the 'nums' array
    // If they are not equal, it means there are duplicates
    return seen.size !== nums.length;
};
```

### Disadvantages:

- **Space Complexity**: While this method has good time complexity, it uses extra space to create a Set that stores unique elements from the array. If memory usage is a concern in your application, this might be a drawback.

- **Compatibility**: While Sets are well-supported in modern JavaScript environments, if you need to support older browsers or environments, you may need to consider compatibility issues.

- **Order of Elements**: The Set approach doesn't preserve the order of elements. If the order of elements in the original array is significant, and you need to maintain that order, this method might not be suitable.

- **Immutability**: This method doesn't modify the original array. If you need to remove duplicates from the original array or perform other operations on it, you'll need to do that separately.

### Solution 2: Using Array.includes()
We iterate through the array and for each element, we check if it exists in the array from its next position to the end using the ```Array.includes()``` method. If we find a duplicate, we return ```true```.

javascript
```JavaScript
function containsDuplicate(nums) {
  for (let i = 0; i < nums.length; i++) {
    if (nums.slice(i + 1).includes(nums[i])) {
      return true; // Found a duplicate
    }
  }

  return false; // No duplicates found
}

```
### Solution 3: Using a Nested Loop
**the least efficient** <br/>
We compare each element in the array with every other element to check for duplicates. If we find any duplicates, we return true. This solution has a time complexity of O(n^2).
```JavaScript
function containsDuplicate(nums) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] === nums[j]) {
        return true; // Found a duplicate
      }
    }
  }

  return false; // No duplicates found
}

```
---



*A **Set** is a built-in data structure in many programming languages, including JavaScript, that represents a collection of unique values. The key characteristics of a Set are:

- **Uniqueness**: A Set can only contain unique values. If you attempt to add a value that is already in the Set, it will not result in a duplicate; the Set will simply remain unchanged.

- **No Specific Order**: The elements in a Set are not stored in any particular order, unlike arrays, which have a specific order based on their indices.

Here's a brief explanation of how a Set works and its basic operations:
- **Initialization:** You can create a Set in JavaScript using the new Set() constructor, and you can optionally pass an iterable (e.g., an array) to initialize the Set with some values.
``` JavaScript
const mySet = new Set(); // Creates an empty Set
const mySetWithValues = new Set([1, 2, 3]); // Creates a Set with initial values 1, 2, and 3

```
- **Adding Elements**: You can add elements to a Set using the add() method. The method ensures that duplicates are not added.
``` JavaScript
mySet.add(4); // Adds the value 4 to the Set
mySet.add(4); // Does nothing since 4 is already in the Set (no duplicates allowed)

```
- **Checking for Existence**: You can check if an element exists in a Set using the has() method.
```JavaScript
const exists = mySet.has(4); // Returns true since 4 is in the Set

```