## Questions:

#### 1.Read N Characters Given Read4

Back to the problem, the question is "how does the memory work":

Because of the physical implementation, loading 4 bytes in DDR is faster than to load 1 byte 4 times.

On the majority of computers today, collection of 4 bytes, or 32 bits, is called a word. Most modern CPUs are optimized for the operations with words.

To sum up, the problem is a practical low-level question. The standard approach (Approach 1) to solve it using the internal buffer of 4 characters:

File -> Internal Buffer of 4 Characters -> Buffer of N Characters.

img Figure 1. Approach 1: solution with internal buffer.

Once it's done, and you show your understanding of memory operations, the follow-up question is how to speed up. The answer (Approach 2) is quite straightforward. If it's possible, 
do not use the internal buffer of 4 characters to avoid the double copy:

File -> Buffer of N Characters.

img Figure 2. Approach 2: solution without internal buffer.
<de


Approach 1: Use Internal Buffer of 4 Characters
img Figure 3. Solution with internal buffer.

Algorithm

Let's use an internal buffer of 4 characters to solve this problem:

File -> Internal Buffer of 4 Characters -> Buffer of N Characters.

Initialize the number of copied characters copiedChars = 0, and the number of read characters: readChars = 4. It's convenient initialize readChars to 4 and then use readChars != 4 as EOF marker.

Initialize an internal buffer of 4 characters: buf4.

While number of copied characters is less than N: copiedChars < n and there are still characters in the file: readChars == 4:

Read from file into internal buffer: readChars = read4(buf4).

Copy the characters from internal buffer buf4 into main buffer buf one by one. Increase copiedChars after each character. In the number of copied characters is equal to N: copiedChars == n, interrupt the copy process and return copiedChars.

Implementation


Complexity Analysis

Time complexity:O(N) to copy N characters.

Space complexity:O(1) to keep buf4 of 4 elements.

<details>
  <summary>code</summary>
  
  ```
class Solution {
public:
    int read(char *buf, int n) {
        int copiedChars = 0, readChars = 4;
        char buf4[4];
        
        while (copiedChars < n && readChars == 4) {
            readChars = read4(buf4);
            
            for (int i = 0; i < readChars; ++i) {
                if (copiedChars == n)
                    return copiedChars;
                buf[copiedChars] = buf4[i];
                ++copiedChars;    
            }    
        }
        return copiedChars;
    }
};
  
  ```
  </details>

Approach 2: Speed Up: No Internal Buffer
img Figure 4. Solution without internal buffer.

This solution is mainly suitable for the languages (C, C++, Golang) where pointers allow to append directly to the primary buffer buf.

Algorithm

Initialize the number of copied characters copiedChars = 0, and the number of read characters: readChars = 4.

While number of copied characters is less than N: copiedChars < n and there are still characters in the file: readChars == 4:

Read from file directly into buffer: read4(buf + copiedChars).

Increase copiedChars: copiedChars += readChars.

Now buf contains at least N characters. Return min(n, copiedChars).

Implementation

<details>
  <summary>code</summary>
  ```
  class Solution {
public:
    int read(char *buf, int n) {
        int copiedChars = 0, readChars = 4;
        
        while (copiedChars < n && readChars == 4) {
            readChars = read4(buf + copiedChars);
            copiedChars += readChars;
        }
        return min(n, copiedChars);
    }
};
                              
 ```
 </details>
Complexity Analysis

Time complexity: \mathcal{O}(N)O(N) to copy N characters.

Space complexity: \mathcal{O}(1)O(1).
