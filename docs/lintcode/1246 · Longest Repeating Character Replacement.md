# 1246 · Longest Repeating Character Replacement



## Description

Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at most k times. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.

Both the string's length and k will not exceed 10^4.

Example

**Example1**

```
Input:
"ABAB"
2
Output:
4
Explanation:
Replace the two 'A's with two 'B's or vice versa.
```

**Example2**

```
Input:
"AABABBA"
1
Output:
4
Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```



## Solutions

### Java

```java
class Solution {
    public int characterReplacement(String s, int k) {
        if (s == null || s.isEmpty()) {
            return 0;
        }
        
        if (k >= s.length()) {
            return k;
        }
        
        int[] chars = new int[26];
        int left = 0;
        int ans = 1;
        int maxCount = 0;
        
        for (int right = 0; right < s.length(); right++) {
            char end = s.charAt(right);
            chars[end - 'A'] += 1;
            maxCount = Math.max(maxCount, chars[end - 'A']);
            int changeCount = right - left + 1 - maxCount;
            if (changeCount > k) {
                chars[s.charAt(left++) - 'A']--;
            } else {
                ans = Math.max(ans, right - left + 1);
            }
        }
        
        return ans;
    }
}
```

