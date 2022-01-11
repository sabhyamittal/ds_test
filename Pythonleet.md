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
 Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children. 
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
#### Question 102:
Given an integer num, repeatedly add all its digits until the result has only one digit, and return it.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
#### Question 103:
Given an array of n integers nums and an integer target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 104:
 Given an integer array nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in any order.

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.

  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 105:
You have a graph of n nodes labeled from 0 to n - 1. You are given an integer n and a list of edges where edges[i] = [ai, bi] indicates that there is an undirected edge between nodes ai and bi in the graph.

Return true if the edges of the given graph make up a valid tree, and false otherwise.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 106:
The cancellation rate is computed by dividing the number of canceled (by client or driver) requests with unbanned users by the total number of requests with unbanned users on that day.

Write a SQL query to find the cancellation rate of requests with unbanned users (both client and driver must not be banned) each day between "2013-10-01" and "2013-10-03". Round Cancellation Rate to two decimal points.

Return the result table in any order. 
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 107:
An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return true if n is an ugly number.
  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 108:
 An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return the nth ugly number.

  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 109:
There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by an n x k cost matrix costs.

For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on...
Return the minimum cost to paint all houses.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 110:
 Given a string s, return true if a permutation of the string could form a palindrome. 
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 111:
Given a string s, return all the palindromic permutations (without duplicates) of it.

You may return the answer in any order. If s has no palindromic permutation, return an empty list.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 112:
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 101:
There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.

You are given a list of strings words from the alien language's dictionary, where the strings in words are sorted lexicographically by the rules of this new language.

Return a string of the unique letters in the new alien language sorted in lexicographically increasing order by the new language's rules. If there is no solution, return "". If there are multiple solutions, return any of them.

A string s is lexicographically smaller than a string t if at the first letter where they differ, the letter in s comes before the letter in t in the alien language. If the first min(s.length, t.length) letters are the same, then s is smaller if and only if s.length < t.length.

   
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 113:
Given the root of a binary search tree and a target value, return the value in the BST that is closest to the target  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 114:
Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.  
<details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 115:
Given the root of a binary search tree, a target value, and an integer k, return the k values in the BST that are closest to the target. You may return the answer in any order.

You are guaranteed to have only one unique set of k values in the BST that are closest to the target.  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 116:
 Convert a non-negative integer num to its English words representation.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 117:
Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper, return compute the researcher's h-index.

According to the definition of h-index on Wikipedia: A scientist has an index h if h of their n papers have at least h citations each, and the other n − h papers have no more than h citations each.

If there are several possible values for h, the maximum one is taken as the h-index.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 118:
Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper and citations is sorted in an ascending order, return compute the researcher's h-index.

According to the definition of h-index on Wikipedia: A scientist has an index h if h of their n papers have at least h citations each, and the other n − h papers have no more than h citations each.

If there are several possible values for h, the maximum one is taken as the h-index.

You must write an algorithm that runs in logarithmic time.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 119:
You are painting a fence of n posts with k different colors. You must paint the posts following these rules:

Every post must be painted exactly one color.
There cannot be three or more consecutive posts with the same color.
Given the two integers n and k, return the number of ways you can paint the fence.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 120:
Suppose you are at a party with n people (labeled from 0 to n - 1), and among them, there may exist one celebrity. The definition of a celebrity is that all the other n - 1 people know him/her, but he/she does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?" to get information about whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).

You are given a helper function bool knows(a, b) which tells you whether A knows B. Implement a function int findCelebrity(n). There will be exactly one celebrity if he/she is in the party. Return the celebrity's label if there is a celebrity in the party. If there is no celebrity, return -1.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 121:
 You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 122:
 Given an integer n, return the least number of perfect square numbers that sum to n.

A perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, 1, 4, 9, and 16 are perfect squares while 3 and 11 are not.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 123:
 Given an integer array nums, reorder it such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

You may assume the input array always has a valid answer.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 123:
 Given two vectors of integers v1 and v2, implement an iterator to return their elements alternately.

Implement the ZigzagIterator class:

ZigzagIterator(List<int> v1, List<int> v2) initializes the object with the two vectors v1 and v2.
boolean hasNext() returns true if the iterator still has elements, and false otherwise.
int next() returns the current element of the iterator and moves the iterator to the next element.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 124:
Given a string num that contains only digits and an integer target, return all possibilities to insert the binary operators '+', '-', and/or '*' between the digits of num so that the resultant expression evaluates to the target value.

Note that operands in the returned expressions should not contain leading zeros.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 125:
 Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 126:
  Design an iterator that supports the peek operation on an existing iterator in addition to the hasNext and the next operations.

Implement the PeekingIterator class:

