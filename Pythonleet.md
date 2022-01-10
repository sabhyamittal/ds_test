#### Question 1.

<details>
<summary>code</summary> 
  
```
class Solution:
    def read(self, buf: List[str], n: int) -> int:
        copied_chars = 0
        read_chars = 4
        buf4 = [''] * 4
        
        while copied_chars < n and read_chars == 4:
            read_chars = read4(buf4)
            
            for i in range(read_chars):
                if copied_chars == n:
                    return copied_chars
                buf[copied_chars] = buf4[i]
                copied_chars += 1
        
        return copied_char
```
</details>

#### Question 2.
  
Given a file and assume that you can only read the file using a given method read4, implement a method read to read n characters. Your method read may be called multiple times.
  
#### Question 3.
 
Given a string s, return the length of the longest substring that contains at most two distinct characters.
  
<details>
<summary>code</summary> 
  
```
 from collections import defaultdict
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s: 'str') -> 'int':
        n = len(s)
        if n < 3:
            return n

        # sliding window left and right pointers
        left, right = 0, 0
        # hashmap character -> its rightmost position
        # in the sliding window
        hashmap = defaultdict()

        max_len = 2

        while right < n:
            # when the slidewindow contains less than 3 characters
            hashmap[s[right]] = right
            right += 1

            # slidewindow contains 3 characters
            if len(hashmap) == 3:
                # delete the leftmost character
                del_idx = min(hashmap.values())
                del hashmap[s[del_idx]]
                # move left pointer of the slidewindow
                left = del_idx + 1

            max_len = max(max_len, right - left)

        return max_len 
```
  </details>
  
 #### Question 4.
  
 Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.
  
  Using Brute Force:
  <details>
  <summary>code</summary>
    
  ```
    class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        while headA is not None:
            pB = headB
            while pB is not None:
                if headA == pB:
                    return headA
                pB = pB.next
            headA = headA.next

        return None
    
  ```
  </details>
  
  Using Hash Table:
  <details>
  <summary>code</summary>
    
 ```
    class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        nodes_in_B = set()

        while headB is not None:
            nodes_in_B.add(headB)
            headB = headB.next

        while headA is not None:
            # if we find the node pointed to by headA,
            # in our set containing nodes of B, then return the node
            if headA in nodes_in_B:
                return headA
            headA = headA.next

        return None
    
  ```
  </details>
  
  Using Two Pointers:
  <details>
  <summary>code</summary>  
    
  ```
    class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        pA = headA
        pB = headB

        while pA != pB:
            pA = headB if pA is None else pA.next
            pB = headA if pB is None else pB.next

        return pA
        # Note: In the case lists do not intersect, the pointers for A and B
        # will still line up in the 2nd iteration, just that here won't be
        # a common node down the list and both will reach their respective ends
        # at the same time. So pA will be NULL in that case.
    
  ```
  </details>
  
 #### Question 5.
 
Given two strings s and t, return true if they are both one edit distance apart, otherwise return false.

A string s is said to be one distance apart from a string t if you can:

Insert exactly one character into s to get t.
Delete exactly one character from s to get t.
Replace exactly one character of s with a different character to get t.
  
<details>
<summary>code</summary>  
 
 ```
  class Solution:
    def isOneEditDistance(self, s: 'str', t: 'str') -> 'bool':
        ns, nt = len(s), len(t)

        # Ensure that s is shorter than t.
        if ns > nt:
            return self.isOneEditDistance(t, s)

        # The strings are NOT one edit away distance  
        # if the length diff is more than 1.
        if nt - ns > 1:
            return False

        for i in range(ns):
            if s[i] != t[i]:
                # if strings have the same length
                if ns == nt:
                    return s[i + 1:] == t[i + 1:]
                # if strings have different lengths
                else:
                    return s[i:] == t[i + 1:]
        
        # If there is no diffs on ns distance
        # the strings are one edit away only if
        # t has one more character. 
        return ns + 1 == nt
  
 ```
 </details> 
  
#### Question 6.

A peak element is an element that is strictly greater than its neighbors.

Given an integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞.

You must write an algorithm that runs in O(log n) time.

<details>
<summary>code in JAVA</summary>  
  
