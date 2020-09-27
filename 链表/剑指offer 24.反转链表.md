# 剑指offer 24.反转链表
## 问题描述
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

**示例:**
```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

**限制：**

```0 <= 节点个数 <= 5000```

**注意**：本题与主站 206 题相同：<https://leetcode-cn.com/problems/reverse-linked-list/>

## 解题思路
**将工作指针p作为head->next,之后将head->next域置为空，如果p不为空,让q=p->next,p-next域指向头结点head,达到反转链表的功能,再将头结点每次往后移一个到p,p往后移一个移到q。**

## 代码示例
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* reverseList(struct ListNode* head){
    if( head == NULL ){
        return head;
    }
    struct ListNode* p;
    p=head->next;
    head->next=0;
    while(p){
        struct ListNode* q;
        q=p->next;
        p->next=head;
        head=p;
        p=q;
    }
    return head;
}
```

链接：https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/solution/c-shi-jian-fu-za-du-on-kong-jian-fu-za-du-o1-by-bi/

来源：力扣（LeetCode）
