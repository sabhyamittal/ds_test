#### Question 1.
Given a file and assume that you can only read the file using a given method read4, implement a method to read n characters.

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
  
<details>
<summary>code</summary>  
  
``` 
class Solution:
    def __init__(self):
        self.buffer = [None] * 4
        self.i = 4
        self.end = 4

    def read(self, buf: List[str], n: int) -> int:
        read = 0

        while self.load() and read < n:
            for _ in range(min(self.end - self.i, n - read)):
                buf[read] = self.buffer[self.i]
                read += 1
                self.i += 1
        return read

    def load(self):
        if self.i == 4 and self.end == 4:
            self.i = 0
            self.end = read4(self.buffer)
        return self.i < self.end
  
 ```
 </details>
  
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
<summary>code</summary>  
  
```
 class Solution(object):
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        left, right = 0, len(nums)
        
        if len(nums) == 1 or nums[0] > nums[1]:
            return 0
        if nums[-1] > nums[-2]:
            return right - 1 
        
        while left < right:
            mid = (left + right) // 2
            
            if nums[mid] > nums[mid - 1] and nums[mid] > nums[mid + 1]:
                return mid
            
            if nums[mid - 1] > nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        
        return left
    
  
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
<summary>code</summary> 
  
```
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        if len(nums)==1 or len(nums)==2:return abs(nums[0]-nums[len(nums)-1])
        else:
            nums.sort()
            j=1
            i=0
            maxx=-1
            while i<len(nums)-1 and j<len(nums):
                ans=abs(nums[i]-nums[j])
                i+=1
                j+=1
                if ans>maxx:maxx=ans
            return maxx 
  
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
<summary>code</summary>  
 
```
class Solution:
    def fractionToDecimal(self, numerator: int, denominator: int) -> str:
        neg = True if numerator/denominator < 0 else False
        numerator = -numerator if numerator < 0 else numerator
        denominator = -denominator if denominator < 0 else denominator
        out = str(numerator//denominator)
        if numerator % denominator:
            out += "."
        remainders = []
        quotients = []
        numerator %= denominator
        while numerator:
            numerator *= 10
            if str(numerator) in remainders:
                duplicateStart = remainders.index(str(numerator))
                out += "".join(quotients[:duplicateStart])
                out += "("+"".join(quotients[duplicateStart:])+")"
                return "-"+out if neg else out
            else:
                remainders.append(str(numerator))
                quotients.append(str(numerator // denominator))
                numerator %= denominator
        out += "".join(quotients)
        return "-"+out if neg else out
  
```  
</details>  
  
#### Question 11:
  
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number.
Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.  
                                                                                                         
<details>
<summary>code</summary>
  
 ```
 def twoSum(self, numbers: List[int], target: int) -> List[int]:
        n = len(numbers)
        l, r = 0, n - 1
        
        while (numbers[l] + numbers[r]) != target:
            if numbers[l] + numbers[r] > target:
                r -= 1
            else:
                l += 1
        
        return list((l + 1, r + 1)) 
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
  
<details>
<summary>code</summary>
  
  ```
  def convertToTitle(self, columnNumber: int) -> str:
        res = ""
        while(columnNumber):
            n = int(columnNumber % 26)
            n += (n == 0) * 26
            res = chr(64 + n) + res
            columnNumber = (columnNumber - n) // 26 
        return res
  
  ```
  </details>
  
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
 def trailingZeroes(self, n: int) -> int:
        
    # Calculate n!
    n_factorial = 1
    for i in range(2, n + 1):
        n_factorial *= i
    
    # Count how many 0's are on the end.
    zero_count = 0
    while n_factorial % 10 == 0:
        zero_count += 1
        n_factorial //= 10
        
    return zero_count
  
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
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator:

    def __init__(self, root: TreeNode):

        # Array containing all the nodes in the sorted order
        self.nodes_sorted = []

        # Pointer to the next smallest element in the BST
        self.index = -1

        # Call to flatten the input binary search tree
        self._inorder(root)

    def _inorder(self, root):
        if not root:
            return
        self._inorder(root.left)
        self.nodes_sorted.append(root.val)
        self._inorder(root.right)

    def next(self) -> int:
        """
        @return the next smallest number
        """
        self.index += 1
        return self.nodes_sorted[self.index]

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        return self.index + 1 < len(self.nodes_sorted)
                                                      
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
 class Solution(object):
    def calculateMinimumHP(self, dungeon):
        """
        :type dungeon: List[List[int]]
        :rtype: int
        """
        rows, cols = len(dungeon), len(dungeon[0])
        dp = [[float('inf')] * cols for _ in range(rows)]

        def get_min_health(currCell, nextRow, nextCol):
            if nextRow >= rows or nextCol >= cols:
                return float('inf')
            nextCell = dp[nextRow][nextCol]
            # hero needs at least 1 point to survive
            return max(1, nextCell - currCell)

        for row in reversed(range(rows)):
            for col in reversed(range(cols)):
                currCell = dungeon[row][col]

                right_health = get_min_health(currCell, row, col+1)
                down_health = get_min_health(currCell, row+1, col)
                next_health = min(right_health, down_health)

                if next_health != float('inf'):
                    min_health = next_health
                else:
                    min_health = 1 if currCell >= 0 else (1 - currCell)

                dp[row][col] = min_health

        return dp[0][0]
  
 ```
</details>
  
 #### Question 19:
Write an SQL query to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table,
report null instead.

Return the result table in any order.  
  
<details>
<summary>code in MYSQL</summary>
  
 ```
SELECT Person.firstName , Person.lastName ,Address.city, Address.state
FROM Person LEFT JOIN Address
ON Person.personId = Address.personId;
  
 ```
</details>
  
 #### Question 20:
Write an SQL query to report the second highest salary from the Employee table. If there is no second highest salary, the query should report null.

The query result format is in the following example. 
<details>
<summary>code</summary>
  
 ```
  with Temp as
    (select salary, dense_rank() over(order by salary desc) as rnk from Employee)
    select case when
           sum(rnk)<2 then
           salary=null
           else
           salary
           end        
     as SecondHighestSalary from Temp where rnk=2
                      
 ```
</details>
  
 #### Question 21:
Write an SQL query to report the nth highest salary from the Employee table. If there is no nth highest salary, the query should report null.

The query result format is in the following example.  
<details>
<summary>code</summary>
  
 ```
  CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
BEGIN
RETURN (

    select salary
    from
   ( select salary,
    Dense_rank() over (order by salary desc) as rnk
    from employee) x
    where Rnk=@N
    group by salary
    
);
END
  
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
select Score, dense_rank() over (order by Score desc) as Rank from Scores
order by Score desc
  
 ```
</details>
  
 #### Question 23:
Given a list of non-negative integers nums, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

   
<details>
<summary>code</summary>
  
 ```
  class LargerNumKey(str):
    def __lt__(x, y):
        return x+y > y+x
        
class Solution:
    def largestNumber(self, nums):
        largest_num = ''.join(sorted(map(str, nums), key=LargerNumKey))
        return '0' if largest_num[0] == '0' else largest_num
  
 ```
</details>
  
 #### Question 24:
Write an SQL query to find all numbers that appear at least three times consecutively.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
SELECT DISTINCT
    l1.Num AS ConsecutiveNums
FROM
    Logs l1,
    Logs l2,
    Logs l3
WHERE
    l1.Id = l2.Id - 1
    AND l2.Id = l3.Id - 1
    AND l1.Num = l2.Num
    AND l2.Num = l3.Num
;
  
 ```
</details>
  
 #### Question 25:
Write an SQL query to find the employees who earn more than their managers.

Return the result table in any order. 
  
<details>
<summary>code</summary>
  
 ```
 1.
  SELECT
    *
FROM
    Employee AS a,
    Employee AS b
WHERE
    a.ManagerId = b.Id
        AND a.Salary > b.Salary
;
  2.MYSQL
SELECT
    a.Name AS 'Employee'
FROM
    Employee AS a,
    Employee AS b
WHERE
    a.ManagerId = b.Id
        AND a.Salary > b.Salary
;  
  3.Using JOIN clause
  SELECT
     a.NAME AS Employee
FROM Employee AS a JOIN Employee AS b
     ON a.ManagerId = b.Id
     AND a.Salary > b.Salary
;
  
 ```
</details>
  
 #### Question 26:
Write an SQL query to report all the duplicate emails.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
  select Email, count(Email) as num
from Person
group by Email;
| Email   | num |
|---------|-----|
| a@b.com | 2   |
| c@d.com | 1   |
Taking this as a temporary table, we can get a solution as below.

select Email from
(
  select Email, count(Email) as num
  from Person
  group by Email
) as statistic
where num > 1
;
  MySQL

select Email
from Person
group by Email
having count(Email) > 1;
  
 ```