```
  public class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0, r = nums.length - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (nums[mid] > nums[mid + 1])
                r = mid;
            else
                l = mid + 1;
        }
        return l;
    }
}
  
```
</details>  
  
#### Question 7. 
  
You are given an inclusive range [lower, upper] and a sorted unique integer array nums, where all elements are in the inclusive range.

A number x is considered missing if x is in the range [lower, upper] and x is not in nums.

Return the smallest sorted list of ranges that cover every missing number exactly. That is, no element of nums is in any of the ranges, 
and each missing number is in one of the ranges.

Each range [a,b] in the list should be output as:

"a->b" if a != b
"a" if a == b
  
<details>
<summary>code</summary>  
  
```
  class Solution:
    def findMissingRanges(self, nums: List[int], lower: int, upper: int) -> List[str]:
        # formats range in the requested format
        def formatRange(lower, upper):
            if lower == upper:
                return str(lower)
            return str(lower) + "->" + str(upper)

        result = []
        prev = lower - 1
        for i in range(len(nums) + 1):
            curr = nums[i] if i < len(nums) else upper + 1
            if prev + 1 <= curr - 1:
                result.append(formatRange(prev + 1, curr - 1))
            prev = curr
        return result

```
</details>  
  
#### Question 8.
  
Given an integer array nums, return the maximum difference between two successive elements in its sorted form. If the array contains less than two elements, return 0.

You must write an algorithm that runs in linear time and uses linear extra space. 
  
<details>
<summary>code in C++</summary> 
  
```
  class Bucket {
public:
    bool used = false;
    int minval = numeric_limits<int>::max();        // same as INT_MAX
    int maxval = numeric_limits<int>::min();        // same as INT_MIN
};

int maximumGap(vector<int>& nums)
{
    if (nums.empty() || nums.size() < 2)
        return 0;

    int mini = *min_element(nums.begin(), nums.end()),
        maxi = *max_element(nums.begin(), nums.end());

    int bucketSize = max(1, (maxi - mini) / ((int)nums.size() - 1));        // bucket size or capacity
    int bucketNum = (maxi - mini) / bucketSize + 1;                         // number of buckets
    vector<Bucket> buckets(bucketNum);

    for (auto&& num : nums) {
        int bucketIdx = (num - mini) / bucketSize;                          // locating correct bucket
        buckets[bucketIdx].used = true;
        buckets[bucketIdx].minval = min(num, buckets[bucketIdx].minval);
        buckets[bucketIdx].maxval = max(num, buckets[bucketIdx].maxval);
    }

    int prevBucketMax = mini, maxGap = 0;
    for (auto&& bucket : buckets) {
        if (!bucket.used)
            continue;

        maxGap = max(maxGap, bucket.minval - prevBucketMax);
        prevBucketMax = bucket.maxval;
    }

    return maxGap;
}
  
```
</details>  
  
#### Question 9.
  
Given two version numbers, version1 and version2, compare them.

Version numbers consist of one or more revisions joined by a dot '.'. Each revision consists of digits and may contain leading zeros. Every revision contains at least one character. Revisions are 0-indexed from left to right, with the leftmost revision being revision 0, the next revision being revision 1, and so on. For example 2.5.33 and 0.1 are valid version numbers.

To compare version numbers, compare their revisions in left-to-right order. Revisions are compared using their integer value ignoring any leading zeros. This means that revisions 1 and 001 are considered equal. If a version number does not specify a revision at an index, then treat the revision as 0. For example, version 1.0 is less than version 1.1 because their revision 0s are the same, but their revision 1s are 0 and 1 respectively, and 0 < 1.

Return the following:

If version1 < version2, return -1.
If version1 > version2, return 1.
Otherwise, return 0.
Using Two Pointers , One Pass:  
  
