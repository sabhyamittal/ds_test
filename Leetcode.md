## Questions:

#### 157. Read N Characters Given Read4
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
        
        return copied_chars
                              
 ```
 </details>

#### 158. Read N Characters Given read4 II - Call Multiple Times
  
<details>
<summary>code</summary>
  
```
class Solution:
    def __init__(self):
        self.q = []
    
    def read(self, buf: List[str], n: int) -> int:
        tot_char_read = 0
        nb_char_read = 4
        buf4 = [""]*4
        while tot_char_read < n and nb_char_read > 0:
            if len(self.q) > 0:
                buf[tot_char_read] = self.q.pop(0)
                tot_char_read += 1
            else:
                nb_char_read = read4(buf4)
                self.q += buf4[:nb_char_read]
        return tot_char_read  
  
```
</details>  

#### 159. Longest Substring with At Most Two Distinct Characters
  
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

#### 161. One Edit Distance
  
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

#### 163. Missing Ranges
  
<details>
<summary>code</summary>
  
```
class Solution:
    def findMissingRanges(self, nums: List[int], lower: int, upper: int) -> List[str]:
        result = []

        def add(low, high):
            if low > high:
                return
            if low == high:
                result.append(str(low))
            else:
                result.append(str(low) + '->' + str(high))

        if not nums: # edge case
            add(lower, upper)
            return result

        add(lower, nums[0] - 1)

        for x in range(len(nums)):
            add(nums[x - 1] + 1, nums[x] - 1)

        add(nums[-1] + 1, upper)

        return result  
  
