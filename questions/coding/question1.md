---
layout: default
title: Sample Coding Question
---

# Find the First Non-Repeating Character

### Problem Statement
Write a program to find the first non-repeating character in a string.

<details>
  <summary>Solution 1 (Using Java 8)</summary>

```java
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.Optional;

public class FirstNonRepeatingCharacter {
    public static void main(String[] args) {
        String word = "swiss";

        Optional<Character> result = word.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()))
                .entrySet()
                .stream()
                .filter(e -> e.getValue() == 1)
                .map(Map.Entry::getKey)
                .findFirst();

        System.out.println("First non-repeating character: " + result.orElse(null));
    }
}
```
</details>

<details>
    <summary>Solution 2 (Without Java 8 Features)</summary>

```Java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeatingCharacter {
    public static void main(String[] args) {
        String word = "swiss";
        Map<Character, Integer> countMap = new LinkedHashMap<>();

        for (char c : word.toCharArray()) {
            countMap.put(c, countMap.getOrDefault(c, 0) + 1);
        }

        for (Map.Entry<Character, Integer> entry : countMap.entrySet()) {
            if (entry.getValue() == 1) {
                System.out.println("First non-repeating character: " + entry.getKey());
                break;
            }
        }
    }
}
```
</details>

### Time & Space Complexity Analysis

| Approach          | Time Complexity | Space Complexity |
|-------------------|-----------------|------------------|
| Java 8 Stream API | O(n)            | O(n)             |
| Without Java 8    | O(n)            | O(n)             |