PeekingIterator(Iterator<int> nums) Initializes the object with the given integer iterator iterator.
int next() Returns the next element in the array and moves the pointer to the next element.
boolean hasNext() Returns true if there are still elements in the array.
int peek() Returns the next element in the array without moving the pointer.
Note: Each language may have a different implementation of the constructor and Iterator, but they all support the int next() and boolean hasNext() functions.

 
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 127:
  Given the root of a binary search tree and a node p in it, return the in-order successor of that node in the BST. If the given node has no in-order successor in the tree, return null.

The successor of a node p is the node with the smallest key greater than p.val.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 128:
 You are given an m x n grid rooms initialized with these three possible values.

-1 A wall or an obstacle.
0 A gate.
INF Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 129:
 Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 130:
 The abbreviation of a word is a concatenation of its first letter, the number of characters between the first and last letter, and its last letter. If a word has only two characters, then it is an abbreviation of itself.

For example:

dog --> d1g because there is one letter between the first letter 'd' and the last letter 'g'.
internationalization --> i18n because there are 18 letters between the first letter 'i' and the last letter 'n'.
it --> it because any word with only two characters is an abbreviation of itself.
Implement the ValidWordAbbr class:

ValidWordAbbr(String[] dictionary) Initializes the object with a dictionary of words.
boolean isUnique(string word) Returns true if either of the following conditions are met (otherwise returns false):
There is no word in dictionary whose abbreviation is equal to word's abbreviation.
For any word in dictionary whose abbreviation is equal to word's abbreviation, that word and word are the same.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 131:
According to Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

The board is made up of an m x n grid of cells, where each cell has an initial state: live (represented by a 1) or dead (represented by a 0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

Any live cell with fewer than two live neighbors dies as if caused by under-population.
Any live cell with two or three live neighbors lives on to the next generation.
Any live cell with more than three live neighbors dies, as if by over-population.
Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the m x n grid board, return the next state.

 
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 132:
  Given a pattern and a string s, find if s follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

 
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 133:
 Given a pattern and a string s, return true if s matches the pattern.

A string s matches a pattern if there is some bijective mapping of single characters to strings such that if each character in pattern is replaced by the string it maps to, then the resulting string is s. A bijective mapping means that no two characters map to the same string, and no character maps to two different strings.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 134:
 You are playing the following Nim Game with your friend:

Initially, there is a heap of stones on the table.
You and your friend will alternate taking turns, and you go first.
On each turn, the person whose turn it is will remove 1 to 3 stones from the heap.
The one who removes the last stone is the winner.
Given n, the number of stones in the heap, return true if you can win the game assuming both you and your friend play optimally, otherwise return false.You are playing the following Nim Game with your friend:

Initially, there is a heap of stones on the table.
You and your friend will alternate taking turns, and you go first.
On each turn, the person whose turn it is will remove 1 to 3 stones from the heap.
The one who removes the last stone is the winner.
Given n, the number of stones in the heap, return true if you can win the game assuming both you and your friend play optimally, otherwise return false.
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
   #### Question 135:
You are playing a Flip Game with your friend.

You are given a string currentState that contains only '+' and '-'. You and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move, and therefore the other person will be the winner.

Return all possible states of the string currentState after one valid move. You may return the answer in any order. If there is no valid move, return an empty list [].

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 136:
You are playing a Flip Game with your friend.

You are given a string currentState that contains only '+' and '-'. You and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move, and therefore the other person will be the winner.

Return true if the starting player can guarantee a win, and false otherwise.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 137:
The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

For example, for arr = [2,3,4], the median is 3.
For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.
Implement the MedianFinder class:

MedianFinder() initializes the MedianFinder object.
void addNum(int num) adds the integer num from the data stream to the data structure.
double findMedian() returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.
   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 138:
 Given an m x n binary grid grid where each 1 marks the home of one friend, return the minimal total travel distance.

The total travel distance is the sum of the distances between the houses of the friends and the meeting point.

The distance is calculated using Manhattan Distance, where distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|.

 
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 139:
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 140:
Given the root of a binary tree, return the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path needs to be from parent to child (cannot be the reverse).

 
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 141:
 You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

The number of "bulls", which are digits in the guess that are in the correct position.
The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 142:
Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 143:
Given a string s that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return all the possible results. You may return the answer in any order.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 144:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 145:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 146:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 147:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 148:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 149:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 150:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 151:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 152:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 153:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 154:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 155:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 156:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 157:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 158:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 159:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 160:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 161:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 162:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 163:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 164:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 165:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   

  
  #### Question 166:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 167:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 168:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 169:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
   
  #### Question 170:
  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  
  
  
 
  
  
  
