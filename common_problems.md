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
Write an algorithm to determine if a number nn is happy.

A happy number is a number defined by the following process:

    - Starting with any positive integer, replace the number by the sum of the squares of its digits.
    - Repeat the process until the number equals 11 (where it will stay), or it loops endlessly in a cycle which does not include 11.
    - Those numbers for which this process ends in 11 are happy.

Return TRUE if nn is a happy number, and FALSE if not.
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

#### Find maximum in sliding window
Given an integer array nums and a window of size w, find the current maximum value in the window as it slides through the entire array.
```c++
std::vector<int> FindMaxSlidingWindow(std::vector<int> &nums, int windowSize)
{
    std::vector<int> result;
    // Initializing doubly ended queue for storing indices
    std::deque<int> window;
    
    // If windowSize is greater than the array size,
    // set the windowSize to nums.size()
    if (windowSize > nums.size())
    {
        windowSize = nums.size();
    }

    // this variable is for the sole purpose of printing
    bool check = false;

    // Find out first maximum in the first window
    std::cout << "Traversing to find maximum in the first window:" << std::endl;
    for (int i = 0; i < windowSize; ++i)
    {
        // For every element, remove the previous smaller elements from window
        while (!window.empty() && nums[i] >= nums[window.back()])
        {
            std::cout << "\t\tnums[" << i << "] = " << nums[i]
                      << " is greater than or equal to nums[window[-1]] = " << nums[window.back()] << std::endl;
            check = true;
            window.pop_back();
            std::cout << "\t\tWindow after popping: " << PrintD(window) << std::endl;
        }
        // this is only for the purpose of printing
        if (!check){
            if (!window.empty())
                std::cout << "\t\tnums[" << i << "] = " << nums[i]
                      << " is less than nums[window[-1]] = " << nums[window.back()] << std::endl;
            else
                std::cout << "\t\tThe window is empty." << std::endl;
        }
        check = false;

        // Add current element at the back of the queue
        window.push_back(i);
    }
    // Appending the largest element in the window to the result
    result.push_back(nums[window.front()]);
    std::cout << "Traversing to find maximum in remaining windows:" << std::endl;
    for (int i = windowSize; i < nums.size(); ++i)
    {
        // remove all numbers that are smaller than current number
        // from the tail of list
        while (!window.empty() && nums[i] >= nums[window.back()])
        {
            check = true;
            std::cout << "\t\tnums[" << i << "] = " << nums[i]
                      << " is greater than or equal to nums[window[-1]] = " << nums[window.back()] << std::endl;
            window.pop_back();
            std::cout << "\t\tWindow after popping: " << PrintD(window) << std::endl;
        }
        
        // this is only for the purpose of printing
        if (!check){
            if (!window.empty())
                std::cout << "\t\tnums[" << i << "] = " << nums[i]
                      << " is less than nums[window[-1]] = " << nums[window.back()] << std::endl;
            else
                std::cout << "\t\tThe window is empty." << std::endl;
        }
        check = false;


        // Remove first index from the window deque if
        // it doesn't fall in the current window anymore
        if (!window.empty() && window.front() <= i - windowSize)
        {
            window.pop_front();
        }
        // Add current element at the back of the queue
        window.push_back(i);
        result.push_back(nums[window.front()]);
    }
    return result;
}
```

#### Minimum window subsequence
Given strings str1 and str2, find the minimum (contiguous) substring subStr of str1, such that every character of str2 appears in subStr in the same order as it is present in str2.
```c++
std::string MinWindow(std::string str1, std::string str2)
{
    // Save the length of str1 and str2
    int sizeStr1 = str1.length(), sizeStr2 = str2.length();
    // Initialize length to a very large number (infinity)
    int length = INT_MAX;
    // Initialize pointers to zero and the min_subsequence to an empty string
    int indexS1 = 0, indexS2 = 0;
    std::string minSubsequence = "";

    // Process every character of str1
    while (indexS1 < sizeStr1)
    {
        // Check if the character pointed by indexS1 in str1
        // is the same as the character pointed by indexS2 in str2
        if (str1[indexS1] == str2[indexS2])
        {
            // If the pointed character is the same
            // in both strings increment indexS2
            indexS2 += 1;
            // Check if indexS2 has reached the end of str2
            if (indexS2 == sizeStr2)
            {
                // At this point the str1 contains all characters of str2
                int start = indexS1, end = indexS1 + 1;
                // Initialize start to the index where all characters of
                // str2 were present in str1
                indexS2 -= 1;
                // Decrement pointer indexS2 and start a reverse loop
                while (indexS2 >= 0)
                {
                    // Decrement pointer indexS2 until all characters of
                    //  str2 are found in str1
                    if (str1[start] == str2[indexS2])
                    {
                        indexS2 -= 1;
                    }
                    // Decrement start pointer everytime to find the
                    // starting point of the required subsequence
                    start -= 1;
                }
                start += 1;
                // Check if length of sub sequence pointed
                // by start and end pointers is less than current min length
                if (end - start < length)
                {
                    // Update length if current sub sequence is shorter
                    length = end - start;
                    // Update minimum subsequence string
                    // to this new shorter string
                    minSubsequence = str1.substr(start, length);
                }
                // Set indexS1 to start to continue checking in str1
                // after this discovered subsequence
                indexS1 = start;
                indexS2 = 0;
            }
        }
        // Increment pointer indexS1 to check next character in str1
        indexS1 += 1;
    }
    return minSubsequence;
}
```

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

#### Valid parentheses
```c++
bool isValid(string s) {
    stack<char> st;
    map<char, char> chars = { {'(', ')'}, {'[', ']'}, {'{', '}'} };

    for (auto c : s)
    {
        if (chars.find(c) != chars.end())
        {
            st.push(c);
        }
        else
        {
            if (st.empty())
            {
                return false;
            } 

            if (chars[st.top()] != c)
            {
                return false;
            }
            else
            {
                st.pop();
            }
        }
    }

    if (!st.empty())
    {
        return false;
    }

    return true;
}
```


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

#### Validate BST
```c++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return helper(root, LONG_MIN, LONG_MAX);
    }
private:
    bool helper(TreeNode* root, long left, long right){
        if (!root)
            return true;
        if (root->val < right && root->val > left){
            return helper(root->left, left, root->val) && helper(root->right, root->val, right);
        }
        return false;
    }
};
```

## Binary Search

#### Classic binary search
```c++
int search(vector<int>& nums, int target) {
        
    int size = nums.size();
    int response = -1;

    if (size == 1 && nums[0] == target)
    {
        return 0;
    }

    int start   = 0;
    int end     = size - 1;


    while (start <= end)
    {
        int middle =  ((end - start) / 2) + start; 

        if (nums[middle]  == target)
        {
            return middle;
        }

        if (target < nums[middle])
        {
            end = middle - 1;
            
        }
        else
        {
            start = middle + 1;
        }

    }

    return response;
}
```