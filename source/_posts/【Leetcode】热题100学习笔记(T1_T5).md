---
title: LeetCode Hot T1-T5
date: 2021-12-09 09:10:11
tags: JAVA
categories: leetcode

---



# T1 两数之和 [题目链接](https://leetcode-cn.com/problems/two-sum/)

## 法一：暴力枚举
### 思路：
#### 逐个遍历两个元素，搜索全部组合，返回满足题意的唯一解。
### 性能分析：
#### 1. 时间复杂度 O（n*n）
#### 2. 空间复杂度 O（1）


    class Solution {
    public int[] twoSum(int[] nums, int target) {
        // 暴力枚举
        int p = 0;
        int q = 0;
        int n = nums.length;
        for(p=0;p<n-1;p++){
            for (q=p+1; q<n;q++){
                if(nums[p] + nums[q] == target){
                   return new int[]{p, q};
                }
            }
        }
        return new int[0];
        return new int[0];
    }
<!--more-->

## 法二：哈希映射

### 思路：
#### 构建哈希表，满足:
>(key=nums[i],value=i)

对于nums[i],遍历nums[i], 检测target-nums[i]是否在哈希表中，如果在，返回对应的哈希值,否则，将nums[i]加入哈希表中。
### 性能分析：
#### 1. 时间复杂度 O（1）
#### 2. 空间复杂度 O（1）


    class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> hashmap = new HashMap<Integer,Integer>();
        for(int i =0;i<nums.length;i++){
            if (hashmap.containsKey(target-nums[i])){
                return new int[]{i, hashmap.get(target-nums[i])};
            }
            hashmap.put(nums[i],i);
        }
        return new int[0];
    } 
}

# T2 两数相加 [题目链接](https://leetcode-cn.com/problems/add-two-numbers/)

## 法一：加法模拟
### 思路：
#### 模拟加法即可，有几个点需要考虑全面：
>(1) 考虑清楚数据是左对齐还是右对齐。   
>(2) 考虑a,b长度不相同时的遍历。  
>(3) 考虑进位的问题，尤其是最后1位和两个列表一个结束，一个没有结束的时候
### 性能分析：
#### 1. 时间复杂度 O（max(n,m)）
#### 2. 空间复杂度 O（1）
    class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
            ListNode p1=l1;
            ListNode p2=l2;
            //统计两个链表的长度
            int len1=0;
            int len2=0;
            while(p1 !=null){
                p1=p1.next;
                len1++;
            }
            while(p2 !=null){
                p2 = p2.next;
                len2++;
            }
            //重新指向链表头部，准备模拟加法
            p1 = l1;
            p2 = l2;
            int jinwei = 0;
            //新建链表，存储结果，p3表示新建链表的尾部
            ListNode result = new ListNode();
            ListNode p3 = result;
            //遍历两个链表，逐个元素相加
            while(p1 != null && p2 != null){              
                int a = p1.val;
                int b = p2.val;
                int sum = jinwei+ a + b;
                if(sum>=10){
                    jinwei = 1;
                    sum = sum-10;
                }else{
                    jinwei = 0;
                }
                ListNode t = new ListNode(sum);
                p3.next =t;
                p3 = t;
                p1 = p1.next;
                p2 = p2.next;
            }
            //长度不等时，处理较长的链表操作。
            if (len1>len2){
                while(p1 !=null){
                    int a = p1.val;
                    int sum = jinwei+ a;
                    if(sum>=10){
                        jinwei = 1;
                        sum = sum-10;
                    }else{
                        jinwei = 0;
                    }
                    ListNode t = new ListNode(sum);
                    p3.next = t;
                    p3 = t;
                    p1 = p1.next;
                }
            }
            else if(len2 > len1){
                while(p2 !=null){
                    int a = p2.val;
                    int sum = jinwei+ a;
                    if(sum>=10){
                        jinwei = 1;
                        sum = sum-10;
                    }else{
                        jinwei = 0;
                    }
                    ListNode t = new ListNode(sum);
                    p3.next = t;
                    p3 = t;
                    p2 = p2.next;
                }
            }
            //特殊处理，最后一位的进位
            if (jinwei == 1){
                 ListNode t = new ListNode(1);
                p3.next = t;
                p3 = t;
            }
        return result.next;
    }
}

# T3 无重复字符的最长子串 [题目链接](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

## 法一：滑动窗口
### 思路：
#### 其实就是定位目标子串的start和end。如何更新start和end的过程。在讲解算法的时候，首先要明白一个原理：
>假设：start = t0， end = tk，那么，t0到tk都是不重复的。现存在一个tm（0<m<k），则tm到tk也一定是不重复的。

这样的话，end只需要沿着字符长度进行遍历，而start去寻找当出现重复字母的时候，tm的位置即可。为了更好的理解这个过程，从一个例子出发：

