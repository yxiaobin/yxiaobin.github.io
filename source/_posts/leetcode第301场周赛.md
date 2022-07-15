---
title: leetcode第301场周赛
date: 2022-07-10 14:51:37
tags: JAVA
categories: leetcode
---

# <center>leetcode 周赛 301</center>

前段时间周日上午需要参加组会，没时间参加周赛，最近暑假了有时间参加了，纪念第一次三题。

* ## [装满杯子需要的最短总时长](https://leetcode.cn/problems/minimum-amount-of-time-to-fill-cups/)

  *  **问题描述** 现有一台饮水机，可以制备冷水、温水和热水。每秒钟，可以装满 2 杯 不同 类型的水或者 1 杯任意类型的水。

    给你一个下标从 0 开始、长度为 3 的整数数组 amount ，其中 amount[0]、amount[1] 和 amount[2] 分别表示需要装满冷水、温水和热水的杯子数量。返回装满所有杯子所需的 最少 秒数。

    <!-- more -->

  * **测试样例** 

    输入：amount = [1,4,2]
    输出：4
    解释：下面给出一种方案：
    第 1 秒：装满一杯冷水和一杯温水。
    第 2 秒：装满一杯温水和一杯热水。
    第 3 秒：装满一杯温水和一杯热水。
    第 4 秒：装满一杯温水。
    可以证明最少需要 4 秒才能装满所有杯子。

  * `amount.length == 3`    `0 <= amount[i] <= 100`

  * **方一:模拟**

    ```java
    /*数据的最大值是100，最大的复杂度是1,000,000.因此字符模拟也是能过这一道题的。
       数组排序 -》 
       取数组中最大的前两个数，都进行amount[i]--操作，且计数变量res++操作-》
       当数组中出现两个0的时候循环结束 
    */ 
    class Solution {
        public int fillCups(int[] a) {
            int res = 0;
            while(true){
                Arrays.sort(a);
                int x = a[2];
                int y = a[1];
                int z=  a[0];
                if(x==0){
                    break;
                }
                if(y==0){
                    res +=x;
                    break;
                }else{
                    a[2]--;
                    a[1]--;
                    res++;
                }
            }
            return res;
        }
    }
    ```

    

  * **方二：数学**

    

    ```java
    	/*为了装水市场最少，每次尽可能的装两杯才能使得总时长最少，假设3种类型的数量分别是a,b,c，且a>=b>=c
    如果 满足 a>=b+c,则需在倒a的时候，顺带倒一杯b或者c，当b，c全部为空的时候，只倒a，此时共计需要时长为a。
    如果 有   a<b+c 的时候，则a是附带着到的那一种，设（b+c）和 a 的差为t。要想总时长最小，则a全部作为附带品被消耗，
    而，他们的差t，最后在b中占t/2，在c中占t/2. 此时只需要消耗a+t/2即可。注意此时t为奇数的情况。
    */
    class Solution {
        public int fillCups(int[] a) {
            Arrays.sort(a);
            int x = a[2];
            int y = a[1];
            int z=  a[0];
            if(x >= y + z) return x;
            else{
                int t = (y + z) - x; 
                return x + t/2 + t%2;
            } 
    
        }
    }	
    ```

* ## [无限集中的最小数字](https://leetcode.cn/problems/smallest-number-in-infinite-set/)

  * **问题描述**：现有一个包含所有正整数的集合 [1, 2, 3, 4, 5, ...] 。

    实现 SmallestInfiniteSet 类：

    现有一个包含所有正整数的集合 [1, 2, 3, 4, 5, ...] 。

    实现 SmallestInfiniteSet 类：

    SmallestInfiniteSet() 初始化 SmallestInfiniteSet 对象以包含 所有 正整数。
    int popSmallest() 移除 并返回该无限集中的最小整数。
    void addBack(int num) 如果正整数 num 不 存在于无限集中，则将一个 num 添加 到该无限集中。

    来源：力扣（LeetCode）
    链接：https://leetcode.cn/problems/smallest-number-in-infinite-set
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

  * **实例**：输入
    ["SmallestInfiniteSet", "addBack", "popSmallest", "popSmallest", "popSmallest", "addBack", "popSmallest", "popSmallest", "popSmallest"]
    [[], [2], [], [], [], [1], [], [], []]
    输出
    [null, null, 1, 2, 3, null, 1, 4, 5]

    解释
    SmallestInfiniteSet smallestInfiniteSet = new SmallestInfiniteSet();
    smallestInfiniteSet.addBack(2);    // 2 已经在集合中，所以不做任何变更。
    smallestInfiniteSet.popSmallest(); // 返回 1 ，因为 1 是最小的整数，并将其从集合中移除。
    smallestInfiniteSet.popSmallest(); // 返回 2 ，并将其从集合中移除。
    smallestInfiniteSet.popSmallest(); // 返回 3 ，并将其从集合中移除。
    smallestInfiniteSet.addBack(1);    // 将 1 添加到该集合中。
    smallestInfiniteSet.popSmallest(); // 返回 1 ，因为 1 在上一步中被添加到集合中， 且 1 是最小的整数，并将其从集合中移除。
    smallestInfiniteSet.popSmallest(); // 返回 4 ，并将其从集合中移除。
    smallestInfiniteSet.popSmallest(); // 返回 5 ，并将其从集合中移除。

  * **模拟**

    ```java
    /* 用一个Set维护列表里面的数据，用一个最小堆存储最小值即可 */
    class SmallestInfiniteSet {
        PriorityQueue<Integer> minheap;
        Set<Integer> set ;
        public SmallestInfiniteSet() {
            minheap = new PriorityQueue<>();
             set = new HashSet<>();
            for(int i=1;i<=1000;i++){
                set.add(i);
                minheap.add(i);
            }
           
        }
        
        public int popSmallest() {
            int t = minheap.poll();
            set.remove(t);
            return t;
        }
        
        public void addBack(int num) {
            if(!set.contains(num)){
                set.add(num);
                minheap.add(num);
            }
        }
    }
    ```

