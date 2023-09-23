Given an array of strings ```strs```, group the **anagrams together**. You can return the answer in **any order**.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

### Example 1:
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

### Example 2:
```
Input: strs = [""]
Output: [[""]]
```
### Example 3:
```
Input: strs = ["a"]
Output: [["a"]]
```

## Solution

- Create an empty object (hashmap) to store groups of anagrams.
- Loop through each word in the input array (strs).
- For each word, sort its characters alphabetically (```split('').sort().join('');```) to create a unique representation for anagrams. This sorted representation will be used as a key in the hashmap. (```tan & ant``` will be ```ant & ant```)
- Check if the sorted representation (```key```) exists in the ```hashmap.```
 - If it exists, push the original ```word``` into the corresponding group.
 - If it doesn't exist, create a new group with the key and add the word to it.
- After processing all words, you can convert the hashmap values to an array of arrays to get the final result.

```JavaScript
function groupAnagrams(strs) {
  const hashmap = {};

  for (const word of strs) {
    // Sort the characters in the word and use it as a key
    const sortedWord = word.split('').sort().join('');

    // Check if the key exists in the hashmap
    if (hashmap[sortedWord]) {
       // If the key exists, push the original word into the corresponding group.
      hashmap[sortedWord].push(word);
    } else {
      // If the key doesn't exist, create a new group for this key
      // and initialize it as an array with the current word.
      hashmap[sortedWord] = [word];
    }
  }

  // Convert the hashmap values to an array to get the result
  const result = Object.values(hashmap);

  return result;
}
```

Simple explanation: A ```hashmap``` is an object that can hold **keys** (such as ```sortedWords```), and each key can have associated **values**. Objects can hold multiple key-value pairs, and the value associated with a key can be of various JavaScript types, including *arrays*, *strings*, or even entire *functions* or other *objects*.

In this specific context, we use an empty object called hashmap to accumulate keys, where each key represents a sorted anagram. The associated value for each key is an array that stores the unsorted words, as if they were the original words before sorting.

The ```Object.values(hashmap)``` method is used to extract only the values (i.e., the arrays of anagrams) from the hashmap object. This means you're essentially taking all the arrays of anagrams and putting them into a new array.


### example how ```Object.values(obj)``` works
```JavaScript
const obj = {
  name: "John",
  age: 30,
  city: "New York"
};

const values = Object.values(obj);

```
``` JavaScript
values = ["John", 30, "New York"];
```