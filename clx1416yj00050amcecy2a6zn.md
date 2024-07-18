---
title: "How to Merge Two Arrays in Java: A Simple Guide"
seoTitle: "Merging Arrays in Java: Simple Guide"
seoDescription: "Learn how to merge two arrays in Java using various methods, including predefined functions, Java Streams, and ArrayList"
datePublished: Wed Jun 05 2024 00:48:23 GMT+0000 (Coordinated Universal Time)
cuid: clx1416yj00050amcecy2a6zn
slug: how-to-merge-two-arrays-in-java-a-simple-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1717548323508/8115cf51-1886-4e36-8258-cd4aff750a86.jpeg
tags: tutorial, code-review, programming-blogs, java, opensource, learning, merge, coding, guide, array, arrays, array-methods, programming-tips, arraylist, array-javascript-array-methods-map-filter-foreach

---

Merging two arrays is a common operation in Java, often encountered in various programming tasks. This article explores multiple methods to merge two arrays in Java, catering to different preferences and scenarios.

## Method 1: Using Predefined Function

```java
import java.util.Arrays;

public class MergeTwoArrays1 {
    public static void main(String[] args) {
        int[] a = {10, 20, 30, 40};
        int[] b = {50, 60, 70, 80};

        int a1 = a.length;
        int b1 = b.length;
        int c1 = a1 + b1;

        int[] c = new int[c1];

        System.arraycopy(a, 0, c, 0, a1);
        System.arraycopy(b, 0, c, a1, b1);

        System.out.println(Arrays.toString(c));
    }
}
```

**Output:**

```bash
[10, 20, 30, 40, 50, 60, 70, 80]
```

**Complexity:**

* Time Complexity: O(M + N)
    
* Auxiliary Space: O(M + N)
    

Here, M is the length of array a, and N is the length of array b.

## Method 2: Without Using Predefined Function

```java
public class MergeTwoArrays2 {
    public static void main(String[] args) {
        int a[] = {30, 25, 40};
        int b[] = {45, 50, 55, 60, 65};

        int a1 = a.length;
        int b1 = b.length;
        int c1 = a1 + b1;

        int[] c = new int[c1];

        for (int i = 0; i < a1; i++) {
            c[i] = a[i];
        }

        for (int i = 0; i < b1; i++) {
            c[a1 + i] = b[i];
        }

        for (int i = 0; i < c1; i++) {
            System.out.println(c[i]);
        }
    }
}
```

**Output:**

```bash
30
25
40
45
50
55
60
65
```

**Complexity:**

* Time Complexity: O(M + N)
    
* Auxiliary Space: O(M + N)
    

Here, M is the length of array a, and N is the length of array b.

## Method 3: Using Java Streams

```java
import java.util.Arrays;
import java.util.stream.IntStream;

public class MergeTwoArraysUsingStreams {
    public static void main(String[] args) {
        int a[] = {30, 25, 40};
        int b[] = {45, 50, 55, 60, 65};

        int[] c = mergeArraysUsingStreams(a, b);

        Arrays.stream(c).forEach(System.out::println);
    }

    public static int[] mergeArraysUsingStreams(int[] arr1, int[] arr2) {
        return IntStream.concat(Arrays.stream(arr1), Arrays.stream(arr2)).toArray();
    }
}
```

**Output:**

```bash
30
25
40
45
50
55
60
65
```

**Complexity:**

* Time Complexity: O(M + N)
    
* Auxiliary Space: O(M + N)
    

Here, M is the length of array a, and N is the length of array b.

## Method 4: Using ArrayList

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class MergeArrays {
    public static int[] mergeArraysUsingArrayList(int[] a, int[] b) {
        List<Integer> resultList = new ArrayList<>();

        for (int num : a) {
            resultList.add(num);
        }

        for (int num : b) {
            resultList.add(num);
        }

        return resultList.stream()
                .mapToInt(Integer::intValue).toArray();
    }

    public static void main(String[] args) {
        int a[] = {30, 25, 40};
        int b[] = {45, 50, 55, 60, 65};
        int[] result = mergeArraysUsingArrayList(a, b);

        for (int i = 0; i < result.length; i++) {
            System.out.println(result[i]);
        }
    }
}
```

**Output:**

```bash
30
25
40
45
50
55
60
65
```

**Complexity:**

* Time Complexity: O(M + N)
    
* Auxiliary Space: O(M + N)
    

Here, M is the length of array a, and N is the length of array b.

These methods offer flexibility in merging arrays, catering to different preferences and requirements. Choose the one that best suits your specific scenario and coding style.