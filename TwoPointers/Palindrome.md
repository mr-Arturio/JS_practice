
### 1. Check for Palindromes With a FOR loop
**more efficient**
---
Half-indexing (len/2) has benefits when processing large strings. We check the end from each part and divide the number of iterations inside the FOR loop by two.

- It performs a single pass over the characters of the string.
- The time complexity of this method is O(n/2), which is essentially O(n), where n is the length of the input string. However, since we are only iterating through half of the string in most cases (due to early exit on mismatch), it is more efficient.
- The space complexity is O(1) because it does not create new string objects; it works directly on the input string.

``` javascript
function palindrome(str) {
 // Step 1. The first part is the same as earlier
 const re = /[^A-Za-z0-9]/g; // or const re = /[\W_]/g;
 str = str.toLowerCase().replace(re, '');

 // Step 2. Create the FOR loop
 let len = str.length; // var len = "A man, a plan, a canal. Panama".length = 30
 
 for (let i = 0; i < len/2; i++) {
   if (str[i] !== str[len - 1 - i]) { // As long as the characters from each part match, the FOR loop will go on
       return false; // When the characters don't match anymore, false is returned and we exit the FOR loop
   }

 }
 return true; // Both parts are strictly equal, it returns true => The string is a palindrome
}

palindrome("A man, a plan, a canal. Panama");
```

Just code
```javascript
function palindrome(str) {
 const re = /[^A-Za-z0-9]/g;
 str = str.toLowerCase().replace(re, '');
 let len = str.length;
 for (let i = 0; i < len/2; i++) {
   if (str[i] !== str[len - 1 - i]) {
       return false;
   }
 }
 return true;
}
palindrome("A man, a plan, a canal. Panama");
```
___
### 2. Check for Palindromes With Built-In Functions 
**less efficient**
---
For this solution, we will use several methods:

* The toLowerCase() method to return the calling string value converted to lowercase.
* The replace() method to return a new string with some or all matches of a pattern replaced by a replacement. We will use one of the RegExp we just created earlier.
* The split() method splits a String object into an array of strings by separating the string into sub strings.
* The reverse() method reverses an array in place. The first array element becomes the last and the last becomes the first.
* The join() method joins all elements of an array into a string.
- The time complexity of this method depends on the lengths of the original string and the modified string created at each step. It is approximately O(n), where n is the length of the input string.
- The space complexity is also O(n) due to the creation of new string objects.

```javascript
function palindrome(str) {
  // Step 1. Lowercase the string and use the RegExp to remove unwanted characters from it
  const re = /[\W_]/g; // or const re = /[^A-Za-z0-9]/g;
  
 let lowRegStr = str.toLowerCase().replace(re, '');
  // str.toLowerCase() = "A man, a plan, a canal. Panama".toLowerCase() = "a man, a plan, a canal. panama"
  // str.replace(/[\W_]/g, '') = "a man, a plan, a canal. panama".replace(/[\W_]/g, '') = "amanaplanacanalpanama"
  // let lowRegStr = "amanaplanacanalpanama";
     
  // Step 2. Use the same chaining methods with built-in functions from the previous article 'Three Ways to Reverse a String in JavaScript'
  let reverseStr = lowRegStr.split('').reverse().join(''); 
   // So, "amanaplanacanalpanama".split('').reverse().join('') = "amanaplanacanalpanama";
  // And, let reverseStr = "amanaplanacanalpanama";
   
  // Step 3. Check if reverseStr is strictly equals to lowRegStr and return a Boolean
  return reverseStr === lowRegStr; // "amanaplanacanalpanama" === "amanaplanacanalpanama"? => true
}
 
palindrome("A man, a plan, a canal. Panama");
```

Just code 
```javascript
function palindrome(str) {
  const re = /[\W_]/g;
  let lowRegStr = str.toLowerCase().replace(re, '');
  let reverseStr = lowRegStr.split('').reverse().join(''); 
  return reverseStr === lowRegStr;
}
palindrome("A man, a plan, a canal. Panama");
```
---