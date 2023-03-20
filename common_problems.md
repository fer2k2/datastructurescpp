# Common problems

## Two pointers

#### Valid palindrome
Write a function that takes a string s as input and checks whether it’s a palindrome or not.
```c++
bool IsPalindrome(string inputString)
{
    int left = 0;
    int right = inputString.size() - 1;

    while (left < right)
    {

        if (inputString.at(left) != inputString.at(right))
        {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

#### Sum of two

#### Sum of three values
Given an array of integers, nums, and an integer value, target, determine if there are any three integers in nums whose sum equals the target. Return TRUE if three such integers are found in the array. Otherwise, return FALSE.
```c++
bool FindSumOfThree(std::vector<int> nums, int target)
{
    // Sorting the input vector
    std::sort(nums.begin(), nums.end());
    // Fix one element at a time and find the other two
    for (int i = 0; i < (nums.size() - 2); i++)
    {
        // Set the indices of the two pointers
        // Index of the first of the remaining elements
        int low = i + 1;
        // Last index
        int high = nums.size() - 1;
        while (low < high)
        {
            // Check if the sum of the triple is equal to the sum
            int triple = nums[i] + nums[low] + nums[high];
            // Found a triple whose sum equals the target
            if (triple == target)
                return true;
            // Move low pointer forward if the triple sum is less
            // than the required sum
            else if (triple < target)
                low += 1;
            // Move the high pointer backwards if the triple
            // sum is greater than the required sum
            else
                high -= 1;
        }
    }
    return false;
}
```

## Fast and slow pointer

#### Happy number
```c++
bool IsHappyNumber(int n){

    int slow = n;
    int fast = SumDigits(n);

    while (fast != 1 && fast != slow)
    {
        slow = SumDigits(slow);
        fast = SumDigits(SumDigits(fast));
    }

    if (fast == 1)
    {
        return true;
    }

    return false;
}

int SumDigits(int number)
{
    int totalSum = 0;
    while (number > 0)
    {
        int digit = number % 10;
        number = std::floor(number / 10);
        totalSum += digit * digit;
    }
    return totalSum;
}
```

## Sliding window

## Linked List

#### Insert node at the end of a list

```c++
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

#### Insert node at n position of a list

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

#### Reverse list
```c++
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;

    while(curr != nullptr)
    {
        // Save temp
        ListNode* nextTemp = curr->next;

        // Point current node next to previous node
        curr->next = prev;
        // Prev now points to current completing the reverse
        prev = curr;

        // new current is the next node
        curr = nextTemp;
    }

    // return the first node on the reversed list;
    return prev;
}
```

#### Detect cycle
```c++
bool DetectCycle(EduLinkedListNode* head){

  if (head == nullptr)
  {
    return false;
  }

  EduLinkedListNode* pSlow = head;
  EduLinkedListNode* pFast = head;

  while(pFast->next && pFast) // while there are no nulls
  {
    pSlow = pSlow->next;
    pFast = pFast->next->next;

    if (!pFast)
    {
      return false;
    }

    if(pSlow == pFast)  
    {
      return true;
    }
  }

  return false;
}
```

## Stack

## Trees

### Tree traversal
#### In order
```c++
void InOrder(Node* root)
{
    if (root != NULL)
    {
        InOrder(root->left);
        std::cout << root->data << " ";
        InOrder(root->right);
    }
}
```
#### Pre order
```c++
void PreOrder(Node* root)
{
    if (root != NULL)
    {
        std::cout << root->data << " ";
        InOrder(root->left);
        InOrder(root->right);
    }
}
```
#### Post order
```c++
void PostOrder(Node* root)
{
    if (root != NULL)
    {
        InOrder(root->left);
        InOrder(root->right);
        std::cout << root->data << " ";
    }
}
```
#### Level order
```c++
vector<int> levelOrder(Node* node)
{
  vector<int> result;

  queue<Node*> q;

  q.push(node);


  while (!q.empty())
  {

      Node* current = q.front();
      q.pop();
      if (current != NULL)
      {
          result.push_back(current->data);
          q.push(current->left);
          q.push(current->right);
      }
  }

  return result;
}
```

#### Lowest common ansestor
```c++
/* Function to find LCA of n1 and n2.
The function assumes that both
n1 and n2 are present in BST */
node* lca(node* root, int n1, int n2)
{
    if (root == NULL) return NULL;

    // If both n1 and n2 are smaller
    // than root, then LCA lies in left 
    if (root->data > n1 && root->data > n2)
        return lca(root->left, n1, n2);

    // If both n1 and n2 are greater than 
    // root, then LCA lies in right 
    if (root->data < n1 && root->data < n2)
        return lca(root->right, n1, n2);

    // Base case, if current node is between the nodes' values
    return root;
}
```

## BSTs

## Binary Search