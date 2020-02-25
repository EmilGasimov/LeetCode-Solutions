Given an array A of integers, for each integer `A[i]` we may choose any x with `-K <= x <= K`, and add x to A[i].

After this process, we have some array B.

Return the smallest possible difference between the maximum value of B and the minimum value of B.

```java
class Solution {
    public int smallestRangeI(int[] A, int K) {
        int min = A[0], max = A[0];
        for (int x: A) {
            min = Math.min(min, x);
            max = Math.max(max, x);
        }
        return Math.max(0, max - min - 2*K);
    }
}
```
