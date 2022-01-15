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
def minArea(self, image, x, y):
    top = self.searchRows(image, 0, x, True)
    bottom = self.searchRows(image, x + 1, len(image), False)
    left = self.searchColumns(image, 0, y, top, bottom, True)
    right = self.searchColumns(image, y + 1, len(image[0]), top, bottom, False)
    return (right - left) * (bottom - top)

def searchRows(self, image, i, j, opt):
    while i != j:
        m = (i + j) / 2
        if ('1' in image[m]) == opt:
            j = m
        else:
            i = m + 1
    return i

def searchColumns(self, image, i, j, top, bottom, opt):
    while i != j:
        m = (i + j) / 2
        if any(image[k][m] == '1' for k in xrange(top, bottom)) == opt:
            j = m
        else:
            i = m + 1
    return i
# Runtime: 56 ms  
  
```
</details>  
	
#### 305. Number of Islands II
  
<details>
<summary>code</summary>
  
```
 class Solution(object):
    def numIslands2(self, m, n, positions):
        ans = []
        islands = Union()
        for p in map(tuple, positions):
            islands.add(p)
            for dp in (0, 1), (0, -1), (1, 0), (-1, 0):
                q = (p[0] + dp[0], p[1] + dp[1])
                if q in islands.id:
                    islands.unite(p, q)
            ans += [islands.count]
        return ans

class Union(object):
    def __init__(self):
        self.id = {}
        self.sz = {}
        self.count = 0

    def add(self, p):
        self.id[p] = p
        self.sz[p] = 1
        self.count += 1

    def root(self, i):
        while i != self.id[i]:
            self.id[i] = self.id[self.id[i]]
            i = self.id[i]
        return i

    def unite(self, p, q):
        i, j = self.root(p), self.root(q)
        if i == j:
            return
        if self.sz[i] > self.sz[j]:
            i, j = j, i
        self.id[i] = j
        self.sz[j] += self.sz[i]
        self.count -= 1

#Runtime: 300 ms 
  
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
class NumMatrix(object):
    def __init__(self, matrix):
        """
        initialize your data structure here.
        :type matrix: List[List[int]]
        """
        for row in matrix:
            for col in xrange(1, len(row)):
                row[col] += row[col-1]
        self.matrix = matrix
        

    def update(self, row, col, val):
        """
        update the element at matrix[row,col] to val.
        :type row: int
        :type col: int
        :type val: int
        :rtype: void
        """
        original = self.matrix[row][col]
        if col != 0:
            original -= self.matrix[row][col-1]
            
        diff = original - val
        
        for y in xrange(col, len(self.matrix[0])):
            self.matrix[row][y] -= diff

    def sumRegion(self, row1, col1, row2, col2):
        """
        sum of elements matrix[(row1,col1)..(row2,col2)], inclusive.
        :type row1: int
        :type col1: int
        :type row2: int
        :type col2: int
        :rtype: int
        """
        sum = 0
        for x in xrange(row1, row2+1):
            sum += self.matrix[x][col2]
            if col1 != 0:
                sum -= self.matrix[x][col1-1]
        return sum  
  
```
</details>  
	
#### 314. Binary Tree Vertical Order Traversal
  
<details>
<summary>code</summary>
  
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from collections import defaultdict
class Solution:
    def verticalOrder(self, root: TreeNode) -> List[List[int]]:
        columnTable = defaultdict(list)
        queue = deque([(root, 0)])

        while queue:
            node, column = queue.popleft()

            if node is not None:
                columnTable[column].append(node.val)
                
                queue.append((node.left, column - 1))
                queue.append((node.right, column + 1))
                        
        return [columnTable[x] for x in sorted(columnTable.keys())]  
  
```
</details>  
	
#### 317. Shortest Distance from All Buildings
  
<details>
<summary>code</summary>
  
```
def shortestDistance(self, grid):
    if not grid or not grid[0]: return -1
    M, N, buildings = len(grid), len(grid[0]), sum(val for line in grid for val in line if val == 1)
    hit, distSum = [[0] * N for i in range(M)], [[0] * N for i in range(M)]
    
    def BFS(start_x, start_y):
        visited = [[False] * N for k in range(M)]
        visited[start_x][start_y], count1, queue = True, 1, collections.deque([(start_x, start_y, 0)])
        while queue:
            x, y, dist = queue.popleft()
            for i, j in ((x + 1, y), (x - 1, y), (x, y + 1), (x, y - 1)):
                if 0 <= i < M and 0 <= j < N and not visited[i][j]:
                    visited[i][j] = True
                    if not grid[i][j]:
                        queue.append((i, j, dist + 1))
                        hit[i][j] += 1
                        distSum[i][j] += dist + 1
                    elif grid[i][j] == 1:
                        count1 += 1
        return count1 == buildings  
    
    for x in range(M):
        for y in range(N):
            if grid[x][y] == 1:
                if not BFS(x, y): return -1
    return min([distSum[i][j] for i in range(M) for j in range(N) if not grid[i][j] and hit[i][j] == buildings] or [-1])  
  
```
</details>  
	
#### 320. Generalized Abbreviation
  
<details>
<summary>code</summary>
  
