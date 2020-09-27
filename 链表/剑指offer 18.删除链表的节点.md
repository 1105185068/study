# 剑指offer 18.删除链表的节点
## 问题描述
给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

**注意**:此题对比原题有改动

**示例 1:**
```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```
**示例 2:**
```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

**说明：**

+ 题目保证链表中节点的值互不相同
+ 若使用 C 或 C++ 语言，你不需要 ```free``` 或 ```delete``` 被删除的节点

## 问题分析
+ 先考虑是否删除头结点，如果删除头结点，则直接返回return头结点的next域所指向的后面的链表。
+ 若不删除头结点，则从头结点的下一个节点一直找，知道找到要删除的节点的前一个节点，让p->next=要删除的节点。

## 代码示例
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* deleteNode(struct ListNode* head, int val){
    struct ListNode* p;
    if(head->val==val){
        return head->next;
    }
    for(p=head;p->next!=NULL&&p->next->val!=val;p=p->next){
    };
    struct ListNode* t=p->next;
    if(p->next!=NULL){
    p->next=t->next;
    free(t);
    }
    return head;
}
```