</details>
  
 #### Question 27:
Write an SQL query to report all customers who never order anything.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
  select customerid from orders;
Then, we can use NOT IN to query the customers who are not in this list.

MySQL

select customers.name as 'Customers'
from customers
where customers.id not in
(
    select customerid from orders
);
  
 ```
</details>
  
 #### Question 28:
Write an SQL query to find employees who have the highest salary in each of the departments.

Return the result table in any order.  
  
<details>
<summary>code</summary>
  
 ```
 MySQL

SELECT
    Department.name AS 'Department',
    Employee.name AS 'Employee',
    Salary
FROM
    Employee
        JOIN
    Department ON Employee.DepartmentId = Department.Id
WHERE
    (Employee.DepartmentId , Salary) IN
    (   SELECT
            DepartmentId, MAX(Salary)
        FROM
            Employee
        GROUP BY DepartmentId
    )
;
| Department | Employee | Salary |
|------------|----------|--------|
| Sales      | Henry    | 80000  |
| IT         | Max      | 90000  |
  
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
  MySQL

SELECT
    d.Name AS 'Department', e1.Name AS 'Employee', e1.Salary
FROM
    Employee e1
        JOIN
    Department d ON e1.DepartmentId = d.Id
WHERE
    3 > (SELECT
            COUNT(DISTINCT e2.Salary)
        FROM
            Employee e2
        WHERE
            e2.Salary > e1.Salary
                AND e1.DepartmentId = e2.DepartmentId
        )
;
| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Joe      | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |
| IT         | Max      | 90000  |
| IT         | Randy    | 85000  |
  
 ```
</details> 

#### Question 30:
Given a character array s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by a single space.

Your code must solve the problem in-place, i.e. without allocating extra space.  
<details>
<summary>code</summary>
  
 ```
  class Solution:
    def reverse(self, l: list, left: int, right: int) -> None:
        while left < right:
            l[left], l[right] = l[right], l[left]
            left, right = left + 1, right - 1
            
    def reverse_each_word(self, l: list) -> None:
        n = len(l)
        start = end = 0
        
        while start < n:
            # go to the end of the word
            while end < n and l[end] != ' ':
                end += 1
            # reverse the word
            self.reverse(l, start, end - 1)
            # move to the next word
            start = end + 1
            end += 1
            
    def reverseWords(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        # reverse the whole string
        self.reverse(s, 0, len(s) - 1)
        
        # reverse each word
        self.reverse_each_word(s)
  
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
  class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        L, n = 10, len(s)     
        seen, output = set(), set()

        # iterate over all sequences of length L
        for start in range(n - L + 1):
            tmp = s[start:start + L]
            if tmp in seen:
                output.add(tmp[:])
            seen.add(tmp)
        return output
  
 ```
</details> 
  
  #### Question 32:
You are given an integer array prices where prices[i] is the price of a given stock on the ith day, and an integer k.

Find the maximum profit you can achieve. You may complete at most k transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        n = len(prices)

        # solve special cases
        if not prices or k==0:
            return 0

        if 2*k > n:
            res = 0
            for i, j in zip(prices[1:], prices[:-1]):
                res += max(0, i - j)
            return res

        # dp[i][used_k][ishold] = balance
        # ishold: 0 nothold, 1 hold
        dp = [[[-math.inf]*2 for _ in range(k+1)] for _ in range(n)]

        # set starting value
        dp[0][0][0] = 0
        dp[0][1][1] = -prices[0]

        # fill the array
        for i in range(1, n):
            for j in range(k+1):
                # transition equation
                dp[i][j][0] = max(dp[i-1][j][0], dp[i-1][j][1]+prices[i])
                # you can't hold stock without any transaction
                if j > 0:
                    dp[i][j][1] = max(dp[i-1][j][1], dp[i-1][j-1][0]-prices[i])

        res = max(dp[n-1][j][0] for j in range(k+1))
        return res
  
 ```
</details> 
  
  #### Question 33:
Given an array, rotate the array to the right by k steps, where k is non-negative.  

<details>
<summary>code</summary>
  
 ```
 class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        # speed up the rotation
        k %= len(nums)

        for i in range(k):
            previous = nums[-1]
            for j in range(len(nums)):
                nums[j], previous = previous, nums[j]
  
 ```
</details> 
  
  #### Question 34:
Reverse bits of a given 32 bits unsigned integer.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):
        ret, power = 0, 31
        while n:
            ret += (n & 1) << power
            n = n >> 1
            power -= 1
        return ret
  
 ```
</details> 
  
  #### Question 35:
Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the Hamming weight).  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def hammingWeight(self, n: int) -> int:
        return len([x for x in bin(n)[2:] if x is '1'])
  
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
 cat words.txt | sed 's/\ /\n/g' | sort | uniq -c |sort -r | awk '{print $2,$1}'
  
 ```
</details> 
  
  #### Question 37:
Given a text file file.txt that contains a list of phone numbers (one per line), write a one-liner bash script to print all valid phone numbers.

You may assume that a valid phone number must appear in one of the following two formats: (xxx) xxx-xxxx or xxx-xxx-xxxx. (x means a digit)

You may also assume each line in the text file must not contain leading or trailing white spaces.  
  
<details>
<summary>code</summary>
  
 ```
  egrep '^[0-9]{3}-[0-9]{3}-[0-9]{4}$|^\([0-9]{3}\)\s[0-9]{3}-[0-9]{4}$' file.txt
  
 ```
</details> 
  
  #### Question 38:
Given a text file file.txt, transpose its content.

You may assume that each row has the same number of columns, and each field is separated by the ' ' character.  
<details>
<summary>code</summary>
  
 ```
  seq "$(awk '{print NF}' file.txt | head -n 1)" |
	xargs -r -I {} sh -c "awk '{print \${}}' file.txt | xargs -r"
  
 ```
</details> 
  
  #### Question 39:
Given a text file file.txt, print just the 10th line of the file.  
<details>
<summary>code</summary>
  
 ```
 f=file.txt line=10; [ "`wc -l $f | cut -f 1 -d ' '`" -ge "$line" ] && head -$line $f | tail -1
  
 ```
</details> 
  
  #### Question 40:
Write an SQL query to delete all the duplicate emails, keeping only one unique email with the smallest id.

Return the result table in any order.  
<details>
<summary>code</summary>
  
 ```
  SELECT p1.*
FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email
;
Then we need to find the bigger id having same email address with other records. So we can add a new condition to the WHERE clause like this.

SELECT p1.*
FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id
;
As we already get the records to be deleted, we can alter this statement to DELETE in the end.

MySQL

DELETE p1 FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > 
  
 ```
</details> 
  
  #### Question 41:
Write an SQL query to find all dates' Id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

<details>
<summary>code</summary>
  
 ```
  MySQL

SELECT
    weather.id AS 'Id'
FROM
    weather
        JOIN
    weather w ON DATEDIFF(weather.recordDate, w.recordDate) = 1
        AND weather.Temperature > w.Temperature
;
  
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
 class Solution:
    
    def __init__(self):
        self.memo = {}
    
    def rob(self, nums: List[int]) -> int:
        
        self.memo = {}
        
        return self.robFrom(0, nums)
    
    def robFrom(self, i, nums):
        
        
        # No more houses left to examine.
        if i >= len(nums):
            return 0
        
        # Return cached value.
        if i in self.memo:
            return self.memo[i]
        
        # Recursive relation evaluation to get the optimal answer.
        ans = max(self.robFrom(i + 1, nums), self.robFrom(i + 2, nums) + nums[i])
        
        # Cache for future use.
        self.memo[i] = ans
        return ans
  
 ```
</details> 
  
  #### Question 43:
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.  
<details>
<summary>code</summary>
  
 ```
  class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        
        next_level = deque([root,])
        rightside = []
        
        while next_level:
            # prepare for the next level
            curr_level = next_level
            next_level = deque()

            while curr_level:
                node = curr_level.popleft()
                    
                # add child nodes of the current level
                # in the queue for the next level
                if node.left:
                    next_level.append(node.left)
                if node.right:
                    next_level.append(node.right)
            
            # The current level is finished.
            # Its last element is the rightmost one.
            rightside.append(node.val)
        
        return rightside
  
 ```