```
 class Solution(object):
    def generateAbbreviations(self, word):
        """
        :type word: str
        :rtype: List[str]
        """
        def helper(word, pos, cur, count, result):
            if len(word) == pos:
                # Once we reach the end, append current to the result
                result.append(cur + str(count) if count > 0 else cur)
            else:
                # Skip current position, and increment count
                helper(word, pos + 1, cur, count + 1, result)
                # Include current position, and zero-out count
                helper(word, pos + 1, cur + (str(count) if count > 0 else '') + word[pos], 0, result)

        result = []
        helper(word, 0, '', 0, result)
        return result 
  
```
</details>  
	
#### 323. Number of Connected Components in an Undirected Graph
  
<details>
<summary>code</summary>
  
```
DFS:

def countComponents(n, edges):
        def dfs(n, g, visited):
            if visited[n]:
                return
            visited[n] = 1
            for x in g[n]:
                dfs(x, g, visited)
                
        visited = [0] * n
        g = {x:[] for x in xrange(n)}
        for x, y in edges:
            g[x].append(y)
            g[y].append(x)
            
        ret = 0
        for i in xrange(n):
            if not visited[i]:
                dfs(i, g, visited)
                ret += 1
                
        return ret
BFS:

def countComponents(n, edges):
        g = {x:[] for x in xrange(n)}
        for x, y in edges:
            g[x].append(y)
            g[y].append(x)
            
        ret = 0
        for i in xrange(n):
            queue = [i]
            ret += 1 if i in g else 0
            for j in queue:
                if j in g:
                    queue += g[j]
                    del g[j]

        return ret
Union Find:

def countComponents(n, edges):
        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])
            return parent[x]
            
        def union(xy):
            x, y = map(find, xy)
            if rank[x] < rank[y]:
                parent[x] = y
            else:
                parent[y] = x
                if rank[x] == rank[y]:
                    rank[x] += 1
        
        parent, rank = range(n), [0] * n
        map(union, edges)
        return len({find(x) for x in parent})  
  
```
</details>  
	
#### 325. Maximum Size Subarray Sum Equals k
  
<details>
<summary>code</summary>
  
```
class Solution:
    def maxSubArrayLen(self, nums: List[int], k: int) -> int:
        prefix_sum = longest_subarray = 0
        indices = {}
        
        for i, num in enumerate(nums):
            prefix_sum += num
            
            # Check if all of the numbers seen so far sum to k.
            if prefix_sum == k:
                longest_subarray = i + 1
                
            # If any subarray seen so far sums to k, then
            # update the length of the longest_subarray. 
            if prefix_sum - k in indices:
                longest_subarray = max(longest_subarray, i - indices[prefix_sum - k])
                
            # Only add the current prefix_sum index pair to the 
            # map if the prefix_sum is not already in the map.
            if prefix_sum not in indices:
                indices[prefix_sum] = i
        
        return longest_subarray  
  
```
</details>  
	
#### 333. Largest BST Subtree
  
<details>
<summary>code</summary>
  
```
class Solution:
    def is_valid_bst(self, root: Optional[TreeNode]) -> bool:
        """Check if given tree is a valid Binary Search Tree."""
        # An empty tree is a valid Binary Search Tree.
        if not root:
            return True

        # Find the max node in the left subtree of current node.
        left_max = self.find_max(root.left)

        # If the left subtree has a node greater than or equal to the current node,
        # then it is not a valid Binary Search Tree.
        if left_max >= root.val:
            return False

        # Find the min node in the right subtree of current node.
        right_min = self.find_min(root.right)

        # If the right subtree has a value less than or equal to the current node,
        # then it is not a valid Binary Search Tree.
        if right_min <= root.val:
            return False

        # If the left and right subtrees of current tree are also valid BST.
        # then the whole tree is a BST.
        return self.is_valid_bst(root.left) and self.is_valid_bst(root.right)

    def find_max(self, root: Optional[TreeNode]) -> int:
        # Max node in a empty tree should be smaller than parent.
        if not root:
            return float('-inf')
    
        # Check the maximum node from the current node, left and right subtree of the current tree.
        return max(root.val, self.find_max(root.left), self.find_max(root.right))

    def find_min(self, root: Optional[TreeNode]) -> int:
        # Min node in a empty tree should be larger than parent.
        if not root:
            return float('inf')
        
        # Check the minimum node from the current node, left and right subtree of the current tree
        return min(root.val, self.find_min(root.left), self.find_min(root.right))

    def count_nodes(self, root: Optional[TreeNode]) -> int:
        if not root: 
            return 0

        # Add nodes in left and right subtree.
        # Add 1 and return total size.
        return 1 + self.count_nodes(root.left) + self.count_nodes(root.right) 

    def largestBSTSubtree(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        # If current subtree is a validBST, its children will have smaller size BST.
        if self.is_valid_bst(root):
            return self.count_nodes(root)
        
        # Find BST in left and right subtrees of current nodes.
        return max(self.largestBSTSubtree(root.left), self.largestBSTSubtree(root.right))  
  
```
</details> 
	
#### 339. Nested List Weight Sum
  
<details>
<summary>code</summary>
  
```
class Solution:
    def depthSum(self, nestedList: List[NestedInteger]) -> int:

        def dfs(nested_list, depth):
            total = 0
            for nested in nested_list:
                if nested.isInteger():
                    total += nested.getInteger() * depth
                else:
                    total += dfs(nested.getList(), depth + 1)
            return total

        return dfs(nestedList, 1)
  
  
```
</details>  
	
