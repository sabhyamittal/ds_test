## Questions:

### 1.Read N Characters Given Read4

Given a file and assume that you can only read the file using a given method read4, implement a method to read n characters.

Method read4:

The API read4 reads four consecutive characters from file, then writes those characters into the buffer array buf4.

The return value is the number of actual characters read.

Note that read4() has its own file pointer, much like FILE *fp in C.

#### Algorithm

Let's use an internal buffer of 4 characters to solve this problem:

File -> Internal Buffer of 4 Characters -> Buffer of N Characters.

Initialize the number of copied characters copiedChars = 0, and the number of read characters: readChars = 4. It's convenient initialize readChars to 4 and then use readChars != 4 as EOF marker.

Initialize an internal buffer of 4 characters: buf4.

While number of copied characters is less than N: copiedChars < n and there are still characters in the file: readChars == 4:

Read from file into internal buffer: readChars = read4(buf4).

Copy the characters from internal buffer buf4 into main buffer buf one by one. Increase copiedChars after each character. In the number of copied characters is equal to N: copiedChars == n, interrupt the copy process and return copiedChars.

#### Complexity Analysis

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

This solution is mainly suitable for the languages (C, C++, Golang) where pointers allow to append directly to the primary buffer buf.

#### Algorithm

Initialize the number of copied characters copiedChars = 0, and the number of read characters: readChars = 4.

While number of copied characters is less than N: copiedChars < n and there are still characters in the file: readChars == 4:

Read from file directly into buffer: read4(buf + copiedChars).

Increase copiedChars: copiedChars += readChars.

Now buf contains at least N characters. Return min(n, copiedChars).

#### Complexity Analysis

Time complexity:O(N) to copy N characters.

Space complexity: O(1).

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
  

