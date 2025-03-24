---
layout: default
title: First Non-Repeating Character
---

# First Non-Repeating Character

### Problem Statement
Find the first non-repeating character in a string.

---

<details>
  <summary><strong>Solution 1 (Java 8)</strong></summary>

```java
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.stream.Collectors;

public class FirstNonRepeatingCharacter {
    public static Character firstNonRepeating(String word) {
        Map<Character, Long> charCount = word.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()));

        return charCount.entrySet().stream()
                .filter(entry -> entry.getValue() == 1)
                .map(Map.Entry::getKey)
                .findFirst()
                .orElse(null);
    }
}```
</details>

<details>
    <summary><strong>Solution 2 (Without Java 8)</strong></summary>
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeatingCharacter {
    public static Character firstNonRepeating(String word) {
        Map<Character, Integer> charCount = new LinkedHashMap<>();

        for (char c : word.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }

        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }
        return null;
    }
}
</details>