#### 340. Longest Substring with At Most K Distinct Characters
  
<details>
<summary>code</summary>
  
```
from collections import OrderedDict
class Solution:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        n = len(s)
        if k == 0 or n == 0:
            return 0

        # sliding window left and right pointers
        left, right = 0, 0
        # hashmap character -> its rightmost position
        # in the sliding window
        hashmap = OrderedDict()

        max_len = 1

        while right < n:
            character = s[right]
            # if character is already in the hashmap -
            # delete it, so that after insert it becomes
            # the rightmost element in the hashmap
            if character in hashmap:
                del hashmap[character]
            hashmap[character] = right
            right += 1

            # slidewindow contains k + 1 characters
            if len(hashmap) == k + 1:
                # delete the leftmost character
                _, del_idx = hashmap.popitem(last = False)
                # move left pointer of the slidewindow
                left = del_idx + 1

            max_len = max(max_len, right - left)

        return max_len  
  
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
class MovingAverage:
    def __init__(self, size: int):
        self.size = size
        self.queue = []

    def next(self, val: int) -> float:
        size, queue = self.size, self.queue
        queue.append(val)
        # calculate the sum of the moving window
        window_sum = sum(queue[-size:])

        return window_sum / min(len(queue), size)  
	
	Approach 2: Double-ended Queue
	
from collections import deque
class MovingAverage:
    def __init__(self, size: int):
        self.size = size
        self.queue = deque()
        # number of elements seen so far
        self.window_sum = 0
        self.count = 0

    def next(self, val: int) -> float:
        self.count += 1
        # calculate the new sum by shifting the window
        self.queue.append(val)
        tail = self.queue.popleft() if self.count > self.size else 0

        self.window_sum = self.window_sum - tail + val

        return self.window_sum / min(self.size, self.count)
	
	Approach 3: Circular Queue with Array
	
	class MovingAverage:
    def __init__(self, size: int):
        self.size = size
        self.queue = [0] * self.size
        self.head = self.window_sum = 0
        # number of elements seen so far
        self.count = 0

    def next(self, val: int) -> float:
        self.count += 1
        # calculate the new sum by shifting the window
        tail = (self.head + 1) % self.size
        self.window_sum = self.window_sum - self.queue[tail] + val
        # move on to the next head
        self.head = (self.head + 1) % self.size
        self.queue[self.head] = val
        return self.window_sum / min(self.size, self.count)
  
```
</details>  
	
#### 353. Design Snake Game
  
<details>
<summary>code</summary>
  
```
class SnakeGame:

    def __init__(self, width: int, height: int, food: List[List[int]]):
        """
        Initialize your data structure here.
        @param width - screen width
        @param height - screen height 
        @param food - A list of food positions
        E.g food = [[1,1], [1,0]] means the first food is positioned at [1,1], the second is at [1,0].
        """
        self.snake = collections.deque([(0,0)])    # snake head is at the front
        self.snake_set = {(0,0) : 1}
        self.width = width
        self.height = height
        self.food = food
        self.food_index = 0
        self.movement = {'U': [-1, 0], 'L': [0, -1], 'R': [0, 1], 'D': [1, 0]}
        

    def move(self, direction: str) -> int:
        """
        Moves the snake.
        @param direction - 'U' = Up, 'L' = Left, 'R' = Right, 'D' = Down 
        @return The game's score after the move. Return -1 if game over. 
        Game over when snake crosses the screen boundary or bites its body.
        """
        
        newHead = (self.snake[0][0] + self.movement[direction][0],
                   self.snake[0][1] + self.movement[direction][1])
        
        # Boundary conditions.
        crosses_boundary1 = newHead[0] < 0 or newHead[0] >= self.height
        crosses_boundary2 = newHead[1] < 0 or newHead[1] >= self.width
        
        # Checking if the snake bites itself.
        bites_itself = newHead in self.snake_set and newHead != self.snake[-1]
     
        # If any of the terminal conditions are satisfied, then we exit with rcode -1.
        if crosses_boundary1 or crosses_boundary2 or bites_itself:
            return -1

        # Note the food list could be empty at this point.
        next_food_item = self.food[self.food_index] if self.food_index < len(self.food) else None
        
        # If there's an available food item and it is on the cell occupied by the snake after the move, eat it
        if self.food_index < len(self.food) and \
            next_food_item[0] == newHead[0] and \
                next_food_item[1] == newHead[1]:  # eat food
            self.food_index += 1
        else:    # not eating food: delete tail                 
            tail = self.snake.pop()  
            del self.snake_set[tail]
            
        # A new head always gets added
        self.snake.appendleft(newHead)
        
        # Also add the head to the set
        self.snake_set[newHead] = 1

        return len(self.snake) - 1
        


# Your SnakeGame object will be instantiated and called as such:
# obj = SnakeGame(width, height, food)
# param_1 = obj.move(direction)  
  
```
</details>  
	
#### 358. Rearrange String k Distance Apart
  
<details>
<summary>code</summary>
  
```
def rearrangeString(self, s, k):
        n = len(s)
        if not k: return s
        count = collections.Counter(s)
        maxf = max(count.values())
        if (maxf - 1) * k + count.values().count(maxf) > len(s):
            return ""
        res = list(s)
        i = (n - 1) % k
        for c in sorted(count, key=lambda i: -count[i]):
            for j in range(count[c]):
                res[i] = c
                i += k
                if i >= n:
                    i = (i - 1) % k
        return "".join(res)  
  
```
</details>
		