<details>
<summary>code</summary> 
  
 ```
  class Solution:
    def get_next_chunk(self, version: str, n: int, p: int) -> List[int]:
        # if pointer is set to the end of string
        # return 0
        if p > n - 1:
            return 0, p
        
        # find the end of chunk
        p_end = p
        while p_end < n and version[p_end] != '.':
            p_end += 1
        # retrieve the chunk
        i = int(version[p:p_end]) if p_end != n - 1 else int(version[p:n])
        # find the beginning of next chunk
        p = p_end + 1
        
        return i, p
        
    def compareVersion(self, version1: str, version2: str) -> int:
        p1 = p2 = 0
        n1, n2 = len(version1), len(version2)
        
        # compare versions
        while p1 < n1 or p2 < n2:
            i1, p1 = self.get_next_chunk(version1, n1, p1)
            i2, p2 = self.get_next_chunk(version2, n2, p2)            
            if i1 != i2:
                return 1 if i1 > i2 else -1
        
        # the versions are equal
        return 0    
 ```
 </details> 
  
 #### Question 10:
  
 Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return any of them.

It is guaranteed that the length of the answer string is less than 104 for all the given inputs.

<details>
<summary>code in JAVA</summary>  
 
```
public String fractionToDecimal(int numerator, int denominator) {
    if (numerator == 0) {
        return "0";
    }
    StringBuilder fraction = new StringBuilder();
    // If either one is negative (not both)
    if (numerator < 0 ^ denominator < 0) {
        fraction.append("-");
    }
    // Convert to Long or else abs(-2147483648) overflows
    long dividend = Math.abs(Long.valueOf(numerator));
    long divisor = Math.abs(Long.valueOf(denominator));
    fraction.append(String.valueOf(dividend / divisor));
    long remainder = dividend % divisor;
    if (remainder == 0) {
        return fraction.toString();
    }
    fraction.append(".");
    Map<Long, Integer> map = new HashMap<>();
    while (remainder != 0) {
        if (map.containsKey(remainder)) {
            fraction.insert(map.get(remainder), "(");
            fraction.append(")");
            break;
        }
        map.put(remainder, fraction.length());
        remainder *= 10;
        fraction.append(String.valueOf(remainder / divisor));
        remainder %= divisor;
    }
    return fraction.toString();
}
  
```  
</details>  
  
#### Question 11:
  
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number.
Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.  
                                                                                                         
<details>
<summary>code in C++</summary>
  
 ```
  class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int low = 0;
        int high = numbers.size() - 1;
        while (low < high) {
            int sum = numbers[low] + numbers[high];
                          
            if (sum == target) {
                return {low + 1, high + 1};
            } else if (sum < target) {
                ++low;
            } else {
                --high;
            }
        }
        // In case there is no solution, return {-1, -1}.
        return {-1, -1};
    }
};
 ```
 </details> 
  
  
#### Question 12.
  
Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

For example:

A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
  
#### Question 13.
  
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array. 
Using Divide And Conquer:  
  
<details>
<summary>code</summary> 
  
```
  class Solution:
    def majorityElement(self, nums, lo=0, hi=None):
        def majority_element_rec(lo, hi):
            # base case; the only element in an array of size 1 is the majority
            # element.
            if lo == hi:
                return nums[lo]

            # recurse on left and right halves of this slice.
            mid = (hi-lo)//2 + lo
            left = majority_element_rec(lo, mid)
            right = majority_element_rec(mid+1, hi)

            # if the two halves agree on the majority element, return it.
            if left == right:
                return left

            # otherwise, count each element and return the "winner".
            left_count = sum(1 for i in range(lo, hi+1) if nums[i] == left)
            right_count = sum(1 for i in range(lo, hi+1) if nums[i] == right)

            return left if left_count > right_count else right

        return majority_element_rec(0, len(nums)-1)

```
</details>  
  
#### Question 14:
Design a data structure that accepts a stream of integers and checks if it has a pair of integers that sum up to a particular value.

Implement the TwoSum class:

TwoSum() Initializes the TwoSum object, with an empty array initially.
void add(int number) Adds number to the data structure.
boolean find(int value) Returns true if there exists any pair of numbers whose sum is equal to value, otherwise, it returns false.
using HashTable:  
<details>
<summary>code</summary>  
  
 ```
  class TwoSum(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.num_counts = {}


    def add(self, number):
        """
        Add the number to an internal data structure..
        :type number: int
        :rtype: None
        """
        if number in self.num_counts:
            self.num_counts[number] += 1
        else:
            self.num_counts[number] = 1

    def find(self, value):
        """
        Find if there exists any pair of numbers which sum is equal to the value.
        :type value: int
        :rtype: bool
        """
        for num in self.num_counts.keys():
            comple = value - num
            if num != comple:
                if comple in self.num_counts:
                    return True
            elif self.num_counts[num] > 1:
                return True
        
        return False

 ```
