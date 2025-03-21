# JavaCodingProblem1
Java Coding Problems - String Manipulation

1. **Introduction** - Brief overview of the document.  
2. **Problem Statement** - Description of each problem.  
3. **Solution (Java 8)** - Code using Java 8 features.  
4. **Solution (Traditional Java)** - Code without Java 8 features.  
5. **Complexity Analysis** - Time and space complexity.  
6. **Explanation** - How the solution works.  
---
### 🚀 **String Manipulation Problems for Technical Interviews**  
This document contains 10 commonly asked string manipulation problems in technical interviews at companies like **TCS, Wipro, Infosys, Cognizant**, and more.  
Each problem includes:  
1. Problem Statement  
2. Solution using **Java 8 (Streams)**  
3. Solution using **Traditional Java**  
4. **Time and Space Complexity Analysis**  

---

## 📝 **1. First Non-Repeating Character**  

### 💡 **Problem Statement:**  
Find the first non-repeating character in a given string.  
**Example:**  
Input: `"success"`  
Output: `'u'`  

---

### 🚀 **Solution (Java 8):**  
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

    public static void main(String[] args) {
        String word = "success";
        System.out.println("First Non-Repeating Character: " + firstNonRepeating(word));
    }
}
```

---

### 🔧 **Solution (Traditional Java):**  
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

    public static void main(String[] args) {
        String word = "success";
        System.out.println("First Non-Repeating Character: " + firstNonRepeating(word));
    }
}
```

---

### 📊 **Complexity Analysis:**  
- **Time Complexity:** O(n)  
  - Both solutions traverse the string twice: once for counting and once for finding the result.  
- **Space Complexity:** O(1) (constant space if character set size is fixed, e.g., ASCII).  

---

## 📝 **2. Reverse Words in a String**  

### 💡 **Problem Statement:**  
Given a string, reverse the order of words.  
**Example:**  
Input: `"Java is fun"`  
Output: `"fun is Java"`  

---

### 🚀 **Solution (Java 8):**  
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

    public static void main(String[] args) {
        String sentence = "Java is fun";
        System.out.println("Reversed Words: " + reverseWords(sentence));
    }
}
```

---

### 🔧 **Solution (Traditional Java):**  
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

    public static void main(String[] args) {
        String sentence = "Java is fun";
        System.out.println("Reversed Words: " + reverseWords(sentence));
    }
}
```

---

### 📊 **Complexity Analysis:**  
- **Time Complexity:** O(n)  
  - Splitting and reversing the list of words take linear time.  
- **Space Complexity:** O(n)  
  - Space is required to store the reversed list.  

---