#### 359. Logger Rate Limiter
  
<details>
<summary>code</summary>
  
```
from collections import deque

class Logger(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self._msg_set = set()
        self._msg_queue = deque()
    
    def shouldPrintMessage(self, timestamp, message):
        """
        Returns true if the message should be printed in the given timestamp, otherwise returns false.
        """
        while self._msg_queue:
            msg, ts = self._msg_queue[0]
            if timestamp - ts >= 10:
                self._msg_queue.popleft()
                self._msg_set.remove(msg)
            else:
                break
        
        if message not in self._msg_set:
            self._msg_set.add(message)
            self._msg_queue.append((message, timestamp))
            return True
        else:
            return False  
		
  Approach 2: Hashtable / Dictionary
		
	class Logger(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self._msg_dict = {}
    
    def shouldPrintMessage(self, timestamp, message):
        """
        Returns true if the message should be printed in the given timestamp, otherwise returns false.
        """
        if message not in self._msg_dict:
            # case 1). add the message to print
            self._msg_dict[message] = timestamp
            return True

        if timestamp - self._msg_dict[message] >= 10:
            # case 2). update the timestamp of the message
            self._msg_dict[message] = timestamp
            return True
        else:
            return False
	
  
```
</details>  
		
#### 360. Sort Transformed Array
  
<details>
<summary>code</summary>
  
```
def sortTransformedArray(self, nums, a, b, c):
    nums = [x*x*a + x*b + c for x in nums]
    ret = [0] * len(nums)
    p1, p2 = 0, len(nums) - 1
    i, d = (p1, 1) if a < 0 else (p2, -1)
    while p1 <= p2:
        if nums[p1] * -d > nums[p2] * -d:
            ret[i] = nums[p1]
            p1 += 1
        else:
            ret[i] = nums[p2]
            p2 -=1
        i += d
    return ret  
  
```
</details>  
		
#### 361. Bomb Enemy
  
<details>
<summary>code</summary>
  
```
class Solution:
    def maxKilledEnemies(self, grid: List[List[str]]) -> int:
        if len(grid) == 0:
            return 0

        rows, cols = len(grid), len(grid[0])

        max_count = 0
        row_hits = 0
        col_hits = [0] * cols

        for row in range(0, rows):
            for col in range(0, cols):
                # reset the hits on the row, if necessary.
                if col == 0 or grid[row][col - 1] == 'W':
                    row_hits = 0
                    for k in range(col, cols):
                        if grid[row][k] == 'W':
                            # stop the scan when we hit the wall.
                            break
                        elif grid[row][k] == 'E':
                            row_hits += 1

                # reset the hits on the col, if necessary.
                if row == 0 or grid[row - 1][col] == 'W':
                    col_hits[col] = 0
                    for k in range(row, rows):
                        if grid[k][col] == 'W':
                            break
                        elif grid[k][col] == 'E':
                            col_hits[col] += 1

                # count the hits for each empty cell.
                if grid[row][col] == '0':
                    total_hits = row_hits + col_hits[col]
                    max_count = max(max_count, total_hits)

        return max_count  
  
```
</details>  
		
#### 362. Design Hit Counter
  
<details>
<summary>code</summary>
  
```
 class HitCounter(object):

def __init__(self):
    """
    Initialize your data structure here.
    """
    from collections import deque
    
    self.num_of_hits = 0
    self.time_hits = deque()
    

def hit(self, timestamp):
    """
    Record a hit.
    @param timestamp - The current timestamp (in seconds granularity).
    :type timestamp: int
    :rtype: void
    """
    if not self.time_hits or self.time_hits[-1][0] != timestamp:
        self.time_hits.append([timestamp, 1])
    else:
        self.time_hits[-1][1] += 1
    
    self.num_of_hits += 1
            
    

def getHits(self, timestamp):
    """
    Return the number of hits in the past 5 minutes.
    @param timestamp - The current timestamp (in seconds granularity).
    :type timestamp: int
    :rtype: int
    """
    while self.time_hits and self.time_hits[0][0] <= timestamp - 300:
        self.num_of_hits -= self.time_hits.popleft()[1]
    
    return self.num_of_hits 
  
```
</details> 
		
#### 364. Nested List Weight Sum II
  
<details>
<summary>code</summary>
  
```
 def depthSumInverse(self, nestedList: List[NestedInteger]) -> int:
        unweighted = 0
        weighted = 0
        while nestedList:
            nextLevel = []
            for item in nestedList:
                if item.isInteger():
                    unweighted += item.getInteger()
                else:
                    nextLevel.extend(item.getList())
            weighted += unweighted
            nestedList = nextLevel
        return weighted 
  
```
</details>  
		
#### 366. Find Leaves of Binary Tree
  
<details>
<summary>code</summary>
  
```
class Solution(object):
    def findLeaves(self, root):
        def order(root, dic):
            if not root:
                return 0
            left = order(root.left, dic)
            right = order(root.right, dic)
            lev = max(left, right) + 1
            dic[lev] += root.val,
            return lev
        dic, ret = collections.defaultdict(list), []
        order(root, dic)
        for i in range(1, len(dic) + 1):
            ret.append(dic[i])
        return ret  
  
```
</details> 
		