</details> 
  
 #### Question 15:
 Given a string columnTitle that represents the column title as appear in an Excel sheet, return its corresponding column number.
  
<details>
<summary>code</summary> 
 
 ```
  class Solution:
    def titleToNumber(self, s: str) -> int:
        result = 0
        n = len(s)
        for i in range(n):
            result = result * 26
            result += (ord(s[i]) - ord('A') + 1)
        return result
 ```
 </details> 
  
#### Question 16:
Given an integer n, return the number of trailing zeroes in n!.

Note that n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1. 
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
#### Question 17:
Implement the BSTIterator class that represents an iterator over the in-order traversal of a binary search tree (BST):

BSTIterator(TreeNode root) Initializes an object of the BSTIterator class. The root of the BST is given as part of the constructor. 
The pointer should be initialized to a non-existent number smaller than any element in the BST.
boolean hasNext() Returns true if there exists a number in the traversal to the right of the pointer, otherwise returns false.
int next() Moves the pointer to the right, then returns the number at the pointer.  
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 18:
  
The demons had captured the princess and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of m x n rooms laid out in a 2D grid. 
Our valiant knight was initially positioned in the top-left room and must fight his way through dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons (represented by negative integers), so the knight loses health upon entering these rooms; 
other rooms are either empty (represented as 0) or contain magic orbs that increase the knight's health (represented by positive integers).

To reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

Return the knight's minimum initial health so that he can rescue the princess. 
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 19:
Write an SQL query to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table,
report null instead.

Return the result table in any order.  
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 20:
Write an SQL query to report the second highest salary from the Employee table. If there is no second highest salary, the query should report null.

The query result format is in the following example. 
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 21:
Write an SQL query to report the nth highest salary from the Employee table. If there is no nth highest salary, the query should report null.

The query result format is in the following example.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 22:
Write an SQL query to rank the scores. The ranking should be calculated according to the following rules:

The scores should be ranked from the highest to the lowest.
If there is a tie between two scores, both should have the same ranking.
After a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no holes between ranks.
Return the result table ordered by score in descending order.
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 23:
Given a list of non-negative integers nums, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 24:
Write an SQL query to find all numbers that appear at least three times consecutively.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 25:
Write an SQL query to find the employees who earn more than their managers.

Return the result table in any order. 
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 26:
Write an SQL query to report all the duplicate emails.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 27:
Write an SQL query to report all customers who never order anything.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 28:
Write an SQL query to find employees who have the highest salary in each of the departments.

Return the result table in any order.  
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>
  
 #### Question 29:
A company's executives are interested in seeing who earns the most money in each of the company's departments. A high earner in a department is an employee who has a
salary in the top three unique salaries for that department.

Write an SQL query to find the employees who are high earners in each of the departments.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 

#### Question 30:
Given a character array s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by a single space.

Your code must solve the problem in-place, i.e. without allocating extra space.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
#### Question 31:
The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'.

For example, "ACGAATTCCG" is a DNA sequence.
When studying DNA, it is useful to identify repeated sequences within the DNA.

Given a string s that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. 
You may return the answer in any order. 
  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 32:
You are given an integer array prices where prices[i] is the price of a given stock on the ith day, and an integer k.

Find the maximum profit you can achieve. You may complete at most k transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 33:
Given an array, rotate the array to the right by k steps, where k is non-negative.  

<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 34:
Reverse bits of a given 32 bits unsigned integer.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 35:
Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the Hamming weight).  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 36:
Write a bash script to calculate the frequency of each word in a text file words.txt.

For simplicity sake, you may assume:

words.txt contains only lowercase characters and space ' ' characters.
Each word must consist of lowercase characters only.
Words are separated by one or more whitespace characters.  
  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 37:
Given a text file file.txt that contains a list of phone numbers (one per line), write a one-liner bash script to print all valid phone numbers.