</details> 
  
  #### Question 44:
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
     
	def numIslands(self, grid: List[List[str]]) -> int:
	
        if not grid:
            return 0
        rows, cols=len(grid), len(grid[0])
        islands=0
        
        for i in range(rows):
            for j in range(cols):
                if grid[i][j]=='1':
                    islands+=1
                    self.explore(grid, i , j)
        return islands           
     
     
    def explore(self, grid, i, j):
	
	# Mark this point as '0', so that it does not count again.
	
        grid[i][j]='0'
        rows, cols=len(grid), len(grid[0])

        if (i+1<rows and grid[i+1][j]=='1'):
            self.explore(grid, i+1, j)
        if (i-1>=0 and grid[i-1][j]=='1'):
            self.explore(grid, i-1, j)
        if (j+1<cols and grid[i][j+1]=='1'):
            self.explore(grid, i, j+1)
        if (j-1>=0 and grid[i][j-1]=='1'):
            self.explore(grid, i, j-1)
 
  
 ```
</details> 
  
  #### Question 45:
Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        shift = 0   
        # find the common 1-bits
        while m < n:
            m = m >> 1
            n = n >> 1
            shift += 1
        return m << shift 
  
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
 def isHappy(self, n: int) -> bool:

    def get_next(n):
        total_sum = 0
        while n > 0:
            n, digit = divmod(n, 10)
            total_sum += digit ** 2
        return total_sum

    seen = set()
    while n != 1 and n not in seen:
        seen.add(n)
        n = get_next(n)

    return n == 1 
  
 ```
</details> 
  
  #### Question 47:
Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.  
  
<details>
<summary>code</summary>
  
 ```
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        sentinel = ListNode(0)
        sentinel.next = head
        
        prev, curr = sentinel, head
        while curr:
            if curr.val == val:
                prev.next = curr.next
            else:
                prev = curr
            curr = curr.next
        
        return sentinel.next  
  
 ```
</details> 
  
  #### Question 48:
Given an integer n, return the number of prime numbers that are strictly less than n.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def countPrimes(self, n: int) -> int:
        if n <= 2:
            return 0
        
        numbers = {}
        for p in range(2, int(sqrt(n)) + 1):
            if p not in numbers:
                for multiple in range(p*p, n, p):
                    numbers[multiple] = 1
        
        # Exclude "1" and the number "n" itself.
        return n - len(numbers) - 2 
  
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
 class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        
        mapping_s_t = {}
        mapping_t_s = {}
        
        for c1, c2 in zip(s, t):
            
            # Case 1: No mapping exists in either of the dictionaries
            if (c1 not in mapping_s_t) and (c2 not in mapping_t_s):
                mapping_s_t[c1] = c2
                mapping_t_s[c2] = c1
            
            # Case 2: Ether mapping doesn't exist in one of the dictionaries or Mapping exists and
            # it doesn't match in either of the dictionaries or both            
            elif mapping_s_t.get(c1) != c2 or mapping_t_s.get(c2) != c1:
                return False
            
        return True 
  
 ```
</details> 
  
  #### Question 50:
Given the head of a singly linked list, reverse the list, and return the reversed list.  
<details>
<summary>code</summary>
  
 ```
  class Solution(object):        
    def reverseList(self, head):  # Iterative
        prev, curr = None, head
        while curr:
            curr.next, prev, curr = prev, curr, curr.next
        return prev
        
    def reverseList_v1(self, head):  # Recursive
        """
        :type head: ListNode
        :rtype: ListNode
        """     
        if not head or not head.next:
            return head
        p = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return p 
  
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
 class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        from collections import defaultdict
        courseDict = defaultdict(list)

        for relation in prerequisites:
            nextCourse, prevCourse = relation[0], relation[1]
            courseDict[prevCourse].append(nextCourse)

        path = [False] * numCourses
        for currCourse in range(numCourses):
            if self.isCyclic(currCourse, courseDict, path):
                return False
        return True


    def isCyclic(self, currCourse, courseDict, path):
        """
        backtracking method to check that no cycle would be formed starting from currCourse
        """
        if path[currCourse]:
            # come across a previously visited node, i.e. detect the cycle
            return True

        # before backtracking, mark the node in the path
        path[currCourse] = True

        # backtracking
        ret = False
        for child in courseDict[currCourse]:
            ret = self.isCyclic(child, courseDict, path)
            if ret: break

        # after backtracking, remove the node from the path
        path[currCourse] = False
        return ret 
  
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
 def __init__(self):
    self.trie = {} # Setting try to dictionary
def insert(self, word: str) -> None:
    t = self.trie # Setting t to the dictionary which we just declared
    for w in word:
        if w not in t: # The word will be inserted if it is not in try
            t[w] = {}
        t = t[w]
    t["end"] = True
    # If the word is lets say "apple" then it will be inserted in the following way: {a:{p:{p:{l:{{l:{e:{end: True}}}}}}}}
    # The key end flag is set to true indicates that the word actually exists
    # If ther is no end flag then it means that the word is just a prefix

def search(self, word: str) -> bool:
    t = self.trie
    # Here I will check the entire word letter by letter. 
    for w in word:
        if w in t:
            t = t[w] # If the letter is found then we will set the trie to that key which means that if we are searching for apple and if our loop is on l letter of the word apple then at that time t = {l:{e:{end:True}}}
        else:
            return False
    return "end" in t
# The value of key end will be returned which is True

def startsWith(self, prefix: str) -> bool:
    t  = self.trie
    # For checking the prefix I will directly check if the letter for the word is in trie. If it is in the trie then setting the value of the letter equal to trie everytime. For example if we are checking for "app"
    for w in prefix:
        if w in t:
            t = t[w] # apple is already in the trie therefore the loop will run till app and if any other letter which is not in the trie  encountered then it will directly return False.
        else:
            return False
    return True 
  
 ```
</details> 
  
  #### Question 53:
 Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] 
  of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

  
<details>
<summary>code</summary>
  
 ```
 total = 0
    res = [-1,-1]
    resLen = float('inf')
    l = 0
    for r in range(len(nums)):
        
        num = nums[r]
        
        total += num
        
        while total >= target:
            if (r-l+1) < resLen:
                resLen = r-l+1
                res = [l, r]
            
            total -= nums[l]
            
            l+=1
    return resLen if resLen != float('inf') else 0 
  
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
 from collections import defaultdict
