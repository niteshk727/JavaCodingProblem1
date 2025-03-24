---
layout: default
title: Difference between Map and FlatMap
---

# Difference between Map and FlatMap

### Map:
- Transforms each element to another using the provided function.
- Returns a stream of the same structure.

### FlatMap:
- Transforms each element and flattens nested structures into a single stream.
- Useful when dealing with `Optional`, `List`, or `Stream` objects.

---

<details>
  <summary><strong>Example</strong></summary>

```java
List<String> words = Arrays.asList("Hello", "World");
List<String[]> result = words.stream()
                             .map(word -> word.split(""))
                             .collect(Collectors.toList());

List<String> resultFlat = words.stream()
                               .flatMap(word -> Arrays.stream(word.split("")))
                               .collect(Collectors.toList());
</details> ```