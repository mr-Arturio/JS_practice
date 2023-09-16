Given two strings ```s``` and ```t```, return ```true``` if ```t``` is an anagram of ```s```, and ```false``` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

#### Example 1:

```
Input: s = "anagram", t = "nagaram"
Output: true
```


#### Example 2:

```Input: s = "rat", t = "car"
Output: false
```
___

### Using a Map 
**most efficient**
```JavaScript
function isAnagram(s, t) {
    if (s.length !== t.length) {
        return false;
    }
    
    const charCount = new Map();
    
     // Step 1: Count the characters in string s
    for (const char of s) {
      // Step 2: Use a Map to store character counts
        charCount.set(char, (charCount.get(char) || 0) + 1);
    }
    
     // Step 3: Iterate through string t
    for (const char of t) {
      // Step 4: Check if the character exists in the charCount map
        if (!charCount.has(char)) {
            return false;
        }

        // Step 5: Decrement the character count and remove if count is zero
        charCount.set(char, charCount.get(char) - 1);
        if (charCount.get(char) === 0) {
            charCount.delete(char);
        }
    }

    // Step 6: Check if all characters have been accounted for
    return charCount.size === 0;
}
```

- **Step 1**: We start by checking if the lengths of strings s and t are different. If they have different lengths, we return false immediately because strings with different lengths cannot be anagrams.

- **Step 2**: We initialize a Map called charCount to store the counts of each character in string s. The charCount map will be used to keep track of how many times each character appears in s. We iterate through s character by character using a for...of loop.

In this step, we use charCount.set(char, (charCount.get(char) || 0) + 1); to increment the count of each character in the map. Here's how it works:

 - charCount.get(char) retrieves the current count of the character. If the character doesn't exist in the map (i.e., it's the first occurrence), charCount.get(char) returns undefined. In that case, we use || 0 to default to 0.
 - We add 1 to the count and set it in the map using charCount.set(char, ...). This way, we keep track of the counts of each character in s.
Step 3: Now, we start iterating through string t, character by character.

- **Step 4:** For each character in t, we check if it exists in the charCount map using charCount.has(char). If the character doesn't exist in the map, it means t contains a character that is not present in s, and therefore, they cannot be anagrams. In this case, we return false.

- **Step 5**: If the character exists in the charCount map, we decrement its count in the map using charCount.set(char, charCount.get(char) - 1);. We also check if the count has reached zero. If it has, we remove the character from the map using charCount.delete(char);. This is done to ensure that we don't count the same character again in t.

- **Step 6:** After processing both strings, we check if the charCount map is empty by comparing its size to 0 using charCount.size === 0. If the map is empty, it means all characters in s and t have been accounted for and have the same counts, so we return true to indicate that s and t are anagrams.
___
### Sorting 
**not efficient**<br>
splits string s into an array, sorts it, and then joins it back into a string. And compare.
The time complexity of this approach is O(n*log(n)), where n is the length of the input strings. The space complexity is O(n) because we create two arrays to store the sorted characters.

```JavaScript
function isAnagram(s, t) {
    return s.split('').sort().join('') === t.split('').sort().join('');
}

```