```
</details>    

#### 170. Two Sum III - Data structure design
  
<details>
<summary>code</summary>
  
```
class TwoSum(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.nums = []
        self.is_sorted = False


    def add(self, number):
        """
        Add the number to an internal data structure..
        :type number: int
        :rtype: None
        """
        # Inserting while maintaining the ascending order.
        # for index, num in enumerate(self.nums):
        #     if number <= num:
        #         self.nums.insert(index, number)
        #         return
        ## larger than any number
        #self.nums.append(number)

        self.nums.append(number)
        self.is_sorted = False
    

    def find(self, value):
        """
        Find if there exists any pair of numbers which sum is equal to the value.
        :type value: int
        :rtype: bool
        """
        if not self.is_sorted:
            self.nums.sort()
            self.is_sorted = True

        low, high = 0, len(self.nums)-1
        while low < high:
            currSum = self.nums[low] + self.nums[high]
            if currSum < value:
                low += 1
            elif currSum > value:
                high -= 1
            else: # currSum == value
                return True
        
        return False
    
```
</details>    

#### 186. Reverse Words in a String II
  
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

#### 243. Shortest Word Distance
  
<details>
<summary>code</summary>
  
```
class Solution:
    def shortestDistance(self, wordsDict: List[str], word1: str, word2: str) -> int:
        slow = fast = 0
        lastw1 = None
        lastw2 = None
        ans = float('inf')
        for i in range(len(wordsDict)):
            if wordsDict[i] == word1:
                lastw1 = i
            if wordsDict[i] == word2:
                lastw2 = i
            if lastw1 is not None and lastw2 is not None:
                ans = min(ans,abs(lastw1-lastw2))
        return ans  
  
```
</details>    

#### 244. Shortest Word Distance II
  
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

#### 245. Shortest Word Distance III
  
<details>
<summary>code</summary>
  
```
class Solution:
    def shortestWordDistance(self, wordsDict: List[str], word1: str, word2: str) -> int:
        mindiff = len(wordsDict)
        if word1 != word2:
            idx1 = - mindiff
            idx2 = - mindiff
            for ite, w in enumerate(wordsDict):
                changed = False
                if w == word1:
                    idx1 = ite
                    changed = True
                elif w == word2:
                    idx2 = ite
                    changed = True
                if changed and abs(idx1 - idx2) < mindiff:
                    mindiff = abs(idx1 - idx2)
                    if mindiff == 1:
                        return 1
            return mindiff
        else:
            lastidx = - mindiff
            for ite, w in enumerate(wordsDict):
                if w == word1:
                    if ite - lastidx < mindiff:
                        mindiff = ite - lastidx
                    lastidx = ite
            return mindiff  
  
```
</details>  
  
#### 247. Strobogrammatic Number II
  
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
  
#### 249. Group Shifted Strings
  
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
  
#### 250. Count Univalue Subtrees
  
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
  
#### 251. Flatten 2D Vector
  
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
  
#### 252. Meeting Rooms
  
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
  
#### 253. Meeting Rooms II
  
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
  
#### 254. Factor Combinations
  
<details>
<summary>code</summary>
  
```
import math
class Solution:
    def getFactors(self, n: int) -> List[List[int]]:
        if n <= 1:
            return []
        
        res = []
        self.dfs(res, [], n, 2)
        return res
    
    def dfs(self, res, cur, num, start):        
        if num == 1:
            if len(cur) > 1: # check by looking at length.
                res.append(list(cur))
            return
        
        
        # sqrt(32) = 5.66
        # 5 * 5 = 25, 6 * 6 = 36
        # so we only need to loop to 5.
        # 32 -> 2, 3, 4, 5
        for i in range(start, int(math.sqrt(num)) + 1):
            if num % i == 0:
                cur.append(i)
                self.dfs(res, cur, num // i, i)
                cur.pop()
        
        # the number can be a factor of itself, 
        # just need to make sure it is not equal to n.
        cur.append(num)
        self.dfs(res, cur, 1, -1)
        cur.pop()  
  
```
</details>  
  
#### 255. Verify Preorder Sequence in Binary Search Tree
  
<details>
<summary>code</summary>
  
```
class Solution:
    def verifyPreorder(self, preorder: List[int]) -> bool:
        stck, lo, n = [], -float('inf'), len(preorder)
        for i in range(n):
            if preorder[i] < lo:
                return False
            if i > 0 and preorder[i] > preorder[i-1]:  # update min threshold
                while stck and stck[-1] < preorder[i]:
                    lo = stck.pop()
            stck.append(preorder[i])
        return True  
  
```
</details> 
  
#### 256. Paint House
  
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
  
#### 259. 3Sum Smaller
  
<details>
<summary>code</summary>
  
```
class Solution(object):
    def threeSumSmaller(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        nums.sort()
        n = len(nums)
        
        res = 0
        for i in range(n-2):
            k = n-1
            for j in range(i+1, n-1):
                while k > j and nums[i] + nums[j] + nums[k] >= target:
                    k -= 1
                if j >= k:
                    break                
                res += k-j
        
        return res  
  
```
</details>  
  
#### 261. Graph Valid Tree
  
<details>
<summary>code</summary>
  
```
 DFS

Simple extension of cycle finding algorithm for directed graphs. You need to include the parent as well in the DFS call.
Now if a nbr is in visited and the nbr is not the parent, then we have a cycle.
Notice how we build an undirected graph: include both edges.
O(V+E)
from collections import defaultdict
class Solution(object):
    def dfs(self, node, parent, graph, visited):
        visited.add(node)
        for nbr in graph[node]:
            if nbr not in visited:
                if self.dfs(nbr, node, graph, visited):
                    return True
            elif nbr in visited and nbr != parent:
                return True
        return False
    
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        graph = defaultdict(list)
        for edge in edges:
            u,v = edge[0], edge[1]
            graph[u].append(v)
            graph[v].append(u)
        visited = set([])
        if self.dfs(0, -1, graph, visited):
            return False
        if len(visited) != n:
            return False
        return True
Union Find: Quick Find

If an edge end points are already part of same component, then we have cycle. Also, we must make sure number of edges is equal to n-1
Quick Find implementation of Union Find is O(V * E) - For every edge, we might have to update the entire component array which is size n
class Solution(object):
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        components = [i for i in range(n)]
        for edge in edges:
            u, v = edge[0], edge[1]
            pid, qid = components[u], components[v]
            if pid == qid:  # If an edge end points are in the same component, we have a cycle.
                return False
            else:
                for idx, x in enumerate(components):
                    if x == pid:
                        components[idx] = qid
        return len(edges) == n - 1 # if the number of edges are not equal to n-1, then not a tree
Union Find: Quick Union

Quick Union is another implementation of Union Find where we build forests. For edge u,v, we find the root of u and root of v, then point root of u to root of v.
http://algs4.cs.princeton.edu/15uf/
class Solution(object):
    def root(self, i, components):
        while i != components[i]:
            i = components[i]
        return i
    
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        components = [i for i in range(n)]
        for edge in edges:
            u, v = edge[0], edge[1]
            root_u, root_v = self.root(u, components), self.root(v, components)
            if root_u == root_v:  # If an edge end points are in the same component, we have a cycle.
                return False
            else:
                components[root_u] = root_v
        return len(edges) == n - 1 # if the number of edges are not equal to n-1, then not a tree
Weighted Quick Union

Another optimization that prevents the trees from getting longer.
class Solution(object):
    def root(self, i, components):
        while i != components[i]:
            i = components[i]
        return i
    
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        parents = [i for i in range(n)]
        forest_size = [1]*n
        for edge in edges:
            u, v = edge[0], edge[1]
            root_u, root_v = self.root(u, parents), self.root(v, parents)
            if root_u == root_v:  # If an edge end points are in the same component, we have a cycle.
                return False
            else:
                if forest_size[root_u] < forest_size[root_v]:
                    parents[root_u] = root_v
                    forest_size[root_v] += forest_size[root_u]
                else:
                    parents[root_v] = root_u
                    forest_size[root_u] += forest_size[root_v]
        return len(edges) == n - 1 # if the number of edges are not equal to n-1, then not a tree 
  
```
</details>  
  
#### 265. Paint House II
  
<details>
<summary>code</summary>
  
```
class Solution:
    def minCostII(self, costs: List[List[int]]) -> int:
        # Start by defining n and k to make the following code cleaner.
        n = len(costs)
        if n == 0: return 0 # No houses is a valid test case!
        k = len(costs[0])

        # If you're not familiar with lru_cache, look it up in the docs as it's
        # essential to know about.
        @lru_cache(maxsize=None)
        def memo_solve(house_num, color):

            # Base case.
            if house_num == n - 1:
                return costs[house_num][color]

            # Recursive case.
            cost = math.inf
            for next_color in range(k):
                if next_color == color:
                    continue # Can't paint adjacent houses the same color!
                cost = min(cost, memo_solve(house_num + 1, next_color))
            return costs[house_num][color] + cost

        # Consider all options for painting house 0 and find the minimum.
        cost = math.inf
        for color in range(k):
            cost = min(cost, memo_solve(0, color))
        return cost  
  
```
</details>  
  
#### 266. Palindrome Permutation
  
<details>
<summary>code</summary>
  
```
def canPermutePalindrome(self, s):
    return sum(v % 2 for v in collections.Counter(s).values()) < 2  
  
```
</details> 
  
#### 267. Palindrome Permutation II
  
<details>
<summary>code</summary>
  
```
def generatePalindromes(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        ans = []
        n = len(s)
        counter = collections.Counter(s)
        
        def helper(tmp):
            if len(tmp) == n:
                ans.append(tmp)
                return 
            for k, v in counter.items():
                if v > 0:
                    counter[k] -= 2
                    helper(k + tmp + k)
                    counter[k] += 2
        
        odd = [key for key, value in counter.items() if value % 2 != 0]
        if len(odd) > 1:
            return []
        if len(odd) == 1:
            counter[odd[0]] -= 1
            helper(odd[0])
        else:
            helper('')
        return ans
				```  
  
```
</details>  
  
#### 269. Alien Dictionary
  
<details>
<summary>code</summary>
  
```

from collections import defaultdict, Counter, deque

def alienOrder(self, words: List[str]) -> str:
    
    # Step 0: create data structures + the in_degree of each unique letter to 0.
    adj_list = defaultdict(set)
    in_degree = Counter({c : 0 for word in words for c in word})
            
    # Step 1: We need to populate adj_list and in_degree.
    # For each pair of adjacent words...
    for first_word, second_word in zip(words, words[1:]):
        for c, d in zip(first_word, second_word):
            if c != d:
                if d not in adj_list[c]:
                    adj_list[c].add(d)
                    in_degree[d] += 1
                break
        else: # Check that second word isn't a prefix of first word.
            if len(second_word) < len(first_word): return ""
    
    # Step 2: We need to repeatedly pick off nodes with an indegree of 0.
    output = []
    queue = deque([c for c in in_degree if in_degree[c] == 0])
    while queue:
        c = queue.popleft()
        output.append(c)
        for d in adj_list[c]:
            in_degree[d] -= 1
            if in_degree[d] == 0:
                queue.append(d)
                
    # If not all letters are in output, that means there was a cycle and so
    # no valid ordering. Return "" as per the problem description.
    if len(output) < len(in_degree):
        return ""
    # Otherwise, convert the ordering we found into a string and return it.
    return "".join(output)  
  
```
</details>  
  
#### 270. Closest Binary Search Tree Value
  
<details>
<summary>code</summary>
  
```
class Solution:
    def closestValue(self, root: TreeNode, target: float) -> int:
        def inorder(r: TreeNode):
            return inorder(r.left) + [r.val] + inorder(r.right) if r else []
        
        return min(inorder(root), key = lambda x: abs(target - x))  
  
```
</details>  
  
#### 271. Encode and Decode Strings
  
<details>
<summary>code</summary>
  
```
class Codec:
    def encode(self, strs):
        """Encodes a list of strings to a single string.
        :type strs: List[str]
        :rtype: str
        """
        if len(strs) == 0: 
            return unichr(258)
        
        # encode here is a workaround to fix BE CodecDriver error
        return unichr(257).join(x.encode('utf-8') for x in strs)
        

    def decode(self, s):
        """Decodes a single string to a list of strings.
        :type s: str
        :rtype: List[str]
        """
        if s == unichr(258): 
            return []
        return s.split(unichr(257))  
  
```
</details>  
  
#### 272. Closest Binary Search Tree Value II
  
<details>
<summary>code</summary>
  
```
def closestKValues(self, root, target, k):

    # Helper, takes a path and makes it the path to the next node
    def nextpath(path, kid1, kid2):
        if path:
            if kid2(path):
                path += kid2(path),
                while kid1(path):
                    path += kid1(path),
            else:
                kid = path.pop()
                while path and kid is kid2(path):
                    kid = path.pop()

    # These customize nextpath as forward or backward iterator
    kidleft = lambda path: path[-1].left
    kidright = lambda path: path[-1].right

    # Build path to closest node
    path = []
    while root:
        path += root,
        root = root.left if target < root.val else root.right
    dist = lambda node: abs(node.val - target)
    path = path[:path.index(min(path, key=dist))+1]

    # Get the path to the next larger node
    path2 = path[:]
    nextpath(path2, kidleft, kidright)

    # Collect the closest k values by moving the two paths outwards
    vals = []
    for _ in range(k):
        if not path2 or path and dist(path[-1]) < dist(path2[-1]):
            vals += path[-1].val,
            nextpath(path, kidright, kidleft)
        else:
            vals += path2[-1].val,
            nextpath(path2, kidleft, kidright)
    return vals  
  
```
</details>  
  
#### 276. Paint Fence
  
<details>
<summary>code</summary>
  
```
class Solution:
    def numWays(self, n: int, k: int) -> int:
        def total_ways(i):
            if i == 1:
                return k
            if i == 2:
                return k * k
            
            # Check if we have already calculated totalWays(i)
            if i in memo:
                return memo[i]
            
            # Use the recurrence relation to calculate total_ways(i)
            memo[i] = (k - 1) * (total_ways(i - 1) + total_ways(i - 2))
            return memo[i]

        memo = {}
        return total_ways(n)  
  
```
</details>  
  
#### 277. Find the Celebrity
  
<details>
<summary>code</summary>
  
```
class Solution:
    def findCelebrity(self, n: int) -> int:
        self.n = n
        for i in range(n):
            if self.is_celebrity(i):
                return i
        return -1
    
    def is_celebrity(self, i):
        for j in range(self.n):
            if i == j: continue # Don't ask if they know themselves.
            if knows(i, j) or not knows(j, i):
                return False
        return True  
  
```
</details>
  
#### 280. Wiggle Sort
  
<details>
<summary>code</summary>
  
```
def wiggleSort(self, nums):
    for i in range(len(nums)):
        nums[i:i+2] = sorted(nums[i:i+2], reverse=i%2)  
  
```
</details> 
  
#### 281. Zigzag Iterator
  
<details>
<summary>code</summary>
  
```
class ZigzagIterator:
    def __init__(self, v1: List[int], v2: List[int]):
        self.vectors = [v1, v2]
        self.p_elem = 0   # pointer to the index of element
        self.p_vec = 0    # pointer to the vector
        # variables for hasNext() function
        self.total_num = len(v1) + len(v2)
        self.output_count = 0

    def next(self) -> int:
        iter_num = 0
        ret = None

        # Iterate over the vectors
        while iter_num < len(self.vectors):
            curr_vec = self.vectors[self.p_vec]
            if self.p_elem < len(curr_vec):
                ret = curr_vec[self.p_elem]

            iter_num += 1
            self.p_vec = (self.p_vec + 1) % len(self.vectors)
            # increment the element pointer once iterating all vectors
            if self.p_vec == 0:
                self.p_elem += 1

            if ret is not None:
                self.output_count += 1
                return ret

        # no more element to output
        raise Exception


    def hasNext(self) -> bool:
        return self.output_count < self.total_num

# Your ZigzagIterator object will be instantiated and called as such:
# i, v = ZigzagIterator(v1, v2), []
# while i.hasNext(): v.append(i.next())  
  
```
</details>  
  
#### 285. Inorder Successor in BST
  
<details>
<summary>code</summary>
  
```
class Solution:
    
    previous = None
    inorder_successor_node = None
    
    def inorderSuccessor(self, root: 'TreeNode', p: 'TreeNode') -> 'TreeNode':
        
        self.previous, self.inorder_successor_node = None, None
        
        # Case 1: We simply need to find the leftmost node in the subtree rooted at p.right.
        if p.right:
            leftmost = p.right
            while leftmost.left:
                leftmost = leftmost.left
                
            self.inorder_successor_node = leftmost
        
        # Case 2: We need to perform the standard inorder traversal and keep track of the previous node.
        else:
            self.inorderCase2(root, p)
        
        return self.inorder_successor_node
        
        
    def inorderCase2(self, node: 'TreeNode', p: 'TreeNode'):
        
        if not node:
            return
        
        # Recurse on the left side
        self.inorderCase2(node.left, p)
        
        # Check if previous is the inorder predecessor of node
        if self.previous == p and not self.inorder_successor_node:
            self.inorder_successor_node = node
            return
        
        # Keeping previous up-to-date for further recursions
        self.previous = node
        
        # Recurse on the right side
        self.inorderCase2(node.right, p)  
  
```
</details>  
  
#### 286. Walls and Gates
  
<details>
<summary>code</summary>
  
```
def wallsAndGates(self, rooms):
    q = [(i, j) for i, row in enumerate(rooms) for j, r in enumerate(row) if not r]
    for i, j in q:
        for I, J in (i+1, j), (i-1, j), (i, j+1), (i, j-1):
            if 0 <= I < len(rooms) and 0 <= J < len(rooms[0]) and rooms[I][J] > 2**30:
                rooms[I][J] = rooms[i][j] + 1
                q += (I, J),  
  
```
</details>
  
#### 291. Word Pattern II
  
<details>
<summary>code</summary>
  
```
def wordPatternMatch(self, pattern, str):
    return self.dfs(pattern, str, {})

def dfs(self, pattern, str, dict):
    if len(pattern) == 0 and len(str) > 0:
        return False
    if len(pattern) == len(str) == 0:
        return True
    for end in range(1, len(str)-len(pattern)+2): # +2 because it is the "end of an end"
        if pattern[0] not in dict and str[:end] not in dict.values():
            dict[pattern[0]] = str[:end]
            if self.dfs(pattern[1:], str[end:], dict):
                return True
            del dict[pattern[0]]
        elif pattern[0] in dict and dict[pattern[0]] == str[:end]:
            if self.dfs(pattern[1:], str[end:], dict):
                return True
    return False  
  
```
</details>  
  
#### 296. Best Meeting Point
  
<details>
<summary>code</summary>
  
```
def minTotalDistance(self, grid):
    row_sum = map(sum, grid)
    col_sum = map(sum, zip(*grid)) # syntax sugar learned from stefan :-)

    def minTotalDistance1D(vec):
        i, j = -1, len(vec)
        d = left = right = 0
        while i != j:
            if left < right:
                d += left
                i += 1
                left += vec[i]
            else:
                d += right
                j -= 1
                right += vec[j]
        return d

    return minTotalDistance1D(row_sum) + minTotalDistance1D(col_sum)  
  
```
</details>  
  
#### 298. Binary Tree Longest Consecutive Sequence
  
<details>
<summary>code</summary>
  
```
class TreeNode(object):
    """ Definition of a binary tree node."""
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None  
  
  # Deserialization 
class Codec:

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        :type data: str
        :rtype: TreeNode
        """
        def rdeserialize(l):
            """ a recursive helper function for deserialization."""
            if l[0] == 'None':
                l.pop(0)
                return None
                
            root = TreeNode(l[0])
            l.pop(0)
            root.left = rdeserialize(l)
            root.right = rdeserialize(l)
            return root

        data_list = data.split(',')
        root = rdeserialize(data_list)
        return root
  
```
</details> 
  
#### 302. Smallest Rectangle Enclosing Black Pixels
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 305. Number of Islands II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 308. Range Sum Query 2D - Mutable
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 311. Sparse Matrix Multiplication
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 314. Binary Tree Vertical Order Traversal
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 317. Shortest Distance from All Buildings
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 320. Generalized Abbreviation
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 323. Number of Connected Components in an Undirected Graph
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 325. Maximum Size Subarray Sum Equals k
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 333. Largest BST Subtree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 339. Nested List Weight Sum
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 340. Longest Substring with At Most K Distinct Characters
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 346. Moving Average from Data Stream
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 348. Design Tic-Tac-Toe
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 353. Design Snake Game
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 358. Rearrange String k Distance Apart
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 359. Logger Rate Limiter
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 360. Sort Transformed Array
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 361. Bomb Enemy
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 362. Design Hit Counter
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 364. Nested List Weight Sum II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 366. Find Leaves of Binary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 369. Plus One Linked List
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 370. Range Addition
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 422. Valid Word Square
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 425. Word Squares
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 426. Convert Binary Search Tree to Sorted Doubly Linked List
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 428. Serialize and Deserialize N-ary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 431. Encode N-ary Tree to Binary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 439. Ternary Expression Parser
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 465. Optimal Account Balancing
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 471. Encode String with Shortest Length
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 484. Find Permutation
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 487. Max Consecutive Ones II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 489. Robot Room Cleaner
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 490. The Maze
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 499. The Maze III
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 505. The Maze II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 510. Inorder Successor in BST II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 527. Word Abbreviation
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 531. Lonely Pixel I
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 536. Construct Binary Tree from String
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 545. Boundary of Binary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 549. Binary Tree Longest Consecutive Sequence II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 562. Longest Line of Consecutive One in Matrix
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 568. Maximum Vacation Days
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 582. Kill Process
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 588. Design In-Memory File System
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 604. Design Compressed String Iterator
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 616. Add Bold Tag in String
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 624. Maximum Distance in Arrays
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 631. Design Excel Sum Formula
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 635. Design Log Storage System
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 642. Design Search Autocomplete System
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 644. Maximum Average Subarray II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 651. 4 Keys Keyboard
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 656. Coin Path
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 694. Number of Distinct Islands
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 702. Search in a Sorted Array of Unknown Size
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 708. Insert into a Sorted Circular Linked List
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 716. Max Stack
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 723. Candy Crush
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 727. Minimum Window Subsequence
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 734. Sentence Similarity
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 737. Sentence Similarity II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 742. Closest Leaf in a Binary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 750. Number Of Corner Rectangles
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 759. Employee Free Time
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 760. Find Anagram Mappings
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 772. Basic Calculator III
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 774. Minimize Max Distance to Gas Station
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1055. Shortest Way to Form String
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1056. Confusing Number
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1057. Campus Bikes
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1059. All Paths from Source Lead to Destination
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1060. Missing Element in Sorted Array
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1061. Lexicographically Smallest Equivalent String
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1062. Longest Repeating Substring
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1064. Fixed Point
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1065. Index Pairs of a String
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1066. Campus Bikes II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1086. High Five
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1087. Brace Expansion
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1088. Confusing Number II
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1099. Two Sum Less Than K
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1100. Find K-Length Substrings With No Repeated Characters
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1101. The Earliest Moment When Everyone Become Friends
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1102. Path With Maximum Minimum Value
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1120. Maximum Average Subtree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1133. Largest Unique Number
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1134. Armstrong Number
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1135. Connecting Cities With Minimum Cost
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1136. Parallel Courses
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1150. Check If a Number Is Majority Element in a Sorted Array
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1151. Minimum Swaps to Group All 1's Together
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1153. String Transforms Into Another String
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1165. Single-Row Keyboard
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1166. Design File System
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1167. Minimum Cost to Connect Sticks
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1168. Optimize Water Distribution in a Village
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1180. Count Substrings with Only One Distinct Letter
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1182. Shortest Distance to Target Color
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1183. Maximum Number of Ones
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1196. How Many Apples Can You Put into the Basket
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1197. Minimum Knight Moves
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1198. Find Smallest Common Element in All Rows
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1199. Minimum Time to Build Blocks
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1213. Intersection of Three Sorted Arrays
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1214. Two Sum BSTs
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1216. Valid Palindrome III
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1228. Missing Number In Arithmetic Progression
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1229. Meeting Scheduler
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1231. Divide Chocolate
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1236. Web Crawler
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1244. Design A Leaderboard
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1245. Tree Diameter
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1259. Handshakes That Don't Cross
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1265. Print Immutable Linked List in Reverse
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1272. Remove Interval
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1274. Number of Ships in a Rectangle
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1426. Counting Elements
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1427. Perform String Shifts
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1428. Leftmost Column with at Least a One
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1429. First Unique Number
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1474. Delete N Nodes After M Nodes of a Linked List
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1485. Clone Binary Tree With Random Pointer
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1490. Clone N-ary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1506. Find Root of N-Ary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1522. Diameter of N-Ary Tree
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1533. Find the Index of the Large Integer
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1538. Guess the Majority in a Hidden Array
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1548. The Most Similar Path in a Graph
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  
#### 1564. Put Boxes Into the Warehouse I
  
<details>
<summary>code</summary>
  
```
  
  
```
</details>  

