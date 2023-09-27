Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

 

### Example 1:
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
### Example 2:
```
Input: nums = [1], k = 1
Output: [1]
```

## 1.Solution:
### not super eficcient time complexity of **O(n log n)**,
1. **Create a Frequency Map (Object)**: You can create an object where the keys represent unique numbers from the ```nums``` array, and the values represent their frequencies. Initialize an empty object for this purpose.

2. **Loop Through ```nums``` and Update Frequencies**: Iterate through the ```nums``` array. For each number, check if it exists as a key in the frequency map (object). If it does, increment the corresponding value (frequency) by 1. If it doesn't exist, create a new key with a value of 1 in the frequency map.

3. **Sort by Frequency**: After you've built the frequency map, you can convert it into an array of key-value pairs, where each pair is an object with keys like "number" and "frequency." Then, sort this array based on the "frequency" value in descending order. This will give you the numbers sorted by their frequencies, with the most frequent ones coming first.

4. **Get the Top K Elements**: You can slice the sorted array to select the top ```k``` elements. These will be the ```k``` most frequent elements.

5. **Return the Result**: You can extract just the "number" part of the selected elements and return them as an array.

```JavaScript
function kMostFrequentElements(nums, k) {
  // Step 1: Create a Frequency Map (Object)
  let frequencyMap = {};

  // Step 2: Loop Through nums and Update Frequencies
  for (let num of nums) {
    if (num in frequencyMap) {
      frequencyMap[num]++;
    } else {
      frequencyMap[num] = 1;
    }
  }

  // Step 3: Sort by Frequency
  let sortedArray = Object.entries(frequencyMap)
    .map(([number, frequency]) => ({ number, frequency }))
    .sort((a, b) => b.frequency - a.frequency);

  // Step 4: Get the Top K Elements
  let topK = sortedArray.slice(0, k);

  // Step 5: Return the Result (extract numbers from selected elements)
  let result = topK.map((element) => parseInt(element.number));

  return result;
}

```
```JavaScript
// Example usage:
let nums1 = [1, 1, 1, 2, 2, 3];
let k1 = 2;
console.log(kMostFrequentElements(nums1, k1)); // Output: [1, 2]

let nums2 = [1];
let k2 = 1;
console.log(kMostFrequentElements(nums2, k2)); // Output: [1]
```
___
## 2.Solution (need to ckeck it for better understanding)
### This code efficiently finds the ```k``` most frequent elements with a time complexity of **O(n)**
1. **Frequency Map (mp)**: A Map is used to store the frequency of each element in the nums array. It iterates through the array, updates the frequency in the map, and keeps track of how many times each element appears.

2. **Frequency Array (arr)**: An array is used to group elements by their frequencies. Each element at index i in arr contains an array of elements that have a frequency of i. This step ensures that elements with the same frequency are grouped together.

3. **Sorting by Frequency (arr.reverse())**: After creating the frequency array, it reverses the array. This step is crucial because it starts from the elements with the highest frequency. So, when you iterate through arr, you are effectively iterating through elements in descending order of frequency.

4. **Getting the Top K Elements:** It iterates through the sorted arr and appends elements to the ans array until you have collected k elements or until there are no more elements left in the arr.

```JavaScript
var topKFrequent = function(nums, k) {
    // Step 1: Create a map to store element frequencies
    const mp = new Map();

    // Step 2: Create an array to group elements by frequency
    const arr = new Array(nums.length + 1).fill(0);

    // Step 3: Create an array to store the final answer
    const ans = [];

    // Step 4: Populate the frequency map
    nums.forEach(el => {
        const val = mp.get(el) || 0;
        mp.set(el, val + 1);
    });

    // Step 5: Group elements by frequency in the 'arr' array
    for (let [key, value] of mp) {
        const prev = arr[value] || [];
        prev.push(key);
        arr[value] = prev;
    }

    // Step 6: Reverse the 'arr' array to start from elements with the highest frequency
    arr.reverse();

    // Step 7: Iterate through 'arr' to collect the top K frequent elements
    for (let el of arr) {
        if (k < 1) break;
        if (el) {
            for (let el2 of el) {
                ans.push(el2);
                k--;
            }
        }
    }

    // Step 8: Return the final answer
    return ans;
};
```