> 现有字符串: abcdecfge
> sart=0,end=4, 当前长度为5  
> end继续遍历，end=5，此时字符为c，字符c前面已经出现，那么start下一个值tm应是什么呢？ 理论上tm可以等于start+1，但是这并不是最优解。本例就很好的解释了这个问题。   
> 如果start=1,2 可以发现此时c还是在串子中出现两次。这两次tm的取值就是多余的。  
> 为了保证c出现一次，此时的start应该直接跳过c。即：start = c的位置 + 1

因此，整个过程应是：
>start 执行开始位置，end向下遍历
>>当end指向的字符，串中没出现的时候，end继续向下遍历
>>串中出现了的时候，把start移到tm的位置，即tm = 串中该字符位置+1  

为了实现上述过程，我们需要一个数据结构存储串中每个字符的位置，以便寻找tm。有很多种方式，比如hashmap（key=字符，value=postion）或者桶排tp[c-'a'] = postion，c表示当前字符，都可以定位其位置。 
>>注意：在start跳到tm的过程中，可能会越过多个字符，注意将这些字符在存储结构中进行更新（删除、或者标志不可用）。
### 性能分析：
#### 1. 时间复杂度 O(n)
#### 2. 空间复杂度 O（M），M表示字符集


    class Solution {
        public int lengthOfLongestSubstring(String s) {
            Map<Character,Integer> hashtable = new HashMap<Character,Integer>();
            int n =s.length();
            int max_length = 0;
            int left = 0;
            for(int right = 0; right<n;right++){
                /*两项，第一项判断是否是重复元素，第二项过滤掉存储结构中淘汰的字符即tm跳过的字符*/
                if(hashtable.containsKey(s.charAt(right))  && hashtable.get(s.charAt(right)) >= left  ){ 
                    //出现了重复元素
                    int cur_length = right -left ;
                    if(cur_length > max_length){
                        max_length = cur_length;
                    }
                    left = hashtable.get(s.charAt(right))+1;
                }else{
                int cur_length =  right -left+1;
                if(cur_length > max_length){
                        max_length = cur_length;
                    }
                }
                hashtable.put(s.charAt(right), right);
            }
            return max_length;
        }
    }


# T4 寻找两个正序数组的中位数 [题目链接](https://leetcode-cn.com/problems/median-of-two-sorted-arrays//)

## 法一：归并排序
### 思路：计算出两个数组的长度m和n，维护两个索引，分别指向两个数组的当前位置，由于提前计算出了中位数的位置，归并排序进行到中位数结束即可。
#### 注意奇数和偶数求中位数的不同。
#### 注意遍历完一个，另一个没有的情况
### 性能分析：
#### 1. 时间复杂度 O（n+n）
#### 2. 空间复杂度 O（1）
    class Solution {
        public double findMedianSortedArrays(int[] nums1, int[] nums2) {
            int len1 = nums1.length;
            int len2 = nums2.length;
            int z1 = (len1 + len2) /2;
            int z2 = (len1 + len2) %2;
            int j = 0;
            int k = 0;
            int count = 0;
            int cur = 0;
            int tmp = 0;
            if(z2 ==0){ //两个中位数
            while(j<len1 && k<len2 && count <= z1){
                if(nums1[j] <nums2[k]){
                        tmp = cur;
                        cur = nums1[j];
                        j++;
                    }else{
                        tmp = cur;
                        cur = nums2[k];
                        k++;
                    }
                    count++;
                    // System.out.println(cur);
            }
            if(count<= z1){
                if( j< len1){
                        while(j<len1 && count <=z1){
                            tmp =cur;
                            cur = nums1[j];
                            j++;
                            count++;
                        }
                }else {
                        while(k<len2 && count <=z1){
                            tmp =cur;
                            cur = nums2[k];
                            k++;
                            count++;
                        }
                }
            }
            return (tmp+cur)/2.0;
            }
            else{//一个中位数
                while(j<len1 && k<len2 && count <= z1){
                    if(nums1[j] <nums2[k]){
                        cur = nums1[j];
                        j++;
                    }else{
                        cur = nums2[k];
                        k++;
                    }
                    count++;
                }
                if(count <= z1){
                    if(len2 <len1){
                        while(j<len1 && count <=z1){
                            cur = nums1[j];
                            j++;
                            count++;
                        }
                    }else{
                        while(k<len2 && count <=z1){
                            cur = nums2[k];
                            k++;
                            count++;
                        }
                    }
                }
                return cur;
            }
            
        }
    }