You may assume that a valid phone number must appear in one of the following two formats: (xxx) xxx-xxxx or xxx-xxx-xxxx. (x means a digit)

You may also assume each line in the text file must not contain leading or trailing white spaces.  
  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 38:
Given a text file file.txt, transpose its content.

You may assume that each row has the same number of columns, and each field is separated by the ' ' character.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 39:
Given a text file file.txt, print just the 10th line of the file.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 40:
Write an SQL query to delete all the duplicate emails, keeping only one unique email with the smallest id.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 41:
Write an SQL query to find all dates' Id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 42:
 You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you 
  from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses 
  were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 43:
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 44:
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 45:
Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 46:
Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 47:
Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.  
  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 48:
Given an integer n, return the number of prime numbers that are strictly less than n.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 49:
Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. 
  No two characters may map to the same character, but a character may map to itself.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 50:
Given the head of a singly linked list, reverse the list, and return the reversed list.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 51:
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1.
You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 52:
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. 
  There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

Trie() Initializes the trie object.
void insert(String word) Inserts the string word into the trie.
boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 53:
 Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] 
  of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 54:
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. 
  You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. 
  If it is impossible to finish all courses, return an empty array.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 55:
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

WordDictionary() Initializes the object.
void addWord(word) Adds word to the data structure, it can be matched later.
bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.'
  where dots can be matched with any letter.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 56:
Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. 
The same letter cell may not be used more than once in a word.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 57:
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. 
  All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, 
  adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 58:
You are given a string s. You can convert s to a palindrome by adding characters in front of it.

Return the shortest palindrome you can find by performing this transformation.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 59:
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 60:
Find all valid combinations of k numbers that sum up to n such that the following conditions are true:

Only numbers 1 through 9 are used.
Each number is used at most once.
Return a list of all possible valid combinations. The list must not contain the same combination twice, and the combinations may be returned in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 61:
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 62:
A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance.
  Given the locations and heights of all the buildings, return the skyline formed by these buildings collectively.

The geometric information of each building is given in the array buildings where buildings[i] = [lefti, righti, heighti]:

lefti is the x coordinate of the left edge of the ith building.
righti is the x coordinate of the right edge of the ith building.
heighti is the height of the ith building.
You may assume all buildings are perfect rectangles grounded on an absolutely flat surface at height 0.

The skyline should be represented as a list of "key points" sorted by their x-coordinate in the form [[x1,y1],[x2,y2],...].
  Each key point is the left endpoint of some horizontal segment in the skyline except the last point in the list, 
  which always has a y-coordinate 0 and is used to mark the skyline's termination where the rightmost building ends.
  Any ground between the leftmost and rightmost buildings should be part of the skyline's contour.

Note: There must be no consecutive horizontal lines of equal height in the output skyline. For instance, [...,[2 3],[4 5],[7 5],[11 5],[12 7],...] 
  is not acceptable; the three lines of height 5 should be merged into one in the final output as such: [...,[2 3],[4 5],[12 7],...]  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 63:
 Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k. 
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 64:
Given an integer array nums and two integers k and t, return true if there are two distinct indices i and j in the array 
  such that abs(nums[i] - nums[j]) <= t and abs(i - j) <= k.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  #### Question 65:
Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 66:
Given the root of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes
  in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Design an algorithm that runs in less than O(n) time complexity.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 67:
Given the coordinates of two rectilinear rectangles in a 2D plane, return the total area covered by the two rectangles.

The first rectangle is defined by its bottom-left corner (ax1, ay1) and its top-right corner (ax2, ay2).

The second rectangle is defined by its bottom-left corner (bx1, by1) and its top-right corner (bx2, by2).  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 68:
Given a string s representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval() 
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 69:
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.
  
###### Notes:

You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.
Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long 
  as you use only a queue's standard operations.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 70:
Given the root of a binary tree, invert the tree, and return its root.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 71:
Given a string s which represents an expression, evaluate this expression and return its value. 

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of [-231, 231 - 1].

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval().  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 72:
You are given a sorted unique integer array nums.

Return the smallest sorted list of ranges that cover all the numbers in the array exactly. That is, each element of nums is covered by exactly one of the ranges,
  and there is no integer x such that x is in one of the ranges but not in nums.

