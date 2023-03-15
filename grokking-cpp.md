# Grokking Cpp
## Two pointers
<br>

### Forward iterator loop
```c++
bool IsPalindrome(string inputString)
{
    // Pointer at first and at the end
    int left = 0;
    int right = inputString.size() - 1;

    while (left < right)
    {

        if (inputString.at(left) != inputString.at(right))
        {
            return false;
        }

        // Increase pointers
        left++;
        right--;
    }

    return true;
}
```

### Sum of three values
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

### Reverse string
Given an array of integers, nums, and an integer value, target, determine if there are any three integers in nums whose sum equals the target. Return TRUE if three such integers are found in the array. Otherwise, return FALSE.
```c++
// A function that reverses a whole sentence character by character
void StrRev(std::string &_str, int startRev, int endRev)
{
    // Starting from the two ends of the list, and moving
    // in towards the centre of the string, swap the characters
    while (startRev < endRev)
    {
        char temp = _str[startRev];    // temp store for swapping
        _str[startRev] = _str[endRev]; // swap step 1
        _str[endRev] = temp;           // swap step 2
        startRev += 1;                 // Move forwards towards the middle
        endRev -= 1;                   // Move backwards towards the middle
    }
}
```

### Reverse words in sentence
```c++
std::string ReverseWords(std::string sentence)
{

    // Removing leading, trailing and extra spaces from a string
    sentence = std::regex_replace(sentence, std::regex("^ +| +$|( ) +"), "$1");
    
    //  To reverse all words in the string, we will first reverse
    //  the entire string.
    int strLen = sentence.size();
    StrRev(sentence, 0, strLen - 1);
    //  Now all the words are in the desired location, but
    //  in reverse order: "Hello World" -> "dlroW olleH".
    // Now, let's iterate the sentence and reverse each word in place.
    // "dlroW olleH" -> "World Hello"
    int start = 0, end = 0;
    while (true)
    {
        // Find the start index of each word by detecting spaces.
        while (start < sentence.size() && sentence[start] == ' ')
            start += 1;
        if (start == strLen)
            break;
        // Find the end index of the word.
        end = start + 1;
        while (end < strLen && sentence[end] != ' ')
            end += 1;
        // Let's call our helper function to reverse the word in-place.
        StrRev(sentence, start, end - 1);
        start = end;
    }
    return sentence;
}
```