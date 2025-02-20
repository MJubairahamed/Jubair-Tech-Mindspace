### **Coding Challenges with Solutions**

#### **1. Reverse a String without using built-in methods**
```java
public class ReverseString {
    public static String reverse(String str) {
        StringBuilder sb = new StringBuilder();
        for (int i = str.length() - 1; i >= 0; i--) {
            sb.append(str.charAt(i));
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        System.out.println(reverse("Hello")); // Output: olleH
    }
}
```

---

#### **2. Find the first non-repeating character in a string**
```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstUniqueChar {
    public static char findFirstUnique(String str) {
        Map<Character, Integer> charCount = new LinkedHashMap<>();
        for (char c : str.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }
        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            if (entry.getValue() == 1) return entry.getKey();
        }
        return '_'; // Return '_' if no unique character found
    }

    public static void main(String[] args) {
        System.out.println(findFirstUnique("swiss")); // Output: w
    }
}
```

---

#### **3. Check if a number is prime**
```java
public class PrimeCheck {
    public static boolean isPrime(int num) {
        if (num <= 1) return false;
        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPrime(11)); // Output: true
    }
}
```

---

#### **4. Find the factorial of a number using recursion**
```java
public class Factorial {
    public static int factorial(int n) {
        return (n == 0) ? 1 : n * factorial(n - 1);
    }

    public static void main(String[] args) {
        System.out.println(factorial(5)); // Output: 120
    }
}
```

---

#### **5. Find the missing number in an array**
```java
public class MissingNumber {
    public static int findMissing(int[] arr, int n) {
        int total = n * (n + 1) / 2;
        int sum = 0;
        for (int num : arr) sum += num;
        return total - sum;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 4, 5, 6};
        System.out.println(findMissing(nums, 6)); // Output: 3
    }
}
```

---

#### **6. Check if a string is a palindrome**
```java
public class PalindromeCheck {
    public static boolean isPalindrome(String str) {
        int left = 0, right = str.length() - 1;
        while (left < right) {
            if (str.charAt(left++) != str.charAt(right--)) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("madam")); // Output: true
    }
}
```

---

#### **7. Implement a simple Singleton pattern**
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

---

#### **8. Find the intersection of two arrays**
```java
import java.util.HashSet;

public class ArrayIntersection {
    public static void findIntersection(int[] arr1, int[] arr2) {
        HashSet<Integer> set = new HashSet<>();
        for (int num : arr1) set.add(num);
        for (int num : arr2) {
            if (set.contains(num)) System.out.print(num + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {3, 4, 5, 6, 7};
        findIntersection(arr1, arr2); // Output: 3 4 5
    }
}
```

---

#### **9. Reverse a linked list**
```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class ReverseLinkedList {
    public static ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```

---

#### **10. Implement a simple Producer-Consumer using `BlockingQueue`**
```java
import java.util.concurrent.*;

class Producer implements Runnable {
    private BlockingQueue<Integer> queue;
    Producer(BlockingQueue<Integer> queue) { this.queue = queue; }
    public void run() {
        try {
            for (int i = 1; i <= 5; i++) {
                queue.put(i);
                System.out.println("Produced: " + i);
                Thread.sleep(500);
            }
        } catch (InterruptedException e) { e.printStackTrace(); }
    }
}
```
### **11. What Happens When You Run `1.0 / 0.0` in Java?**  

- In Java, **floating-point division by zero** follows the **IEEE 754 standard** for floating-point arithmetic.  
- **`1.0 / 0.0`** results in **`Infinity`** instead of throwing an exception.  
- Example:  
  ```java
  public class Test {
      public static void main(String[] args) {
          System.out.println(1.0 / 0.0); // Output: Infinity
      }
  }
  ```
- However, **integer division by zero (`1 / 0`)** throws an `ArithmeticException`.  
- **Conclusion:** In **floating-point arithmetic**, division by zero **does not cause an exception**, but returns **positive or negative infinity** depending on the sign of the numerator. 🚀
---
