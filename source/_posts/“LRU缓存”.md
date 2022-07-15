---
title: LRU缓存
date: 2022-07-12 16:51:28
tags: LRU
categories: leetcode
---

* ## [LRU 缓存](https://leetcode.cn/problems/lru-cache/)

  * 请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。
    实现 LRUCache 类：

    * LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存

    * int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。

    * void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。

    * 函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

      <!-- more -->

  * 输入
    ["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
    [[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
    输出
    [null, null, null, 1, null, -1, null, -1, 3, 4]

    解释
    LRUCache lRUCache = new LRUCache(2);
    lRUCache.put(1, 1); // 缓存是 {1=1}
    lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
    lRUCache.get(1);    // 返回 1
    lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
    lRUCache.get(2);    // 返回 -1 (未找到)
    lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
    lRUCache.get(1);    // 返回 -1 (未找到)
    lRUCache.get(3);    // 返回 3
    lRUCache.get(4);    // 返回 4

  * **思路：**

    * LRU每次淘汰最久不使用的，用队列模拟可以嘛，如果又一个队列[2,3,4]下次访问3需要把3从队列取出来放到最后面使队列变成[2,4,3]这个操作不是O(1)
    * map 很容易到达O(1), 我们可以使用HashMap存取(key,index)这样就定位到index位置，删除掉这个，再最后添加一个，数组的话需要移动，也不是O(1)， 那么只能用链表了。
    * 链表删除的话，需要知道前一个节点，如果从头遍历到前一个节点操作还不是O(1)的，因此考虑用双向链表。当前节点的pre的next 指向当前节点的next节点即可完成删除操作，这是O(1)的。
    * 理清了数据结构接下来就是模拟了。

    ```java
    class LRUCache {
        Node head , tail ;
        int nodeCapacity = 0;
        Map<Integer, Node> map = new HashMap<>();
        public LRUCache(int capacity) {
            head = new Node();
            nodeCapacity = capacity;
            tail = head;
        }
        
        public int get(int key) {
            Node ans = map.get(key);
            if(ans == null){
                return -1;
            }else{
                //删除当前节点，把该节点新添加到尾部，注意当前节点本身就是尾节点的时候
                //删除
                Node tmpPre = ans.pre;
                Node tmpNext = ans.next;
                tmpPre.next = tmpNext;
                if(tmpNext != null)
                    tmpNext.pre = tmpPre;
                if(tail == ans){
                    tail = tmpPre;
                }
                //新添
                Node t2 = new Node();
                t2.val = ans.val;
                t2.key = ans.key;
                t2.pre = tail;
                tail.next = t2;
                tail = t2;
                map.put(key,t2);
               
                return ans.val;
            }
        }
        
        public void put(int key, int value) {
            boolean include = map.containsKey(key); 
            if(include){
                //双向链表里面存在该节点需要删除，考虑本身是尾节点的时候
                Node tmp = map.get(key);
                Node tmpPre = tmp.pre;
                Node tmpNext = tmp.next;
                tmpPre.next = tmpNext;
                if(tmpNext != null)
                tmpNext.pre = tmpPre;
                if(tail == tmp){
                    tail = tmpPre;
                }
            }
            //将新值封装成节点并且插入到链表表尾
            Node t2 = new Node();
            t2.val = value;
            t2.key = key;
            t2.pre = tail;
            tail.next = t2;
            tail = t2;
            map.put(key,t2);
            //超过最大容量需要删除头节点
            if(!include && map.size() > nodeCapacity){
                Node t = head.next;
                head.next =t.next;
                t.next.pre = head;
                map.remove(t.key);
            }
        }
        
    }
    
    class Node{
        int key;
        int val;
        Node pre;
        Node next;
    }
    
    ```

    

  * **LinkedHashMap：**    LinkedHashMap，是使得Key保证了顺序的HashMap，其底层就是双向链表实现的，可以使用lInkedHashMap轻松实现这个功能

    ```java
    class LRUCache {
        HashMap<Integer, Integer> map;
        int lruCapacity;
        public LRUCache(int capacity) {
            map = new LinkedHashMap<>();
            lruCapacity = capacity;
        }
        
        public int get(int key) {
            Integer res = map.get(key);
            if(res == null){
                return -1;
            }else{
                map.remove(key);
                map.put(key,res);
                return res;
            }
        }
        
        public void put(int key, int value) {
            if(map.containsKey(key)){
                map.remove(key);
            }
            map.put(key,value);
            if(map.size() > lruCapacity){
                for(int key0: map.keySet()){
                    map.remove(key0);
                    break;
                }
            }
        }
    }
    
    ```

    

