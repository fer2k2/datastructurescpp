# Strings and Arrays
### Iterators

#### Forward iterator loop
```c++
for (auto it = s.begin(); it != s.end(); ++it)
{
    std::cout << *it;
}
```
#### Forward iterator loop
```c++
for (auto it = s.rbegin(); it != s.rend(); ++it)
{
    std::cout << *it;
}
```

### Algorithms
#### Reverse
```c++
std::reverse(s.begin(), s.end());
```
#### Sort (min to max)
```c++
std::sort(s.begin(), s.end());
```
#### Sort (max to min)
```c++
std::sort(s.begin(), s.end(), std::greater<int>());
```
#### Get max element
```c++
std::cout << *max_element(s.begin(), s.end());
```
#### Get min element
```c++
std::cout << *min_element(s.begin(), s.end());
```
#### Sum
```c++
int sum = std::accumulate(v.begin(), v.end(), 0);
```
#### Count


#### Find


#### Binary search


#### Erase

#### Unique

#### Distance

# Sets and maps

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
    SinglyLinkedListNode* curr = head;

    // Move pointer until we reach the end of the list
    while (curr->next != NULL)
    {
        // Asigning to the pointer doesn't affect original list since only moves what are pointing to
        curr = curr->next;
    }
    
    // Point the last node to a new node
    // since the helper pointer point to the last node, it's correct to use ->next
    // that will affect to last node as if we were using it directly
    curr->next = new SinglyLinkedListNode(data);

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
    
    // Create helper node
    SinglyLinkedListNode* curr = head;
    
    // Parse the list
    int iPos = 0;
    while (curr != nullptr)
    {
        // If found the position
        if (iPos == (position - 1) )
        {
            // New node will point to the next node
            pNewNode->next = curr->next;
            // Current node to the new node
            curr->next = pNewNode;
        }
        
        curr = curr->next;
        iPos++;
    }


    return head;
}
```

### Cycle Detection

```c++
bool has_cycle(SinglyLinkedListNode* head) {

    // If head is null just return false
    if (head == nullptr)
        return false;


    // Set two helper pointers one in the head and one ahead one position
    SinglyLinkedListNode* pSlow = head;
    SinglyLinkedListNode* pFast = head->next;

    // Check null pointers for safety
    while(pFast != nullptr && pFast->next != nullptr)
    {
        // If pointers match, then there is a cycle
        if(pFast == pSlow)
            return true;

        // Advance pointers
        pSlow = pSlow->next;
        pFast = pFast->next->next;
    }

    // If anyone is poining to null then it doesn't contains a cycle
    return false;
}
```
