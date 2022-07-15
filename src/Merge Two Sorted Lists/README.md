# Merge Two Sorted List

## Question:

Merge two sorted linked lists and return it as a sorted list. The list
should be made by splicing together the nodes of the first two lists.

## How to Solve:

Create an empty answer list. As long as list1 and list2 are not both exhausted (`while (l1 && l2)`), at each iteration
we append smaller-valued node after our eventual answer list, before
advancing either list1 or list2 to the "next" node for our next
iteration's comparison.

After the main while loop, we check if there are leftovers from list1
or list2, then loop through the leftover list and append them to our
answer list.

Return the answer list.

Note: It may be easier to create the answer list with a dummy head,
and in the end return `dummy.next` as the "actual head". Just a
convenience of implementation detail.

## My C++ Solution:

```cpp
class Solution {
 public:
  ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
    auto sentinel = make_unique<ListNode>(0);
    auto curr = sentinel.get();
    while (l1 && l2) {
      if (l1->val < l2->val) {
        curr->next = l1;
        l1 = l1->next;
      } else {
        curr->next = l2;
        l2 = l2->next;
      }
      curr = curr->next;
    }
    if (l1) {
      curr->next = l1;
    } else if (l2) {
      curr->next = l2;
    }
    return sentinel->next;
  }
};
```