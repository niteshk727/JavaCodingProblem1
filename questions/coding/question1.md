---
layout: default
title: First Non-Repeating Character
---

# First Non-Repeating Character

### Problem Statement
Find the first non-repeating character in a given string. If all characters repeat, return a message saying so.

---

<details>
  <summary>Solution 1 (Java 8)</summary>

```java
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.stream.Collectors;

public class FirstNonRepeatingCharacter {
    public static void main(String[] args) {
        String word = "swiss";
        
        Character result = word.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.toMap(
                c -> c,
                c -> 1,
                Integer::sum,
                LinkedHashMap::new
            ))
            .entrySet()
            .stream()
            .filter(entry -> entry.getValue() == 1)
            .map(Map.Entry::getKey)
            .findFirst()
            .orElse(null);

        System.out.println("First non-repeating character: " + result);
    }
}
```

</details>

---

<details>
  <summary>Solution 2 (Without Java 8 Features)</summary>

```java
import java.util.HashMap;
import java.util.Map;

public class FirstNonRepeatingCharacter {
    public static void main(String[] args) {
        String word = "swiss";
        Map<Character, Integer> charCountMap = new HashMap<>();

        for (char c : word.toCharArray()) {
            charCountMap.put(c, charCountMap.getOrDefault(c, 0) + 1);
        }

        for (char c : word.toCharArray()) {
            if (charCountMap.get(c) == 1) {
                System.out.println("First non-repeating character: " + c);
                return;
            }
        }

        System.out.println("No non-repeating character found.");
    }
}
```

</details>

---