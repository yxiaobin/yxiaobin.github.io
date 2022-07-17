---
title: leetcode第302场周赛
date: 2022-07-17 14:23:09
tags: leetcode
categories: leetcode
---

### <center>leetcode 周赛 301 </center> 

* 这次周赛的整体难度不大，第一次四题全a，不过排名变化还是不大1400左右，下次继续努力

# [数组能形成多少数对](https://leetcode.cn/problems/maximum-number-of-pairs-in-array/)

* 给你一个下标从 0 开始的整数数组 nums 。在一步操作中，你可以执行以下步骤：

  从 nums 选出 两个 相等的 整数
  从 nums 中移除这两个整数，形成一个 数对
  请你在 nums 上多次执行此操作直到无法继续执行。

  返回一个下标从 0 开始、长度为 2 的整数数组 answer 作为答案，其中 answer[0] 是形成的数对数目，answer[1] 是对 nums 尽可能执行上述操作后剩下的整数数目。

* 示例

```
输入：nums = [1,3,2,1,3,2,2]
输出：[3,1]
解释：
nums[0] 和 nums[3] 形成一个数对，并从 nums 中移除，nums = [3,2,3,2,2] 。
nums[0] 和 nums[2] 形成一个数对，并从 nums 中移除，nums = [2,2,2] 。
nums[0] 和 nums[1] 形成一个数对，并从 nums 中移除，nums = [2] 。
无法形成更多数对。总共形成 3 个数对，nums 中剩下 1 个数字。
```

<!-- more -->

```
输入：nums = [1,1]
输出：[1,0]
解释：nums[0] 和 nums[1] 形成一个数对，并从 nums 中移除，nums = [] 。
无法形成更多数对。总共形成 1 个数对，nums 中剩下 0 个数字。
```

* ##### 这道题比较简单实际问的就是，一个数组有多少数可以形成数对，多少不能形成数对。我们可以使用桶排的思想（HashMap）统计每一个数出现的次数。对2取整就是能凑成的，取余就是不能凑成的。

  ```java
  class Solution {
      public int[] numberOfPairs(int[] nums) {
          int a = 0;
          int b = 0;
          Map<Integer, Integer> map = new HashMap<>();
          for(int i=0;i<nums.length;i++){
              map.put(nums[i], map.getOrDefault(nums[i],0)+1);
          }
          for(Integer x: map.keySet()){
              int t = map.get(x);
              a+=t/2;
              b+=t%2;
          }
          return new int[]{a,b};
      }
  }
  ```

  

# [数位和相等数对的最大和](https://leetcode.cn/problems/max-sum-of-a-pair-with-equal-sum-of-digits/)

* 给你一个下标从 0 开始的数组 nums ，数组中的元素都是 正 整数。请你选出两个下标 i 和 j（i != j），且 nums[i] 的数位和 与  nums[j] 的数位和相等。

  请你找出所有满足条件的下标 i 和 j ，找出并返回 nums[i] + nums[j] 可以得到的 最大值 。

* 示例

  ```
  输入：nums = [18,43,36,13,7]
  输出：54
  解释：满足条件的数对 (i, j) 为：
  - (0, 2) ，两个数字的数位和都是 9 ，相加得到 18 + 36 = 54 。
  - (1, 4) ，两个数字的数位和都是 7 ，相加得到 43 + 7 = 50 。
  所以可以获得的最大和是 54 。
  ```

  ```
  输入：nums = [10,12,19,14]
  输出：-1
  解释：不存在满足条件的数对，返回 -1 。
  ```