#### 369. Plus One Linked List
  
<details>
<summary>code</summary>
  
```
class Solution:
    def plusOne(self, head: ListNode) -> ListNode:
        # sentinel head
        sentinel = ListNode(0)
        sentinel.next = head
        not_nine = sentinel

        # find the rightmost not-nine digit
        while head:
            if head.val != 9:
                not_nine = head
            head = head.next

        # increase this rightmost not-nine digit by 1
        not_nine.val += 1
        not_nine = not_nine.next

        # set all the following nines to zeros
        while not_nine:
            not_nine.val = 0
            not_nine = not_nine.next

        return sentinel if sentinel.val else sentinel.next  
  
```
</details>  
		
#### 370. Range Addition
  
<details>
<summary>code</summary>
  
```
class Solution(object):
    def getModifiedArray(self, length, updates):
        """
        :type length: int
        :type updates: List[List[int]]
        :rtype: List[int]
        """
        res = [0] * length
        for update in updates:
            start, end, inc = update
            res[start] += inc
            
            if end + 1 <= length - 1:
                res[end+1] -= inc

        sum = 0
        for i in range(length):
            sum += res[i]
            res[i] = sum
        return res  
  
```
</details>  
		
#### 422. Valid Word Square
  
<details>
<summary>code</summary>
  
```
def validWordSquare(self, words):
    return map(None, *words) == map(None, *map(None, *words))
Or saving some work but taking two lines:

def validWordSquare(self, words):
    t = map(None, *words)
    return t == map(None, *t)  
  
```
</details>  
		
#### 425. Word Squares
  
<details>
<summary>code</summary>
  
```
class Solution {
  int N = 0;
  String[] words = null;
  HashMap<String, List<String>> prefixHashTable = null;

  public List<List<String>> wordSquares(String[] words) {
    this.words = words;
    this.N = words[0].length();

    List<List<String>> results = new ArrayList<List<String>>();
    this.buildPrefixHashTable(words);

    for (String word : words) {
      LinkedList<String> wordSquares = new LinkedList<String>();
      wordSquares.addLast(word);
      this.backtracking(1, wordSquares, results);
    }
    return results;
  }

  protected void backtracking(int step, LinkedList<String> wordSquares,
                              List<List<String>> results) {
    if (step == N) {
      results.add((List<String>) wordSquares.clone());
      return;
    }

    StringBuilder prefix = new StringBuilder();
    for (String word : wordSquares) {
      prefix.append(word.charAt(step));
    }

    for (String candidate : this.getWordsWithPrefix(prefix.toString())) {
      wordSquares.addLast(candidate);
      this.backtracking(step + 1, wordSquares, results);
      wordSquares.removeLast();
    }
  }

  protected void buildPrefixHashTable(String[] words) {
    this.prefixHashTable = new HashMap<String, List<String>>();

    for (String word : words) {
      for (int i = 1; i < this.N; ++i) {
        String prefix = word.substring(0, i);
        List<String> wordList = this.prefixHashTable.get(prefix);
        if (wordList == null) {
          wordList = new ArrayList<String>();
          wordList.add(word);
          this.prefixHashTable.put(prefix, wordList);
        } else {
          wordList.add(word);
        }
      }
    }
  }

  protected List<String> getWordsWithPrefix(String prefix) {
    List<String> wordList = this.prefixHashTable.get(prefix);
    return (wordList != null ? wordList : new ArrayList<String>());
  }
}  
  
```
</details>  
		
#### 426. Convert Binary Search Tree to Sorted Doubly Linked List
  
<details>
<summary>code</summary>
  
```
class Solution:
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        def helper(node):
            """
            Performs standard inorder traversal:
            left -> node -> right
            and links all nodes into DLL
            """
            nonlocal last, first
            if node:
                # left
                helper(node.left)
                # node 
                if last:
                    # link the previous node (last)
                    # with the current one (node)
                    last.right = node
                    node.left = last
                else:
                    # keep the smallest node
                    # to close DLL later on
                    first = node        
                last = node
                # right
                helper(node.right)
        
        if not root:
            return None
        
        # the smallest (first) and the largest (last) nodes
        first, last = None, None
        helper(root)
        # close DLL
        last.right = first
        first.left = last
        return first  
  
```
</details>  
		
#### 428. Serialize and Deserialize N-ary Tree
  
<details>
<summary>code</summary>
  
```
class Codec:
    def serialize(self, root):	
        serial = []

        def preorder(node):

            if not node:
                return

            serial.append(str(node.val))

            for child in node.children:
                preorder(child)

            serial.append("#")      # indicates no more children, continue serialization from parent

        preorder(root)
        return " ".join(serial)

    def deserialize(self, data):	
        if not data:
            return None

        tokens = deque(data.split())
        root = Node(int(tokens.popleft()), [])

        def helper(node):

            if not tokens:
                return

            while tokens[0] != "#": # add child nodes with subtrees
                value = tokens.popleft()
                child = Node(int(value), [])
                node.children.append(child)
                helper(child)

            tokens.popleft()        # discard the "#"

        helper(root)
        return root  
  
```
</details>  
		
#### 431. Encode N-ary Tree to Binary Tree
  
<details>
<summary>code</summary>
  
