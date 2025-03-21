# 📚 **String Manipulation Problems - Technical Interviews**  
This document contains 10 commonly asked string manipulation problems in technical interviews at companies like **TCS, Wipro, Infosys, Cognizant**, etc.  
Each problem includes:  
- Problem Statement  
- Solution 1 (Java 8)  
- Solution 2 (Without Java 8)  
- Time & Space Complexity Analysis  

---

## 🔥 **1. First Non-Repeating Character**  
**Problem Statement:**  
Find the first non-repeating character in a given string.  
**Example:**  
Input: `"success"`  
Output: `'u'`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.*;
import java.util.stream.*;

public class FirstNonRepeating {
    public static Character firstNonRepeating(String word) {
        return word.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() == 1)
                .map(Map.Entry::getKey)
                .findFirst()
                .orElse(null);
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeating {
    public static Character firstNonRepeating(String word) {
        Map<Character, Integer> countMap = new LinkedHashMap<>();
        for (char ch : word.toCharArray()) {
            countMap.put(ch, countMap.getOrDefault(ch, 0) + 1);
        }
        for (Map.Entry<Character, Integer> entry : countMap.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }
        return null;
    }
}
```

</details>

**Time Complexity:** O(n) - Both solutions.  
**Space Complexity:** O(1) - Both solutions (for fixed character set size like ASCII).  

---

## 🔥 **2. Reverse Words in a String**  
**Problem Statement:**  
Reverse the order of words in a string.  
**Example:**  
Input: `"Java is fun"`  
Output: `"fun is Java"`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.Arrays;
import java.util.stream.Collectors;

public class ReverseWords {
    public static String reverseWords(String sentence) {
        return Arrays.stream(sentence.split(" "))
                .collect(Collectors.collectingAndThen(
                        Collectors.toList(), list -> {
                            Collections.reverse(list);
                            return String.join(" ", list);
                        }
                ));
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.*;

public class ReverseWords {
    public static String reverseWords(String sentence) {
        String[] words = sentence.split(" ");
        StringBuilder reversed = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--) {
            reversed.append(words[i]).append(" ");
        }
        return reversed.toString().trim();
    }
}
```

</details>

**Time Complexity:** O(n) - Both solutions.  
**Space Complexity:** O(n) - Both solutions.  

---

## 🔥 **3. Check If Two Strings Are Anagrams**  
**Problem Statement:**  
Check if two strings are anagrams of each other.  
**Example:**  
Input: `"listen", "silent"`  
Output: `True`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.stream.Collectors;

public class AnagramCheck {
    public static boolean areAnagrams(String str1, String str2) {
        return str1.chars().sorted().boxed().collect(Collectors.toList())
                .equals(str2.chars().sorted().boxed().collect(Collectors.toList()));
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.Arrays;

public class AnagramCheck {
    public static boolean areAnagrams(String str1, String str2) {
        if (str1.length() != str2.length()) return false;
        
        char[] arr1 = str1.toCharArray();
        char[] arr2 = str2.toCharArray();
        
        Arrays.sort(arr1);
        Arrays.sort(arr2);
        
        return Arrays.equals(arr1, arr2);
    }
}
```

</details>

**Time Complexity:** O(n log n) - Sorting both strings.  
**Space Complexity:** O(n) - For storing sorted characters.  

---

## 🔥 **4. Remove Duplicates From a String**  
**Problem Statement:**  
Remove all duplicate characters from a string.  
**Example:**  
Input: `"programming"`  
Output: `"progamin"`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.stream.Collectors;

public class RemoveDuplicates {
    public static String removeDuplicates(String str) {
        return str.chars().distinct()
                .mapToObj(c -> String.valueOf((char) c))
                .collect(Collectors.joining());
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.LinkedHashSet;

public class RemoveDuplicates {
    public static String removeDuplicates(String str) {
        LinkedHashSet<Character> set = new LinkedHashSet<>();
        StringBuilder result = new StringBuilder();
        
        for (char c : str.toCharArray()) {
            if (set.add(c)) {
                result.append(c);
            }
        }
        return result.toString();
    }
}
```

</details>

**Time Complexity:** O(n) - Traversing the string once.  
**Space Complexity:** O(n) - For storing unique characters.  

---

## 🔥 **5. Count Vowels and Consonants**  
**Problem Statement:**  
Count the number of vowels and consonants in a string.  
**Example:**  
Input: `"hello"`  
Output: `Vowels: 2, Consonants: 3`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.stream.Stream;

public class VowelConsonantCount {
    public static void countVowelsConsonants(String str) {
        long vowels = str.chars()
                         .filter(c -> "AEIOUaeiou".indexOf(c) != -1)
                         .count();
        long consonants = str.chars()
                             .filter(c -> Character.isLetter(c) && "AEIOUaeiou".indexOf(c) == -1)
                             .count();

        System.out.println("Vowels: " + vowels + ", Consonants: " + consonants);
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
public class VowelConsonantCount {
    public static void countVowelsConsonants(String str) {
        int vowels = 0, consonants = 0;

        for (char c : str.toCharArray()) {
            if (Character.isLetter(c)) {
                if ("AEIOUaeiou".indexOf(c) != -1) vowels++;
                else consonants++;
            }
        }

        System.out.println("Vowels: " + vowels + ", Consonants: " + consonants);
    }
}
```

</details>

**Time Complexity:** O(n) - Traversing the string once.  
**Space Complexity:** O(1) - Constant space usage.  

---

## 🔥 **6. Check if a String is a Palindrome**  
**Problem Statement:**  
Check if a given string is a palindrome (reads the same backward and forward).  
**Example:**  
Input: `"madam"`  
Output: `True`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.stream.IntStream;

public class PalindromeCheck {
    public static boolean isPalindrome(String str) {
        return IntStream.range(0, str.length() / 2)
                        .allMatch(i -> str.charAt(i) == str.charAt(str.length() - i - 1));
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
public class PalindromeCheck {
    public static boolean isPalindrome(String str) {
        int left = 0, right = str.length() - 1;

        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

</details>

**Time Complexity:** O(n) - Traverses half of the string.  
**Space Complexity:** O(1) - Constant space usage.  

---

## 🔥 **7. Longest Substring Without Repeating Characters**  
**Problem Statement:**  
Find the length of the longest substring without repeating characters.  
**Example:**  
Input: `"abcabcbb"`  
Output: `3` (Substring: `"abc"`)  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.*;
import java.util.stream.IntStream;

public class LongestSubstring {
    public static int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        return IntStream.range(0, s.length()).map(i -> {
            if (map.containsKey(s.charAt(i))) {
                map.clear();
            }
            map.put(s.charAt(i), i);
            return map.size();
        }).max().orElse(0);
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.HashSet;

public class LongestSubstring {
    public static int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        int left = 0;
        HashSet<Character> set = new HashSet<>();

        for (int right = 0; right < s.length(); right++) {
            while (set.contains(s.charAt(right))) {
                set.remove(s.charAt(left++));
            }
            set.add(s.charAt(right));
            maxLength = Math.max(maxLength, right - left + 1);
        }
        return maxLength;
    }
}
```

</details>

**Time Complexity:** O(n) - Linear traversal.  
**Space Complexity:** O(min(n, m)) - Where m is the charset size.  

---

## 🔥 **8. Count Frequency of Characters**  
**Problem Statement:**  
Count the frequency of each character in a string.  
**Example:**  
Input: `"apple"`  
Output: `{a=1, p=2, l=1, e=1}`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.*;
import java.util.stream.Collectors;

public class CharacterFrequency {
    public static Map<Character, Long> countFrequency(String str) {
        return str.chars()
                  .mapToObj(c -> (char) c)
                  .collect(Collectors.groupingBy(c -> c, Collectors.counting()));
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.HashMap;
import java.util.Map;

public class CharacterFrequency {
    public static Map<Character, Integer> countFrequency(String str) {
        Map<Character, Integer> frequencyMap = new HashMap<>();
        
        for (char c : str.toCharArray()) {
            frequencyMap.put(c, frequencyMap.getOrDefault(c, 0) + 1);
        }
        return frequencyMap;
    }
}
```

</details>

**Time Complexity:** O(n) - Traversing the string once.  
**Space Complexity:** O(n) - Storing frequency of all characters.  

---

## 🔥 **9. Find All Permutations of a String**  
**Problem Statement:**  
Generate all permutations of a given string.  
**Example:**  
Input: `"abc"`  
Output: `abc, acb, bac, bca, cab, cba`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class StringPermutations {
    public static Set<String> findPermutations(String str) {
        if (str.length() == 1) return Collections.singleton(str);
        
        return IntStream.range(0, str.length())
                .mapToObj(i -> findPermutations(str.substring(0, i) + str.substring(i + 1))
                        .stream().map(c -> str.charAt(i) + c)
                        .collect(Collectors.toSet()))
                .flatMap(Set::stream)
                .collect(Collectors.toSet());
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
import java.util.HashSet;
import java.util.Set;

public class StringPermutations {
    public static Set<String> findPermutations(String str) {
        Set<String> result = new HashSet<>();
        if (str.length() == 0) {
            result.add("");
            return result;
        }

        char firstChar = str.charAt(0);
        String remaining = str.substring(1);
        Set<String> words = findPermutations(remaining);
        
        for (String word : words) {
            for (int i = 0; i <= word.length(); i++) {
                result.add(word.substring(0, i) + firstChar + word.substring(i));
            }
        }
        return result;
    }
}
```

</details>

**Time Complexity:** O(n!) - Generating all permutations.  
**Space Complexity:** O(n!) - Storing all permutations.  

---

## 🔥 **10. Longest Palindromic Substring**  
**Problem Statement:**  
Find the longest palindromic substring in a string.  
**Example:**  
Input: `"babad"`  
Output: `"bab"` or `"aba"`  

<details>
<summary>Solution 1 (Java 8)</summary>

```java
public class LongestPalindrome {
    public static String longestPalindrome(String s) {
        return java.util.stream.IntStream.range(0, s.length())
                .mapToObj(i -> expandFromCenter(s, i, i))
                .max(java.util.Comparator.comparingInt(String::length))
                .orElse("");
    }

    private static String expandFromCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return s.substring(left + 1, right);
    }
}
```

</details>

<details>
<summary>Solution 2 (Without Java 8)</summary>

```java
public class LongestPalindrome {
    public static String longestPalindrome(String s) {
        String result = "";
        for (int i = 0; i < s.length(); i++) {
            String odd = expandFromCenter(s, i, i);
            String even = expandFromCenter(s, i, i + 1);
            
            if (odd.length() > result.length()) result = odd;
            if (even.length() > result.length()) result = even;
        }
        return result;
    }

    private static String expandFromCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return s.substring(left + 1, right);
    }
}
```

</details>

**Time Complexity:** O(n²) - Checking all substrings.  
**Space Complexity:** O(1) - Constant space.  