Each range [a,b] in the list should be output as:

"a->b" if a != b
"a" if a == b  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 73:
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 74:
  Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 75:
 Given an integer n, return true if it is a power of two. Otherwise, return false.

An integer n is a power of two, if there exists an integer x such that n == 2x. 
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 76:
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.
Notes:

You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue)
  as long as you use only a stack's standard operations.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 77:
Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 78:
Given the head of a singly linked list, return true if it is a palindrome. 
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 79:
 Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has 
  both p and q as descendants (where we allow a node to be a descendant of itself).”

  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 80:
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both 
  p and q as descendants (where we allow a node to be a descendant of itself).”  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 81:
Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access 
  to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 82:
 Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation. 
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 83:
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right.
  You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 84:
Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 85:
Given a string expression of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators.
  You may return the answer in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 86:
Given two strings s and t, return true if t is an anagram of s, and false otherwise.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 87:
Given an array of strings wordsDict and two different strings that already exist in the array word1 and word2, return the shortest distance between these two words in the list.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 88:
Design a data structure that will be initialized with a string array, and then it should answer queries of the shortest distance between two different strings from the array.

Implement the WordDistance class:

WordDistance(String[] wordsDict) initializes the object with the strings array wordsDict.
int shortest(String word1, String word2) returns the shortest distance between word1 and word2 in the array wordsDict.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 89:
Given an array of strings wordsDict and two strings that already exist in the array word1 and word2, return the shortest distance between these two words in the list.

Note that word1 and word2 may be the same. It is guaranteed that they represent two individual words in the list.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 90:
Given a string num which represents an integer, return true if num is a strobogrammatic number.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 91:
Given an integer n, return all the strobogrammatic numbers that are of length n. You may return the answer in any order.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 92:
Given two strings low and high that represent two integers low and high where low <= high, return the number of strobogrammatic numbers in the range [low, high].

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 93:
We can shift a string by shifting each of its letters to its successive letter.

For example, "abc" can be shifted to be "bcd".
We can keep shifting the string to form a sequence.

For example, we can keep shifting "abc" to form the sequence: "abc" -> "bcd" -> ... -> "xyz".
Given an array of strings strings, group all strings[i] that belong to the same shifting sequence. You may return the answer in any order.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 94:
Given the root of a binary tree, return the number of uni-value subtrees.

A uni-value subtree means all nodes of the subtree have the same value.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 95:
Design an iterator to flatten a 2D vector. It should support the next and hasNext operations.

Implement the Vector2D class:

Vector2D(int[][] vec) initializes the object with the 2D vector vec.
next() returns the next element from the 2D vector and moves the pointer one step forward. You may assume that all the calls to next are valid.
hasNext() returns true if there are still some elements in the vector, and false otherwise.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 96:
Given an array of meeting time intervals where intervals[i] = [starti, endi], determine if a person could attend all meetings.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 97:
Given an array of meeting time intervals intervals where intervals[i] = [starti, endi], return the minimum number of conference rooms required.
  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 98:
Numbers can be regarded as the product of their factors.

For example, 8 = 2 x 2 x 2 = 2 x 4.
Given an integer n, return all possible combinations of its factors. You may return the answer in any order.

Note that the factors should be in the range [2, n - 1].

   
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
  #### Question 99:
Given an array of unique integers preorder, return true if it is the correct preorder traversal sequence of a binary search tree.  
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
 #### Question 100:
 There is a row of n houses, where each house can be painted one of three colors: red, blue, or green. The cost of painting each house with a certain color is different. 
  You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by an n x 3 cost matrix costs.

For example, costs[0][0] is the cost of painting house 0 with the color red; costs[1][2] is the cost of painting house 1 with color green, and so on...
Return the minimum cost to paint all houses. 
<details>
<summary>code</summary>
  
 ```
 ```
</details> 
  
 #### Question 101:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
#### Question 102:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
#### Question 103:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 104:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 105:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 106:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 107:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 108:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 109:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 110:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 111:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 112:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 101:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 114:
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 115:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 116:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 117:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  
  
  
  
 
  
  
  
