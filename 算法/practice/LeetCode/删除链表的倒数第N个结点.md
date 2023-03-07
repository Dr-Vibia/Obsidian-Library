给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

**示例 1：**

输入：head = [1,2,3,4,5], n = 2
输出：1,2,3,5]

**示例 2：**

输入：head = [1], n = 1
输出：[]

**示例 3：**

输入：head = [1,2], n = 1
输出：[1]

双指针法：构造虚拟头结点dummy（避免讨论）

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0, head);
        ListNode* first = head;
        ListNode* second = dummy;
        for (int i = 0; i < n; ++i) {
            first = first->next;
        }
        while (first) {
            first = first->next;
            second = second->next;
        }
        second->next = second->next->next;
        ListNode* ans = dummy->next;
        delete dummy;
        return ans;
    }
};
```