```
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
"""
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
"""
class Codec:
    def encode(self, root):
        """Encodes an n-ary tree to a binary tree.
        :type root: Node
        :rtype: TreeNode
        """
        if not root:
            return None

        rootNode = TreeNode(root.val)
        queue = deque([(rootNode, root)])

        while queue:
            parent, curr = queue.popleft()
            prevBNode = None
            headBNode = None
            # traverse each child one by one
            for child in curr.children:
                newBNode = TreeNode(child.val)
                if prevBNode:
                    prevBNode.right = newBNode
                else:
                    headBNode = newBNode
                prevBNode = newBNode
                queue.append((newBNode, child))

            # use the first child in the left node of parent
            parent.left = headBNode

        return rootNode


    def decode(self, data):
        """Decodes your binary tree to an n-ary tree.
        :type data: TreeNode
        :rtype: Node
        """
        if not data:
            return None

        # should set the default value to [] rather than None,
        # otherwise it wont pass the test cases.
        rootNode = Node(data.val, [])

        queue = deque([(rootNode, data)])

        while queue:
            parent, curr = queue.popleft()

            firstChild = curr.left
            sibling = firstChild

            while sibling:
                # Note: the initial value of the children list should not be None, which is assumed by the online judge.
                newNode = Node(sibling.val, [])
                parent.children.append(newNode)
                queue.append((newNode, sibling))
                sibling = sibling.right

        return rootNode  
  
```
</details>  
		
#### 439. Ternary Expression Parser
  
<details>
<summary>code</summary>
  
```
class Solution(object):
    def parseTernary(self, expression):
        """
        :type expression: str
        :rtype: str
        """
        stack = []
        d = {}
        for i in xrange(0, len(expression)):
            if expression[i] == "?":
                stack.append(("?", i))
            elif expression[i] == ":":
                _, pos = stack.pop()
                d[pos] = i

        def dfs(expr, start, end, d):
            if end - start + 1 < 5:
                return expr[start:end+1]
            iSep = d[start + 1]
            stmt = expr[start]
            return dfs(expr, start + 2, iSep - 1, d) if stmt == "T" else dfs(expr, iSep + 1, end, d)
        return dfs(expression, 0, len(expression), d)  
  
```
</details>  
		
#### 465. Optimal Account Balancing
  
<details>
<summary>code</summary>
  
```
 def minTransfers(self, transactions):
        """
        :type transactions: List[List[int]]
        :rtype: int
        """
        m = collections.defaultdict(int)
        
        for t in transactions:
            m[t[0]]-=t[2]
            m[t[1]]+=t[2]
        
        debt = m.values()
        
        def dfs(s):
            while(s<len(debt) and debt[s]==0):
                s+=1
            if s==len(debt): return 0
            
            r = float('inf')
            for i in range(s+1,len(debt)):
                if debt[i]*debt[s]<0:
                    # settle s with i
                    debt[i]+=debt[s]
                    r=min(r,1+dfs(s+1))
                    # backtrack
                    debt[i]-=debt[s]
            return r
        
        return dfs(0)  
  
```
</details>  
		
#### 471. Encode String with Shortest Length
  
<details>
<summary>code</summary>
  
```
def encode(self, s, memo={}):
    if s not in memo:
        n = len(s)
        i = (s + s).find(s, 1)
        one = '%d[%s]' % (n / i, self.encode(s[:i])) if i < n else s
        multi = [self.encode(s[:i]) + self.encode(s[i:]) for i in xrange(1, n)]
        memo[s] = min([s, one] + multi, key=len)
    return memo[s]  
  
```
</details>  
		
#### 484. Find Permutation
  
<details>
<summary>code</summary>
  
```
def findPermutation(self, s):
    ret = []
    for i in range(len(s)):
      if s[i] == 'I':
        ret.extend(range(i + 1, len(ret), -1))
    ret.extend(range(len(s) + 1, len(ret), -1))
    return ret 
  
```
</details>  
		
#### 487. Max Consecutive Ones II
  
<details>
<summary>code</summary>
  
```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        longest_sequence = 0
        for left in range(len(nums)):
            num_zeroes = 0
            for right in range(left, len(nums)):   # check every consecutive sequence
                if num_zeroes == 2:
                    break
                if nums[right] == 0:               # count how many 0's
                    num_zeroes += 1
                if num_zeroes <= 1:                 # update answer if it's valid
                    longest_sequence = max(longest_sequence, right - left + 1)
        return longest_sequence  
  
```
</details>  
		
#### 489. Robot Room Cleaner
  
<details>
<summary>code</summary>
  
```
class Solution(object):       
    def cleanRoom(self, robot):
        """
        :type robot: Robot
        :rtype: None
        """
        def go_back():
            robot.turnRight()
            robot.turnRight()
            robot.move()
            robot.turnRight()
            robot.turnRight()
            
        def backtrack(cell = (0, 0), d = 0):
            visited.add(cell)
            robot.clean()
            # going clockwise : 0: 'up', 1: 'right', 2: 'down', 3: 'left'
            for i in range(4):
                new_d = (d + i) % 4
                new_cell = (cell[0] + directions[new_d][0], \
                            cell[1] + directions[new_d][1])
                
                if not new_cell in visited and robot.move():
                    backtrack(new_cell, new_d)
                    go_back()
                # turn the robot following chosen direction : clockwise
                robot.turnRight()
    
        # going clockwise : 0: 'up', 1: 'right', 2: 'down', 3: 'left'
        directions = [(-1, 0), (0, 1), (1, 0), (0, -1)]
        visited = set()
        backtrack()  
  
```
</details>  
	
