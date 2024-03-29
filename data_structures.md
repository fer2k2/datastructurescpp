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