* 根据题意是根据**数位和**进行分组的，因此，我们可以维护一个**HashMap**，**key是数位和，value是该数为和的最大值和次大值**，再统计结果的过程中，同时维护最终结果。

  ```java
  class Solution {
      public int maximumSum(int[] nums) {
          int res = -1;
          Map<Integer, Node> map = new HashMap<>();
          for(int i=0;i<nums.length;i++){
              int index = getIndexSum(nums[i]);
              Node tmp = map.get(index);
              if(tmp == null){
                  tmp = new Node();
              }
              if(nums[i] >= tmp.firstMax){
                  tmp.secondMax = tmp.firstMax;
                  tmp.firstMax= nums[i];
              }else if(nums[i] >= tmp.secondMax){
                   tmp.secondMax = nums[i];
              }
              if(tmp.firstMax != -1 && tmp.secondMax!=-1){
                  res = Math.max(res, tmp.firstMax+tmp.secondMax);
              }
              map.put(index,tmp);
          }
          return res;
      }
      public int getIndexSum(int a){
          int sum = 0;
          while(a>0){
              sum += a%10;
              a = a/10;
          }
          return sum;
      }
  }
  class Node{
      int firstMax ;
      int secondMax;
      public Node(){
          firstMax = -1;
          secondMax = -1;
  
      }
  }
  ```

  

#  [裁剪数字后查询第 K 小的数字](https://leetcode.cn/problems/query-kth-smallest-trimmed-number/)

* 给你一个下标从 0 开始的字符串数组 nums ，其中每个字符串 长度相等 且只包含数字。

  再给你一个下标从 0 开始的二维整数数组 queries ，其中 queries[i] = [ki, trimi] 。对于每个 queries[i] ，你需要：

  * 将 nums 中每个数字 裁剪 到剩下 最右边 trimi 个数位。
  * 在裁剪过后的数字中，找到 nums 中第 ki 小数字对应的 下标 。如果两个裁剪后数字一样大，那么下标 更            小 的数字视为更小的数字。 
  * 将 nums 中每个数字恢复到原本字符串。
  * 请你返回一个长度与 queries 相等的数组 answer，其中 answer[i]是第 i 次查询的结果。
  * 提示：裁剪到剩下 x 个数位的意思是不断删除最左边的数位，直到剩下 x 个数位。
    nums 中的字符串可能会有前导 0 。

* 示例

  ```
  输入：nums = ["102","473","251","814"], queries = [[1,1],[2,3],[4,2],[1,2]]
  输出：[2,2,1,0]
  解释：
  1. 裁剪到只剩 1 个数位后，nums = ["2","3","1","4"] 。最小的数字是 1 ，下标为 2 。
  2. 裁剪到剩 3 个数位后，nums 没有变化。第 2 小的数字是 251 ，下标为 2 。
  3. 裁剪到剩 2 个数位后，nums = ["02","73","51","14"] 。第 4 小的数字是 73 ，下标为 1 。
  4. 裁剪到剩 2 个数位后，最小数字是 2 ，下标为 0 。
     注意，裁剪后数字 "02" 值为 2 。
  ```

  ```
  输入：nums = ["24","37","96","04"], queries = [[2,1],[2,2]]
  输出：[3,0]
  解释：
  1. 裁剪到剩 1 个数位，nums = ["4","7","6","4"] 。第 2 小的数字是 4 ，下标为 3 。
     有两个 4 ，下标为 0 的 4 视为小于下标为 3 的 4 。
  2. 裁剪到剩 2 个数位，nums 不变。第二小的数字是 24 ，下标为 0 。
  ```

* ##### topK的变形，Kth小则维护最大堆,求Kth大则维护最大堆。

  ```
  class Solution {
      public int[] smallestTrimmedNumbers(String[] nums, int[][] queries) {
          int n = nums.length;
          int len = nums[0].length();
          int m = queries.length;
          int k = 0;
          int[] res = new int[m];
          PriorityQueue<Node> maxheap;
          while(k<m){
              maxheap = new PriorityQueue<>(new Comparator<Node>(){
                  public int compare(Node a, Node b){
                      if(b.val.compareTo(a.val) >0 ){
                          return 1;
                      }else if(b.val.compareTo(a.val) <0){
                          return -1;
                      }else{
                          
                          return b.index-a.index;
                      }
                  }
              });
              int ki = queries[k][0];
              int trim = queries[k][1];
            
              for(int i=0;i<n;i++){
                  String tmp = nums[i].substring(len-trim,len);
                  
                  if(maxheap.size() < ki){
                      Node t = new Node();
                      t.index = i;
                      t.val = tmp;
                      maxheap.add(t);
                  }else{
                      if(maxheap.peek().val.compareTo(tmp)>0){
                          maxheap.poll();
                          Node t = new Node();
                          t.index = i;
                          t.val = tmp;
                          maxheap.add(t);
                      }
                  }       
                      
              }
              //System.out.println("k="+ki + "   "+maxheap);
              res[k] = maxheap.peek().index;
              k++;
          }
          
          return res;
      }
  }
  class Node{
      int index;
      String val;
      public String toString(){
          return "["+"index=" + index + " val=" + val +"]";
      }
  }
  ```

  

