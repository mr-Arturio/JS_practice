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

## Solution:
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