#### 490. The Maze
  
<details>
<summary>code</summary>
  
```
 def hasPath(self, maze, start, destination):

        Q = [start]
        n = len(maze)
        m = len(maze[0])
        dirs = ((0, 1), (0, -1), (1, 0), (-1, 0))
        
        while Q:
            # Use Q.pop() as DFS or Q.popleft() with deque from collections library for better performance. Kudos to @whglamrock
            i, j = Q.pop(0)
            maze[i][j] = 2

            if i == destination[0] and j == destination[1]:
                return True
            
            for x, y in dirs:
                row = i + x
                col = j + y
                while 0 <= row < n and 0 <= col < m and maze[row][col] != 1:
                    row += x
                    col += y
                row -= x
                col -= y
                if maze[row][col] == 0:
                    Q.append([row, col])
        
        return False 
  
```
</details>  
	
#### 499. The Maze III
  
<details>
<summary>code</summary>
  
```
def findShortestWay(self, A, ball, hole):
    ball, hole = tuple(ball), tuple(hole)
    R, C = len(A), len(A[0])
    
    def neighbors(r, c):
        for dr, dc, di in [(-1, 0, 'u'), (0, 1, 'r'), 
                           (0, -1, 'l'), (1, 0, 'd')]:
            cr, cc, dist = r, c, 0
            while (0 <= cr + dr < R and 
                    0 <= cc + dc < C and
                    not A[cr+dr][cc+dc]):
                cr += dr
                cc += dc
                dist += 1
                if (cr, cc) == hole:
                    break
            yield (cr, cc), di, dist
    
    pq = [(0, '', ball)]
    seen = set()
    while pq:
        dist, path, node = heapq.heappop(pq)
        if node in seen: continue
        if node == hole: return path
        seen.add(node)
        for nei, di, nei_dist in neighbors(*node):
            heapq.heappush(pq, (dist+nei_dist, path+di, nei) )
        
    return "impossible"  
  
```
</details>  
	
#### 505. The Maze II
  
<details>
<summary>code</summary>
  
```
class Solution:
    def shortestDistance(self, maze, start, destination):
        m, n, q, stopped = len(maze), len(maze[0]), [(0, start[0], start[1])], {(start[0], start[1]):0}
        while q:
            dist, x, y = heapq.heappop(q)
            if [x, y] == destination:
                return dist
            for i, j in ((-1, 0), (1, 0), (0, -1), (0, 1)):
                newX, newY, d = x, y, 0
                while 0 <= newX + i < m and 0 <= newY + j < n and maze[newX + i][newY + j] != 1:
                    newX += i
                    newY += j
                    d += 1
                if (newX, newY) not in stopped or dist + d < stopped[(newX, newY)]:
                    stopped[(newX, newY)] = dist + d
                    heapq.heappush(q, (dist + d, newX, newY))
        return -1  
  
```
</details>  
	
#### 510. Inorder Successor in BST II
  
<details>
<summary>code</summary>
  
```
class Solution:
    def inorderSuccessor(self, node: 'Node') -> 'Node':
        # the successor is somewhere lower in the right subtree
        if node.right:
            node = node.right
            while node.left:
                node = node.left
            return node
        
        # the successor is somewhere upper in the tree
        while node.parent and node == node.parent.right:
            node = node.parent
        return node.parent  
  
```
</details>  
	
#### 527. Word Abbreviation
  
<details>
<summary>code</summary>
  
```
class Solution(object):
    def wordsAbbreviation(self, words):
        def abbrev(word, i = 0):
            if (len(word) - i <= 3): return word
            return word[:i+1] + str(len(word) - i - 2) + word[-1]

        N = len(words)
        ans = map(abbrev, words)
        prefix = [0] * N

        for i in xrange(N):
            while True:
                dupes = set()
                for j in xrange(i+1, N):
                    if ans[i] == ans[j]:
                        dupes.add(j)

                if not dupes: break
                dupes.add(i)
                for k in dupes:
                    prefix[k] += 1
                    ans[k] = abbrev(words[k], prefix[k])

        return ans  
  
```
</details>  
	
#### 531. Lonely Pixel I
  
<details>
<summary>code</summary>
  
```
def findLonelyPixel(self, picture):
    return sum(col.count('B') == 1 == picture[col.index('B')].count('B') for col in zip(*picture))  
  
```
</details> 
	
#### 536. Construct Binary Tree from String
  
<details>
<summary>code</summary>
  
```
class Solution:
    def str2tree(self, s: str) -> TreeNode:
        return self._str2treeInternal(s, 0)[0]
    
    def _getNumber(self, s: str, index: int) -> (int, int):
        
        is_negative = False
        
        # A negative number
        if s[index] == '-':
            is_negative = True
            index = index + 1
        
        number = 0
        while index < len(s) and s[index].isdigit():
            number = number * 10 + int(s[index])
            index += 1
        
        return number if not is_negative else -number, index
            
    
    def _str2treeInternal(self, s: str, index: int) -> (TreeNode, int):
        
        if index == len(s):
            return None, index
        
        # Start of the tree will always contain a number representing
        # the root of the tree. So we calculate that first.
        value, index = self._getNumber(s, index)
        node = TreeNode(value)
        
        # Next, if there is any data left, we check for the first subtree
        # which according to the problem statement will always be the left child.
        if index < len(s) and s[index] == '(':
            node.left, index = self._str2treeInternal(s, index + 1)
        
        # Indicates a right child
        if node.left and index < len(s) and s[index] == '(':
            node.right, index = self._str2treeInternal(s, index + 1)
        
        return node, index + 1 if index < len(s) and s[index] == ')' else index  
  
```
</details>  
	
