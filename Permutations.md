```java

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(res, nums, new ArrayList<>(), new boolean[nums.length]);
        return res;
    }
    
    private void dfs(List<List<Integer>> res, int[] nums, List<Integer> temp, boolean[] isUsed) {
        if(temp.size() == nums.length) {
            res.add(new ArrayList<>(temp));
            return;
        }
        
        for(int i = 0; i < nums.length; i++) {
            if(!isUsed[i]) {
                temp.add(nums[i]);
                isUsed[i] = true;
                dfs(res, nums, temp, isUsed);
                temp.remove(temp.size() - 1);
                isUsed[i] = false;
            }
        }
    }
}
```