## 法二：寻找第K小的数
### 思路：
#### 中位数实际上就是两个数组求第K小的数的一种特殊情况，可以用求第K小的数的方案解决。
> 一般来讲，有两个数组  
> A[1] ,A[2],A[3]...A[k/2]..A[M]....  
> B[1] ,B[2]...B[k/2]..B[N]....  
> if  A[k/2] < B[k/2]  
> 那么 A[1] 到 A[k/2]-1 都不是第K小的数字。
>>why:   
>>A数组中小于A[k/2]的有 k/2-1 个，B中小于B[K/2]的 也有有K/2-1个，如果A[k/2]<B[K/2],那么，A中的前K/2个一定小于B[K/2]，此时比 B[K/2] 共有 B[1] 到B[K/2 -1 ] 共K/2-1个 ， 以及 A[1] 到A[K/2 -1] 共 K/2-1 个，一共有K-2个。 
### 性能分析：
#### 1. 时间复杂度 O（log(m+n)）
#### 2. 空间复杂度 O（1）
    class Solution {
        public double findMedianSortedArrays(int[] nums1, int[] nums2) {
            int n = nums1.length;
            int m = nums2.length;
            int left = (n + m + 1) / 2;
            int right = (n + m + 2) / 2;
            //将偶数和奇数的情况合并，如果是奇数，会求两次同样的 k 。
            return (getKth(nums1, 0, n - 1, nums2, 0, m - 1, left) + getKth(nums1, 0, n - 1, nums2, 0, m - 1, right)) * 0.5;  
        }
            
        private int getKth(int[] nums1, int start1, int end1, int[] nums2, int start2, int end2, int k) {
            int len1 = end1 - start1 + 1;
            int len2 = end2 - start2 + 1;
            //让 len1 的长度小于 len2，这样就能保证如果有数组空了，一定是 len1 
            if (len1 > len2) return getKth(nums2, start2, end2, nums1, start1, end1, k);
            if (len1 == 0) return nums2[start2 + k - 1];
    
            if (k == 1) return Math.min(nums1[start1], nums2[start2]);
    
            int i = start1 + Math.min(len1, k / 2) - 1;
            int j = start2 + Math.min(len2, k / 2) - 1;
    
            if (nums1[i] > nums2[j]) {
                return getKth(nums1, start1, end1, nums2, j + 1, end2, k - (j - start2 + 1));
            }
            else {
                return getKth(nums1, i + 1, end1, nums2, start2, end2, k - (i - start1 + 1));
            }
        }
    }
    
    /*
    ref：https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-w-2/
    */



# T5 最长回文子串 [题目链接](https://leetcode-cn.com/problems/longest-palindromic-substring/)

## 法一：动态规划
### 思路：
#### 根据回文串的性质，若[start, end]是回文串，则[strat+1，end-1]也一定是回文串。
因此我们借助dp[start+1][end-1]是否是回文串和 s[start]，s[end]是否相等来判定dp[start][end]的值。
* 明白了上面说的这一点，那么接下来就是dp过程中，如何先从外由内更新，即先更新[start+1:end-1],在更新dp[start][end],做法也很简单，外层遍历end，内层遍历start。
* 注意边界，首先，区间[start+1:end-1]长度是0和1的时候，一定为true.
### 性能分析：
#### 1. 时间复杂度 O（n*n）
#### 2. 空间复杂度 O（n*n）
        class Solution {
        public String longestPalindrome(String s) {
            int n= s.length();
            int[][] dp = new int[n][n]; //dp[start][end] 是否是回文串 s[start]==s[end] && dp[i+1][j-1]=true 
            int max_length = 1;
            int index = 0;
            for(int i=0; i<n ;i++){
                dp[i][i] = 1; //只有一个字符的时候一定是回文串
            }
            for(int j =0; j<n;j++){
                for(int i=0;i<j;i++){
                    if(s.charAt(i) ==s.charAt(j) && ( i+1>j-1 ||dp[i+1][j-1] ==1)){
                        dp[i][j] = 1;
                        if(j-i+1 >max_length){
                            max_length = j-i+1;
                            index = i;
                        }
                    }
                }
            }
            return s.substring(index,index+max_length);
        }
    }

## 法二：中心拓展
#### 思路：回文串是一种由中间向外拓展的特殊串形式。换个说法也就是去找回文串的中心，对于某一字符串来说每个字符都可以为其中心，有n种，同时，字符间隔也可以是回文串的中心，例如，回文串： abccba， 因此，对于某一字符串，其一共有 2n-1个串中心。
### 性能分析：
#### 1. 时间复杂度 O（n*n）
#### 2. 空间复杂度 O（1）
因此，我只需要遍历中心节点，找到最优的即可。
    
    class Solution {
        public String longestPalindrome(String s) {
            int n= s.length();
            int max_length = 1;
            int index = 0;
    
            for(int i=0;i<n;i++){
                //node = i
                int pre   = i-1;
                int later = i+1;
                while(pre >=0 && later <n && s.charAt(pre)==s.charAt(later)){
                    pre--;
                    later++;
                }
                int cur_length = later-pre-1;
                if(cur_length > max_length){
                    max_length = cur_length;
                    index = pre+1;
                }
                //node = between(i,i+1)
                pre   = i;
                later = i+1;
                while(pre >=0 && later <n && s.charAt(pre)==s.charAt(later)){
                    pre--;
                    later++;
                }
                cur_length = later-pre-1;
                if(cur_length > max_length){
                    max_length = cur_length;
                    index = pre+1;
                }
            }
            return s.substring(index,index+max_length);
        }
    }