#### 545. Boundary of Binary Tree
  
<details>
<summary>code</summary>
  
```
class Solution(object):
    def boundaryOfBinaryTree(self, root):
        def dfs_leftmost(node):
            if not node or not node.left and not node.right:
                return
            boundary.append(node.val)
            if node.left:
                dfs_leftmost(node.left)
            else:
                dfs_leftmost(node.right)

        def dfs_leaves(node):
            if not node:
                return
            dfs_leaves(node.left)
            if node != root and not node.left and not node.right:
                boundary.append(node.val)
            dfs_leaves(node.right)

        def dfs_rightmost(node):
            if not node or not node.left and not node.right:
                return
            if node.right:
                dfs_rightmost(node.right)
            else:
                dfs_rightmost(node.left)
            boundary.append(node.val)

        if not root:
            return []
        boundary = [root.val]
        dfs_leftmost(root.left)
        dfs_leaves(root)
        dfs_rightmost(root.right)
        return boundary  
  
```
</details>  
	
#### 549. Binary Tree Longest Consecutive Sequence II
  
<details>
<summary>code</summary>
  
```
class Solution:
    def longestConsecutive(self, root: TreeNode) -> int:
                
        def longest_path(root: TreeNode) -> List[int]:
            nonlocal maxval
            
            if not root:
                return [0, 0]
            
            inr = dcr = 1
            if root.left:
                left = longest_path(root.left)
                if (root.val == root.left.val + 1):
                    dcr = left[1] + 1
                elif (root.val == root.left.val - 1):
                    inr = left[0] + 1
            
            if root.right:
                right = longest_path(root.right)
                if (root.val == root.right.val + 1):
                    dcr = max(dcr, right[1] + 1)
                elif (root.val == root.right.val - 1):
                    inr = max(inr, right[0] + 1)
                    
            maxval = max(maxval, dcr + inr - 1)
            return [inr, dcr]
        
        maxval = 0
        longest_path(root)
        return maxval  
  
```
</details>  
	
#### 562. Longest Line of Consecutive One in Matrix
  
<details>
<summary>code</summary>
  
```
def longestLine(self, M):
    maxlen = 0
    currlen = collections.Counter()
    for i, row in enumerate(M):
        for j, a in enumerate(row):
            for key in i, j+.1, i+j+.2, i-j+.3:
                currlen[key] = (currlen[key] + 1) * a
                maxlen = max(maxlen, currlen[key])
    return maxlen  
  
```
</details>  
	
#### 568. Maximum Vacation Days
  
<details>
<summary>code</summary>
  
```
def maxVacationDays(self, flights, days):
    NINF = float('-inf')
    N, K = len(days), len(days[0])
    best = [NINF] * N
    best[0] = 0
    
    for t in xrange(K):
        cur = [NINF] * N
        for i in xrange(N):
            for j, adj in enumerate(flights[i]):
                if adj or i == j:
                    cur[j] = max(cur[j], best[i] + days[j][t])
        best = cur
    return max(best)  
  
```
</details>  
	
#### 582. Kill Process
  
<details>
<summary>code</summary>
  
```
def killProcess(self, pid, ppid, kill):
        d = collections.defaultdict(list)
        for c, p in zip(pid, ppid): d[p].append(c)
        bfs = [kill]
        for i in bfs: bfs.extend(d.get(i, []))
        return bfs  
  
```
</details>  
	
#### 588. Design In-Memory File System
  
<details>
<summary>code</summary>
  
```
from collections import defaultdict
class Node:
    def __init__(self):
        self.child=defaultdict(Node)
        self.content=""
        
class FileSystem(object):

    def __init__(self):
        self.root=Node()
        
    def find(self,path):#find and return node at path.
        curr=self.root
        if len(path)==1:
            return self.root
        for word in path.split("/")[1:]:
            curr=curr.child[word]
        return curr
        
    def ls(self, path):
        curr=self.find(path)
        if curr.content:#file path,return file name
            return [path.split('/')[-1]]
        return sorted(curr.child.keys())
		
    def mkdir(self, path):
        self.find(path)

    def addContentToFile(self, filePath, content):
        curr=self.find(filePath)
        curr.content+=content

    def readContentFromFile(self, filePath):
        curr=self.find(filePath)
        return curr.content  
  
```
</details>  
	
#### 604. Design Compressed String Iterator
  
<details>
<summary>code</summary>
  
```
import re
class StringIterator(object):
    def __init__(self, compressedString):
        self.tokens = []
        for token in re.findall('\D\d+', compressedString):
            self.tokens.append((token[0], int(token[1:])))
        self.tokens = self.tokens[::-1]

    def next(self):
        if not self.tokens: return ' '
        t, n = self.tokens.pop()
        if n > 1: 
            self.tokens.append((t, n - 1))
        return t

    def hasNext(self):
        return bool(self.tokens)  
  
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