class Solution:

    WHITE = 1
    GRAY = 2
    BLACK = 3

    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """

        # Create the adjacency list representation of the graph
        adj_list = defaultdict(list)

        # A pair [a, b] in the input represents edge from b --> a
        for dest, src in prerequisites:
            adj_list[src].append(dest)

        topological_sorted_order = []
        is_possible = True

        # By default all vertces are WHITE
        color = {k: Solution.WHITE for k in range(numCourses)}
        def dfs(node):
            nonlocal is_possible

            # Don't recurse further if we found a cycle already
            if not is_possible:
                return

            # Start the recursion
            color[node] = Solution.GRAY

            # Traverse on neighboring vertices
            if node in adj_list:
                for neighbor in adj_list[node]:
                    if color[neighbor] == Solution.WHITE:
                        dfs(neighbor)
                    elif color[neighbor] == Solution.GRAY:
                         # An edge to a GRAY vertex represents a cycle
                        is_possible = False

            # Recursion ends. We mark it as black
            color[node] = Solution.BLACK
            topological_sorted_order.append(node)

        for vertex in range(numCourses):
            # If the node is unprocessed, then call dfs on it.
            if color[vertex] == Solution.WHITE:
                dfs(vertex)

        return topological_sorted_order[::-1] if is_possible else [] 
  
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
 class WordDictionary:
    def __init__(self):
        self.d = defaultdict(set)


    def addWord(self, word: str) -> None:
        self.d[len(word)].add(word)


    def search(self, word: str) -> bool:
        m = len(word)
        for dict_word in self.d[m]:
            i = 0
            while i < m and (dict_word[i] == word[i] or word[i] == '.'):
                i += 1
            if i == m:
                return True
        return False 
  
 ```
</details> 
  
  #### Question 56:
Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. 
The same letter cell may not be used more than once in a word.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        WORD_KEY = '$'
        
        trie = {}
        for word in words:
            node = trie
            for letter in word:
                # retrieve the next node; If not found, create a empty node.
                node = node.setdefault(letter, {})
            # mark the existence of a word in trie node
            node[WORD_KEY] = word
        
        rowNum = len(board)
        colNum = len(board[0])
        
        matchedWords = []
        
        def backtracking(row, col, parent):    
            
            letter = board[row][col]
            currNode = parent[letter]
            
            # check if we find a match of word
            word_match = currNode.pop(WORD_KEY, False)
            if word_match:
                # also we removed the matched word to avoid duplicates,
                #   as well as avoiding using set() for results.
                matchedWords.append(word_match)
            
            # Before the EXPLORATION, mark the cell as visited 
            board[row][col] = '#'
            
            # Explore the neighbors in 4 directions, i.e. up, right, down, left
            for (rowOffset, colOffset) in [(-1, 0), (0, 1), (1, 0), (0, -1)]:
                newRow, newCol = row + rowOffset, col + colOffset     
                if newRow < 0 or newRow >= rowNum or newCol < 0 or newCol >= colNum:
                    continue
                if not board[newRow][newCol] in currNode:
                    continue
                backtracking(newRow, newCol, currNode)
        
            # End of EXPLORATION, we restore the cell
            board[row][col] = letter
        
            # Optimization: incrementally remove the matched leaf node in Trie.
            if not currNode:
                parent.pop(letter)

        for row in range(rowNum):
            for col in range(colNum):
                # starting from each of the cells
                if board[row][col] in trie:
                    backtracking(row, col, trie)
        
        return matchedWords     
  
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
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 0 or nums is None:
            return 0

        if len(nums) == 1:
            return nums[0]

        return max(self.rob_simple(nums[:-1]), self.rob_simple(nums[1:]))

    def rob_simple(self, nums: List[int]) -> int:
        t1 = 0
        t2 = 0
        for current in nums:
            temp = t1
            t1 = max(current + t2, t1)
            t2 = temp

        return t1  
  
 ```
</details> 
  
  #### Question 58:
You are given a string s. You can convert s to a palindrome by adding characters in front of it.

Return the shortest palindrome you can find by performing this transformation.  
Using Hashing:  
<details>
<summary>code</summary>
  
 ```
class Hasher:
    MAX = 50002
    MOD = 1000000007
    BASE = 1331
    
    def __init__(self, n):
        Hasher.MAX = n + 2
        self.storage = [0 for _ in range(Hasher.MAX)]
        self.precompute()
    
    def precompute(self):
        self.storage[0] = 1
        for i in range(1, Hasher.MAX):
            self.storage[i] = (self.storage[i-1] * Hasher.BASE) % Hasher.MOD
    
    def populateHash(self, H, s):
        H[0] = 0
        for i, ch in enumerate(s):
            H[i+1] = (H[i] * Hasher.BASE + ord(ch)) % Hasher.MOD
    
    def getHash(self, s):
        hashValue = 0
        for i, ch in enumerate(s):
            hashValue = (hashValue * Hasher.BASE + ord(ch)) % Hasher.MOD
        return hashValue
    
    def getHash(self, H, l, r):
        MOD = Hasher.MOD
        return (H[r] - (H[l-1] * self.storage[r-l+1]) % MOD + MOD) % MOD
        

class Solution:
    def shortestPalindrome(self, s: str) -> str:
        n = len(s)

        hasher = Hasher(n)
        H1 = [0 for _ in range(hasher.MAX)]
        H2 = [0 for _ in range(hasher.MAX)]
        
        hasher.populateHash(H1, s)
        hasher.populateHash(H2, s[::-1])
        
        idx = 0
        for i in range(n):
            if H1[i+1] == hasher.getHash(H2, n - i, n):
                idx = i

        return s[idx+1:][::-1] + s  
  
 ```
</details> 
  
  #### Question 59:
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.  
<details>
<summary>code</summary>
  
 ```
class Solution:
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        return heapq.nlargest(k, nums)[-1]  
  
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
 class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        results = []
        def backtrack(remain, comb, next_start):
            if remain == 0 and len(comb) == k:
                # make a copy of current combination
                # Otherwise the combination would be reverted in other branch of backtracking.
                results.append(list(comb))
                return
            elif remain < 0 or len(comb) == k:
                # exceed the scope, no need to explore further.
                return

            # Iterate through the reduced list of candidates.
            for i in range(next_start, 9):
                comb.append(i+1)
                backtrack(remain-i-1, comb, i+1)
                # backtrack the current choice
                comb.pop()

        backtrack(n, [], 0)

        return results 
  
 ```
</details> 
  
  #### Question 61:
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

   
<details>
<summary>code</summary>
  
 ```
 Python Solution Using Dictionary

class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        hash={}
        flag=0
        for i in nums:
            hash[i]=0
            
        for i in nums:
            hash[i]+=1
            
        for i in nums:
            if hash[i]>1:
                flag=1
                break
        return bool(flag)    
	
python solution using set

class Solution:
    # @param {integer[]} nums
    # @return {boolean}
    def containsDuplicate(self, nums):
        return (len(nums) >len(set(nums))) 
  
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
 class Solution:
    def getSkyline(self, buildings: 'List[List[int]]') -> 'List[List[int]]':
        """
        Divide-and-conquer algorithm to solve skyline problem,
        which is similar with the merge sort algorithm.
        """
        n = len(buildings)
        # The base cases
        if n == 0:
            return []
        if n == 1:
            x_start, x_end, y = buildings[0]
            return [[x_start, y], [x_end, 0]]

        # If there is more than one building,
        # recursively divide the input into two subproblems.
        left_skyline = self.getSkyline(buildings[: n // 2])
        right_skyline = self.getSkyline(buildings[n // 2 :])

        # Merge the results of subproblem together.
        return self.merge_skylines(left_skyline, right_skyline)

    def merge_skylines(self, left, right):
        """
        Merge two skylines together.
        """
        def update_output(x, y):
            """
            Update the final output with the new element.
            """
            # if skyline change is not vertical -
            # add the new point
            if not output or output[-1][0] != x:
                output.append([x, y])
            # if skyline change is vertical -
            # update the last point
            else:
                output[-1][1] = y

        def append_skyline(p, lst, n, y, curr_y):
            """
            Append the rest of the skyline elements with indice (p, n)
            to the final output.
            """
            while p < n:
                x, y = lst[p]
                p += 1
                if curr_y != y:
                    update_output(x, y)
                    curr_y = y

        n_l, n_r = len(left), len(right)
        p_l = p_r = 0
        curr_y  = left_y = right_y = 0
        output = []

        # while we're in the region where both skylines are present
        while p_l < n_l and p_r < n_r:
            point_l, point_r = left[p_l], right[p_r]
            # pick up the smallest x
            if point_l[0] < point_r[0]:
                x, left_y = point_l
                p_l += 1
            else:
                x, right_y = point_r
                p_r += 1
            # max height (i.e. y) between both skylines
            max_y = max(left_y, right_y)
            # if there is a skyline change
            if curr_y != max_y:
                update_output(x, max_y)
                curr_y = max_y

        # there is only left skyline
        append_skyline(p_l, left, n_l, left_y, curr_y)

        # there is only right skyline
        append_skyline(p_r, right, n_r, right_y, curr_y)

        return output 
  
 ```
</details> 
  
  #### Question 63:
 Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k. 
<details>
<summary>code</summary>
  
 ```
 def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
    nums_length = len(nums)
    if nums_length == len(set(nums)):
        return False
    else:
        for i in range(0, nums_length):
            for j in range(i+1, nums_length):
                if nums[i] == nums[j] and abs(i-j) <= k:
                    return True

        return False             
              
 ```
</details> 
  
  #### Question 64:
Given an integer array nums and two integers k and t, return true if there are two distinct indices i and j in the array 
  such that abs(nums[i] - nums[j]) <= t and abs(i - j) <= k.  
<details>
<summary>code</summary>
  
 ```
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], k: int, t: int) -> bool:
        bucket={}## key: index of bucket, val:elements within bucket, range for each bucket is t+1
        bucket_size=t+1
        for i,n in enumerate(nums):
            bucket_index=n//bucket_size
            if bucket_index not in bucket:
                bucket[bucket_index]=[i]
            else:
                if abs(bucket[bucket_index][-1]-i)<=k:
                    return True
                bucket[bucket_index].append(i)
            ## Check neighbor buckets
            if bucket_index-1 in bucket:
                last_index=bucket[bucket_index-1][-1]
                if abs(last_index-i)<=k and abs(nums[last_index]-nums[i])<=t:
                    return True
            if bucket_index+1 in bucket:
                last_index=bucket[bucket_index+1][-1]
                if abs(last_index-i)<=k and abs(nums[last_index]-nums[i])<=t:
                    return True
        return False
              
 ```
</details> 
  
  #### Question 65:
Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def maximalSquare(self, M):
        m, n, ans = len(M), len(M[0]), 0
        def get_max_square_len(row, col):
            all_ones_row_len, sq_len, i, j = min(m-row, n-col), 0, 0, 0
            while i < all_ones_row_len:
                j = 0
                while j < all_ones_row_len and M[i+row][j+col] != '0': 
                    j += 1
                all_ones_row_len = j
                sq_len = min(all_ones_row_len, i := i + 1)
            return sq_len
        
        for row in range(m):
            for col in range(n):
                ans = max(ans, get_max_square_len(row, col))
        return ans * ans
  
Time Complexity : O(MN*min(M,N)2)
Space Complexity : O(1) 
  
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
 class Solution:
    def compute_depth(self, node: TreeNode) -> int:
        """
        Return tree depth in O(d) time.
        """
        d = 0
        while node.left:
            node = node.left
            d += 1
        return d

    def exists(self, idx: int, d: int, node: TreeNode) -> bool:
        """
        Last level nodes are enumerated from 0 to 2**d - 1 (left -> right).
        Return True if last level node idx exists. 
        Binary search with O(d) complexity.
        """
        left, right = 0, 2**d - 1
        for _ in range(d):
            pivot = left + (right - left) // 2
            if idx <= pivot:
                node = node.left
                right = pivot
            else:
                node = node.right
                left = pivot + 1
        return node is not None
        
    def countNodes(self, root: TreeNode) -> int:
        # if the tree is empty
        if not root:
            return 0
        
        d = self.compute_depth(root)
        # if the tree contains 1 node
        if d == 0:
            return 1
        
        # Last level nodes are enumerated from 0 to 2**d - 1 (left -> right).
        # Perform binary search to check how many nodes exist.
        left, right = 1, 2**d - 1
        while left <= right:
            pivot = left + (right - left) // 2
            if self.exists(pivot, d, root):
                left = pivot + 1
            else:
                right = pivot - 1
        
        # The tree contains 2**d - 1 nodes on the first (d - 1) levels
        # and left nodes on the last level.
        return (2**d - 1) + left 
  
 ```
</details> 
  
  #### Question 67:
Given the coordinates of two rectilinear rectangles in a 2D plane, return the total area covered by the two rectangles.

The first rectangle is defined by its bottom-left corner (ax1, ay1) and its top-right corner (ax2, ay2).

The second rectangle is defined by its bottom-left corner (bx1, by1) and its top-right corner (bx2, by2).  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def computeArea(self, ax1: int, ay1: int, ax2: int, ay2: int, bx1: int, by1: int, bx2: int, by2: int) -> int:
        if (ax2 >= bx1 and ay2 >= by1) and not (by2 < ay1 or bx2 < ax1):
            cx1 = max(ax1, bx1)
            cy1 = max(ay1, by1)
            cx2 = min(ax2, bx2)
            cy2 = min(ay2, by2)
            sharedArea = (cx2 - cx1) * (cy2 - cy1)
        else:
            sharedArea = 0
        return (((ax2 - ax1) * (ay2 - ay1)) + ((bx2 - bx1) * (by2 - by1)) - sharedArea) 
  
 ```
</details> 
  
  #### Question 68:
Given a string s representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval() 
<details>
<summary>code</summary>
  
 ```
class Solution:

    def evaluate_expr(self, stack):
        
        # If stack is empty or the expression starts with
        # a symbol, then append 0 to the stack.
        # i.e. [1, '-', 2, '-'] becomes [1, '-', 2, '-', 0]
        if not stack or type(stack[-1]) == str:
            stack.append(0)
            
        res = stack.pop()

        # Evaluate the expression till we get corresponding ')'
        while stack and stack[-1] != ')':
            sign = stack.pop()
            if sign == '+':
                res += stack.pop()
            else:
                res -= stack.pop()
        return res       

    def calculate(self, s: str) -> int:

        stack = []
        n, operand = 0, 0

        for i in range(len(s) - 1, -1, -1):
            ch = s[i]

            if ch.isdigit():

                # Forming the operand - in reverse order.
                operand = (10**n * int(ch)) + operand
                n += 1

            elif ch != " ":
                if n:
                    # Save the operand on the stack
                    # As we encounter some non-digit.
                    stack.append(operand)
                    n, operand = 0, 0

                if ch == '(':         
                    res = self.evaluate_expr(stack)
                    stack.pop()        

                    # Append the evaluated result to the stack.
                    # This result could be of a sub-expression within the parenthesis.
                    stack.append(res)

                # For other non-digits just push onto the stack.
                else:
                    stack.append(ch)

        # Push the last operand to stack, if any.
        if n:
            stack.append(operand)

        # Evaluate any left overs in the stack.
        return self.evaluate_expr(stack) 
  
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
class MyStack:

  def __init__(self):
    self._queue = []

  def push(self, x: int) -> None:
    # queue push to back: list.append()
    self._queue.append(x)
    return
        
  def pop(self) -> int:
    # queue pop from front: list.pop(0)
    for i in range(len(self._queue)-1):
      self._queue.append(self._queue.pop(0))
    return self._queue.pop(0)

  def top(self) -> int:
    # queue peek from front: list[0]
    holder = None
    for i in range(len(self._queue)-1):
      self._queue.append(self._queue.pop(0))
    holder = self._queue[0]
    self._queue.append(self._queue.pop(0))
    return holder

  def empty(self) -> bool:
    # queue get length: len(list)
    return len(self._queue) == 0
	```  
  
 ```
</details> 
  
  #### Question 70:
Given the root of a binary tree, invert the tree, and return its root.  
<details>
<summary>code</summary>
  
 ```
def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
     if root:
         root.left, root.right = root.right, root.left
         self.invertTree(root.left)
         self.invertTree(root.right)  
     return root    
  
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
 class Solution:
    def calculate(self, s):
        def precedence(c):
            return c == '*' or c == '/'
        def toPostfix(s):
            op, post = deque(), ''
            for c in s:
                if c == ' ': continue
                elif c.isdigit(): post += c
                else:
                    post += '|'
                    while op and precedence(c) <= precedence(op[-1]):
                        post += op.pop()
                    op.append(c)
                    
            return post + '|' + ''.join(reversed(op))
        
        s, num, i = toPostfix(s), deque(), 0
        while i < len(s):
            if s[i].isdigit():
                j = s.find('|', i+1)
                num.append(int(s[i:j]))
                i = j
            else:
                num1, num2 = num.pop(), num.pop()
                if   s[i] == '*': num.append(num2 * num1)
                elif s[i] == '/': num.append(num2 // num1)
                elif s[i] == '+': num.append(num2 + num1)
                elif s[i] == '-': num.append(num2 - num1)
            i += 1

        return num.pop() 
  
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
 class Solution(object):
    def summaryRanges(self, nums):
        """
        :type nums: List[int]
        :rtype: List[str]
        """
        L = 0
        R = 0
        s = []
        if len(nums) == 1:
            s.append(str(nums[L]))
        for i in range(1, len(nums)):
            if nums[i]-nums[i-1] == 1:
                R += 1
                if i == len(nums)-1:
                    s.append("%d->%d"%(nums[L],nums[R]))
            else:
                if L == R:
                    s.append(str(nums[L]))
                else:
                    s.append("%d->%d"%(nums[L],nums[R]))
                if i == len(nums)-1:
                    s.append(str(nums[i]))
                else:
                    L = i
                    R = i
        return s 
  
 ```
</details> 
  
  #### Question 73:
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.  
<details>
<summary>code</summary>
  
 ```
class Solution:

    def majorityElement(self, nums):
        if not nums:
            return []
        
        # 1st pass
        count1, count2, candidate1, candidate2 = 0, 0, None, None
        for n in nums:
            if candidate1 == n:
                count1 += 1
            elif candidate2 == n:
                count2 += 1
            elif count1 == 0:
                candidate1 = n
                count1 += 1
            elif count2 == 0:
                candidate2 = n
                count2 += 1
            else:
                count1 -= 1
                count2 -= 1
        
        # 2nd pass
        result = []
        for c in [candidate1, candidate2]:
            if nums.count(c) > len(nums)//3:
                result.append(c)

        return result  
  
 ```
</details> 
  
  #### Question 74:
  Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.
<details>
<summary>code</summary>
  
 ```
class Solution:
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        stack = []
        
        while True:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            k -= 1
            if not k:
                return root.val
            root = root.right  
  
 ```
</details> 
  
  #### Question 75:
 Given an integer n, return true if it is a power of two. Otherwise, return false.

An integer n is a power of two, if there exists an integer x such that n == 2x. 
<details>
<summary>code</summary>
  
 ```
 class Solution(object):
    def isPowerOfTwo(self, n):
        if n == 0:
            return False
        return n & (-n) == n 
  
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
class Stack:
    def __init__(self, val, prev=None):
        self.val = val
        self.prev = prev

class MyQueue:
    def __init__(self):
        self.front = None
        self.back = None

    def push(self, x: int) -> None:
        if self.back == None:
            self.back = Stack(x, None)
            self.front = self.back
        else:
            self.back.prev = Stack(x, None)
            self.back = self.back.prev

    def pop(self) -> int:
        val = self.front.val
        self.front = self.front.prev

        if self.front == None:
            self.back = None
        
        return val
            

    def peek(self) -> int:
        return self.front.val

    def empty(self) -> bool:
        return self.front == None  
  
 ```
</details> 
  
  #### Question 77:
Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def countDigitOne(self, n: int) -> int:
        
        #O(logn) mathematical solution
        #intervals of new 1s: 0-9, 10-99, 100-999, 1000,9999... 
            #each interval yields 1,10,100,etc. new '1's respectively
		#first and foremost, we want to check how many of each interval repeats 
        #conditions for FULL yield when curr%upper bound+1: 1 <=, 19 <=, 199 <=...
        #conditions for PARTIAL yielf when curr%upper bound+1: None, 10 <= < 19,  100 <= < 199, 1000 <= < 1999 ... 
        
        ans = 0
        for i in range(len(str(n))):
            curr = 10**(i+1)
            hi,lo = int('1'+'9'*i), int('1'+'0'*i)
            ans += (n//curr) * 10**i
            if (pot:=n%curr) >= hi: ans += 10**i
            elif lo <= pot < hi: 
                ans += pot - lo + 1
        return ans 
  
 ```
</details> 
  
  #### Question 78:
Given the head of a singly linked list, return true if it is a palindrome. 
<details>
<summary>code</summary>
  
 ```
def isPalindrome(self, head: ListNode) -> bool:
    vals = []
    current_node = head
    while current_node is not None:
        vals.append(current_node.val)
        current_node = current_node.next
    return vals == vals[::-1]  
  
 ```
</details> 
  
  #### Question 79:
 Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has 
  both p and q as descendants (where we allow a node to be a descendant of itself).”

  
<details>
<summary>code</summary>
  
 ```
 class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        # Value of current node or parent node.
        parent_val = root.val

        # Value of p
        p_val = p.val

        # Value of q
        q_val = q.val

        # If both p and q are greater than parent
        if p_val > parent_val and q_val > parent_val:    
            return self.lowestCommonAncestor(root.right, p, q)
        # If both p and q are lesser than parent
        elif p_val < parent_val and q_val < parent_val:    
            return self.lowestCommonAncestor(root.left, p, q)
        # We have found the split point, i.e. the LCA node.
        else:
            return root 
  
 ```
</details> 
  
  #### Question 80:
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both 
  p and q as descendants (where we allow a node to be a descendant of itself).”  
<details>
<summary>code</summary>
  
 ```
class Solution:

    def __init__(self):
        # Variable to store LCA node.
        self.ans = None

    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        def recurse_tree(current_node):

            # If reached the end of a branch, return False.
            if not current_node:
                return False

            # Left Recursion
            left = recurse_tree(current_node.left)

            # Right Recursion
            right = recurse_tree(current_node.right)

            # If the current node is one of p or q
            mid = current_node == p or current_node == q

            # If any two of the three flags left, right or mid become True.
            if mid + left + right >= 2:
                self.ans = current_node

            # Return True if either of the three bool values is True.
            return mid or left or right

        # Traverse the tree
        recurse_tree(root)
        return self.ans  
  
 ```
</details> 
  
  #### Question 81:
Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access 
  to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.  
<details>
<summary>code</summary>
  
 ```
class Solution(object):
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next	
	
 ```
</details> 
  
  #### Question 82:
 Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation. 
<details>
<summary>code</summary>
  
 ```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        
        # The length of the input array 
        length = len(nums)
        
        # The left and right arrays as described in the algorithm
        L, R, answer = [0]*length, [0]*length, [0]*length
        
        # L[i] contains the product of all the elements to the left
        # Note: for the element at index '0', there are no elements to the left,
        # so the L[0] would be 1
        L[0] = 1
        for i in range(1, length):
            
            # L[i - 1] already contains the product of elements to the left of 'i - 1'
            # Simply multiplying it with nums[i - 1] would give the product of all 
            # elements to the left of index 'i'
            L[i] = nums[i - 1] * L[i - 1]
        
        # R[i] contains the product of all the elements to the right
        # Note: for the element at index 'length - 1', there are no elements to the right,
        # so the R[length - 1] would be 1
        R[length - 1] = 1
        for i in reversed(range(length - 1)):
            
            # R[i + 1] already contains the product of elements to the right of 'i + 1'
            # Simply multiplying it with nums[i + 1] would give the product of all 
            # elements to the right of index 'i'
            R[i] = nums[i + 1] * R[i + 1]
        
        # Constructing the answer array
        for i in range(length):
            # For the first element, R[i] would be product except self
            # For the last element of the array, product except self would be L[i]
            # Else, multiple product of all elements to the left and to the right
            answer[i] = L[i] * R[i]
        
        return answer	
	
 ```
</details> 
  
  #### Question 83:
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right.
  You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.  
<details>
<summary>code</summary>
  
 ```
class Solution:
    def maxSlidingWindow(self, nums: 'List[int]', k: 'int') -> 'List[int]':
        n = len(nums)
        if n * k == 0:
            return []
        
        return [max(nums[i:i + k]) for i in range(n - k + 1)]	
	
 ```
</details> 
  
  #### Question 84:
Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.  
<details>
<summary>code</summary>
  
 ```
	class Solution:
    def binary_search(self, matrix, target, start, vertical):
        lo = start
        hi = len(matrix[0]) - 1 if vertical else len(matrix) - 1

        while hi >= lo:
            mid = (lo + hi) // 2
            if vertical: # searching a column
                if matrix[start][mid] < target:
                    lo = mid + 1
                elif matrix[start][mid] > target:
                    hi = mid - 1
                else:
                    return True
            else: # searching a row
                if matrix[mid][start] < target:
                    lo = mid + 1
                elif matrix[mid][start] > target:
                    hi = mid - 1
                else:
                    return True
        
        return False

    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        # an empty matrix obviously does not contain `target`
        if not matrix:
            return False

        # iterate over matrix diagonals starting in bottom left.
        for i in range(min(len(matrix), len(matrix[0]))):
            vertical_found = self.binary_search(matrix, target, i, True)
            horizontal_found = self.binary_search(matrix, target, i, False)
            if vertical_found or horizontal_found:
                return True
        
        return False
	
 ```
</details> 
  
  #### Question 85:
Given a string expression of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators.
  You may return the answer in any order.  
<details>
<summary>code</summary>
  
 ```
	class Solution:
    def diffWaysToCompute(self, expression: str) -> List[int]:
        def parenthesis(s):
            stk = []
            for c in range(len(s)):
                if s[c] == "+" or s[c] == "*" or s[c]== "-":
                    a = s[0:c]
                    b = s[c+1:]
                    res1 = parenthesis(a)
                    res2 = parenthesis(b)
                    for i in res1:
                        for j in res2:
                            if s[c]== "+":
                                stk.append(int(i) + int(j))

                            elif s[c]== "-":
                                stk.append(int(i) - int(j))

                            elif s[c] == "*":
                                stk.append(int(i) * int(j))


            if len(stk) == 0 :
                stk.append(s)

            # print(stk)
            return (stk)


        return (parenthesis(expression))
	
 ```
</details> 
  
  #### Question 86:
Given two strings s and t, return true if t is an anagram of s, and false otherwise.  
Using Hash Table:	
<details>
<summary>code</summary>
  
 ```
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) {
        return false;
    }
    int[] counter = new int[26];
    for (int i = 0; i < s.length(); i++) {
        counter[s.charAt(i) - 'a']++;
        counter[t.charAt(i) - 'a']--;
    }
    for (int count : counter) {
        if (count != 0) {
            return false;
        }
    }
    return true;
}	
	
 ```
</details> 
  
  #### Question 87:
Given an array of strings wordsDict and two different strings that already exist in the array word1 and word2, return the shortest distance between these two words in the list.  
<details>
<summary>code</summary>
  
 ```
	class Solution(object):
	def shortestDistance(self, wordsDict, word1, word2):
		"""
		:type wordsDict: List[str]
		:type word1: str
		:type word2: str
		:rtype: int
		"""
		word1_idx = []
		word2_idx = []

		for idx,word in enumerate(wordsDict):
			if word == word1:
				word1_idx.append(idx)
			elif word == word2:
				word2_idx.append(idx)
		final = 9999999999
		for i in word1_idx:
			for j in word2_idx:
				final = min(abs(i-j),final)

		return final
	
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
	from collections import defaultdict
class WordDistance:

    def __init__(self, words):
        """
        :type words: List[str]
        """
        self.locations = defaultdict(list)

        # Prepare a mapping from a word to all it's locations (indices).
        for i, w in enumerate(words):
            self.locations[w].append(i)

    def shortest(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        loc1, loc2 = self.locations[word1], self.locations[word2]
        l1, l2 = 0, 0
        min_diff = float("inf")

        # Until the shorter of the two lists is processed
        while l1 < len(loc1) and l2 < len(loc2):
            min_diff = min(min_diff, abs(loc1[l1] - loc2[l2]))
            if loc1[l1] < loc2[l2]:
                l1 += 1
            else:
                l2 += 1
        return min_diff
	
 ```
</details> 
  
  #### Question 89:
Given an array of strings wordsDict and two strings that already exist in the array word1 and word2, return the shortest distance between these two words in the list.

Note that word1 and word2 may be the same. It is guaranteed that they represent two individual words in the list.

   
<details>
<summary>code</summary>
  
 ```
 def shortestWordDistance(self, wordsDict: List[str], word1: str, word2: str) -> int:
        ans = len(wordsDict)
        first = -1
        second = -1
        for idx,word in enumerate(wordsDict):
            if word==word1:
                prev = first# we use prev to record the last idx of same word
                first = idx
            if word==word2:
                if word != word1:
                    second = idx
                else:
                    second = prev
            if first !=-1 and second !=-1:
                ans = min(ans,abs(second-first))
        return ans	
	
 ```
</details> 
  
  #### Question 90:
Given a string num which represents an integer, return true if num is a strobogrammatic number.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

   
<details>
<summary>code</summary>
  
 ```
class Solution:
    def isStrobogrammatic(self, num: str) -> bool:
        
        # In Python, we use a list as a string builder.
        rotated_string_builder = []
        
        # Remember that we want to loop backward through the string.
        for c in reversed(num):
            if c in {'0', '1', '8'}:
                rotated_string_builder.append(c)
            elif c == '6':
                rotated_string_builder.append('9')
            elif c == '9':
                rotated_string_builder.append('6')
            else: # This must be an invalid digit.
                return False
        
        # In Python, we convert a list of characters to
        # a string using join.
        rotated_string = "".join(rotated_string_builder)
        return rotated_string == num	
	
 ```
</details> 
  
  #### Question 91:
Given an integer n, return all the strobogrammatic numbers that are of length n. You may return the answer in any order.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

   
<details>
<summary>code</summary>
  
 ```
	class Solution(object):
    def __init__(self):
        self._pairs = {"0":"0", "1":"1", "8":"8", "6":"9", "9":"6"}
            
    
    def findStrobogrammatic(self, n):
		"""
        :type n: int
        :rtype: List[str]
        """
        return self.findStrobogrammaticRec(n , False)
        
    def findStrobogrammaticRec(self, n, leadingZeroesAllowed):
       
        out = []
        if n <= 0:
            return out
        elif n == 1:
            return ["0", "1", "8"]
        else:
            torso = self.findStrobogrammaticRec(n-2, True)
            for key  in self._pairs.keys():
                head = key
                tail = self._pairs[key]
                if head != "0" or leadingZeroesAllowed:
                    if torso:
                        _torso = torso[:]
                        for i in range(len(_torso)):
                            _torso[i] = head+_torso[i]+tail
                        out.extend(_torso)
                    else:
                        out.append(head+tail)
        return out
	
 ```
</details> 
  
  #### Question 92:
Given two strings low and high that represent two integers low and high where low <= high, return the number of strobogrammatic numbers in the range [low, high].

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

   
<details>
<summary>code</summary>
  
 ```
	import bisect

class Solution:
    def strobogrammaticInRange(self, low, high):
        if len(high) == len(low):
            lows = self.helper(len(low), True)
            lows = [int(l) for l in lows if str(int(l)) == str(l)]
            
            low_index = bisect.bisect_left(lows, int(low))
            high_index = bisect.bisect_right(lows, int(high))
            return high_index - low_index
        
        lows = self.helper(len(low), True)
        highs = self.helper(len(high), True)

        low_index = bisect.bisect_left(lows, int(low))
        high_index = bisect.bisect_right(highs, int(high))
        
        cnt = len(lows)
        
        prev = len(lows)
        for i in range(len(low) + 1, len(high)):
            if i == 2:
                cnt += 4
                prev = 4
                continue
            cnt += prev * (3 if i % 2 else 5)
            if not i % 2:
                prev = prev * 5

        return cnt - low_index + high_index
    
    def helper(self, l, is_start):
        if l == 0:
            return ['']
        if l == 1:
            return ['0', '1', '8'] if not is_start else [0, 1, 8]
        rst = []
        center = self.helper(l - 2, False)
        
        cs = [['0','0'],['1','1'],['6','9'],['8','8'],['9','6']] if not is_start else [['1','1'],['6','9'],['8','8'],['9','6']]
        for c in cs:
            for w in center:
                rst.append(c[0] + w + c[1] if not is_start else int(c[0] + w + c[1]))
        
        return rst
	
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
	class Solution:
    def groupStrings(self, strings: List[str]) -> List[List[str]]:
        
        def shift_letter(letter: str, shift: int):
            return chr((ord(letter) - shift) % 26 + ord('a'))
        
        # Create a hash value
        def get_hash(string: str):
            # Calculate the number of shifts to make the first character to be 'a'
            shift = ord(string[0])
            return ''.join(shift_letter(letter, shift) for letter in string)
        
        # Create a hash_value (hashKey) for each string and append the string
        # to the list of hash values i.e. mapHashToList["abc"] = ["abc", "bcd"]
        groups = collections.defaultdict(list)
        for string in strings:
            hash_key = get_hash(string)
            groups[hash_key].append(string)
        
        # Return a list of all of the grouped strings
        return list(groups.values())
	
 ```
</details> 
  
  #### Question 94:
Given the root of a binary tree, return the number of uni-value subtrees.

A uni-value subtree means all nodes of the subtree have the same value.  
<details>
<summary>code</summary>
  
 ```
	class Solution:
    def countUnivalSubtrees(self, root):
        if root is None: return 0
        self.count = 0
        self.is_uni(root)
        return self.count

    def is_uni(self, node):

        # base case - if the node has no children this is a univalue subtree
        if node.left is None and node.right is None:

            # found a univalue subtree - increment
            self.count += 1
            return True

        is_uni = True

        # check if all of the node's children are univalue subtrees and if they have the same value
        # also recursively call is_uni for children
        if node.left is not None:
            is_uni = self.is_uni(node.left) and is_uni and node.left.val == node.val

        if node.right is not None:
            is_uni = self.is_uni(node.right) and is_uni and node.right.val == node.val

        # increment self.res and return whether a univalue tree exists here
        self.count += is_uni
        return is_uni
	
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
	class Vector2D:

    def __init__(self, v: List[List[int]]):
        # We need to iterate over the 2D vector, getting all the integers
        # out of it and putting them into the nums list.
        for (int[] innerVector : v) {
        self.nums = []
        for inner_list in v:
            for num in inner_list:
                self.nums.append(num)
        # We'll keep position 1 behind the next number to return.
        self.position = -1

    def next(self) -> int:
        # Move up to the current element and return it.
        self.position += 1
        return self.nums[self.position]

    def hasNext(self) -> bool:
        # If the next position is a valid index of nums, return True.
        return self.position + 1 < len(self.nums)
	
 ```
</details> 
  
  #### Question 96:
Given an array of meeting time intervals where intervals[i] = [starti, endi], determine if a person could attend all meetings.

   
<details>
<summary>code</summary>
  
 ```
	class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        def overlap(interval1: List[int], interval2: List[int]) -> bool:
            return (interval1[0] >= interval2[0] and interval1[0] < interval2[1]
                or interval2[0] >= interval1[0] and interval2[0] < interval1[1])

        for i in range(len(intervals)):
            for j in range(i + 1, len(intervals)):
                if overlap(intervals[i], intervals[j]):
                    return False
        return True
	
 ```
</details> 
  
  #### Question 97:
Given an array of meeting time intervals intervals where intervals[i] = [starti, endi], return the minimum number of conference rooms required.
  
<details>
<summary>code</summary>
  
 ```
	class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        
        # If there is no meeting to schedule then no room needs to be allocated.
        if not intervals:
            return 0

        # The heap initialization
        free_rooms = []

        # Sort the meetings in increasing order of their start time.
        intervals.sort(key= lambda x: x[0])

        # Add the first meeting. We have to give a new room to the first meeting.
        heapq.heappush(free_rooms, intervals[0][1])

        # For all the remaining meeting rooms
        for i in intervals[1:]:

            # If the room due to free up the earliest is free, assign that room to this meeting.
            if free_rooms[0] <= i[0]:
                heapq.heappop(free_rooms)

            # If a new room is to be assigned, then also we add to the heap,
            # If an old room is allocated, then also we have to add to the heap with updated end time.
            heapq.heappush(free_rooms, i[1])

        # The size of the heap tells us the minimum rooms required for all the meetings.
        return len(free_rooms)
	
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
class Solution:
    def getFactors(self, n: int) -> List[List[int]]:
        res, level = [], []
        for d in range(2, int(sqrt(n))+1):
            if n % d == 0:
                level.append( [d, n//d] )
        while level:
            new = []
            for chain in level:
                res.append( chain[:] )
                cur = chain.pop()
                start, end = chain[-1], int(sqrt(cur))
                for d in range(start, end+1): # key: gurantee monotonous increase
                    if (cur % d == 0):
                        new.append( chain + [d, cur//d] )
            level = new
        return res	
	
 ```
</details> 
  
  #### Question 99:
Given an array of unique integers preorder, return true if it is the correct preorder traversal sequence of a binary search tree.  
<details>
<summary>code</summary>
  
 ```
class Solution:
    def verifyPreorder(self, preorder: List[int]) -> bool:
        lower = -float('inf')
        stack = []
        
        for curr in preorder:
            if curr <= lower: # break BST rule
                return False
            if not stack or curr < stack[-1]:
                stack.append(curr)
                continue
            while stack and curr >= stack[-1]:
                lower = stack.pop()
            stack.append(curr)
            
        return True	
	
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
	def minCost(self, costs):
    """
    :type costs: List[List[int]]
    :rtype: int
    """

    def paint_cost(n, color):
        total_cost = costs[n][color]
        if n == len(costs) - 1:
            pass
        elif color == 0: # Red
            total_cost += min(paint_cost(n + 1, 1), paint_cost(n + 1, 2))
        elif color == 1: # Green
            total_cost += min(paint_cost(n + 1, 0), paint_cost(n + 1, 2))
        else: # Blue
            total_cost += min(paint_cost(n + 1, 0), paint_cost(n + 1, 1))
        return total_cost

    if costs == []:
        return 0
    return min(paint_cost(0, 0), paint_cost(0, 1), paint_cost(0, 2))
	
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
You are given an m x n binary matrix image where 0 represents a white pixel and 1 represents a black pixel.

The black pixels are connected (i.e., there is only one black region). Pixels are connected horizontally and vertically.

Given two integers x and y that represents the location of one of the black pixels, return the area of the smallest (axis-aligned) rectangle that encloses all black pixels.

You must write an algorithm with less than O(mn) runtime complexity

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 145:
Given an integer array nums, handle multiple queries of the following type:

Calculate the sum of the elements of nums between indices left and right inclusive where left <= right.
Implement the NumArray class:

NumArray(int[] nums) Initializes the object with the integer array nums.
int sumRange(int left, int right) Returns the sum of the elements of nums between indices left and right inclusive (i.e. nums[left] + nums[left + 1] + ... + nums[right]).
   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 146:
Given a 2D matrix matrix, handle multiple queries of the following type:

Calculate the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
Implement the NumMatrix class:

NumMatrix(int[][] matrix) Initializes the object with the integer matrix matrix.
int sumRegion(int row1, int col1, int row2, int col2) Returns the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 147:
You are given an empty 2D binary grid grid of size m x n. The grid represents a map where 0's represent water and 1's represent land. Initially, all the cells of grid are water cells (i.e., all the cells are 0's).

We may perform an add land operation which turns the water at position into a land. You are given an array positions where positions[i] = [ri, ci] is the position (ri, ci) at which we should operate the ith operation.

Return an array of integers answer where answer[i] is the number of islands after turning the cell (ri, ci) into a land.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 148:
An additive number is a string whose digits can form an additive sequence.

A valid additive sequence should contain at least three numbers. Except for the first two numbers, each subsequent number in the sequence must be the sum of the preceding two.

Given a string containing only digits, return true if it is an additive number or false otherwise.

Note: Numbers in the additive sequence cannot have leading zeros, so sequence 1, 2, 03 or 1, 02, 3 is invalid.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 149:
Given an integer array nums, handle multiple queries of the following types:

Update the value of an element in nums.
Calculate the sum of the elements of nums between indices left and right inclusive where left <= right.
Implement the NumArray class:

NumArray(int[] nums) Initializes the object with the integer array nums.
void update(int index, int val) Updates the value of nums[index] to be val.
int sumRange(int left, int right) Returns the sum of the elements of nums between indices left and right inclusive (i.e. nums[left] + nums[left + 1] + ... + nums[right]).
   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 150:
Given a 2D matrix matrix, handle multiple queries of the following types:

Update the value of a cell in matrix.
Calculate the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
Implement the NumMatrix class:

NumMatrix(int[][] matrix) Initializes the object with the integer matrix matrix.
void update(int row, int col, int val) Updates the value of matrix[row][col] to be val.
int sumRegion(int row1, int col1, int row2, int col2) Returns the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 151:
You are given an array prices where prices[i] is the price of a given stock on the ith day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).
Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 152:
A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of n nodes labelled from 0 to n - 1, and an array of n - 1 edges where edges[i] = [ai, bi] indicates that there is an undirected edge between the two nodes ai and bi in the tree, you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h))  are called minimum height trees (MHTs).

Return a list of all MHTs' root labels. You can return the answer in any order.

The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
 
  #### Question 153:
Given two sparse matrices mat1 of size m x k and mat2 of size k x n, return the result of mat1 x mat2. You may assume that multiplication is always possible.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 154:
You are given n balloons, indexed from 0 to n - 1. Each balloon is painted with a number on it represented by an array nums. You are asked to burst all the balloons.

If you burst the ith balloon, you will get nums[i - 1] * nums[i] * nums[i + 1] coins. If i - 1 or i + 1 goes out of bounds of the array, then treat it as if there is a balloon with a 1 painted on it.

Return the maximum coins you can collect by bursting the balloons wisely.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 155:
A super ugly number is a positive integer whose prime factors are in the array primes.

Given an integer n and an array of integers primes, return the nth super ugly number.

The nth super ugly number is guaranteed to fit in a 32-bit signed integer.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 156:
Given the root of a binary tree, return the vertical order traversal of its nodes' values. (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 157:
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 158:
Given a string s, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 159:
You are given an m x n grid grid of values 0, 1, or 2, where:

each 0 marks an empty land that you can pass by freely,
each 1 marks a building that you cannot pass through, and
each 2 marks an obstacle that you cannot pass through.
You want to build a house on an empty land that reaches all buildings in the shortest total travel distance. You can only move up, down, left, and right.

Return the shortest travel distance for such a house. If it is not possible to build such a house according to the above rules, return -1.

The total travel distance is the sum of the distances between the houses of the friends and the meeting point.

The distance is calculated using Manhattan Distance, where distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 160:
Given a string array words, return the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. If no such two words exist, return 0.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 161:
There are n bulbs that are initially off. You first turn on all the bulbs, then you turn off every second bulb.

On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the ith round, you toggle every i bulb. For the nth round, you only toggle the last bulb.

Return the number of bulbs that are on after n rounds.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 162:
Medium

565

198

Add to List

Share
A word's generalized abbreviation can be constructed by taking any number of non-overlapping and non-adjacent substrings and replacing them with their respective lengths.

For example, "abcde" can be abbreviated into:
"a3e" ("bcd" turned into "3")
"1bcd1" ("a" and "e" both turned into "1")
"5" ("abcde" turned into "5")
"abcde" (no substrings replaced)
However, these abbreviations are invalid:
"23" ("ab" turned into "2" and "cde" turned into "3") is invalid as the substrings chosen are adjacent.
"22de" ("ab" turned into "2" and "bc" turned into "2") is invalid as the substring chosen overlap.
Given a string word, return a list of all the possible generalized abbreviations of word. Return the answer in any order.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 163:
You are given two integer arrays nums1 and nums2 of lengths m and n respectively. nums1 and nums2 represent the digits of two numbers. You are also given an integer k.

Create the maximum number of length k <= m + n from digits of the two numbers. The relative order of the digits from the same array must be preserved.

Return an array of the k digits representing the answer.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 164:
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 165:
You have a graph of n nodes. You are given an integer n and an array edges where edges[i] = [ai, bi] indicates that there is an edge between ai and bi in the graph.

Return the number of connected components in the graph.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   

  
  #### Question 166:
Given an integer array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

You may assume the input array always has a valid answer.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 167:
Given an integer array nums and an integer k, return the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 168:
Given an integer n, return true if it is a power of three. Otherwise, return false.

An integer n is a power of three, if there exists an integer x such that n == 3x.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  #### Question 169:
Given an integer array nums and two integers lower and upper, return the number of range sums that lie in [lower, upper] inclusive.

Range sum S(i, j) is defined as the sum of the elements in nums between indices i and j inclusive, where i <= j.

   
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
   
  #### Question 170:
Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in O(1) extra space complexity and O(n) time complexity.

  
  <details>
<summary>code</summary>
  
 ```
 ```
</details>   
  
  
  
  
 
  
  
  