# [使数组可以被整除的最少删除次数](https://leetcode.cn/problems/minimum-deletions-to-make-array-divisible/)

* 给你两个正整数数组 nums 和 numsDivide 。你可以从 nums 中删除任意数目的元素。

  请你返回使 nums 中 最小 元素可以整除 numsDivide 中所有元素的 最少 删除次数。如果无法得到这样的元素，返回 -1 。

  如果 y % x == 0 ，那么我们说整数 x 整除 y 。

* 示例

  ```
  输入：nums = [2,3,2,4,3], numsDivide = [9,6,9,3,15]
  输出：2
  解释：
  [2,3,2,4,3] 中最小元素是 2 ，它无法整除 numsDivide 中所有元素。
  我们从 nums 中删除 2 个大小为 2 的元素，得到 nums = [3,4,3] 。
  [3,4,3] 中最小元素为 3 ，它可以整除 numsDivide 中所有元素。
  可以证明 2 是最少删除次数。
  ```

  ```
  输入：nums = [4,3,6], numsDivide = [8,2,6,10]
  输出：-1
  解释：
  我们想 nums 中的最小元素可以整除 numsDivide 中的所有元素。
  没有任何办法可以达到这一目的。
  ```

* **法一：暴力加剪枝：**遍历数组nums每一个值，检测当前值能够均被numsDivide整除，复杂度O(mn)。剪枝思路，对数组进行排序，如果nums[i]==nums[i-1],nums[i-1]已经被检测过了，则nums[i]不用再处理了，也可以跳过了。

  ```java
  class Solution {
      public int minOperations(int[] nums, int[] numsDivide) {
          Arrays.sort(nums);
          int n = nums.length;
          int res= 0;
          for(int i=0;i<n;i++){
              if(i>0 && nums[i] == nums[i-1]){
                  res++;
                  continue;
              }else if(f(nums[i], numsDivide)){
                  return res;
              }else{
                  res++;
              }
          }
          return -1;
      }
      public boolean f(int x, int[] numsDivide){
          for(int i=0; i< numsDivide.length;i++){
              if(numsDivide[i] %x !=0){
                  return false;
              }
          }
          return true;
      }
  }
  ```

  

* **法二：数学**：

  * 只有 numsDivide 的最大公约数的因数才能整除 numsDivide 中的所有数。设该最大公约数为 g，

    问题变为：

    **从 nums 中删除尽量少的元素，使得 nums 中的最小值可以整除g。**

  * 若当前 nums 不满足条件，我们必须删除 nums 中的最小值。否则 nums 中的最小值一直不变，那么条件也一直不可能达成。因此我们将 nums 排序，每次删掉 nums 中第一个数，直到第一个数可以整除 g 为止。复杂度 O(nlog A + nlogn)其中 A 是 numsDivide 中的最大元素。

    ```java
    class Solution {
        public int minOperations(int[] nums, int[] numsDivide) {
            Arrays.sort(nums);
            int f = numsDivide[0];
            for(int i=1; i < numsDivide.length; i++){
                f = getMaxFactor(numsDivide[i], f);
            }
           
            int res = 0;
            for(int i=0;i<nums.length;i++){
                if(i>0 && nums[i] == nums[i-1]){
                    res++;
                    continue;
                }
                if(f%nums[i] ==0){
                    return res;
                }else{
                    res++;
                }
            }
            return -1;
        }
        public int getMaxFactor(int a, int b){
            if(a<b){
                int t = a;
                a = b;
                b = t;
            }
             int r = a;
            while(r>0){
                r = a%b;
                a = b;
                b = r;
            }
            
            return a;
        }
    }
    ```

    