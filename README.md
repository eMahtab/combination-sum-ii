# Combination Sum II

https://leetcode.com/problems/combination-sum-ii

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.

```
Example 1:

Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

Example 2:

Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

### Constraints:

1. 1 <= candidates.length <= 100
2. 1 <= candidates[i] <= 50
3. 1 <= target <= 30

## Approach :
This problem is similar to [Combination Sum](https://github.com/eMahtab/combination-sum) problem, with couple of conditions, a number n can only be used x times, where x is number of times n appears in candidates array. And we should not add duplicate combinations. To solve this problem we sort the candidates array and then find the combinations, we skip the processing if we encounter same number which is not the starting of the group of same numbers.

## Implementation : 
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if(candidates == null || candidates.length == 0)
          return result;
        Arrays.sort(candidates);
        findCombination(candidates, target, 0, new ArrayList<Integer>(), result);
        return result;
    }

    private void findCombination(int[] candidates, int target, int index, List<Integer> combination,
  	      List<List<Integer>> result) {
  	 if(target == 0) {
  	    result.add(new ArrayList<Integer>(combination));
  	    return;
  	 }
  	 for(int i = index; i < candidates.length; i++) {
  	    if(i > index && candidates[i] == candidates[i-1]) continue; 
  	
  	    if(candidates[i] <= target) {
  	        combination.add(candidates[i]);
  	        if(target - candidates[i] >= 0)
  	          findCombination(candidates, target - candidates[i], i+1, combination, result);
  	        combination.remove(combination.size()-1);
  	    }   
  	 }
    }
}
```
## Time and Space Complexity
The time complexity of the combinationSum2 function is exponential because for each element in the candidates array, the function makes a recursive call.

### Time Complexity = O(2^N)

### Space Complexity = O(N)

# References :
