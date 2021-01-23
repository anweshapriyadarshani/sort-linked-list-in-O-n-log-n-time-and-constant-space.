# sort-linked-list-in-O-n-log-n-time-and-constant-space.
Given a linked list, sort it in O(n log n) time and constant space.  For example, the linked list 4 -> 1 -> -3 -> 99 should become -3 -> 1 -> 4 -> 99.

ListNode *mergeSort(ListNode *head) {
    if(!head || !head->next) return head;
    // get middle node
    // not right if write: *fast = head. Otherwise, {2,1} will not be sorted.
    ListNode *slow = head, *fast = head->next; 
    while(fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    ListNode *left = head, *right = slow->next;
    slow->next = NULL;
    left = mergeSort(left);
    right = mergeSort(right);
    return merge(left, right);
}

ListNode *merge(ListNode *L, ListNode *R) {
    if(!L) return R;
    if(!R) return L;
    ListNode *h = NULL;
    if(L->val < R->val) {
        h = L;
        h->next = merge(L->next, R);
    } else {
        h = R;
        h->next = merge(L, R->next);
    }
    return h;
}
