Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

### Example 1

Input:

  `5`
 `/  \`
`2   -3`

return `[2, -3, 4]`, since all the values happen only once, return all of them in any order.

### Example 2

Input:

  `5`
 `/  \`
`2   -5`

return [2], since 2 happens twice, however -5 only occur once.


```java
public class Solution {
    Map<Integer, Integer> sumToCount;
    int maxCount;
    
    public int[] findFrequentTreeSum(TreeNode root) {
        maxCount = 0;
        sumToCount = new HashMap<Integer, Integer>();
        
        postOrder(root);
        
        List<Integer> res = new ArrayList<>();
        for (int key : sumToCount.keySet()) {
            if (sumToCount.get(key) == maxCount) {
                res.add(key);
            }
        }
        
        int[] result = new int[res.size()];
        for (int i = 0; i < res.size(); i++) {
            result[i] = res.get(i);
        }
        return result;
    }
    
    private int postOrder(TreeNode root) {
        if (root == null) return 0;
        
        int left = postOrder(root.left);
        int right = postOrder(root.right);
        
        int sum = left + right + root.val;
        int count = sumToCount.getOrDefault(sum, 0) + 1;
        sumToCount.put(sum, count);
        
        maxCount = Math.max(maxCount, count);
        
        return sum;
    }
}
```
