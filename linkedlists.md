# Linked Lists

## Singly-Linked List

```c++
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};
```
or

```c++
struct SinglyLinkedListNode {
    int data;
    SinglyLinkedListNode* next;
 };
```

### Insert node at the end of a list

```c++
/*
 * For your reference:
 *
 * SinglyLinkedListNode {
 *     int data;
 *     SinglyLinkedListNode* next;
 * };
 *
 */
SinglyLinkedListNode* insertNodeAtTail(SinglyLinkedListNode* head, int data) {
    // Special case, if head is NULL
    if (head == NULL)
    {
        head = new SinglyLinkedListNode(data);
        head->next = NULL;
        return head;
    }

    // Temporary pointer on the stack pointing to head
    SinglyLinkedListNode* l = head;

    // Move pointer until we reach the end of the list
    while (l->next != NULL)
    {
        // Asigning to the pointer doesn't affect original list since only moves what are pointing to
        l = l->next;
    }
    
    // Point the last node to a new node
    // since the helper pointer point to the last node, it's correct to use ->next
    // that will affect to last node as if we were using it directly
    l->next = new SinglyLinkedListNode(data);

    // Return the head
    return head;
}
```

### Insert node at n position of a list

```c++
SinglyLinkedListNode* insertNodeAtPosition(SinglyLinkedListNode* head, int data, int position) {

    SinglyLinkedListNode* pNewNode = new SinglyLinkedListNode(data);
    pNewNode->next = nullptr;

    if (head == nullptr)
        return pNewNode;

    if (position == 0)
    {
        pNewNode->next = head;
        return pNewNode;
    }

    SinglyLinkedListNode* pNode = head;
    int iPos = 0;
    while (pNode != nullptr)
    {
        if (iPos == (position - 1) )
        {
            pNewNode->next = pNode->next;
            pNode->next = pNewNode;
        }

        pNode = pNode->next;
        iPos++;
    }


    return head;
}
```

### Cycle Detection

```c++
bool has_cycle(SinglyLinkedListNode* head) {

    if (head == nullptr)
        return false;

    SinglyLinkedListNode* pSlow = head;
    SinglyLinkedListNode* pFast = head->next;

    while(pFast != nullptr && pFast->next != nullptr)
    {
        if(pFast == pSlow)
            return true;

        pSlow = pSlow->next;
        pFast = pFast->next->next;
    }

    return false;
}
```
