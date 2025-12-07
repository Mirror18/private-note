## 两数之和
### 题目
给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** _`target`_  的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。

你可以按任意顺序返回答案。

**示例 1：**

**输入：**nums = [2,7,11,15], target = 9
**输出：**[0,1]
**解释：**因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

**示例 2：**

**输入：**nums = [3,2,4], target = 6
**输出：**[1,2]

**示例 3：**

**输入： **nums = [3,3], target = 6
**输出：**[0,1]

### 题解
```java
/**  
 * 两数之和  
 * @param nums  
 * @param target  
 * @return  
 */  
public int[]  twoSum(int[] nums,int target){  
    int[] result = new int[2];  
    for (int i = 0; i < nums.length; i++) {  
        for (int j = nums.length-1; j >i ; j--) {  
            if (nums[i] + nums[j] == target) {  
                result[0] = i;  
                result[1] = j;  
            }  
        }  
    }  
    return result;  
}  
  
/**  
 * 两数之和优化版  
 * @param nums  
 * @param target  
 * @return  
 */  
public int[] twoSum_1(int[] nums,int target){  
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();  
    int n = nums.length;  
    for (int i = 0; i < n; i++) {  
        if (map.containsKey(target - nums[i])) {  
            return new int[]{map.get(target - nums[i]), i};  
        }  
        map.put(nums[i], i);  
    }  
    return new int[]{-1,-1};  
}
```

## 字母异位词分组
给你一个字符串数组，请你将 字母异位词 组合在一起。可以按任意顺序返回结果列表。

**示例 1:**

**输入:** strs = ` ["eat", "tea", "tan", "ate", "nat", "bat"]`

**输出:**` [["bat"],["nat","tan"],["ate","eat","tea"]]`

**解释：**

- 在 strs 中没有字符串可以通过重新排列来形成 `"bat"`。
- 字符串 `"nat"` 和 `"tan"` 是字母异位词，因为它们可以重新排列以形成彼此。
- 字符串 `"ate"` ，`"eat"` 和 `"tea"` 是字母异位词，因为它们可以重新排列以形成彼此。

**示例 2:**

**输入:** `strs = [""]`

**输出:** `[[""]] `

**示例 3:**

**输入:** `strs = ["a"]`

**输出:**` [["a"]] `

### 题解
```java
/**  
 * 字母异位词  
 * @param strs  
 * @return  
 */  
public List<List<String>> groupAnagrams(String[] strs){  
 List<List<String>> result = new ArrayList<>();  
 Map<String, List<String>> map = new HashMap<>();  
 for (String str : strs) {  
     char[] chars = str.toCharArray();  
     Arrays.sort(chars);  
     String key = new String(chars);  
     if (!map.containsKey(key)) {  
         map.put(key, new ArrayList<>());  
     }  
     map.get(key).add(str);  
  
 }  
 result.addAll(map.values());  
 return result;  
}
```

### 最长连续序列
### 题目
给定一个未排序的整数数组 `nums` ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

**示例 1：**

**输入：** nums = [100,4,200,1,3,2]
**输出：** 4
**解释：** 最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。

**示例 2：**

**输入：** nums = [0,3,7,2,5,8,4,6,0,1]
**输出：** 9

**示例 3：**

**输入：** nums = [1,0,1,2]
**输出：** 3

### 题解
```java
public int longestConsecutive(int[] nums){  
    HashSet<Integer> set = new HashSet<>();  
    for(int num : nums){  
        set.add(num);  
    }  
    int max = 0;  
    for(int num : set){  
        if(set.contains(num-1)){  
            continue;  
        }  
        int count = 1;  
        while(set.contains(num+count)){  
            count++;  
        }  
          max =Math.max(max,count);
    }  
    return max;  
}
```


## 移动零
给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**请注意** ，必须在不复制数组的情况下原地对数组进行操作。

**示例 1:**

**输入:** nums = `[0,1,0,3,12]`
**输出:** `[1,3,12,0,0]`

**示例 2:**

**输入:** nums = `[0]`
**输出:** `[0]`

```java
public void moveZeroes(int[] nums) {  
    int n = nums.length;  
    for (int i = 0; i < nums.length; i++) {  
        if (nums[i] != 0) {  
            continue;  
        }  
        for (int j = i+1; j < n; j++) {  
            if (nums[j] != 0) {  
                nums[i] = nums[j];  
                nums[j] = 0;  
                break;  
            }  
        }  
  
    }  
}  
  
public void moveZeroes1(int[] nums){  
    int slow =0;  
    for (int fast = 0; fast < nums.length; fast++) {  
        if (nums[fast] != 0) {  
            nums[slow] = nums[fast];  
            slow++;  
        }  
    }  
    for (int i = slow; i < nums.length; i++) {  
        nums[i] = 0;  
    }  
}
```

## 盛最多水的容器
给定一个长度为 `n` 的整数数组 `height` 。有 `n` 条垂线，第 `i` 条线的两个端点是 `(i, 0)` 和 `(i, height[i])` 。

找出其中的两条线，使得它们与 `x` 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

**输入：**[1,8,6,2,5,4,8,3,7]
**输出：** 49

```java
class Solution {

    public int maxArea(int[] height) {

       int result = 0;

        int left = 0;

        int right = height.length - 1;

        while (left < right) {

            result = Math.max(result, Math.min(height[left], height[right]) * (right - left));

            if (height[left] < height[right]) {

                left++;

            }else {

                right--;

            }

        }

        return result;

    }

}
```

## 三数之和
给你一个整数数组 `nums` ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j`、`i != k` 且 `j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请你返回所有和为 `0` 且不重复的三元组。
**注意：** 答案中不可以包含重复的三元组。

**示例 1：**

**输入：** nums = [-1,0,1,2,-1,-4]
**输出：** `[[-1,-1,2],[-1,0,1]]`
**解释：**
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0 。
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0 。
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0 。
不同的三元组是 [-1,0,1] 和 [-1,-1,2] 。
注意，输出的顺序和三元组的顺序并不重要。

**示例 2：**

**输入：** `nums = [0,1,1]`
**输出：**[]
**解释：** 唯一可能的三元组和不为 0 。

**示例 3：**

**输入：** nums = [0,0,0]
**输出：** `[[0,0,0]]`
**解释：** 唯一可能的三元组和为 0 。

```java
class Solution {

    public List<List<Integer>> threeSum(int[] nums) {

                List<List<Integer>> result = new ArrayList<>();

        Arrays.sort(nums);

        int n = nums.length;

        for (int i = 0; i < n; i++) {

            if (i > 0 && nums[i] == nums[i - 1]) {

                continue;

            }

            int right = n-1;

            int target = -nums[i];

            for (int j = i + 1; j < n; j++) {

                if (j > i + 1 && nums[j] == nums[j - 1]) {

                    continue;

                }

               while(j<right && nums[j] +nums[right] > target){

                   right--;

               }

               if (j == right) {

                   break;

               }

               if(nums[j]+nums[right] == target){

                   List<Integer> temp = new ArrayList<>();

                   temp.add(nums[i]);

                   temp.add(nums[j]);

                   temp.add(nums[right]);

                   result.add(temp);

               }

            }

        }

        return result;

    }

}
```
