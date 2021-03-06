# Strings and Arrays
### Iterators

#### Forward iterator loop
```c++
for (auto it = s.begin(); it != s.end(); ++it)
{
    std::cout << *it;
}
```
#### Reverse iterator loop
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
```c++
int n = 2;
int counts = std::count(v.begin(), v.end(), n);
```
#### Find
```c++
auto result1 = std::find(begin(v), end(v), n1);
```
#### Find if
```c++
auto is_even = [](int i){ return i%2 == 0; };
auto result3 = std::find_if(begin(v), end(v), is_even);
```
#### Binary search (for sorted arrays)
```c++
bool found = std::binary_search(haystack.begin(), haystack.end(), needle);
```
#### Erase
```c++
std::vector<int> c{0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
print_container(c);

c.erase(c.begin());
print_container(c);

c.erase(c.begin()+2, c.begin()+5);
print_container(c);

// Erase all even numbers (C++11 and later)
for (auto it = c.begin(); it != c.end(); ) {
    if (*it % 2 == 0) {
        it = c.erase(it);
    } else {
        ++it;
    }
}
```
#### Unique
```c++
// remove consecutive (adjacent) duplicates
auto last = std::unique(v.begin(), v.end());
// v now holds {1 2 1 3 4 5 4 x x x}, where 'x' is indeterminate
v.erase(last, v.end());
print(2);

// sort followed by unique, to remove all duplicates
std::sort(v.begin(), v.end()); // {1 1 2 3 4 4 5}
print(3);

last = std::unique(v.begin(), v.end());
// v now holds {1 2 3 4 5 x x}, where 'x' is indeterminate
v.erase(last, v.end());
print(4);
```
#### Distance
```c++
std::vector<int> v{ 3, 1, 4 };

std::cout << "distance(first, last) = "
    << std::distance(v.begin(), v.end()) << '\n'
    << "distance(last, first) = "
    << std::distance(v.end(), v.begin()) << '\n';
```
# Sets and maps

## Sets

#### Insert
```c++
std::set<int> set;
 
auto result_1 = set.insert(3);
assert(result_1.first != set.end()); // it's a valid iterator
assert(*result_1.first == 3);
if (result_1.second)
    std::cout << "insert done\n";
```
## Maps

#### Insert
```c++
std::map<std::string, float> karasunoPlayerHeights;

const auto [it_hinata, success] = karasunoPlayerHeights.insert({"Hinata"s, 162.8});
printInsertionStatus(it_hinata, success);
```

#### Erase
```c++
std::map<int, std::string> c = {
    {1, "one" }, {2, "two" }, {3, "three"},
    {4, "four"}, {5, "five"}, {6, "six"  }
};

// erase all odd numbers from c
for(auto it = c.begin(); it != c.end(); ) {
    if(it->first % 2 != 0)
        it = c.erase(it);
    else
        ++it;
}
```
# Stacks and Queues

## Stacks

#### Push, Pop, Top
```c++
std::stack<int>   s;

s.push( 2 );
s.push( 6 );
s.push( 51 );

std::cout << s.size() << " elements on stack\n";
std::cout << "Top element: "
      << s.top()         // Leaves element on stack
      << "\n";
std::cout << s.size() << " elements on stack\n";
s.pop();
std::cout << s.size() << " elements on stack\n";
std::cout << "Top element: " << s.top() << "\n";
```

## Queue

#### Front, Back, Push, Pop

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

### Reverse list
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

# Binary Trees
```c++
class Node {
public:
    int data;
    Node* left;
    Node* right;
    Node(int d) {
        data = d;
        left = NULL;
        right = NULL;
    }
};
```

## Tree traversal

### In order
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
### Pre order
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
### Post order
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

### Level order
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

### Lowest common ansestor
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

# Graphs

## Representation


## Grap Traversal
### Depth first search (DFS)
```c++
void Graph::DFS(int v)
{
    // Mark the current node as visited and
    // print it
    visited[v] = true;
    cout << v << " ";
 
    // Recur for all the vertices adjacent
    // to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFS(*i);
}
```

### Breath first search (BFS)
```c++
vector<int>bfsOfGraph(int V, vector<int> adj[])
{
    std::vector<int> response;

    // Code here
    vector<bool> vVisitedNodes(V);
    std::queue<int> queue;

    // Strat from the node 0;
    // Mark it as visited
    vVisitedNodes[0] = true;
    response.push_back(0);
    //std::cout << 0 << std::endl;

    queue.push(0);

    while(!queue.empty())
    {
        int current = queue.front();
        queue.pop();

        // Get all the adjacent nodes to the current
        for (int i=0; i < adj[current].size(); i++)
        {
            if (!vVisitedNodes.at(adj[current][i]))
            {
                vVisitedNodes.at(adj[current][i]) = true;
                response.push_back(adj[current][i]);
                //std::cout << adj[current][i] << std::endl;
                queue.push(adj[current][i]);
            }
        }
    }

    return response;
}
```