* ## [移动片段得到字符串](https://leetcode.cn/problems/move-pieces-to-obtain-a-string/)

  * **描述**给你两个字符串 start 和 target ，长度均为 n 。每个字符串 仅 由字符 'L'、'R' 和 '_' 组成，其中：

    字符 'L' 和 'R' 表示片段，其中片段 'L' 只有在其左侧直接存在一个 空位 时才能向 左 移动，而片段 'R' 只有在其右侧直接存在一个 空位 时才能向 右 移动。
    字符 '_' 表示可以被 任意 'L' 或 'R' 片段占据的空位。
    如果在移动字符串 start 中的片段任意次之后可以得到字符串 target ，返回 true ；否则，返回 false 。

    

  * **样例1**   输入：start = "_L__R__R_", target = "L______RR"
    输出：true
    解释：可以从字符串 start 获得 target ，需要进行下面的移动：

    - 将第一个片段向左移动一步，字符串现在变为 "L___R__R_" 。
    - 将最后一个片段向右移动一步，字符串现在变为 "L___R___R" 。
    - 将第二个片段向右移动散步，字符串现在变为 "L______RR" 。
    可以从字符串 start 得到 target ，所以返回 true 。

    

  * **样例2**  输入：start = "R_L_", target = "__LR"
    输出：false
    解释：字符串 start 中的 'R' 片段可以向右移动一步得到 "_RL_" 。
    但是，在这一步之后，不存在可以移动的片段，所以无法从字符串 start 得到 target 。

  * **样例3 ** 输入：start = "_R", target = "R_"
    输出：false
    解释：字符串 start 中的片段只能向右移动，所以无法从字符串 start 得到 target 。

  * **思路：**

    ```java
    	/*start 和 target 字符中的LR相对顺序肯定是不变的，这是保证能匹配的前提，如果相对顺序发生改变，则一定不能匹配*/
    	/*L是可以向左移动的，R是可以向有移动的，假如在i处，start为_，而target是R，则需要看在start的[0,i-1]中是否有多余的R移动到i处 */
    	/*对于i处，start为_，而target是L也是同理的，只不过需要看[i+1,n-1]中否有足够的L来完成这件事 */
    	/*因此采取两边便利的思路，从0到N遍历来匹配R，从N到0便利来匹配L，如果都匹配上了则表示正确。 */
    	
    	class Solution {
        public boolean canChange(String start, String target) {
            StringBuilder sb1 = new StringBuilder();
            StringBuilder sb2 = new StringBuilder();
             for(int i=0; i<start.length();i++){
                char ch1 = start.charAt(i);
                char ch2 = target.charAt(i);
                if(ch1 !='_'){
                    sb1.append(ch1);
                }
                 if(ch2 !='_'){
                    sb2.append(ch2);
                }
             }
            boolean tag = sb1.toString().equals(sb2.toString());
            if(!tag) return false;
            
            
            int Rnum = 0;
            for(int i=0; i<start.length();i++){
                char ch1 = start.charAt(i);
                char ch2 = target.charAt(i);
                if(ch1 =='R'){
                    Rnum++;               
                }
                if (ch1 == ch2){
                    if(ch1 =='R')
                        Rnum--;
                    continue;
                }else{
                    if(ch1 =='_' && ch2=='R'){
                        if(Rnum<=0){
                            return false;
                        }else{
                            Rnum--;
                        }
                    }
                }
                
            }
            
            int Lnum = 0;
            for(int i=start.length()-1; i>=0;i--){
                char ch1 = start.charAt(i);
                char ch2 = target.charAt(i);
                if(ch1 =='L'){
                    Lnum++;               
                }
                if (ch1 == ch2){
                     if(ch1 =='L')
                        Lnum--;
                    continue;
                }else{
                    if(ch1 =='_' && ch2=='L'){
                        if(Lnum<=0){
                            return false;
                        }else{
                            Lnum--;
                        }
                    }
                }
                
            }
            
            return true;
        }
    }
    
    ```

    