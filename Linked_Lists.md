# Linked Lists

+ [Reorder List](#reorder_list)
+ [Linked List Cycle II](#linked_list_cycle_2)
+ [Linked List Cycle](#linked_list_cycle)
+ [Merge Two Sorted Lists](#merge_two_sorted_lists)
+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Delete Node in a Linked List](#delete-node-in-a-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Reverse Linked List](#reverse-linked-list)
+ [Remove Linked List Elements](#remove-linked-list-elements)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Sort List](#sort-list)

## Reorder List

https://leetcode.com/problems/reorder-list/

```cpp
class Solution {
public:
    public:
    ListNode* middleNode(ListNode* head) {
        ListNode* middle = head;
        while(head->next){
            middle = middle->next;
            head = head->next;
            if(head->next)
                head = head->next;
        }
        return middle;
    }
    ListNode* reverseList(ListNode* head) {
        ListNode* temp;
        ListNode* prev = NULL;
        while(head){
            temp = head->next;
            head->next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
    void reorderList(ListNode* head) {
        if(!head || !head->next)
            return;
        ListNode* mid = middleNode(head);
        ListNode* rev = reverseList(mid);
        ListNode* temp;
        while(head->next){
            temp = head->next;
            head->next = rev;
            if(rev)
                rev = rev->next;
            head = head->next;
            if(head)
                head->next = temp;
            head = temp;
        }
    }
};
```
## Linked List Cycle II

https://leetcode.com/problems/linked-list-cycle-ii/submissions/

```cpp
class Solution {
public:
     ListNode *detectCycle(ListNode *head) {
        if(!head)
            return NULL;
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast){
            slow = slow->next;
            fast = fast->next;
            if(!fast)
                break;
            fast = fast->next;
            if(fast == slow)
                break;
        }
        if(!fast){
            return NULL;
        }
        fast = head;
        while(fast != slow){
            fast = fast->next;
            slow = slow->next;
        }
        return fast;   
    }
};
```
## Linked List Cycle

https://leetcode.com/problems/linked-list-cycle/submissions/

```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head)
            return NULL;
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast){
            slow = slow->next;
            fast = fast->next;
            if(!fast)
                break;
            fast = fast->next;
            if(fast == slow)
                break;
        }
        return fast != NULL;
    }
};
```
## Merge Two Sorted Lists

https://leetcode.com/problems/merge-two-sorted-lists/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1)
            return l2;
        if(!l2)
            return l1;
        ListNode* head;
        ListNode* start = l1->val > l2->val ? l2 : l1;
        if(start == l1)
                l1 = l1->next;
            else
                l2 = l2->next;
        head = start;
        while(l1 && l2){
            head->next = l1->val > l2->val ? l2 : l1;
            if(head->next == l1)
                l1 = l1->next;
            else
                l2 = l2->next;
            head = head->next;
        }
        head->next = l1? l1 : l2;
        return start;
        }
};
```
## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* temp = head;
        ListNode* N_elem = head;
        ListNode* N_elem_prev = NULL;
        int size = 1;
        while(temp->next){
            if(size - n >= 0){
                N_elem_prev = N_elem;
                N_elem = N_elem->next;
            }
            size++; 
            temp = temp->next;
        }
        if(N_elem_prev){
            N_elem_prev->next = N_elem->next;
        }
        if(N_elem == head)
            head = N_elem->next;
        delete(N_elem);
        return head;    
    }
};
```

## Middle of the Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

```cpp
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* middle = head;
        while(head->next){
            middle = middle->next;
            head = head->next;
            if(head->next)
                head = head->next;
        }
        return middle;
    }
};
```

## Delete Node in a Linked List

https://leetcode.com/problems/delete-node-in-a-linked-list/

```cpp
class Solution {
public:
    void deleteNode(ListNode* node) {
        ListNode* temp = node->next;
        node->val = temp->val;
        node->next = temp->next;
        delete(temp);
    }
};
```

## Palindrome Linked List

https://leetcode.com/problems/palindrome-linked-list/

```cpp
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* middle = head;
        while(head->next){
            middle = middle->next;
            head = head->next;
            if(head->next)
                head = head->next;
        }
        return middle;
    }
    ListNode* reverseList(ListNode* head) {
        ListNode* temp;
        ListNode* prev = NULL;
        while(head){
            temp = head->next;
            head->next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
    bool isPalindrome(ListNode* head) {
        if(!head || !head->next)
            return true;
        ListNode* mid = middleNode(head);
        ListNode* rev = reverseList(mid);
        ListNode* list = head;
        while(list != mid){
            if(list->val != rev->val)
                return false;
            list = list->next;
            rev = rev->next;
        }
        return true;
    }
};
```
##  Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* temp;
        ListNode* prev = NULL;
        while(head){
            temp = head->next;
            head->next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
};
```
## Remove Linked List Elements

https://leetcode.com/problems/remove-linked-list-elements/

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* list = head;
        ListNode* prev = NULL;
        while(list->val == val){
            head = list->next;
            delete(list);
            list = head;
        }
        while(list){
            if(list->val == val){
                prev->next = list->next;
                delete(list);
                list = prev->next;
            }
            prev = list;
            list = list->next;
        }
        return head;
    }
};
```
## Intersection of Two Linked Lists

https://leetcode.com/problems/intersection-of-two-linked-lists/

```cpp
class Solution {
public:
    int getLen(ListNode *head){
        int i = 0;
        while(head){
            i++;
            head = head->next;
        }
        return i;
    }
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(!headA || !headA)
            return NULL;
        int delta = getLen(headA) - getLen(headB);
        ListNode* min = delta > 0 ? headB : headA;
        ListNode* max = delta <= 0 ? headB : headA;
        delta = abs(delta);
        while(delta){
                max = max->next;
                delta--;
            }
        while(max && max != min){
            max = max->next;
            min = min->next;
        }
        return max;
    }
};
```
## Sort List

https://leetcode.com/problems/sort-list/

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1)
            return l2;
        if(!l2)
            return l1;
        ListNode* head;
        ListNode* start = l1->val > l2->val ? l2 : l1;
        if(start == l1)
                l1 = l1->next;
            else
                l2 = l2->next;
        head = start;
        while(l1 && l2){
            head->next = l1->val > l2->val ? l2 : l1;
            if(head->next == l1)
                l1 = l1->next;
            else
                l2 = l2->next;
            head = head->next;
        }
        head->next = l1? l1 : l2;
        return start;
        }
    public:
    ListNode* middleNode(ListNode* head) {
        ListNode* middle = head;
        ListNode* prev;
        while(head->next){
            prev = middle;
            middle = middle->next;
            head = head->next;
            if(head->next)
                head = head->next;
        }
        prev->next = NULL;
        return middle;
    }
    ListNode* sortList(ListNode* head) {
        if(!head || !head->next)
            return head;
        return mergeTwoLists(sortList(head), sortList(middleNode(head)));
    }
};
```
