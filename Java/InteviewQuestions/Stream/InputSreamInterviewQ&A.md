# IntStream Interview Questions — — ——
- What is IntStream in Java?
- IntStream is a specialized stream for handling primitive integers (int). It provides a sequence of primitive int values and supports various operations such as filtering, mapping, reduction, and iteration.

- How do you create an IntStream in Java?
- You can create an IntStream in Java using factory methods like IntStream.range(int startInclusive, int endExclusive) or IntStream.rangeClosed(int startInclusive, int endInclusive) to create a stream of integers within a specified range, or by converting other data structures like arrays or collections using Arrays.stream(int[] array) or Collection.stream().mapToInt().

- What are the terminal operations you can perform on an IntStream
- Common terminal operations include forEach, sum, average, min, max, count, and reduce. These operations consume the elements of the stream and produce a result or a side effect.

- How do you perform mapping operations on an IntStream?
- You can perform mapping operations on an IntStream using methods like mapToInt, mapToLong, and mapToDouble. These methods transform each element of the stream into another type or value.

- Explain the usage of filter in IntStream.
- The filter method in IntStream is used to eliminate elements from the stream based on a specified condition. It takes a predicate as an argument and retains only those elements that satisfy the predicate.
Question: How can you filter elements in an IntStream?

You can use the filter method, which takes a predicate. For example:
```java
IntStream.range(1, 10)
          .filter(n -> n % 2 == 0)
          .forEach(System.out::println);
```
- How do you perform reduction operations on an IntStream?
- Reduction operations in IntStream are performed using methods like reduce, sum, average, min, and max. These operations aggregate the elements of the stream into a single result by applying a binary operator to each element.

- Sample Program
- [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/Stream/PrimitiveStreamExample.java)