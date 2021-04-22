# Introduction to Algorithms
##  Foundations

### The role of algorithm in computing

#### Algorithms

 Algorithms are definite number of steps to solve a given problem in definite amount of time.
 
#### Algorithms as a technology

 For example:The travelling salesman problem,
 which finds out the shortest path /route between two cities hence it is used by GPS which is used all over globe.
 
### Getting Started

#### Insertion Sort

Efficient algorithm for sorting small number of elements.EX: sorting a deck of cards.

#### Analyzing insertion sort

Consider sorting n numbers stored in array A by first finding the smallest element of A and exchanging it with the element in A[1]. Then find the second smallest 
element of A, and exchange it with A[2]. Continue in this manner for the first n - 1 elements of A.

#### Designing algorithms

In designing of Algorithm, complexity analysis of an algorithm is an essential aspect. Mainly, algorithmic complexity is concerned about its performance, how fast or slow it works.

The complexity of an algorithm describes the efficiency of the algorithm in terms of the amount of the memory required to process the data and the processing time.

Complexity of an algorithm is analyzed in two perspectives: Time and Space.

#### Code in c

<details>
<summary>Answer</summary>
 
```
void insertionSort(int arr[], int n)
{
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
          
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
 
void printArray(int arr[], int n)
{
    int i;
    for (i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}
 
int main()
{
    int arr[] = { 12, 11, 13, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
 
    insertionSort(arr, n);
    printArray(arr, n);
 
    return 0;
}
```
</details>

### Growth of functions

#### Asymtotic notations

Execution time of an algorithm depends on the instruction set, processor speed, disk I/O speed, etc. Hence, we estimate the efficiency of an algorithm asymptotically.

Time function of an algorithm is represented by T(n), where n is the input size.

Different types of asymptotic notations are used to represent the complexity of an algorithm. Following asymptotic notations are used to calculate the running time complexity of an algorithm.

O − Big Oh

Ω − Big omega

θ − Big theta

o − Little Oh

ω − Little omega


#### Standard notations and common functions

O: Asymptotic Upper Bound
‘O’ (Big Oh) is the most commonly used notation. A function f(n) can be represented is the order of g(n) that is O(g(n)), if there exists a value of positive integer n as n0 and a positive constant c such that −

f(n)⩽c.g(n) for n>n0 in all case

Hence, function g(n) is an upper bound for function f(n), as g(n) grows faster than f(n).

Example
Let us consider a given function, f(n)=4.n3+10.n2+5.n+1
Considering g(n)=n3,

f(n)⩽5.g(n) for all the values of n>2
Hence, the complexity of f(n) can be represented as O(g(n)), i.e. O(n3)
Ω: Asymptotic Lower Bound
We say that f(n)=Ω(g(n)) when there exists constant c that f(n)⩾c.g(n) for all sufficiently large value of n. Here n is a positive integer. It means function g is a lower bound for function f; after a certain value of n, f will never go below g.

Example
Let us consider a given function, f(n)=4.n3+10.n2+5.n+1.

Considering g(n)=n3, f(n)⩾4.g(n) for all the values of n>0.

Hence, the complexity of f(n) can be represented as Ω(g(n)), i.e. Ω(n3)
θ: Asymptotic Tight Bound
We say that f(n)=θ(g(n)) when there exist constants c1 and c2 that c1.g(n)⩽f(n)⩽c2.g(n) for all sufficiently large value of n. Here n is a positive integer.

This means function g is a tight bound for function f.

Example
Let us consider a given function, f(n)=4.n3+10.n2+5.n+1
Considering g(n)=n3, 4.g(n)⩽f(n)⩽5.g(n) for all the large values of n.

Hence, the complexity of f(n) can be represented as θ(g(n)), i.e. θ(n3).

O - Notation
The asymptotic upper bound provided by O-notation may or may not be asymptotically tight. The bound 2.n2=O(n2) is asymptotically tight, but the bound 2.n=O(n2) is not.

We use o-notation to denote an upper bound that is not asymptotically tight.

We formally define o(g(n)) (little-oh of g of n) as the set f(n) = o(g(n)) for any positive constant c>0 and there exists a value n0>0, such that 0⩽f(n)⩽c.g(n).

Intuitively, in the o-notation, the function f(n) becomes insignificant relative to g(n) as n approaches infinity; that is,

limn→∞(f(n)g(n))=0
Example
Let us consider the same function, f(n)=4.n3+10.n2+5.n+1
Considering g(n)=n4,

limn→∞(4.n3+10.n2+5.n+1n4)=0
Hence, the complexity of f(n) can be represented as o(g(n)), i.e. o(n4).

ω – Notation
We use ω-notation to denote a lower bound that is not asymptotically tight. Formally, however, we define ω(g(n)) (little-omega of g of n) as the set f(n) = ω(g(n)) for any positive constant C > 0 and there exists a value n0>0, such that 0⩽c.g(n)<f(n).

For example, n22=ω(n), but n22≠ω(n2). The relation f(n)=ω(g(n)) implies that the following limit exists

limn→∞(f(n)g(n))=∞
That is, f(n) becomes arbitrarily large relative to g(n) as n approaches infinity.

Example
Let us consider same function, f(n)=4.n3+10.n2+5.n+1
Considering g(n)=n2,

limn→∞(4.n3+10.n2+5.n+1n2)=∞
Hence, the complexity of f(n) can be represented as o(g(n)), i.e. ω(n2).


### Divide and conquer

#### The maximum subarray problem

To find a subarray of the given array whose sum is maximum.
By divide and conquer->find the center indices->max on the LHS and RHS->sum of max.

#### Code in c
<details>
<summary>Answer</summary>
 
```
 
#include <stdio.h>
#include <limits.h>
 
// A naive solution to finding maximum subarray sum using divide-and-conquer
int maximum_sum(int A[], int n)
{
    int max_sum = INT_MIN;
    int sum = 0;
 
    // do for each subarray starting with `i`
    for (int i = 0; i < n - 1; i++)
    {
        // calculate the sum of subarray `A[i…j]`
 
        sum = 0;    // reset sum
 
        // do for each subarray ending at `j`
        for (int j = i; j < n; j++)
        {
            sum += A[j];
 
            // if the current subarray sum is greater than the maximum
            // sum calculated so far, update the maximum sum
            if (sum > max_sum) {
                max_sum = sum;
            }
        }
    }
 
    return max_sum;
}
 
int main(void)
{
    int arr[] = { 2, -4, 1, 9, -6, 7, -3 };
    int n = sizeof(arr) / sizeof(arr[0]);
 
    printf("The maximum sum of the subarray is %d", maximum_sum(arr, n));
 
    return 0;
}

```

</details>

#### Strassen’s Algorithm for matrix multiplication

Following is simple Divide and Conquer method to multiply two square matrices.
1) Divide matrices A and B in 4 sub-matrices of size N/2 x N/2 .
2) Calculate following values recursively. 

#### Code in c
<details>
<summary>Answer</summary>
 
```

#include<stdio.h>
int main(){
  int a[2][2], b[2][2], c[2][2], i, j;
  int m1, m2, m3, m4 , m5, m6, m7;
 
  printf("Enter the 4 elements of first matrix: ");
  for(i = 0;i < 2; i++)
      for(j = 0;j < 2; j++)
           scanf("%d", &a[i][j]);
 
  printf("Enter the 4 elements of second matrix: ");
  for(i = 0; i < 2; i++)
      for(j = 0;j < 2; j++)
           scanf("%d", &b[i][j]);
 
  printf("\nThe first matrix is\n");
  for(i = 0; i < 2; i++){
      printf("\n");
      for(j = 0; j < 2; j++)
           printf("%d\t", a[i][j]);
  }
 
  printf("\nThe second matrix is\n");
  for(i = 0;i < 2; i++){
      printf("\n");
      for(j = 0;j < 2; j++)
           printf("%d\t", b[i][j]);
  }
 
  m1= (a[0][0] + a[1][1]) * (b[0][0] + b[1][1]);
  m2= (a[1][0] + a[1][1]) * b[0][0];
  m3= a[0][0] * (b[0][1] - b[1][1]);
  m4= a[1][1] * (b[1][0] - b[0][0]);
  m5= (a[0][0] + a[0][1]) * b[1][1];
  m6= (a[1][0] - a[0][0]) * (b[0][0]+b[0][1]);
  m7= (a[0][1] - a[1][1]) * (b[1][0]+b[1][1]);
 
  c[0][0] = m1 + m4- m5 + m7;
  c[0][1] = m3 + m5;
  c[1][0] = m2 + m4;
  c[1][1] = m1 - m2 + m3 + m6;
 
   printf("\nAfter multiplication using Strassen's algorithm \n");
   for(i = 0; i < 2 ; i++){
      printf("\n");
      for(j = 0;j < 2; j++)
           printf("%d\t", c[i][j]);
   }
 
   return 0;
}
```
</details>

#### The substitution method for solving recurrences

The substitution method is a condensed way of proving an asymptotic bound on a recurrence by induction. In the substitution method, instead of trying to find an exact closed-form solution, we only try to find a closed-form bound on the recurrence.

#### The recursion tree method for solving recurrences

In this method, we draw a recurrence tree and calculate the time taken by every level of tree. Finally, we sum the work done at all levels. To draw the recurrence tree, we start from the given recurrence and keep drawing till we find a pattern among levels. The pattern is typically a arithmetic or geometric series.

For example consider the recurrence relation 
T(n) = T(n/4) + T(n/2) + cn2

           cn2
         /      \
     T(n/4)     T(n/2)

If we further break down the expression T(n/4) and T(n/2), 
we get following recursion tree.

                cn2
           /           \      
       c(n2)/16      c(n2)/4
      /      \          /     \
  T(n/16)     T(n/8)  T(n/8)    T(n/4) 
Breaking down further gives us following
                 cn2
            /            \      
       c(n2)/16          c(n2)/4
       /      \            /      \
c(n2)/256   c(n2)/64  c(n2)/64    c(n2)/16
 /    \      /    \    /    \       /    \  

To know the value of T(n), we need to calculate sum of tree 
nodes level by level. If we sum the above tree level by level, 
we get the following series
T(n)  = c(n^2 + 5(n^2)/16 + 25(n^2)/256) + ....
The above series is geometrical progression with ratio 5/16.

To get an upper bound, we can sum the infinite series. 
We get the sum as (n2)/(1 - 5/16) which is O(n2).



#### The master method for solving recurrences

Master Method is a direct way to get the solution. The master method works only for following type of recurrences or for recurrences that can be transformed to following type.

T(n) = aT(n/b) + f(n) where a >= 1 and b > 1
There are following three cases:
1. If f(n) = Θ(nc) where c < Logba then T(n) = Θ(nLogba)

2. If f(n) = Θ(nc) where c = Logba then T(n) = Θ(ncLog n)

3.If f(n) = Θ(nc) where c > Logba then T(n) = Θ(f(n))

#### Proof for master's theorem
From above function, we have:
T(n) = aT(n-b) + f(n)
T(n-b) = aT(n-2b) + f(n-b)
T(n-2b) = aT(n-3b) + f(n-2b)

Now,
T(n-b) = a2T(n-3b) + af(n-2b) + f(n-b)
T(n) = a3T(n-3b) + a2f(n-2b) + af(n-b) + f(n)
T(n) = Σi=0 to n ai f(n-ib) + constant, where f(n-ib) is O(n-ib)
T(n) = O(nk Σi=0 to n/b ai )

Where,
If a<1 then Σi=0 to n/b ai = O(1), T(n) = O(nk)

If a=1 then Σi=0 to n/b ai = O(n), T(n) = O(nk+1)

If a>1 then Σi=0 to n/b ai = O(an/b), T(n) = O(nkan/b)



### Probabilistic analysis and randomized theorem

#### The hiring problem

Suppose that you need to hire a new office assistant. Your previous attempts at hiring have been unsuccessful, and you decide to use an employment agency. The employment agency will send you one candidate each day. You will interview that person and then decide to either hire that person or not. You must pay the employment agency a small fee to interview an applicant. To actually hire an applicant is more costly, however, since you must fire your current office assistant and pay a large hiring fee to the employment agency. You are committed to having, at all times, the best possible person for the job. Therefore, you decide that, after interviewing each applicant, if that applicant is better qualified than the current office assistant, you will fire the current office assistant and hire the new applicant. You are willing to pay the resulting price of this strategy, but you wish to estimate what that price will be.

The procedure HIRE-ASSISTANT, given below, expresses this strategy for hiring in pseudocode. It assumes that the candidates for the office assistant job are numbered 1 through n. The procedure assumes that you are able to, after interviewing candidate i, determine if candidate i is the best candidate you have seen so far. To initialize, the procedure creates a dummy candidate, numbered 0, who is less qualified than each of the other candidates.

HIRE-ASSISTANT(n)
1  best ← 0     ® candidate 0 is a least-qualified dummy candidate
2  for i ← 1 to n
3       do interview candidate i
4          if candidate i is better than candidate best
5             then best ← i
6                  hire candidate i

#### Indicator random variables

#### Randomized algorithms

We might not know the distribution of inputs or be able to model it.

However, uniform random distributions are easier to analyze than unknown distributions.

To obtain such a distribution regardless of input distribution, we can randomize within the algorithm to impose a distribution on the inputs. Then it is easier to analzye expected behavior.

An algorithm is randomized if its behavior is determined in parts by values provided by a random number generator.

This requires a change in the hiring problem scenario:

The employment agency sends us a list of n candidates in advance and lets us choose the interview order.
We choose randomly.

#### Probabilistic analysis and further uses of indicator random variables


## Sorting and order statistics

### Heap Sort

#### Heaps

Heap sort can be understood as the improved version of the binary search tree. It does not create a node as in case of binary search tree instead it builds the heap by adjusting the position of elements within the array itself.

#### Maintaining the heap property

<details>
<summary>Answer</summary>
	
```
MIN-HEAPIFY(A, i)
l = LEFT(i)
r = RIGHT(i)
if l <= A.heap-size and A[l] < A[i]
    min = l
else
    min = i
if r <= A.heap-size and A[r] < A[min]
    min = r
if min != i
    exchange A[i] with A[min]
    MIN-HEAPIFY(A, min)
The running time is still O(log n).



MAX-HEAPIFY(A, i)
largest = -1
root = i
while largest != root
    l = LEFT(root)
    r = RIGHT(root)
    if l <= A.heap-size and A[l] > A[root]
        largest = l
    else
        largest = root
    if r <= A.heap-size and A[r] > A[largest]
        largest = r
    if largest != root:
        exchange A[root] with A[largest]
        root = largest
        largest = -1
	
```
</details>


#### Building a heap

<details>
<summary>Answer</summary>

```
BUILD-MAX-HEAP(A)
1.A.heap-size=A.length
2.for i=A.lengtgh/2 (floor function) down to 1
3. MAX-HEAPIFY(A,i)

```
</details>

#### The heapsort algorithm

1.Since the tree satisfies Max-Heap property, then the largest item is stored at the root node.
2.Swap: Remove the root element and put at the end of the array (nth position) Put the last item of the tree (heap) at the vacant place.
3.Remove: Reduce the size of the heap by 1.
4.Heapify: Heapify the root element again so that we have the highest element at root.
5.The process is repeated until all the items of the list are sorted.


#### Priority queues 

Data structure for maintaining a set S of elements,each with an associated value called as key.

<details>
<summary>Answer</summary>

```

HEAP-MINIMUM(A)
    return A[1]
    
    
HEAP-EXTRACT-MIN(A)
    if A.heap-size < 1
        error "heap underflow"
    min = A[1]
    A[1] = A[A.heap-size]
    A.heap-size = A.heap-size - 1
    MIN-HEAPIFY(A, 1)
    return max
    
    
HEAP-DECREASE-KEY(A, i, key)
    if key > A[i]
        error "new key is bigger than current key"
    A[i] = key
    while i > 1 and A[PARENT(i)] > A[i]
        exchange A[i] with A[PARENT(i)]
        i = PARENT(i)
	
	
MIN-HEAP-INSERT(A, key)
    A.heap-size = A.heap-size + 1
    A[A.heap-size] = +∞
    HEAP-DECREASE-KEY(A, A.heap-size, key)
```
</details>

#### Code in c
<details>
<summary>Answer</summary>
 
```

#include <stdio.h>
  
  void swap(int *a, int *b) {
    int tmp = *a;
    *a = *b;
    *b = tmp;
  }
  
  void heapify(int arr[], int n, int i) {
    int max = i; //Initialize max as root
    int leftChild = 2 * i + 1;
    int rightChild = 2 * i + 2;
  
    //If left child is greater than root
    if (leftChild < n && arr[leftChild] > arr[max])
      max = leftChild;
  
    //If right child is greater than max
    if (rightChild < n && arr[rightChild] > arr[max])
      max = rightChild;
  
    //If max is not root
    if (max != i) {
      swap(&arr[i], &arr[max]);
      //heapify the affected sub-tree recursively
      heapify(arr, n, max);
    }
  }

  //Main function to perform heap sort
  void heapSort(int arr[], int n) {
    //Rearrange array (building heap)
    for (int i = n / 2 - 1; i >= 0; i--)
      heapify(arr, n, i);
 
    //Extract elements from heap one by one
    for (int i = n - 1; i >= 0; i--) {
      swap(&arr[0], &arr[i]); //Current root moved to the end
  
      heapify(arr, i, 0); //calling max heapify on the heap reduced
    }
  }

  //print size of array n using utility function
  void display(int arr[], int n) {
    for (int i = 0; i < n; ++i)
      printf("%d ", arr[i]);
    printf("\n");
  }

  //Driver code
  int main() {
    int arr[] = {11, 34, 9, 5, 16, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
	
    printf("Original array:\n");
    display(arr, n);
    heapSort(arr, n);
  
    printf("Sorted array:\n");
    display(arr, n);
  }

 `````
 </details>
 
 ### Quick sort
 
 #### Description of quick sort 
 
follows divide and conquer strategy.
starting from the first element(pivot);
It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, 
according to whether they are less than or greater than the pivot. ... The sub-arrays are then sorted recursively.

<details>
<summary>Answer</summary>
 
```
PARTITION(A, p, r)
x = A[r]
i = p - 1
for j = p to r - 1
    if A[j] >= x
        i = i + 1
        exchange A[i] with A[j]
exchange A[i + 1] with A[r]
return i + 1

    
    QUICKSORT(A, p, r)
if p < r
    q = PARTITION(A, p, r)
    QUICKSORT(A, p, q - 1)
    QUICKSORT(A, q + 1, r)


    
  ```
  </details>

#### Performance of quick sort 

In this section we will investigate how quick sort performs under the assumptions of balanced versus unbalanced partitioning.

1. Time Complexities
Worst Case Complexity [Big-O]: O(n2)
It occurs when the pivot element picked is either the greatest or the smallest element.

This condition leads to the case in which the pivot element lies in an extreme end of the sorted array. One sub-array is always empty and another sub-array contains n - 1 elements. Thus, quicksort is called only on this sub-array.

However, the quicksort algorithm has better performance for scattered pivots.
Best Case Complexity [Big-omega]: O(n*log n)
It occurs when the pivot element is always the middle element or near to the middle element.
Average Case Complexity [Big-theta]: O(n*log n)
It occurs when the above conditions do not occur.
2. Space Complexity
The space complexity for quicksort is O(log n).



#### A randomized version of quicksort

An algorithm that uses random numbers to decide what to do next anywhere in its logic is called a Randomized Algorithm. For example, in Randomized Quick Sort, we use a random number to pick the next pivot .
// Sorts an array arr[low..high]
randQuickSort(arr[], low, high)

1. If low >= high, then EXIT.

2. While pivot 'x' is not a Central Pivot.
  (i)   Choose uniformly at random a number from [low..high]. 
        Let the randomly picked number number be x.
  (ii)  Count elements in arr[low..high] that are smaller 
        than arr[x]. Let this count be sc.
  (iii) Count elements in arr[low..high] that are greater 
        than arr[x]. Let this count be gc.
  (iv)  Let n = (high-low+1). If sc >= n/4 and
        gc >= n/4, then x is a central pivot.

3. Partition arr[low..high] around the pivot x.

4. // Recur for smaller elements
   randQuickSort(arr, low, sc-1) 

5. // Recur for greater elements
   randQuickSort(arr, high-gc+1, high) 


#### Code in c
<details>
<summary>Answer</summary>

 ```
#include<stdio.h>
void quicksort(int number[25],int first,int last){
   int i, j, pivot, temp;

   if(first<last){
      pivot=first;
      i=first;
      j=last;

      while(i<j){
         while(number[i]<=number[pivot]&&i<last)
            i++;
         while(number[j]>number[pivot])
            j--;
         if(i<j){
            temp=number[i];
            number[i]=number[j];
            number[j]=temp;
         }
      }

      temp=number[pivot];
      number[pivot]=number[j];
      number[j]=temp;
      quicksort(number,first,j-1);
      quicksort(number,j+1,last);

   }
}

int main(){
   int i, count, number[25];

   printf("How many elements are u going to enter?: ");
   scanf("%d",&count);

   printf("Enter %d elements: ", count);
   for(i=0;i<count;i++)
      scanf("%d",&number[i]);

   quicksort(number,0,count-1);

   printf("Order of Sorted elements: ");
   for(i=0;i<count;i++)
      printf(" %d",number[i]);

   return 0;
}
```
</details>

### Sorting in linear time

#### Lower bounds for sorting

A lower bound for a problem is the worst-case running time of the best possible algorithm for that problem. To prove a lower bound of Ω(n lg n) for sorting, we would have to prove that no algorithm, however smart, could possibly be faster, in the worst-case, then n lg n.



#### Counting sort

Counting sort is a sorting technique based on keys between a specific range. It works by counting the number of objects having distinct key values (kind of hashing). 
Then doing some arithmetic to calculate the position of each object in the output sequence. for example:
<details>
<summary>Example</summary>

 ```

For simplicity, consider the data in the range 0 to 9. 
Input data: 1, 4, 1, 2, 7, 5, 2
  1) Take a count array to store the count of each unique object.
  Index:     0  1  2  3  4  5  6  7  8  9
  Count:     0  2  2  0   1  1  0  1  0  0

  2) Modify the count array such that each element at each index 
  stores the sum of previous counts. 
  Index:     0  1  2  3  4  5  6  7  8  9
  Count:     0  2  4  4  5  6  6  7  7  7

The modified count array indicates the position of each object in 
the output sequence.
 
  3) Output each object from the input sequence followed by 
  decreasing its count by 1.
  Process the input data: 1, 4, 1, 2, 7, 5, 2. Position of 1 is 2.
  Put data 1 at index 2 in output. Decrease count by 1 to place 
  next data 1 at an index 1 smaller than this index.
  
  ```
  </details>
  
  #### Code in c
<details>
<summary>Answer</summary>

 ```
#include <stdio.h>

void countingSort(int array[], int size) {
  int output[10];

  // Find the largest element of the array
  int max = array[0];
  for (int i = 1; i < size; i++) {
    if (array[i] > max)
      max = array[i];
  }

  // The size of count must be at least (max+1) but
  // we cannot declare it as int count(max+1) in C as
  // it does not support dynamic memory allocation.
  // So, its size is provided statically.
  int count[10];

  // Initialize count array with all zeros.
  for (int i = 0; i <= max; ++i) {
    count[i] = 0;
  }

  // Store the count of each element
  for (int i = 0; i < size; i++) {
    count[array[i]]++;
  }

  // Store the cummulative count of each array
  for (int i = 1; i <= max; i++) {
    count[i] += count[i - 1];
  }

  // Find the index of each element of the original array in count array, and
  // place the elements in output array
  for (int i = size - 1; i >= 0; i--) {
    output[count[array[i]] - 1] = array[i];
    count[array[i]]--;
  }

  // Copy the sorted elements into original array
  for (int i = 0; i < size; i++) {
    array[i] = output[i];
  }
}

// Function to print an array
void printArray(int array[], int size) {
  for (int i = 0; i < size; ++i) {
    printf("%d  ", array[i]);
  }
  printf("\n");
}

// Driver code
int main() {
  int array[] = {4, 2, 2, 8, 3, 3, 1};
  int n = sizeof(array) / sizeof(array[0]);
  countingSort(array, n);
  printArray(array, n);
}
```
</details>

#### Radix sort

The idea of Radix Sort is to do digit by digit sort starting from least significant digit to most significant digit. Radix sort uses counting sort as a subroutine to sort.
For example: 
<details>
<summary>Answer</summary>

 ```

Original, unsorted list:
170, 45, 75, 90, 802, 24, 2, 66

Sorting by least significant digit (1s place) gives: 
[*Notice that we keep 802 before 2, because 802 occurred 
before 2 in the original list, and similarly for pairs 
170 & 90 and 45 & 75.]

170, 90, 802, 2, 24, 45, 75, 66

Sorting by next digit (10s place) gives: 
[*Notice that 802 again comes before 2 as 802 comes before 
2 in the previous list.]

802, 2, 24, 45, 66, 170, 75, 90

Sorting by the most significant digit (100s place) gives:
2, 24, 45, 66, 75, 90, 170, 802
```
</details>

#### Code in c

<details>
<summary>Answer</summary>

 ```
// Radix Sort in C Programming

#include <stdio.h>

// Function to get the largest element from an array
int getMax(int array[], int n) {
  int max = array[0];
  for (int i = 1; i < n; i++)
    if (array[i] > max)
      max = array[i];
  return max;
}

// Using counting sort to sort the elements in the basis of significant places
void countingSort(int array[], int size, int place) {
  int output[size + 1];
  int max = (array[0] / place) % 10;

  for (int i = 1; i < size; i++) {
    if (((array[i] / place) % 10) > max)
      max = array[i];
  }
  int count[max + 1];

  for (int i = 0; i < max; ++i)
    count[i] = 0;

  // Calculate count of elements
  for (int i = 0; i < size; i++)
    count[(array[i] / place) % 10]++;
    
  // Calculate cummulative count
  for (int i = 1; i < 10; i++)
    count[i] += count[i - 1];

  // Place the elements in sorted order
  for (int i = size - 1; i >= 0; i--) {
    output[count[(array[i] / place) % 10] - 1] = array[i];
    count[(array[i] / place) % 10]--;
  }

  for (int i = 0; i < size; i++)
    array[i] = output[i];
}

// Main function to implement radix sort
void radixsort(int array[], int size) {
  // Get maximum element
  int max = getMax(array, size);

  // Apply counting sort to sort elements based on place value.
  for (int place = 1; max / place > 0; place *= 10)
    countingSort(array, size, place);
}

// Print an array
void printArray(int array[], int size) {
  for (int i = 0; i < size; ++i) {
    printf("%d  ", array[i]);
  }
  printf("\n");
}

// Driver code
int main() {
  int array[] = {121, 432, 564, 23, 1, 45, 788};
  int n = sizeof(array) / sizeof(array[0]);
  radixsort(array, n);
  printArray(array, n);
}
```
</details>

#### Bucket sort

Bucket Sort is a sorting technique that sorts the elements by first dividing the elements into several groups called buckets. The elements inside each bucket are sorted using any of the suitable sorting algorithms or recursively calling the same algorithm.

#### Code in c
<details>
<summary>Answer</summary>

 ```
 #include <stdio.h>
#include <stdlib.h>

#define NARRAY 7   // Array size
#define NBUCKET 6  // Number of buckets
#define INTERVAL 10  // Each bucket capacity

struct Node {
  int data;
  struct Node *next;
};

void BucketSort(int arr[]);
struct Node *InsertionSort(struct Node *list);
void print(int arr[]);
void printBuckets(struct Node *list);
int getBucketIndex(int value);

// Sorting function
void BucketSort(int arr[]) {
  int i, j;
  struct Node **buckets;

  // Create buckets and allocate memory size
  buckets = (struct Node **)malloc(sizeof(struct Node *) * NBUCKET);

  // Initialize empty buckets
  for (i = 0; i < NBUCKET; ++i) {
    buckets[i] = NULL;
  }

  // Fill the buckets with respective elements
  for (i = 0; i < NARRAY; ++i) {
    struct Node *current;
    int pos = getBucketIndex(arr[i]);
    current = (struct Node *)malloc(sizeof(struct Node));
    current->data = arr[i];
    current->next = buckets[pos];
    buckets[pos] = current;
  }

  // Print the buckets along with their elements
  for (i = 0; i < NBUCKET; i++) {
    printf("Bucket[%d]: ", i);
    printBuckets(buckets[i]);
    printf("\n");
  }

  // Sort the elements of each bucket
  for (i = 0; i < NBUCKET; ++i) {
    buckets[i] = InsertionSort(buckets[i]);
  }

  printf("-------------\n");
  printf("Bucktets after sorting\n");
  for (i = 0; i < NBUCKET; i++) {
    printf("Bucket[%d]: ", i);
    printBuckets(buckets[i]);
    printf("\n");
  }

  // Put sorted elements on arr
  for (j = 0, i = 0; i < NBUCKET; ++i) {
    struct Node *node;
    node = buckets[i];
    while (node) {
      arr[j++] = node->data;
      node = node->next;
    }
  }

  return;
}

// Function to sort the elements of each bucket
struct Node *InsertionSort(struct Node *list) {
  struct Node *k, *nodeList;
  if (list == 0 || list->next == 0) {
    return list;
  }

  nodeList = list;
  k = list->next;
  nodeList->next = 0;
  while (k != 0) {
    struct Node *ptr;
    if (nodeList->data > k->data) {
      struct Node *tmp;
      tmp = k;
      k = k->next;
      tmp->next = nodeList;
      nodeList = tmp;
      continue;
    }

    for (ptr = nodeList; ptr->next != 0; ptr = ptr->next) {
      if (ptr->next->data > k->data)
        break;
    }

    if (ptr->next != 0) {
      struct Node *tmp;
      tmp = k;
      k = k->next;
      tmp->next = ptr->next;
      ptr->next = tmp;
      continue;
    } else {
      ptr->next = k;
      k = k->next;
      ptr->next->next = 0;
      continue;
    }
  }
  return nodeList;
}

int getBucketIndex(int value) {
  return value / INTERVAL;
}

void print(int ar[]) {
  int i;
  for (i = 0; i < NARRAY; ++i) {
    printf("%d ", ar[i]);
  }
  printf("\n");
}

// Print buckets
void printBuckets(struct Node *list) {
  struct Node *cur = list;
  while (cur) {
    printf("%d ", cur->data);
    cur = cur->next;
  }
}

// Driver code
int main(void) {
  int array[NARRAY] = {42, 32, 33, 52, 37, 47, 51};

  printf("Initial array: ");
  print(array);
  printf("-------------\n");

  BucketSort(array);
  printf("-------------\n");
  printf("Sorted array: ");
  print(array);
  return 0;
}
 ```
 </details>

### Medians and order statistics

#### Minimum and maximum

How many comparisons are necessary to determine the minimum of a set of n elements? We can easily obtain an upper bound of n - 1 comparisons: examine each element of the set in turn and keep track of the smallest element seen so far. In the following procedure, we assume that the set resides in array A, where length[A] = n.


MINIMUM (A)

1  min  A[1]

2  for i  2 to length[A]

3        do if min > A[i]

4              then min  A[i]

5  return min

#### Selection in expected linear time

The general selection problem appears more difficult than the simple problem of finding a minimum, yet, surprisingly, the asymptotic running time for both problems is the same: (n). In this section, we present a divide-and-conquer algorithm for the selection problem. The algorithm RANDOMIZED-SELECT is modeled after the quicksort algorithm of Chapter 8. As in quicksort, the idea is to partition the input array recursively. But unlike quicksort, which recursively processes both sides of the partition, RANDOMIZED-SELECT only works on one side of the partition. This difference shows up in the analysis: whereas quicksort has an expected running time of (n lg n), the expected time of RANDOMIZED-SELECT is (n).


#### Selection in worst-case linear time

We now examine a selection algorithm whose running time is O(n) in the worst case. Like RANDOMIZED-SELECT, the algorithm SELECT finds the desired element by recursively partitioning the input array. The idea behind the algorithm, however, is to guarantee a good split when the array is partitioned. SELECT uses the deterministic partitioning algorithm PARTITION from quicksort (see Section 8.1), modified to take the element to partition around as an input parameter.


## Data structures

Data Structure is a way to store and organize data so that it can be used efficiently. Data Structure includes topics such as Array, Pointer, Structure, Linked List, Stack, Queue, Graph, Searching, Sorting, Programs, etc.

### Elementary data structures

#### Stacks and queues
A stack is a useful data structure in programming. It is just like a pile of plates kept on top of each other.
If you want the plate at the bottom, you must first remove all the plates on top. Such an arrangement is called Last In First Out - the last item that is the first item to go out.
In programming terms, putting an item on top of the stack is called push and removing an item is called pop.

##### Working of Stack Data Structure
<details>
<summary>Answer</summary>

 ```

The operations work as follows:

A pointer called TOP is used to keep track of the top element in the stack.
When initializing the stack, we set its value to -1 so that we can check if the stack is empty by comparing TOP == -1.
On pushing an element, we increase the value of TOP and place the new element in the position pointed to by TOP.
On popping an element, we return the element pointed to by TOP and reduce its value.
Before pushing, we check if the stack is already full
Before popping, we check if the stack is already empty
```
</details>

#### Code in c
<details>
<summary>Answer</summary>

 ```
 #include <stdio.h>
#include <stdlib.h>

#define MAX 10

int count = 0;

// Creating a stack
struct stack {
  int items[MAX];
  int top;
};
typedef struct stack st;

void createEmptyStack(st *s) {
  s->top = -1;
}

// Check if the stack is full
int isfull(st *s) {
  if (s->top == MAX - 1)
    return 1;
  else
    return 0;
}

// Check if the stack is empty
int isempty(st *s) {
  if (s->top == -1)
    return 1;
  else
    return 0;
}

// Add elements into stack
void push(st *s, int newitem) {
  if (isfull(s)) {
    printf("STACK FULL");
  } else {
    s->top++;
    s->items[s->top] = newitem;
  }
  count++;
}

// Remove element from stack
void pop(st *s) {
  if (isempty(s)) {
    printf("\n STACK EMPTY \n");
  } else {
    printf("Item popped= %d", s->items[s->top]);
    s->top--;
  }
  count--;
  printf("\n");
}

// Print elements of stack
void printStack(st *s) {
  printf("Stack: ");
  for (int i = 0; i < count; i++) {
    printf("%d ", s->items[i]);
  }
  printf("\n");
}

// Driver code
int main() {
  int ch;
  st *s = (st *)malloc(sizeof(st));

  createEmptyStack(s);

  push(s, 1);
  push(s, 2);
  push(s, 3);
  push(s, 4);

  printStack(s);

  pop(s);

  printf("\nAfter popping out\n");
  printStack(s);
}
 ```
 </details>
 
 Queues:Queue follows the First In First Out (FIFO) rule - the item that goes in first is the item that comes out first.
 
 In programming terms, putting items in the queue is called enqueue, and removing items from the queue is called dequeue.
 
 Working of Queue
Queue operations work as follows:

two pointers FRONT and REAR
FRONT track the first element of the queue
REAR track the last element of the queue
initially, set value of FRONT and REAR to -1

Enqueue Operation
check if the queue is full
for the first element, set the value of FRONT to 0
increase the REAR index by 1
add the new element in the position pointed to by REAR

Dequeue Operation
check if the queue is empty
return the value pointed by FRONT
increase the FRONT index by 1
for the last element, reset the values of FRONT and REAR to -1


 #### Code in c
 <details>
<summary>Answer</summary>

 ```
 
 
 #include <stdio.h>
#define SIZE 5

void enQueue(int);
void deQueue();
void display();

int items[SIZE], front = -1, rear = -1;

int main() {
  //deQueue is not possible on empty queue
  deQueue();

  //enQueue 5 elements
  enQueue(1);
  enQueue(2);
  enQueue(3);
  enQueue(4);
  enQueue(5);

  // 6th element can't be added to because the queue is full
  enQueue(6);

  display();

  //deQueue removes element entered first i.e. 1
  deQueue();

  //Now we have just 4 elements
  display();

  return 0;
}

void enQueue(int value) {
  if (rear == SIZE - 1)
    printf("\nQueue is Full!!");
  else {
    if (front == -1)
      front = 0;
    rear++;
    items[rear] = value;
    printf("\nInserted -> %d", value);
  }
}

void deQueue() {
  if (front == -1)
    printf("\nQueue is Empty!!");
  else {
    printf("\nDeleted : %d", items[front]);
    front++;
    if (front > rear)
      front = rear = -1;
  }
}

// Function to print the queue
void display() {
  if (rear == -1)
    printf("\nQueue is Empty!!!");
  else {
    int i;
    printf("\nQueue elements are:\n");
    for (i = front; i <= rear; i++)
      printf("%d  ", items[i]);
  }
  printf("\n");
}
```
</details>

#### Linked list

In computer science, a linked list is a linear collection of data elements whose order is not given by their physical placement in memory. Instead, each element points to the next. It is a data structure consisting of a collection of nodes which together represent a sequence.

#### Code in c
 <details>
<summary>Answer</summary>

 ```

#include <stdio.h>
#include <stdlib.h>

// Creating a node
struct node {
  int value;
  struct node *next;
};

// print the linked list value
void printLinkedlist(struct node *p) {
  while (p != NULL) {
    printf("%d ", p->value);
    p = p->next;
  }
}

int main() {
  // Initialize nodes
  struct node *head;
  struct node *one = NULL;
  struct node *two = NULL;
  struct node *three = NULL;

  // Allocate memory
  one = malloc(sizeof(struct node));
  two = malloc(sizeof(struct node));
  three = malloc(sizeof(struct node));

  // Assign value values
  one->value = 1;
  two->value = 2;
  three->value = 3;

  // Connect nodes
  one->next = two;
  two->next = three;
  three->next = NULL;

  // printing node-value
  head = one;
  printLinkedlist(head);
}
```
</details>

#### Implementing pointers and objects

Pointers are symbolic representation of addresses. They enable programs to simulate call-by-reference as well as to create and manipulate dynamic data structures. Pointers are symbolic representation of addresses. They enable programs to simulate call-by-reference as well as to create and manipulate dynamic data structures. 
syntax:
datatype *var_name; 
int *ptr;   //ptr can point to an address which holds int data


#### Representing rooted trees

• A direct way to represent a tree is to use a data structure
where every node has three references:
o one reference to the object stored at that node,
o one reference to the node's parent, and
o one reference to the node's children.
• The child-sibling (CS) representation is another popular tree
representation. It spurns separately encapsulated linked lists
so that siblings are directly linked.
o It retains the item and parent references, but instead of
referencing a list of children, each node references just its
leftmost child.
o Each node also references its next sibling to the right.
o These nextSibling references are used to join the children of a
node in a singly-linked list, whose head is the node's firstChild. 

### Hash tables

 its a searching technique, designed using mathematical model of functions. its fastest searching technique. ideal hashing takes O(1).


#### Direct address table

#### Hash tables

In computing, a hash table (hash map) is a data structure which implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found

Ideally, the hash function will assign each key to a unique bucket, but most hash table designs employ an imperfect hash function, which might cause hash collisions where the hash function generates the same index for more than one key. Such collisions must be accommodated in some way.

#### Hash functions

Earlier when this concept introduced programmers used to create “Direct address table”. Direct address table means, when we have “n” number of unique keys we create an array of length “n” and insert element “i” at ith index of the array. That array is called Hash Table. But due to this method even we have 10 elements of each range 1 lack, we should create table of size 1 lack for only 10 elements. Which is going to be waste of memory.

To avoid this problem we fix the size of hash table (array) and map our elements into that table using a function, called Hash function. This function decides where to put a given element into that table. If we want to search also first apply hash function decide whether the element present in hash table or not.

Example

We have numbers from 1 to 100 and hash table of size 10. Hash function is mod 10. That means number 23 will be mapped to (23 mod 10 = 3) 3rd index of hash table.

#### Open addressing

In case if we have collision we again calculate the hash value using corresponding hash function. But this time we do some minor modifications to that input. This process of searching for empty space to insert element in called Probing.

Probing hash function is: h (k, i)

here k is the key value which is to be inserted. And i is number of collision with that element.

Example: If we are inserting 2, we find its hash value using h (2, 0) because it’s first collision. Suppose the answer (index) to this function index already occupied we again need to apply h (2, 1) to hash function.

#### Perfect hashing

Perfect hashing is defined as a model of hashing in which any set of n elements can be stored in a hash table of equal size and can have lookups performed in constant time. It was specifically invented and discussed by Fredman, Komlos and Szemeredi (1984) and has therefore been nicknamed as "FKS Hashing".
 
### Binary search tree

it is a binary tree in which each node is having value lesser than itself at left side and greater
than itself at right hand side.

#### What is binary search tree?

In computer science, binary search trees (BST), sometimes called ordered or sorted binary trees, are a particular type of container: data structures that store "items" (such as numbers, names etc.) in memory. They allow fast lookup, addition and removal of items, and can be used to implement either dynamic sets of items, or lookup tables that allow finding an item by its key (e.g., finding the phone number of a person by name).

Binary search trees keep their keys in sorted order, so that lookup and other operations can use the principle of binary search: when looking for a key in a tree (or a place to insert a new key), they traverse the tree from root to leaf, making comparisons to keys stored in the nodes of the tree and deciding, on the basis of the comparison, to continue searching in the left or right subtrees. On average, this means that each comparison allows the operations to skip about half of the tree, so that each lookup, insertion or deletion takes time proportional to the logarithm of the number of items stored in the tree. This is much better than the linear time required to find items by key in an (unsorted) array, but slower than the corresponding operations on hash tables.


#### Querying in binary search tree

A common operation performed on a binary search tree is searching for a key stored in the tree. Besides the SEARCH operation, binary search trees can support such queries as MINIMUM, MAXIMUM, SUCCESSOR, and PREDECESSOR. In this section, we shall examine these operations and show that each can be supported in time O(h) on a binary search tree of height h.

#### Insertion and deletion
#### pseudo code for insertion and deletion

<details>
<summary>Answer</summary>
 
```

insert(value)
  Pre: value has passed custom type checks for type T
  Post: value has been placed in the correct location in the tree
  if root = ø
    root ← node(value)
  else
    insertNode(root, value)
  end if
end insert
insertNode(current, value)
  Pre: current is the node to start from
  Post: value has been placed in the correct location in the tree
  if value < current.value
    if current.left = ø
      current.left ← node(value)
    else
      InsertNode(current.left, value)
    end if
  else
    if current.right = ø
      current.right ← node(value)
    else
      InsertNode(current.right, value)
    end if
  end if
end insertNode


remove(value)
  Pre: value is the value of the node to remove, root is the node of the BST
      count is the number of items in the BST
  Post: node with value is removed if found in which case yields true, otherwise false
  nodeToRemove ← findNode(value)
  if nodeToRemove = ø
    return false
  end if
  parent ← findParent(value)
  if count = 1
    root ← ø
  else if nodeToRemove.left = ø and nodeToRemove.right = ø
    if nodeToRemove.value < parent.value
      parent.left ←  nodeToRemove.right
    else
      parent.right ← nodeToRemove.right
    end if
  else if nodeToRemove.left != ø and nodeToRemove.right != ø
    next ← nodeToRemove.right
    while next.left != ø
      next ← next.left
    end while
    if next != nodeToRemove.right
      remove(next.value)
      nodeToRemove.value ← next.value
    else
      nodeToRemove.value ← next.value
      nodeToRemove.right ← nodeToRemove.right.right
    end if
  else
    if nodeToRemove.left = ø
      next ← nodeToRemove.right
    else
      next ← nodeToRemove.left
    end if
    if root = nodeToRemove
      root = next
    else if parent.left = nodeToRemove
      parent.left = next
    else if parent.right = nodeToRemove
      parent.right = next
    end if
  end if
  count ← count - 1
  return true
end remove


```
</details>

#### Randomly built binary search trees


#### Code in c

<details>
<summary>Answer</summary>
 
```
 
 
 
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data; //node will store an integer
    struct node *right_child; // right child
    struct node *left_child; // left child
};

struct node* search(struct node *root, int x)
{
    if(root==NULL || root->data==x) //if root->data is x then the element is found
        return root;
    else if(x>root->data) // x is greater, so we will search the right subtree
        return search(root->right_child, x);
    else //x is smaller than the data, so we will search the left subtree
        return search(root->left_child,x);
}

//function to find the minimum value in a node
struct node* find_minimum(struct node *root)
{
    if(root == NULL)
        return NULL;
    else if(root->left_child != NULL) // node with minimum value will have no left child
        return find_minimum(root->left_child); // left most element will be minimum
    return root;
}

//function to create a node
struct node* new_node(int x)
{
    struct node *p;
    p = malloc(sizeof(struct node));
    p->data = x;
    p->left_child = NULL;
    p->right_child = NULL;

    return p;
}

struct node* insert(struct node *root, int x)
{
    //searching for the place to insert
    if(root==NULL)
        return new_node(x);
    else if(x>root->data) // x is greater. Should be inserted to right
        root->right_child = insert(root->right_child, x);
    else // x is smaller should be inserted to left
        root->left_child = insert(root->left_child,x);
    return root;
}

// funnction to delete a node
struct node* delete(struct node *root, int x)
{
    //searching for the item to be deleted
    if(root==NULL)
        return NULL;
    if (x>root->data)
        root->right_child = delete(root->right_child, x);
    else if(x<root->data)
        root->left_child = delete(root->left_child, x);
    else
    {
        //No Children
        if(root->left_child==NULL && root->right_child==NULL)
        {
            free(root);
            return NULL;
        }

        //One Child
        else if(root->left_child==NULL || root->right_child==NULL)
        {
            struct node *temp;
            if(root->left_child==NULL)
                temp = root->right_child;
            else
                temp = root->left_child;
            free(root);
            return temp;
        }

        //Two Children
        else
        {
            struct node *temp = find_minimum(root->right_child);
            root->data = temp->data;
            root->right_child = delete(root->right_child, temp->data);
        }
    }
    return root;
}

void inorder(struct node *root)
{
    if(root!=NULL) // checking if the root is not null
    {
        inorder(root->left_child); // visiting left child
        printf(" %d ", root->data); // printing data at root
        inorder(root->right_child);// visiting right child
    }
}

int main()
{
    /*
                   20
                 /    \
                /      \
               5       30
             /   \     /\
            /     \   /  \
           1      15 25  40
                /          \
               /            \
              9             45
            /   \          /
           /     \        /
          7      12      42
    */
    struct node *root;
    root = new_node(20);
    insert(root,5);
    insert(root,1);
    insert(root,15);
    insert(root,9);
    insert(root,7);
    insert(root,12);
    insert(root,30);
    insert(root,25);
    insert(root,40);
    insert(root, 45);
    insert(root, 42);

    inorder(root);
    printf("\n");

    root = delete(root, 1);
    /*
                   20
                 /    \
                /      \
               5       30
                 \     /\
                  \   /  \
                  15 25   40
                /           \
               /             \
              9              45
            /   \           /
           /     \         /
          7      12       42
    */

    root = delete(root, 40);
    /*
                   20
                 /    \
                /      \
               5       30
                 \     /\
                  \   /  \
                  15 25  45
                 /       / 
                /       /   
               9       42    
             /   \          
            /     \        
           7      12      
    */

    root = delete(root, 45);
    /*
                   20
                 /    \
                /      \
               5       30
                 \     /\
                  \   /  \
                  15 25  42
                 /          
                /            
               9            
             /   \          
            /     \        
           7      12      
    */
    root = delete(root, 9);
    inorder(root);
    /*
                   20
                 /    \
                /      \
               5       30
                 \     /\
                  \   /  \
                  15 25  42
                 /          
                /            
               12            
             /             
            /             
           7            
    */
    printf("\n");

    return 0;
} 
 
 ```
 </details>
 
 ### Red black trees
 
 #### Properties of red black trees
 
 A red-black tree is a kind of self-balancing binary search tree where each node has an extra bit, and that bit is often interpreted as the colour (red or black). These colours are used to ensure that the tree remains balanced during insertions and deletions. Although the balance of the tree is not perfect, it is good enough to reduce the searching time and maintain it around O(log n) time, where n is the total number of elements in the tree. This tree was invented in 1972 by Rudolf Bayer. 

It must be noted that as each node requires only 1 bit of space to store the colour information. 

Rules That Every Red-Black Tree Follows: 
Every node has a colour either red or black.
The root of the tree is always black.
There are no two adjacent red nodes (A red node cannot have a red parent or red child).
Every path from a node (including root) to any of its descendants NULL nodes has the same number of black nodes.


#### Rotations

In rotation operation, the positions of the nodes of a subtree are interchanged.

Rotation operation is used for maintaining the properties of a red-black tree when they are violated by other operations such as insertion and deletion.

#### Insertions

While inserting a new node, the new node is always inserted as a RED node. After insertion of a new node, if the tree is violating the properties of the red-black tree then, we do the following operations.

Recolor
Rotation

#### Code in c (Insertions)

 <details>
<summary>Answer</summary>
 
```
#include <stdio.h>
#include <stdlib.h>
  
// Structure to represent each 
// node in a red-black tree
struct node {
    int d; // data
    int c; // 1-red, 0-black
    struct node* p; // parent
    struct node* r; // right-child
    struct node* l; // left child
};
  
// global root for the entire tree
struct node* root = NULL;
  
// function to perform BST insertion of a node
struct node* bst(struct node* trav, 
                      struct node* temp)
{
    // If the tree is empty, 
    // return a new node
    if (trav == NULL)
        return temp;
  
    // Otherwise recur down the tree
    if (temp->d < trav->d) 
    {
        trav->l = bst(trav->l, temp);
        trav->l->p = trav;
    }
    else if (temp->d > trav->d) 
    {
        trav->r = bst(trav->r, temp);
        trav->r->p = trav;
    }
  
    // Return the (unchanged) node pointer
    return trav;
}
  
// Function performing right rotation 
// of the passed node
void rightrotate(struct node* temp)
{
    struct node* left = temp->l;
    temp->l = left->r;
    if (temp->l)
        temp->l->p = temp;
    left->p = temp->p;
    if (!temp->p)
        root = left;
    else if (temp == temp->p->l)
        temp->p->l = left;
    else
        temp->p->r = left;
    left->r = temp;
    temp->p = left;
}
  
// Function performing left rotation 
// of the passed node
void leftrotate(struct node* temp)
{
    struct node* right = temp->r;
    temp->r = right->l;
    if (temp->r)
        temp->r->p = temp;
    right->p = temp->p;
    if (!temp->p)
        root = right;
    else if (temp == temp->p->l)
        temp->p->l = right;
    else
        temp->p->r = right;
    right->l = temp;
    temp->p = right;
}
  
// This function fixes violations 
// caused by BST insertion
void fixup(struct node* root, struct node* pt)
{
    struct node* parent_pt = NULL;
    struct node* grand_parent_pt = NULL;
  
    while ((pt != root) && (pt->c != 0)
           && (pt->p->c == 1)) 
    {
        parent_pt = pt->p;
        grand_parent_pt = pt->p->p;
  
        /*  Case : A
             Parent of pt is left child 
             of Grand-parent of
           pt */
        if (parent_pt == grand_parent_pt->l) 
        {
  
            struct node* uncle_pt = grand_parent_pt->r;
  
            /* Case : 1
                The uncle of pt is also red
                Only Recoloring required */
            if (uncle_pt != NULL && uncle_pt->c == 1) 
            {
                grand_parent_pt->c = 1;
                parent_pt->c = 0;
                uncle_pt->c = 0;
                pt = grand_parent_pt;
            }
  
            else {
  
                /* Case : 2
                     pt is right child of its parent
                     Left-rotation required */
                if (pt == parent_pt->r) {
                    leftrotate(parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->p;
                }
  
                /* Case : 3
                     pt is left child of its parent
                     Right-rotation required */
                rightrotate(grand_parent_pt);
                int t = parent_pt->c;
                parent_pt->c = grand_parent_pt->c;
                grand_parent_pt->c = t;
                pt = parent_pt;
            }
        }
  
        /* Case : B
             Parent of pt is right 
             child of Grand-parent of
           pt */
        else {
            struct node* uncle_pt = grand_parent_pt->l;
  
            /*  Case : 1
                The uncle of pt is also red
                Only Recoloring required */
            if ((uncle_pt != NULL) && (uncle_pt->c == 1)) 
            {
                grand_parent_pt->c = 1;
                parent_pt->c = 0;
                uncle_pt->c = 0;
                pt = grand_parent_pt;
            }
            else {
                /* Case : 2
                   pt is left child of its parent
                   Right-rotation required */
                if (pt == parent_pt->l) {
                    rightrotate(parent_pt);
                    pt = parent_pt;
                    parent_pt = pt->p;
                }
  
                /* Case : 3
                     pt is right child of its parent
                     Left-rotation required */
                leftrotate(grand_parent_pt);
                int t = parent_pt->c;
                parent_pt->c = grand_parent_pt->c;
                grand_parent_pt->c = t;
                pt = parent_pt;
            }
        }
    }
  
    root->c = 0;
}
  
// Function to print inorder traversal 
// of the fixated tree
void inorder(struct node* trav)
{
    if (trav == NULL)
        return;
    inorder(trav->l);
    printf("%d ", trav->d);
    inorder(trav->r);
}
  
// driver code
int main()
{
    int n = 7;
    int a[7] = { 7, 6, 5, 4, 3, 2, 1 };
  
    for (int i = 0; i < n; i++) {
  
        // allocating memory to the node and initializing:
        // 1. color as red
        // 2. parent, left and right pointers as NULL
        // 3. data as i-th value in the array
        struct node* temp
            = (struct node*)malloc(sizeof(struct node));
        temp->r = NULL;
        temp->l = NULL;
        temp->p = NULL;
        temp->d = a[i];
        temp->c = 1;
  
        // calling function that performs bst insertion of
        // this newly created node
        root = bst(root, temp);
  
        // calling function to preserve properties of rb
        // tree
        fixup(root, temp);
    }
  
    printf("Inoder Traversal of Created Tree\n");
    inorder(root);
  
    return 0;
} 
 
 ```
 </details>



#### Deletion

Algorithm to delete a node
Save the color of nodeToBeDeleted in origrinalColor.
If the left child of nodeToBeDeleted is NULL
Assign the right child of nodeToBeDeleted to x.
Transplant nodeToBeDeleted with x.
Else if the right child of nodeToBeDeleted is NULL
Assign the left child of nodeToBeDeleted into x.
Transplant nodeToBeDeleted with x.
Else
Assign the minimum of right subtree of noteToBeDeleted into y.
Save the color of y in originalColor.
Assign the rightChild of y into x.
If y is a child of nodeToBeDeleted, then set the parent of x as y.
Else, transplant y with rightChild of y.
Transplant nodeToBeDeleted with y.
Set the color of y with originalColor.
If the originalColor is BLACK, call DeleteFix(x).


#### Code in c
  <details>
<summary>Answer</summary>
 
```
 

// Implementing Red-Black Tree in C

#include <stdio.h>
#include <stdlib.h>

enum nodeColor {
  RED,
  BLACK
};

struct rbNode {
  int data, color;
  struct rbNode *link[2];
};

struct rbNode *root = NULL;

// Create a red-black tree
struct rbNode *createNode(int data) {
  struct rbNode *newnode;
  newnode = (struct rbNode *)malloc(sizeof(struct rbNode));
  newnode->data = data;
  newnode->color = RED;
  newnode->link[0] = newnode->link[1] = NULL;
  return newnode;
}

// Insert an node
void insertion(int data) {
  struct rbNode *stack[98], *ptr, *newnode, *xPtr, *yPtr;
  int dir[98], ht = 0, index;
  ptr = root;
  if (!root) {
    root = createNode(data);
    return;
  }

  stack[ht] = root;
  dir[ht++] = 0;
  while (ptr != NULL) {
    if (ptr->data == data) {
      printf("Duplicates Not Allowed!!\n");
      return;
    }
    index = (data - ptr->data) > 0 ? 1 : 0;
    stack[ht] = ptr;
    ptr = ptr->link[index];
    dir[ht++] = index;
  }
  stack[ht - 1]->link[index] = newnode = createNode(data);
  while ((ht >= 3) && (stack[ht - 1]->color == RED)) {
    if (dir[ht - 2] == 0) {
      yPtr = stack[ht - 2]->link[1];
      if (yPtr != NULL && yPtr->color == RED) {
        stack[ht - 2]->color = RED;
        stack[ht - 1]->color = yPtr->color = BLACK;
        ht = ht - 2;
      } else {
        if (dir[ht - 1] == 0) {
          yPtr = stack[ht - 1];
        } else {
          xPtr = stack[ht - 1];
          yPtr = xPtr->link[1];
          xPtr->link[1] = yPtr->link[0];
          yPtr->link[0] = xPtr;
          stack[ht - 2]->link[0] = yPtr;
        }
        xPtr = stack[ht - 2];
        xPtr->color = RED;
        yPtr->color = BLACK;
        xPtr->link[0] = yPtr->link[1];
        yPtr->link[1] = xPtr;
        if (xPtr == root) {
          root = yPtr;
        } else {
          stack[ht - 3]->link[dir[ht - 3]] = yPtr;
        }
        break;
      }
    } else {
      yPtr = stack[ht - 2]->link[0];
      if ((yPtr != NULL) && (yPtr->color == RED)) {
        stack[ht - 2]->color = RED;
        stack[ht - 1]->color = yPtr->color = BLACK;
        ht = ht - 2;
      } else {
        if (dir[ht - 1] == 1) {
          yPtr = stack[ht - 1];
        } else {
          xPtr = stack[ht - 1];
          yPtr = xPtr->link[0];
          xPtr->link[0] = yPtr->link[1];
          yPtr->link[1] = xPtr;
          stack[ht - 2]->link[1] = yPtr;
        }
        xPtr = stack[ht - 2];
        yPtr->color = BLACK;
        xPtr->color = RED;
        xPtr->link[1] = yPtr->link[0];
        yPtr->link[0] = xPtr;
        if (xPtr == root) {
          root = yPtr;
        } else {
          stack[ht - 3]->link[dir[ht - 3]] = yPtr;
        }
        break;
      }
    }
  }
  root->color = BLACK;
}

// Delete a node
void deletion(int data) {
  struct rbNode *stack[98], *ptr, *xPtr, *yPtr;
  struct rbNode *pPtr, *qPtr, *rPtr;
  int dir[98], ht = 0, diff, i;
  enum nodeColor color;

  if (!root) {
    printf("Tree not available\n");
    return;
  }

  ptr = root;
  while (ptr != NULL) {
    if ((data - ptr->data) == 0)
      break;
    diff = (data - ptr->data) > 0 ? 1 : 0;
    stack[ht] = ptr;
    dir[ht++] = diff;
    ptr = ptr->link[diff];
  }

  if (ptr->link[1] == NULL) {
    if ((ptr == root) && (ptr->link[0] == NULL)) {
      free(ptr);
      root = NULL;
    } else if (ptr == root) {
      root = ptr->link[0];
      free(ptr);
    } else {
      stack[ht - 1]->link[dir[ht - 1]] = ptr->link[0];
    }
  } else {
    xPtr = ptr->link[1];
    if (xPtr->link[0] == NULL) {
      xPtr->link[0] = ptr->link[0];
      color = xPtr->color;
      xPtr->color = ptr->color;
      ptr->color = color;

      if (ptr == root) {
        root = xPtr;
      } else {
        stack[ht - 1]->link[dir[ht - 1]] = xPtr;
      }

      dir[ht] = 1;
      stack[ht++] = xPtr;
    } else {
      i = ht++;
      while (1) {
        dir[ht] = 0;
        stack[ht++] = xPtr;
        yPtr = xPtr->link[0];
        if (!yPtr->link[0])
          break;
        xPtr = yPtr;
      }

      dir[i] = 1;
      stack[i] = yPtr;
      if (i > 0)
        stack[i - 1]->link[dir[i - 1]] = yPtr;

      yPtr->link[0] = ptr->link[0];

      xPtr->link[0] = yPtr->link[1];
      yPtr->link[1] = ptr->link[1];

      if (ptr == root) {
        root = yPtr;
      }

      color = yPtr->color;
      yPtr->color = ptr->color;
      ptr->color = color;
    }
  }

  if (ht < 1)
    return;

  if (ptr->color == BLACK) {
    while (1) {
      pPtr = stack[ht - 1]->link[dir[ht - 1]];
      if (pPtr && pPtr->color == RED) {
        pPtr->color = BLACK;
        break;
      }

      if (ht < 2)
        break;

      if (dir[ht - 2] == 0) {
        rPtr = stack[ht - 1]->link[1];

        if (!rPtr)
          break;

        if (rPtr->color == RED) {
          stack[ht - 1]->color = RED;
          rPtr->color = BLACK;
          stack[ht - 1]->link[1] = rPtr->link[0];
          rPtr->link[0] = stack[ht - 1];

          if (stack[ht - 1] == root) {
            root = rPtr;
          } else {
            stack[ht - 2]->link[dir[ht - 2]] = rPtr;
          }
          dir[ht] = 0;
          stack[ht] = stack[ht - 1];
          stack[ht - 1] = rPtr;
          ht++;

          rPtr = stack[ht - 1]->link[1];
        }

        if ((!rPtr->link[0] || rPtr->link[0]->color == BLACK) &&
          (!rPtr->link[1] || rPtr->link[1]->color == BLACK)) {
          rPtr->color = RED;
        } else {
          if (!rPtr->link[1] || rPtr->link[1]->color == BLACK) {
            qPtr = rPtr->link[0];
            rPtr->color = RED;
            qPtr->color = BLACK;
            rPtr->link[0] = qPtr->link[1];
            qPtr->link[1] = rPtr;
            rPtr = stack[ht - 1]->link[1] = qPtr;
          }
          rPtr->color = stack[ht - 1]->color;
          stack[ht - 1]->color = BLACK;
          rPtr->link[1]->color = BLACK;
          stack[ht - 1]->link[1] = rPtr->link[0];
          rPtr->link[0] = stack[ht - 1];
          if (stack[ht - 1] == root) {
            root = rPtr;
          } else {
            stack[ht - 2]->link[dir[ht - 2]] = rPtr;
          }
          break;
        }
      } else {
        rPtr = stack[ht - 1]->link[0];
        if (!rPtr)
          break;

        if (rPtr->color == RED) {
          stack[ht - 1]->color = RED;
          rPtr->color = BLACK;
          stack[ht - 1]->link[0] = rPtr->link[1];
          rPtr->link[1] = stack[ht - 1];

          if (stack[ht - 1] == root) {
            root = rPtr;
          } else {
            stack[ht - 2]->link[dir[ht - 2]] = rPtr;
          }
          dir[ht] = 1;
          stack[ht] = stack[ht - 1];
          stack[ht - 1] = rPtr;
          ht++;

          rPtr = stack[ht - 1]->link[0];
        }
        if ((!rPtr->link[0] || rPtr->link[0]->color == BLACK) &&
          (!rPtr->link[1] || rPtr->link[1]->color == BLACK)) {
          rPtr->color = RED;
        } else {
          if (!rPtr->link[0] || rPtr->link[0]->color == BLACK) {
            qPtr = rPtr->link[1];
            rPtr->color = RED;
            qPtr->color = BLACK;
            rPtr->link[1] = qPtr->link[0];
            qPtr->link[0] = rPtr;
            rPtr = stack[ht - 1]->link[0] = qPtr;
          }
          rPtr->color = stack[ht - 1]->color;
          stack[ht - 1]->color = BLACK;
          rPtr->link[0]->color = BLACK;
          stack[ht - 1]->link[0] = rPtr->link[1];
          rPtr->link[1] = stack[ht - 1];
          if (stack[ht - 1] == root) {
            root = rPtr;
          } else {
            stack[ht - 2]->link[dir[ht - 2]] = rPtr;
          }
          break;
        }
      }
      ht--;
    }
  }
}

// Print the inorder traversal of the tree
void inorderTraversal(struct rbNode *node) {
  if (node) {
    inorderTraversal(node->link[0]);
    printf("%d  ", node->data);
    inorderTraversal(node->link[1]);
  }
  return;
}

// Driver code
int main() {
  int ch, data;
  while (1) {
    printf("1. Insertion\t2. Deletion\n");
    printf("3. Traverse\t4. Exit");
    printf("\nEnter your choice:");
    scanf("%d", &ch);
    switch (ch) {
      case 1:
        printf("Enter the element to insert:");
        scanf("%d", &data);
        insertion(data);
        break;
      case 2:
        printf("Enter the element to delete:");
        scanf("%d", &data);
        deletion(data);
        break;
      case 3:
        inorderTraversal(root);
        printf("\n");
        break;
      case 4:
        exit(0);
      default:
        printf("Not available\n");
        break;
    }
    printf("\n");
  }
  return 0;
}
```
</details>

### Augumenting data structures

Augmenting a data structure is the process of taking an existing data structure and customizing it a little bit to fit your needs. This lets you take advantage of a clever stock data structure that almost, but not quite, solves your problem, and add that finishing touch that makes it do the trick.


#### Dynamic order statistics
OS-SELECT(i, S): returns the ith smallest element
in the dynamic set S.
OS-RANK(x, S): returns the rank of x  S in the
sorted order of S’s elements.
IDEA: Use a red-black tree for the set S, but keep
subtree sizes in the nodes

#### How to augument a data structure

Basic Algorithm for Augmentation of Data Structures
Choose underlying data structure on which you want to add additional information to make new data structure(Red-Black Tree).
Add additional information on the selected data structure(Sub-Tree Size).
Verify that information can be maintained for modifying operations(Insertion,Deletion,Rotation of nodes).
Develop new operations that can be performed on the new data structure depending on your requirements(OS_Select,OS_Rank).

#### Interval trees

Consider a situation where we have a set of intervals and we need following operations to be implemented efficiently.
1) Add an interval
2) Remove an interval
3) Given an interval x, find if x overlaps with any of the existing intervals.

Interval Tree: The idea is to augment a self-balancing Binary Search Tree (BST) like Red Black Tree, AVL Tree, etc to maintain set of intervals so that all operations can be done in O(Logn) time.

Every node of Interval Tree stores following information.
a) i: An interval which is represented as a pair [low, high]
b) max: Maximum high value in subtree rooted with this node.

The low value of an interval is used as key to maintain order in BST. The insert and delete operations are same as insert and delete in self-balancing BST used.


#### Code in c++

 <details>
<summary>Answer</summary>
</details>

```
#include <iostream>
using namespace std;
  
// Structure to represent an interval
struct Interval
{
    int low, high;
};
  
// Structure to represent a node in Interval Search Tree
struct ITNode
{
    Interval *i;  // 'i' could also be a normal variable
    int max;
    ITNode *left, *right;
};
  
// A utility function to create a new Interval Search Tree Node
ITNode * newNode(Interval i)
{
    ITNode *temp = new ITNode;
    temp->i = new Interval(i);
    temp->max = i.high;
    temp->left = temp->right = NULL;
    return temp;
};
  
// A utility function to insert a new Interval Search Tree Node
// This is similar to BST Insert.  Here the low value of interval
// is used tomaintain BST property
ITNode *insert(ITNode *root, Interval i)
{
    // Base case: Tree is empty, new node becomes root
    if (root == NULL)
        return newNode(i);
  
    // Get low value of interval at root
    int l = root->i->low;
  
    // If root's low value is smaller, then new interval goes to
    // left subtree
    if (i.low < l)
        root->left = insert(root->left, i);
  
    // Else, new node goes to right subtree.
    else
        root->right = insert(root->right, i);
  
    // Update the max value of this ancestor if needed
    if (root->max < i.high)
        root->max = i.high;
  
    return root;
}
  
// A utility function to check if given two intervals overlap
bool doOVerlap(Interval i1, Interval i2)
{
    if (i1.low <= i2.high && i2.low <= i1.high)
        return true;
    return false;
}
  
// The main function that searches a given interval i in a given
// Interval Tree.
Interval *overlapSearch(ITNode *root, Interval i)
{
    // Base Case, tree is empty
    if (root == NULL) return NULL;
  
    // If given interval overlaps with root
    if (doOVerlap(*(root->i), i))
        return root->i;
  
    // If left child of root is present and max of left child is
    // greater than or equal to given interval, then i may
    // overlap with an interval is left subtree
    if (root->left != NULL && root->left->max >= i.low)
        return overlapSearch(root->left, i);
  
    // Else interval can only overlap with right subtree
    return overlapSearch(root->right, i);
}
  
void inorder(ITNode *root)
{
    if (root == NULL) return;
  
    inorder(root->left);
  
    cout << "[" << root->i->low << ", " << root->i->high << "]"
         << " max = " << root->max << endl;
  
    inorder(root->right);
}
  
// Driver program to test above functions
int main()
{
    // Let us create interval tree shown in above figure
    Interval ints[] = {{15, 20}, {10, 30}, {17, 19},
        {5, 20}, {12, 15}, {30, 40}
    };
    int n = sizeof(ints)/sizeof(ints[0]);
    ITNode *root = NULL;
    for (int i = 0; i < n; i++)
        root = insert(root, ints[i]);
  
    cout << "Inorder traversal of constructed Interval Tree is\n";
    inorder(root);
  
    Interval x = {6, 7};
  
    cout << "\nSearching for interval [" << x.low << "," << x.high << "]";
    Interval *res = overlapSearch(root, x);
    if (res == NULL)
        cout << "\nNo Overlapping Interval";
    else
        cout << "\nOverlaps with [" << res->low << ", " << res->high << "]";
    return 0;
}
Output:

Inorder traversal of constructed Interval Tree is
[5, 20] max = 20
[10, 30] max = 30
[12, 15] max = 15
[15, 20] max = 40
[17, 19] max = 40
[30, 40] max = 40

Searching for interval [6,7]
Overlaps with [5, 20]

```
</details>

## Advanced design and analysis techniques

### Dynamic programming

storing intermediate results and using it for solving further sub problems.ex: fibonacci series.

#### Rod cutting

Given a rod of length n inches and an array of prices that contains prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces

#### Code in c
  <details>
<summary>Answer</summary>
 
```
 
#include <limits.h>
#include <stdio.h>
  
// A utility function to get the maximum of two integers
int max(int a, int b) { return (a > b) ? a : b; }
  
/* Returns the best obtainable price for a rod of length n and
   price[] as prices of different pieces */
int cutRod(int price[], int n)
{
    if (n <= 0)
        return 0;
    int max_val = INT_MIN;
  
    // Recursively cut the rod in different pieces and compare different
    // configurations
    for (int i = 0; i < n; i++)
        max_val = max(max_val, price[i] + cutRod(price, n - i - 1));
  
    return max_val;
}
  
/* Driver program to test above functions */
int main()
{
    int arr[] = { 1, 5, 8, 9, 10, 17, 17, 20 };
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("Maximum Obtainable Value is %d", cutRod(arr, size));
    getchar();
    return 0;
}
 ```
 </details> 
 


#### Matrix chain multiplication

Given a sequence of matrices, find the most efficient way to multiply these matrices together. The problem is not actually to perform the multiplications, but merely to decide in which order to perform the multiplications.

 <details>
<summary>Answer</summary>
 
```
/* A naive recursive implementation that simply
  follows the above optimal substructure property */
#include <limits.h>
#include <stdio.h>
  
// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
int MatrixChainOrder(int p[], int i, int j)
{
    if (i == j)
        return 0;
    int k;
    int min = INT_MAX;
    int count;
  
    // place parenthesis at different places between first
    // and last matrix, recursively calculate count of
    // multiplications for each parenthesis placement and
    // return the minimum count
    for (k = i; k < j; k++) {
        count = MatrixChainOrder(p, i, k) + 
                MatrixChainOrder(p, k + 1, j) + 
                p[i - 1] * p[k] * p[j];
  
        if (count < min)
            min = count;
    }
  
    // Return minimum count
    return min;
}
  
// Driver program to test above function
int main()
{
    int arr[] = { 1, 2, 3, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
  
    printf("Minimum number of multiplications is %d ",
           MatrixChainOrder(arr, 1, n - 1));
  
    getchar();
    return 0;
}

```
</details>

#### Elements of dynamic programming

Substructure: Decompose the given problem into smaller subproblems. Express the solution of the original problem in terms of the solution for smaller problems. Table Structure: After solving the sub-problems, store the results to the sub problems in a table.

#### Longest common subsequence

given two sequenceS, find the longest common terms between them.
 Example: ABCDEF & ABC
 Answer: ABC
 
 #### Code in c
  <details>
<summary>Answer</summary>
 
```
 #include<bits/stdc++.h>
  
int max(int a, int b);
  
/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int lcs( char *X, char *Y, int m, int n )
{
   if (m == 0 || n == 0)
     return 0;
   if (X[m-1] == Y[n-1])
     return 1 + lcs(X, Y, m-1, n-1);
   else
     return max(lcs(X, Y, m, n-1), lcs(X, Y, m-1, n));
}
  
/* Utility function to get max of 2 integers */
int max(int a, int b)
{
    return (a > b)? a : b;
}
  
/* Driver program to test above function */
int main()
{
  char X[] = "AGGTAB";
  char Y[] = "GXTXAYB";
  
  int m = strlen(X);
  int n = strlen(Y);
  
  printf("Length of LCS is %d", lcs( X, Y, m, n ) );
  
  return 0;
}
 
 ```
 </details>

#### Optimal binary search tree

Given a sorted array keys[0.. n-1] of search keys and an array freq[0.. n-1] of frequency counts, where freq[i] is the number of searches to keys[i]. Construct a binary search tree of all keys such that the total cost of all the searches is as small as possible.

Let us first define the cost of a BST. The cost of a BST node is level of that node multiplied by its frequency. Level of root is 1.

Examples:

Input:  keys[] = {10, 12}, freq[] = {34, 50}
There can be following two possible BSTs 
        10                       12
          \                     / 
           12                 10
          I                     II
Frequency of searches of 10 and 12 are 34 and 50 respectively.
The cost of tree I is 34*1 + 50*2 = 134
The cost of tree II is 50*1 + 34*2 = 118 


Input:  keys[] = {10, 12, 20}, freq[] = {34, 8, 50}
There can be following possible BSTs
    10                12                 20         10              20
      \             /    \              /             \            /
      12          10     20           12               20         10  
        \                            /                 /           \
         20                        10                12             12  
     I               II             III             IV             V
Among all possible BSTs, cost of the fifth BST is minimum.  
Cost of the fifth BST is 1*50 + 2*34 + 3*8 = 142

#### Code in c
   <details>
<summary>Answer</summary>
 
```
// A naive recursive implementation of optimal binary 
// search tree problem
#include <stdio.h>
#include <limits.h>
  
// A utility function to get sum of array elements 
// freq[i] to freq[j]
int sum(int freq[], int i, int j);
  
// A recursive function to calculate cost of optimal 
// binary search tree
int optCost(int freq[], int i, int j)
{
   // Base cases
   if (j < i)      // no elements in this subarray
     return 0;
   if (j == i)     // one element in this subarray
     return freq[i];
  
   // Get sum of freq[i], freq[i+1], ... freq[j]
   int fsum = sum(freq, i, j);
  
   // Initialize minimum value
   int min = INT_MAX;
  
   // One by one consider all elements as root and
   // recursively find cost of the BST, compare the
   // cost with min and update min if needed
   for (int r = i; r <= j; ++r)
   {
       int cost = optCost(freq, i, r-1) + 
                  optCost(freq, r+1, j);
       if (cost < min)
          min = cost;
   }
  
   // Return minimum value
   return min + fsum;
}
  
// The main function that calculates minimum cost of
// a Binary Search Tree. It mainly uses optCost() to 
// find the optimal cost.
int optimalSearchTree(int keys[], int freq[], int n)
{
     // Here array keys[] is assumed to be sorted in 
     // increasing order. If keys[] is not sorted, then 
     // add code to sort keys, and rearrange freq[] 
     // accordingly.
     return optCost(freq, 0, n-1);
}
  
// A utility function to get sum of array elements 
// freq[i] to freq[j]
int sum(int freq[], int i, int j)
{
    int s = 0;
    for (int k = i; k <=j; k++)
       s += freq[k];
    return s;
}
  
// Driver program to test above functions
int main()
{
    int keys[] = {10, 12, 20};
    int freq[] = {34, 8, 50};
    int n = sizeof(keys)/sizeof(keys[0]);
    printf("Cost of Optimal BST is %d ", 
               optimalSearchTree(keys, freq, n));
    return 0;
}

```
</details>
 
 ### Greedy algorithm
 
 Used for solving optimizing problems which either require max result or min result.
 
#### An activity selection problem

You are given n activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time.

 #### Code in c
   <details>
<summary>Answer</summary>
 
```
  
 void printMaxActivities(int s[], int f[], int n)
{
    int i, j;
  
    printf("Following activities are selected n");
  
    // The first activity always gets selected
    i = 0;
    printf("%d ", i);
  
    // Consider rest of the activities
    for (j = 1; j < n; j++) {
        // If this activity has start time greater than or
        // equal to the finish time of previously selected
        // activity, then select it
        if (s[j] >= f[i]) {
            printf("%d ", j);
            i = j;
        }
    }
}
  
// driver program to test above function
int main()
{
    int s[] = { 1, 3, 0, 5, 8, 5 };
    int f[] = { 2, 4, 6, 7, 9, 9 };
    int n = sizeof(s) / sizeof(s[0]);
    printMaxActivities(s, f, n);
    return 0;
}
```
</details>

#### Elements of the Greedy Strategy

Elements of the Greedy Strategy
Optimal Substructure: An optimal solution to the problem contains within it optimal solutions to sub-problems. ...
The 0 - 1 knapsack problem: A thief has a knapsack that holds at most W pounds. ...
Fractional knapsack problem: takes parts, as well as wholes.

#### Huffman codes

Huffman coding is a lossless data compression algorithm. The idea is to assign variable-length codes to input characters, lengths of the assigned codes are based on the frequencies of corresponding characters. The most frequent character gets the smallest code and the least frequent character gets the largest code.

 
#### Code in c
   <details>
<summary>Answer</summary>
 
```
// C program for Huffman Coding
#include <stdio.h>
#include <stdlib.h>
 
// This constant can be avoided by explicitly
// calculating height of Huffman Tree
#define MAX_TREE_HT 100
 
// A Huffman tree node
struct MinHeapNode {
 
    // One of the input characters
    char data;
 
    // Frequency of the character
    unsigned freq;
 
    // Left and right child of this node
    struct MinHeapNode *left, *right;
};
 
// A Min Heap:  Collection of
// min-heap (or Huffman tree) nodes
struct MinHeap {
 
    // Current size of min heap
    unsigned size;
 
    // capacity of min heap
    unsigned capacity;
 
    // Array of minheap node pointers
    struct MinHeapNode** array;
};
 
// A utility function allocate a new
// min heap node with given character
// and frequency of the character
struct MinHeapNode* newNode(char data, unsigned freq)
{
    struct MinHeapNode* temp = (struct MinHeapNode*)malloc(
        sizeof(struct MinHeapNode));
 
    temp->left = temp->right = NULL;
    temp->data = data;
    temp->freq = freq;
 
    return temp;
}
 
// A utility function to create
// a min heap of given capacity
struct MinHeap* createMinHeap(unsigned capacity)
 
{
 
    struct MinHeap* minHeap
        = (struct MinHeap*)malloc(sizeof(struct MinHeap));
 
    // current size is 0
    minHeap->size = 0;
 
    minHeap->capacity = capacity;
 
    minHeap->array = (struct MinHeapNode**)malloc(
        minHeap->capacity * sizeof(struct MinHeapNode*));
    return minHeap;
}
 
// A utility function to
// swap two min heap nodes
void swapMinHeapNode(struct MinHeapNode** a,
                     struct MinHeapNode** b)
 
{
 
    struct MinHeapNode* t = *a;
    *a = *b;
    *b = t;
}
 
// The standard minHeapify function.
void minHeapify(struct MinHeap* minHeap, int idx)
 
{
 
    int smallest = idx;
    int left = 2 * idx + 1;
    int right = 2 * idx + 2;
 
    if (left < minHeap->size
        && minHeap->array[left]->freq
               < minHeap->array[smallest]->freq)
        smallest = left;
 
    if (right < minHeap->size
        && minHeap->array[right]->freq
               < minHeap->array[smallest]->freq)
        smallest = right;
 
    if (smallest != idx) {
        swapMinHeapNode(&minHeap->array[smallest],
                        &minHeap->array[idx]);
        minHeapify(minHeap, smallest);
    }
}
 
// A utility function to check
// if size of heap is 1 or not
int isSizeOne(struct MinHeap* minHeap)
{
 
    return (minHeap->size == 1);
}
 
// A standard function to extract
// minimum value node from heap
struct MinHeapNode* extractMin(struct MinHeap* minHeap)
 
{
 
    struct MinHeapNode* temp = minHeap->array[0];
    minHeap->array[0] = minHeap->array[minHeap->size - 1];
 
    --minHeap->size;
    minHeapify(minHeap, 0);
 
    return temp;
}
 
// A utility function to insert
// a new node to Min Heap
void insertMinHeap(struct MinHeap* minHeap,
                   struct MinHeapNode* minHeapNode)
 
{
 
    ++minHeap->size;
    int i = minHeap->size - 1;
 
    while (i
           && minHeapNode->freq
                  < minHeap->array[(i - 1) / 2]->freq) {
 
        minHeap->array[i] = minHeap->array[(i - 1) / 2];
        i = (i - 1) / 2;
    }
 
    minHeap->array[i] = minHeapNode;
}
 
// A standard function to build min heap
void buildMinHeap(struct MinHeap* minHeap)
 
{
 
    int n = minHeap->size - 1;
    int i;
 
    for (i = (n - 1) / 2; i >= 0; --i)
        minHeapify(minHeap, i);
}
 
// A utility function to print an array of size n
void printArr(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        printf("%d", arr[i]);
 
    printf("\n");
}
 
// Utility function to check if this node is leaf
int isLeaf(struct MinHeapNode* root)
 
{
 
    return !(root->left) && !(root->right);
}
 
// Creates a min heap of capacity
// equal to size and inserts all character of
// data[] in min heap. Initially size of
// min heap is equal to capacity
struct MinHeap* createAndBuildMinHeap(char data[],
                                      int freq[], int size)
 
{
 
    struct MinHeap* minHeap = createMinHeap(size);
 
    for (int i = 0; i < size; ++i)
        minHeap->array[i] = newNode(data[i], freq[i]);
 
    minHeap->size = size;
    buildMinHeap(minHeap);
 
    return minHeap;
}
 
// The main function that builds Huffman tree
struct MinHeapNode* buildHuffmanTree(char data[],
                                     int freq[], int size)
 
{
    struct MinHeapNode *left, *right, *top;
 
    // Step 1: Create a min heap of capacity
    // equal to size.  Initially, there are
    // modes equal to size.
    struct MinHeap* minHeap
        = createAndBuildMinHeap(data, freq, size);
 
    // Iterate while size of heap doesn't become 1
    while (!isSizeOne(minHeap)) {
 
        // Step 2: Extract the two minimum
        // freq items from min heap
        left = extractMin(minHeap);
        right = extractMin(minHeap);
 
        // Step 3:  Create a new internal
        // node with frequency equal to the
        // sum of the two nodes frequencies.
        // Make the two extracted node as
        // left and right children of this new node.
        // Add this node to the min heap
        // '$' is a special value for internal nodes, not
        // used
        top = newNode('$', left->freq + right->freq);
 
        top->left = left;
        top->right = right;
 
        insertMinHeap(minHeap, top);
    }
 
    // Step 4: The remaining node is the
    // root node and the tree is complete.
    return extractMin(minHeap);
}
 
// Prints huffman codes from the root of Huffman Tree.
// It uses arr[] to store codes
void printCodes(struct MinHeapNode* root, int arr[],
                int top)
 
{
 
    // Assign 0 to left edge and recur
    if (root->left) {
 
        arr[top] = 0;
        printCodes(root->left, arr, top + 1);
    }
 
    // Assign 1 to right edge and recur
    if (root->right) {
 
        arr[top] = 1;
        printCodes(root->right, arr, top + 1);
    }
 
    // If this is a leaf node, then
    // it contains one of the input
    // characters, print the character
    // and its code from arr[]
    if (isLeaf(root)) {
 
        printf("%c: ", root->data);
        printArr(arr, top);
    }
}
 
// The main function that builds a
// Huffman Tree and print codes by traversing
// the built Huffman Tree
void HuffmanCodes(char data[], int freq[], int size)
 
{
    // Construct Huffman Tree
    struct MinHeapNode* root
        = buildHuffmanTree(data, freq, size);
 
    // Print Huffman codes using
    // the Huffman tree built above
    int arr[MAX_TREE_HT], top = 0;
 
    printCodes(root, arr, top);
}
 
// Driver code
int main()
{
 
    char arr[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
    int freq[] = { 5, 9, 12, 13, 16, 45 };
 
    int size = sizeof(arr) / sizeof(arr[0]);
 
    HuffmanCodes(arr, freq, size);
 
    return 0;
}
```
</details>

#### Matroids and greedy strategy

Matroid: A matroid consists of a base set U and a collection I of independent
subsets. Independence will be related to different objects depending on the
problem - for the minimum spanning tree, an independent subset could be a
tree. In linear algebra, an independent subset could be linearly independent
vectors. A matroid’s notion of independence is as follows. A, B ⊆ U satisfy:
1. If A is a subset of B and B is independent subset, then A is independent
subset, too. In other words:
A ⊆ B, B ∈ I ⇒ A ∈ I
2. The empty set is independent.
3. Suppose A and B are indepedent sets and A is smaller than B. Then
there is some element e in B that is not in A such that A plus e is also
an independent set. In other words:
A, B ∈ I, |A| < |B| ⇒ ∃e ∈ B\A such that A ∪ {e} ∈ I

#### A task scheduling problem using matroid

An interesting problem that can be solved using matroid is the problem of optimally scheduling unit-time tasks on a single processor, where each task has a deadline, along with a penalty paid if the task misses its deadline.

### Amortized algorithm

is used for algorithms where an occasional operation is very slow, but most of the other operations are faster. In Amortized Analysis, we analyze a sequence of operations and guarantee a worst case average time which is lower than the worst case time of a particular expensive operation. 
The example data structures whose operations are analyzed using Amortized Analysis are Hash Tables, Disjoint Sets and Splay Trees. 

#### Aggregate analysis

In fact, a sequence of n operations on an initially empty stack cost at most O(n).

 

·        Each object can be POP only once (including in MULTIPOP) for each time it is PUSHed. #POPs is at most #PUSHs, which is at most n.

 

·        Thus the average cost of an operation is O(n)/n = O(1).

 

·        Amortized cost in aggregate analysis is defined to be average cost.

 

#### The accounting method

An accounting method consists of the rules and procedures a company follows in reporting its revenues and expenses. The two main accounting methods are cash accounting and accrual accounting. Cash accounting records revenues and expenses when they are received and paid.

Types of Accounting Methods
Cash Accounting
Cash accounting is an accounting method that is relatively simple and is commonly used by small businesses. In cash accounting, transactions are only recorded when cash is spent or received.

In cash accounting, a sale is recorded when the payment is received and an expense is recorded only when a bill is paid. The cash accounting method is, of course, the method most people use in managing their personal finances and it is appropriate for businesses up to a certain size.

If a business generates more than $25 million in average annual gross receipts for the preceding three years, however, it must use the accrual method, according to Internal Revenue Service rules.1﻿

Accrual Accounting
Accrual accounting is based on the matching principle, which is intended to match the timing of revenue and expense recognition. By matching revenues with expenses, the accrual method gives a more accurate picture of a company's true financial condition.

Under the accrual method, transactions are recorded when they are incurred rather than awaiting payment. This means a purchase order is recorded as revenue even though the funds are not received immediately. The same goes for expenses in that they are recorded even though no payment has been made.



#### The potential method

In computational complexity theory, the potential method is a method used to analyze the amortized time and space complexity of a data structure, a measure of its performance over sequences of operations that smooths out the cost of infrequent but expensive operations.


#### Dynamic tables



## Advanced data structures

### B-trees

#### Definition of b-trees

 guidelines to make m-way search trees are known as b-trees.(dynamic multilevel index).
{B-tree is a special type of self-balancing search tree in which each node can contain more than one key and can have more than two children. It is a generalized form of the binary search tree.}

#### Basic operations on b tree

Algorithm for Searching an Element
BtreeSearch(x, k)
 i = 1
 while i ≤ n[x] and k ≥ keyi[x]        // n[x] means number of keys in x node
    do i = i + 1
if i  n[x] and k = keyi[x]
    then return (x, i)
if leaf [x]
    then return NIL
else
    return BtreeSearch(ci[x], k)

#### Deleting a tree from a b tree

Before going through the steps below, one must know these facts about a B tree of degree m.

A node can have a maximum of m children. (i.e. 3)
A node can contain a maximum of m - 1 keys. (i.e. 2)
A node should have a minimum of ⌈m/2⌉ children. (i.e. 2)
A node (except root node) should contain a minimum of ⌈m/2⌉ - 1 keys. (i.e. 1)
There are three main cases for deletion operation in a B tree.

#### code in c(deletion)

<details>
<summary>Answer</summary>

```
#include <stdio.h>
#include <stdlib.h>

#define MAX 3
#define MIN 2

struct BTreeNode {
  int item[MAX + 1], count;
  struct BTreeNode *linker[MAX + 1];
};

struct BTreeNode *root;

// Node creation
struct BTreeNode *createNode(int item, struct BTreeNode *child) {
  struct BTreeNode *newNode;
  newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  newNode->item[1] = item;
  newNode->count = 1;
  newNode->linker[0] = root;
  newNode->linker[1] = child;
  return newNode;
}

// Add value to the node
void addValToNode(int item, int pos, struct BTreeNode *node,
          struct BTreeNode *child) {
  int j = node->count;
  while (j > pos) {
    node->item[j + 1] = node->item[j];
    node->linker[j + 1] = node->linker[j];
    j--;
  }
  node->item[j + 1] = item;
  node->linker[j + 1] = child;
  node->count++;
}

// Split the node
void splitNode(int item, int *pval, int pos, struct BTreeNode *node,
         struct BTreeNode *child, struct BTreeNode **newNode) {
  int median, j;

  if (pos > MIN)
    median = MIN + 1;
  else
    median = MIN;

  *newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  j = median + 1;
  while (j <= MAX) {
    (*newNode)->item[j - median] = node->item[j];
    (*newNode)->linker[j - median] = node->linker[j];
    j++;
  }
  node->count = median;
  (*newNode)->count = MAX - median;

  if (pos <= MIN) {
    addValToNode(item, pos, node, child);
  } else {
    addValToNode(item, pos - median, *newNode, child);
  }
  *pval = node->item[node->count];
  (*newNode)->linker[0] = node->linker[node->count];
  node->count--;
}

// Set the value in the node
int setValueInNode(int item, int *pval,
           struct BTreeNode *node, struct BTreeNode **child) {
  int pos;
  if (!node) {
    *pval = item;
    *child = NULL;
    return 1;
  }

  if (item < node->item[1]) {
    pos = 0;
  } else {
    for (pos = node->count;
       (item < node->item[pos] && pos > 1); pos--)
      ;
    if (item == node->item[pos]) {
      printf("Duplicates not allowed\n");
      return 0;
    }
  }
  if (setValueInNode(item, pval, node->linker[pos], child)) {
    if (node->count < MAX) {
      addValToNode(*pval, pos, node, *child);
    } else {
      splitNode(*pval, pval, pos, node, *child, child);
      return 1;
    }
  }
  return 0;
}

// Insertion operation
void insertion(int item) {
  int flag, i;
  struct BTreeNode *child;

  flag = setValueInNode(item, &i, root, &child);
  if (flag)
    root = createNode(i, child);
}

// Copy the successor
void copySuccessor(struct BTreeNode *myNode, int pos) {
  struct BTreeNode *dummy;
  dummy = myNode->linker[pos];

  for (; dummy->linker[0] != NULL;)
    dummy = dummy->linker[0];
  myNode->item[pos] = dummy->item[1];
}

// Remove the value
void removeVal(struct BTreeNode *myNode, int pos) {
  int i = pos + 1;
  while (i <= myNode->count) {
    myNode->item[i - 1] = myNode->item[i];
    myNode->linker[i - 1] = myNode->linker[i];
    i++;
  }
  myNode->count--;
}

// Do right shift
void rightShift(struct BTreeNode *myNode, int pos) {
  struct BTreeNode *x = myNode->linker[pos];
  int j = x->count;

  while (j > 0) {
    x->item[j + 1] = x->item[j];
    x->linker[j + 1] = x->linker[j];
  }
  x->item[1] = myNode->item[pos];
  x->linker[1] = x->linker[0];
  x->count++;

  x = myNode->linker[pos - 1];
  myNode->item[pos] = x->item[x->count];
  myNode->linker[pos] = x->linker[x->count];
  x->count--;
  return;
}

// Do left shift
void leftShift(struct BTreeNode *myNode, int pos) {
  int j = 1;
  struct BTreeNode *x = myNode->linker[pos - 1];

  x->count++;
  x->item[x->count] = myNode->item[pos];
  x->linker[x->count] = myNode->linker[pos]->linker[0];

  x = myNode->linker[pos];
  myNode->item[pos] = x->item[1];
  x->linker[0] = x->linker[1];
  x->count--;

  while (j <= x->count) {
    x->item[j] = x->item[j + 1];
    x->linker[j] = x->linker[j + 1];
    j++;
  }
  return;
}

// Merge the nodes
void mergeNodes(struct BTreeNode *myNode, int pos) {
  int j = 1;
  struct BTreeNode *x1 = myNode->linker[pos], *x2 = myNode->linker[pos - 1];

  x2->count++;
  x2->item[x2->count] = myNode->item[pos];
  x2->linker[x2->count] = myNode->linker[0];

  while (j <= x1->count) {
    x2->count++;
    x2->item[x2->count] = x1->item[j];
    x2->linker[x2->count] = x1->linker[j];
    j++;
  }

  j = pos;
  while (j < myNode->count) {
    myNode->item[j] = myNode->item[j + 1];
    myNode->linker[j] = myNode->linker[j + 1];
    j++;
  }
  myNode->count--;
  free(x1);
}

// Adjust the node
void adjustNode(struct BTreeNode *myNode, int pos) {
  if (!pos) {
    if (myNode->linker[1]->count > MIN) {
      leftShift(myNode, 1);
    } else {
      mergeNodes(myNode, 1);
    }
  } else {
    if (myNode->count != pos) {
      if (myNode->linker[pos - 1]->count > MIN) {
        rightShift(myNode, pos);
      } else {
        if (myNode->linker[pos + 1]->count > MIN) {
          leftShift(myNode, pos + 1);
        } else {
          mergeNodes(myNode, pos);
        }
      }
    } else {
      if (myNode->linker[pos - 1]->count > MIN)
        rightShift(myNode, pos);
      else
        mergeNodes(myNode, pos);
    }
  }
}

// Delete a value from the node
int delValFromNode(int item, struct BTreeNode *myNode) {
  int pos, flag = 0;
  if (myNode) {
    if (item < myNode->item[1]) {
      pos = 0;
      flag = 0;
    } else {
      for (pos = myNode->count; (item < myNode->item[pos] && pos > 1); pos--)
        ;
      if (item == myNode->item[pos]) {
        flag = 1;
      } else {
        flag = 0;
      }
    }
    if (flag) {
      if (myNode->linker[pos - 1]) {
        copySuccessor(myNode, pos);
        flag = delValFromNode(myNode->item[pos], myNode->linker[pos]);
        if (flag == 0) {
          printf("Given data is not present in B-Tree\n");
        }
      } else {
        removeVal(myNode, pos);
      }
    } else {
      flag = delValFromNode(item, myNode->linker[pos]);
    }
    if (myNode->linker[pos]) {
      if (myNode->linker[pos]->count < MIN)
        adjustNode(myNode, pos);
    }
  }
  return flag;
}

// Delete operaiton
void delete (int item, struct BTreeNode *myNode) {
  struct BTreeNode *tmp;
  if (!delValFromNode(item, myNode)) {
    printf("Not present\n");
    return;
  } else {
    if (myNode->count == 0) {
      tmp = myNode;
      myNode = myNode->linker[0];
      free(tmp);
    }
  }
  root = myNode;
  return;
}

void searching(int item, int *pos, struct BTreeNode *myNode) {
  if (!myNode) {
    return;
  }

  if (item < myNode->item[1]) {
    *pos = 0;
  } else {
    for (*pos = myNode->count;
       (item < myNode->item[*pos] && *pos > 1); (*pos)--)
      ;
    if (item == myNode->item[*pos]) {
      printf("%d present in B-tree", item);
      return;
    }
  }
  searching(item, pos, myNode->linker[*pos]);
  return;
}

void traversal(struct BTreeNode *myNode) {
  int i;
  if (myNode) {
    for (i = 0; i < myNode->count; i++) {
      traversal(myNode->linker[i]);
      printf("%d ", myNode->item[i + 1]);
    }
    traversal(myNode->linker[i]);
  }
}

int main() {
  int item, ch;

  insertion(8);
  insertion(9);
  insertion(10);
  insertion(11);
  insertion(15);
  insertion(16);
  insertion(17);
  insertion(18);
  insertion(20);
  insertion(23);

  traversal(root);

  delete (20, root);
  printf("\n");
  traversal(root);
}


```
</details>

#### Code in c
<details>
<summary>Answer</summary>
 
```
 #include "stdio.h"
#include "stdlib.h"

#define M 3

typedef struct _node {
        int    n; /* n < M No. of keys in node will always less than order of B tree */
        int              keys[M - 1]; /*array of keys*/
        struct _node *p[M]; /* (n+1 pointers will be in use) */
} node;
node *root = NULL;

typedef enum KeyStatus {
        Duplicate,
        SearchFailure,
        Success,
        InsertIt,
        LessKeys,
} KeyStatus;

void insert(int key);
void display(node *root, int);
void DelNode(int x);
void search(int x);
KeyStatus ins(node *r, int x, int* y, node** u);
int searchPos(int x, int *key_arr, int n);
KeyStatus del(node *r, int x);
void eatline(void);
void inorder(node *ptr);
int totalKeys(node *ptr);
void printTotal(node *ptr);
int getMin(node *ptr);
int getMax(node *ptr);
void getMinMax(node *ptr);
int max(int first, int second, int third);
int maxLevel(node *ptr);
void printMaxLevel(node *ptr);


int main() {
        int key;
        int choice;
        printf("Creation of B tree for M=%d\n", M);
        while (1) {
                printf("1.Insert\n");
                printf("2.Delete\n");
                printf("3.Search\n");
                printf("4.Display\n");
                printf("5.Quit\n");
                printf("6.Enumerate\n");
                printf("7.Total Keys\n");
                printf("8.Min and Max Keys\n");
                printf("9.Max Level\n");
                printf("Enter your choice : ");
                scanf("%d", &choice); eatline();

                switch (choice) {
                case 1:
                        printf("Enter the key : ");
                        scanf("%d", &key); eatline();
                        insert(key);
                        break;
                case 2:
                        printf("Enter the key : ");
                        scanf("%d", &key); eatline();
                        DelNode(key);
                        break;
                case 3:
                        printf("Enter the key : ");
                        scanf("%d", &key); eatline();
                        search(key);
                        break;
                case 4:
                        printf("Btree is :\n");
                        display(root, 0);
                        break;
                case 5:
                        exit(1);
                case 6:
                        printf("Btree in sorted order is:\n");
                        inorder(root); putchar('\n');
                        break;
                case 7:
                        printf("The total number of keys in this tree is:\n");
                        printTotal(root);
                        break;
                case 8:
                        getMinMax(root);
                        break;
                case 9:
                        printf("The maximum level in this tree is:\n");
                        printMaxLevel(root);
                        break;
                default:
                        printf("Wrong choice\n");
                        break;
                }/*End of switch*/
        }/*End of while*/
        return 0;
}/*End of main()*/

void insert(int key) {
        node *newnode;
        int upKey;
        KeyStatus value;
        value = ins(root, key, &upKey, &newnode);
        if (value == Duplicate)
                printf("Key already available\n");
        if (value == InsertIt) {
                node *uproot = root;
                root = (node*)malloc(sizeof(node));
                root->n = 1;
                root->keys[0] = upKey;
                root->p[0] = uproot;
                root->p[1] = newnode;
        }/*End of if */
}/*End of insert()*/

KeyStatus ins(node *ptr, int key, int *upKey, node **newnode) {
        node *newPtr, *lastPtr;
        int pos, i, n, splitPos;
        int newKey, lastKey;
        KeyStatus value;
        if (ptr == NULL) {
                *newnode = NULL;
                *upKey = key;
                return InsertIt;
        }
        n = ptr->n;
        pos = searchPos(key, ptr->keys, n);
        if (pos < n && key == ptr->keys[pos])
                return Duplicate;
        value = ins(ptr->p[pos], key, &newKey, &newPtr);
        if (value != InsertIt)
                return value;
        /*If keys in node is less than M-1 where M is order of B tree*/
        if (n < M - 1) {
                pos = searchPos(newKey, ptr->keys, n);
                /*Shifting the key and pointer right for inserting the new key*/
                for (i = n; i>pos; i--) {
                        ptr->keys[i] = ptr->keys[i - 1];
                        ptr->p[i + 1] = ptr->p[i];
                }
                /*Key is inserted at exact location*/
                ptr->keys[pos] = newKey;
                ptr->p[pos + 1] = newPtr;
                ++ptr->n; /*incrementing the number of keys in node*/
                return Success;
        }/*End of if */
         /*If keys in nodes are maximum and position of node to be inserted is last*/
        if (pos == M - 1) {
                lastKey = newKey;
                lastPtr = newPtr;
        }
        else { /*If keys in node are maximum and position of node to be inserted is not last*/
                lastKey = ptr->keys[M - 2];
                lastPtr = ptr->p[M - 1];
                for (i = M - 2; i>pos; i--) {
                        ptr->keys[i] = ptr->keys[i - 1];
                        ptr->p[i + 1] = ptr->p[i];
                }
                ptr->keys[pos] = newKey;
                ptr->p[pos + 1] = newPtr;
        }
        splitPos = (M - 1) / 2;
        (*upKey) = ptr->keys[splitPos];

        (*newnode) = (node*)malloc(sizeof(node));/*Right node after split*/
        ptr->n = splitPos; /*No. of keys for left splitted node*/
        (*newnode)->n = M - 1 - splitPos;/*No. of keys for right splitted node*/
        for (i = 0; i < (*newnode)->n; i++) {
                (*newnode)->p[i] = ptr->p[i + splitPos + 1];
                if (i < (*newnode)->n - 1)
                        (*newnode)->keys[i] = ptr->keys[i + splitPos + 1];
                else
                        (*newnode)->keys[i] = lastKey;
        }
        (*newnode)->p[(*newnode)->n] = lastPtr;
        return InsertIt;
}/*End of ins()*/

void display(node *ptr, int blanks) {
        if (ptr) {
                int i;
                for (i = 1; i <= blanks; i++)
                        printf(" ");
                for (i = 0; i < ptr->n; i++)
                        printf("%d ", ptr->keys[i]);
                printf("\n");
                for (i = 0; i <= ptr->n; i++)
                        display(ptr->p[i], blanks + 10);
        }/*End of if*/
}/*End of display()*/

void search(int key) {
        int pos, i, n;
        node *ptr = root;
        printf("Search path:\n");
        while (ptr) {
                n = ptr->n;
                for (i = 0; i < ptr->n; i++)
                        printf(" %d", ptr->keys[i]);
                printf("\n");
                pos = searchPos(key, ptr->keys, n);
                if (pos < n && key == ptr->keys[pos]) {
                        printf("Key %d found in position %d of last dispalyed node\n", key, i);
                        return;
                }
                ptr = ptr->p[pos];
        }
        printf("Key %d is not available\n", key);
}/*End of search()*/

int searchPos(int key, int *key_arr, int n) {
        int pos = 0;
        while (pos < n && key > key_arr[pos])
                pos++;
        return pos;
}/*End of searchPos()*/

void DelNode(int key) {
        node *uproot;
        KeyStatus value;
        value = del(root, key);
        switch (value) {
        case SearchFailure:
                printf("Key %d is not available\n", key);
                break;
        case LessKeys:
                uproot = root;
                root = root->p[0];
                free(uproot);
                break;
        default:
                return;
        }/*End of switch*/
}/*End of delnode()*/

KeyStatus del(node *ptr, int key) {
        int pos, i, pivot, n, min;
        int *key_arr;
        KeyStatus value;
        node **p, *lptr, *rptr;

        if (ptr == NULL)
                return SearchFailure;
        /*Assigns values of node*/
        n = ptr->n;
        key_arr = ptr->keys;
        p = ptr->p;
        min = (M - 1) / 2;/*Minimum number of keys*/

                                          //Search for key to delete
        pos = searchPos(key, key_arr, n);
        // p is a leaf
        if (p[0] == NULL) {
                if (pos == n || key < key_arr[pos])
                        return SearchFailure;
                /*Shift keys and pointers left*/
                for (i = pos + 1; i < n; i++)
                {
                        key_arr[i - 1] = key_arr[i];
                        p[i] = p[i + 1];
                }
                return --ptr->n >= (ptr == root ? 1 : min) ? Success : LessKeys;
        }/*End of if */

         //if found key but p is not a leaf
        if (pos < n && key == key_arr[pos]) {
                node *qp = p[pos], *qp1;
                int nkey;
                while (1) {
                        nkey = qp->n;
                        qp1 = qp->p[nkey];
                        if (qp1 == NULL)
                                break;
                        qp = qp1;
                }/*End of while*/
                key_arr[pos] = qp->keys[nkey - 1];
                qp->keys[nkey - 1] = key;
        }/*End of if */
        value = del(p[pos], key);
        if (value != LessKeys)
                return value;

        if (pos > 0 && p[pos - 1]->n > min) {
                pivot = pos - 1; /*pivot for left and right node*/
                lptr = p[pivot];
                rptr = p[pos];
                /*Assigns values for right node*/
                rptr->p[rptr->n + 1] = rptr->p[rptr->n];
                for (i = rptr->n; i>0; i--) {
                        rptr->keys[i] = rptr->keys[i - 1];
                        rptr->p[i] = rptr->p[i - 1];
                }
                rptr->n++;
                rptr->keys[0] = key_arr[pivot];
                rptr->p[0] = lptr->p[lptr->n];
                key_arr[pivot] = lptr->keys[--lptr->n];
                return Success;
        }/*End of if */
         //if (posn > min)
        if (pos < n && p[pos + 1]->n > min) {
                pivot = pos; /*pivot for left and right node*/
                lptr = p[pivot];
                rptr = p[pivot + 1];
                /*Assigns values for left node*/
                lptr->keys[lptr->n] = key_arr[pivot];
                lptr->p[lptr->n + 1] = rptr->p[0];
                key_arr[pivot] = rptr->keys[0];
                lptr->n++;
                rptr->n--;
                for (i = 0; i < rptr->n; i++) {
                        rptr->keys[i] = rptr->keys[i + 1];
                        rptr->p[i] = rptr->p[i + 1];
                }/*End of for*/
                rptr->p[rptr->n] = rptr->p[rptr->n + 1];
                return Success;
        }/*End of if */

        if (pos == n)
                pivot = pos - 1;
        else
                pivot = pos;

        lptr = p[pivot];
        rptr = p[pivot + 1];
        /*merge right node with left node*/
        lptr->keys[lptr->n] = key_arr[pivot];
        lptr->p[lptr->n + 1] = rptr->p[0];
        for (i = 0; i < rptr->n; i++) {
                lptr->keys[lptr->n + 1 + i] = rptr->keys[i];
                lptr->p[lptr->n + 2 + i] = rptr->p[i + 1];
        }
        lptr->n = lptr->n + rptr->n + 1;
        free(rptr); /*Remove right node*/
        for (i = pos + 1; i < n; i++) {
                key_arr[i - 1] = key_arr[i];
                p[i] = p[i + 1];
        }
        return --ptr->n >= (ptr == root ? 1 : min) ? Success : LessKeys;
}/*End of del()*/

void eatline(void) {
        char c;
        while ((c = getchar()) != '\n');
}

void inorder(node *ptr) {
        if (ptr) {
                if (ptr->n >= 1) {
                        inorder(ptr->p[0]);
                        printf("%d ", ptr->keys[0]);
                        inorder(ptr->p[1]);
                        if (ptr->n == 2) {
                                printf("%d ", ptr->keys[1]);
                                inorder(ptr->p[2]);
                        }
                }
        }
}
int totalKeys(node *ptr) {
        if (ptr) {
                int count = 1;
                if (ptr->n >= 1) {
                        count += totalKeys(ptr->p[0]);
                        count += totalKeys(ptr->p[1]);
                        if (ptr->n == 2) count += totalKeys(ptr->p[2]) + 1;
                }
                return count;
        }
        return 0;
}


void printTotal(node *ptr) {
        printf("%d\n", totalKeys(ptr));
}


int getMin(node *ptr) {
        if (ptr) {
                int min;
                if (ptr->p[0] != NULL) min = getMin(ptr->p[0]);
                else min = ptr->keys[0];
                return min;
        }
        return 0;
}
int getMax(node *ptr) {
        if (ptr) {
                int max;
                if (ptr->n == 1) {
                        if (ptr->p[1] != NULL) max = getMax(ptr->p[1]);
                        else max = ptr->keys[0];
                }
                if (ptr->n == 2) {
                        if (ptr->p[2] != NULL) max = getMax(ptr->p[2]);
                        else max = ptr->keys[1];
                }
                return max;
        }
        return 0;
}


void getMinMax(node *ptr) {
        printf("%d %d\n", getMin(ptr), getMax(ptr));
}


int max(int first, int second, int third) {
        int max = first;
        if (second > max) max = second;
        if (third > max) max = third;
        return max;
}


int maxLevel(node *ptr) {
        if (ptr) {
                int l = 0, mr = 0, r = 0, max_depth;
                if (ptr->p[0] != NULL) l = maxLevel(ptr->p[0]);
                if (ptr->p[1] != NULL) mr = maxLevel(ptr->p[1]);
                if (ptr->n == 2) {
                        if (ptr->p[2] != NULL) r = maxLevel(ptr->p[2]);
                }
                max_depth = max(l, mr, r) + 1;
                return max_depth;
        }
        return 0;
}


void printMaxLevel(node *ptr) {
        int max = maxLevel(ptr) - 1;
        if (max == -1) printf("tree is empty\n");
        else printf("%d\n", max);
}
```
</details>

### Fibonacci heaps

linked list of heap ordered trees.(min heap)
Fibonacci Heap is a collection of trees with min-heap or max-heap property. In Fibonacci Heap, trees can can have any shape even all trees can be single nodes.

#### Structure of fibonacci heaps

Important properties of a Fibonacci heap are:

It is a set of min heap-ordered trees. (i.e. The parent is always smaller than the children.)
A pointer is maintained at the minimum element node.
It consists of a set of marked nodes. (Decrease key operation)
The trees within a Fibonacci heap are unordered but rooted.


#### Mergeable heap operations

Any data structure representing a set of ordered elements that can support the insertion and deletion of elements as well as the set operation of union and the calculation of the minimum elements in a set.

A mergeable heap supports the usual heap operations: Make-Heap() , create an empty heap. Insert(H,x) , insert an element x into the heap H . Min(H) , return the minimum element, or Nil if no such element exists.

#### Decreasing a tree and deleting a node

<details>
<summary>Answer</summary>
	
```
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <math.h>

typedef struct _NODE
{
  int key;
  int degree;
  struct _NODE *left_sibling;
  struct _NODE *right_sibling;
  struct _NODE *parent;
  struct _NODE *child;
  bool mark;
  bool visited;
} NODE;

typedef struct fibanocci_heap
{
  int n;
  NODE *min;
  int phi;
  int degree;
} FIB_HEAP;

FIB_HEAP *make_fib_heap();
void insertion(FIB_HEAP *H, NODE *new, int val);
NODE *extract_min(FIB_HEAP *H);
void consolidate(FIB_HEAP *H);
void fib_heap_link(FIB_HEAP *H, NODE *y, NODE *x);
NODE *find_min_node(FIB_HEAP *H);
void decrease_key(FIB_HEAP *H, NODE *node, int key);
void cut(FIB_HEAP *H, NODE *node_to_be_decrease, NODE *parent_node);
void cascading_cut(FIB_HEAP *H, NODE *parent_node);
void Delete_Node(FIB_HEAP *H, int dec_key);

FIB_HEAP *make_fib_heap()
{
  FIB_HEAP *H;
  H = (FIB_HEAP *)malloc(sizeof(FIB_HEAP));
  H->n = 0;
  H->min = NULL;
  H->phi = 0;
  H->degree = 0;
  return H;
}
void new_print_heap(NODE *n)
{
  NODE *x;
  for (x = n;; x = x->right_sibling)
  {

    if (x->child == NULL)
    {
      printf("node with no child (%d) \n", x->key);
    }
    else
    {

      printf("NODE(%d) with child (%d)\n", x->key, x->child->key);
      new_print_heap(x->child);
    }
    if (x->right_sibling == n)
    {
      break;
    }
  }
}

void insertion(FIB_HEAP *H, NODE *new, int val)
{
  new = (NODE *)malloc(sizeof(NODE));
  new->key = val;
  new->degree = 0;
  new->mark = false;
  new->parent = NULL;
  new->child = NULL;
  new->visited = false;
  new->left_sibling = new;
  new->right_sibling = new;
  if (H->min == NULL)
  {
    H->min = new;
  }
  else
  {
    H->min->left_sibling->right_sibling = new;
    new->right_sibling = H->min;
    new->left_sibling = H->min->left_sibling;
    H->min->left_sibling = new;
    if (new->key < H->min->key)
    {
      H->min = new;
    }
  }
  (H->n)++;
}

NODE *find_min_node(FIB_HEAP *H)
{
  if (H == NULL)
  {
    printf(" \n Fibonacci heap not yet created \n");
    return NULL;
  }
  else
    return H->min;
}

FIB_HEAP *unionHeap(FIB_HEAP *H1, FIB_HEAP *H2)
{
  FIB_HEAP *Hnew;
  Hnew = make_fib_heap();
  Hnew->min = H1->min;

  NODE *temp1, *temp2;
  temp1 = Hnew->min->right_sibling;
  temp2 = H2->min->left_sibling;

  Hnew->min->right_sibling->left_sibling = H2->min->left_sibling;
  Hnew->min->right_sibling = H2->min;
  H2->min->left_sibling = Hnew->min;
  temp2->right_sibling = temp1;

  if ((H1->min == NULL) || (H2->min != NULL && H2->min->key < H1->min->key))
    Hnew->min = H2->min;
  Hnew->n = H1->n + H2->n;
  return Hnew;
}

int cal_degree(int n)
{
  int count = 0;
  while (n > 0)
  {
    n = n / 2;
    count++;
  }
  return count;
}
void consolidate(FIB_HEAP *H)
{
  int degree, i, d;
  degree = cal_degree(H->n);
  NODE *A[degree], *x, *y, *z;
  for (i = 0; i <= degree; i++)
  {
    A[i] = NULL;
  }
  x = H->min;
  do
  {
    d = x->degree;
    while (A[d] != NULL)
    {
      y = A[d];
      if (x->key > y->key)
      {
        NODE *exchange_help;
        exchange_help = x;
        x = y;
        y = exchange_help;
      }
      if (y == H->min)
        H->min = x;
      fib_heap_link(H, y, x);
      if (y->right_sibling == x)
        H->min = x;
      A[d] = NULL;
      d++;
    }
    A[d] = x;
    x = x->right_sibling;
  } while (x != H->min);

  H->min = NULL;
  for (i = 0; i < degree; i++)
  {
    if (A[i] != NULL)
    {
      A[i]->left_sibling = A[i];
      A[i]->right_sibling = A[i];
      if (H->min == NULL)
      {
        H->min = A[i];
      }
      else
      {
        H->min->left_sibling->right_sibling = A[i];
        A[i]->right_sibling = H->min;
        A[i]->left_sibling = H->min->left_sibling;
        H->min->left_sibling = A[i];
        if (A[i]->key < H->min->key)
        {
          H->min = A[i];
        }
      }
      if (H->min == NULL)
      {
        H->min = A[i];
      }
      else if (A[i]->key < H->min->key)
      {
        H->min = A[i];
      }
    }
  }
}

void fib_heap_link(FIB_HEAP *H, NODE *y, NODE *x)
{
  y->right_sibling->left_sibling = y->left_sibling;
  y->left_sibling->right_sibling = y->right_sibling;

  if (x->right_sibling == x)
    H->min = x;

  y->left_sibling = y;
  y->right_sibling = y;
  y->parent = x;

  if (x->child == NULL)
  {
    x->child = y;
  }
  y->right_sibling = x->child;
  y->left_sibling = x->child->left_sibling;
  x->child->left_sibling->right_sibling = y;
  x->child->left_sibling = y;
  if ((y->key) < (x->child->key))
    x->child = y;

  (x->degree)++;
}
NODE *extract_min(FIB_HEAP *H)
{

  if (H->min == NULL)
    printf("\n The heap is empty");
  else
  {
    NODE *temp = H->min;
    NODE *pntr;
    pntr = temp;
    NODE *x = NULL;
    if (temp->child != NULL)
    {

      x = temp->child;
      do
      {
        pntr = x->right_sibling;
        (H->min->left_sibling)->right_sibling = x;
        x->right_sibling = H->min;
        x->left_sibling = H->min->left_sibling;
        H->min->left_sibling = x;
        if (x->key < H->min->key)
          H->min = x;
        x->parent = NULL;
        x = pntr;
      } while (pntr != temp->child);
    }

    (temp->left_sibling)->right_sibling = temp->right_sibling;
    (temp->right_sibling)->left_sibling = temp->left_sibling;
    H->min = temp->right_sibling;

    if (temp == temp->right_sibling && temp->child == NULL)
      H->min = NULL;
    else
    {
      H->min = temp->right_sibling;
      consolidate(H);
    }
    H->n = H->n - 1;
    return temp;
  }
  return H->min;
}

void cut(FIB_HEAP *H, NODE *node_to_be_decrease, NODE *parent_node)
{
  NODE *temp_parent_check;

  if (node_to_be_decrease == node_to_be_decrease->right_sibling)
    parent_node->child = NULL;

  node_to_be_decrease->left_sibling->right_sibling = node_to_be_decrease->right_sibling;
  node_to_be_decrease->right_sibling->left_sibling = node_to_be_decrease->left_sibling;
  if (node_to_be_decrease == parent_node->child)
    parent_node->child = node_to_be_decrease->right_sibling;
  (parent_node->degree)--;

  node_to_be_decrease->left_sibling = node_to_be_decrease;
  node_to_be_decrease->right_sibling = node_to_be_decrease;
  H->min->left_sibling->right_sibling = node_to_be_decrease;
  node_to_be_decrease->right_sibling = H->min;
  node_to_be_decrease->left_sibling = H->min->left_sibling;
  H->min->left_sibling = node_to_be_decrease;

  node_to_be_decrease->parent = NULL;
  node_to_be_decrease->mark = false;
}

void cascading_cut(FIB_HEAP *H, NODE *parent_node)
{
  NODE *aux;
  aux = parent_node->parent;
  if (aux != NULL)
  {
    if (parent_node->mark == false)
    {
      parent_node->mark = true;
    }
    else
    {
      cut(H, parent_node, aux);
      cascading_cut(H, aux);
    }
  }
}

void decrease_key(FIB_HEAP *H, NODE *node_to_be_decrease, int new_key)
{
  NODE *parent_node;
  if (H == NULL)
  {
    printf("\n FIbonacci heap not created ");
    return;
  }
  if (node_to_be_decrease == NULL)
  {
    printf("Node is not in the heap");
  }

  else
  {
    if (node_to_be_decrease->key < new_key)
    {
      printf("\n Invalid new key for decrease key operation \n ");
    }
    else
    {
      node_to_be_decrease->key = new_key;
      parent_node = node_to_be_decrease->parent;
      if ((parent_node != NULL) && (node_to_be_decrease->key < parent_node->key))
      {
        printf("\n cut called");
        cut(H, node_to_be_decrease, parent_node);
        printf("\n cascading cut called");
        cascading_cut(H, parent_node);
      }
      if (node_to_be_decrease->key < H->min->key)
      {
        H->min = node_to_be_decrease;
      }
    }
  }
}

void *find_node(FIB_HEAP *H, NODE *n, int key, int new_key)
{
  NODE *find_use = n;
  NODE *f = NULL;
  find_use->visited = true;
  if (find_use->key == key)
  {
    find_use->visited = false;
    f = find_use;
    decrease_key(H, f, new_key);
  }
  if (find_use->child != NULL)
  {
    find_node(H, find_use->child, key, new_key);
  }
  if ((find_use->right_sibling->visited != true))
  {
    find_node(H, find_use->right_sibling, key, new_key);
  }

  find_use->visited = false;
}

FIB_HEAP *insertion_procedure()
{
  FIB_HEAP *temp;
  int no_of_nodes, ele, i;
  NODE *new_node;
  temp = (FIB_HEAP *)malloc(sizeof(FIB_HEAP));
  temp = NULL;
  if (temp == NULL)
  {
    temp = make_fib_heap();
  }
  printf(" \n enter number of nodes to be insert = ");
  scanf("%d", &no_of_nodes);
  for (i = 1; i <= no_of_nodes; i++)
  {
    printf("\n node %d and its key value = ", i);
    scanf("%d", &ele);
    insertion(temp, new_node, ele);
  }
  return temp;
}
void Delete_Node(FIB_HEAP *H, int dec_key)
{
  NODE *p = NULL;
  find_node(H, H->min, dec_key, -5000);
  p = extract_min(H);
  if (p != NULL)
    printf("\n Node deleted");
  else
    printf("\n Node not deleted:some error");
}

int main(int argc, char **argv)
{
  NODE *new_node, *min_node, *extracted_min, *node_to_be_decrease, *find_use;
  FIB_HEAP *heap, *h1, *h2;
  int operation_no, new_key, dec_key, ele, i, no_of_nodes;
  heap = (FIB_HEAP *)malloc(sizeof(FIB_HEAP));
  heap = NULL;
  while (1)
  {

    printf(" \n choose below operations \n 1. Create Fibonacci heap \n 2. Insert nodes into fibonacci heap \n 3. Find min \n 4. Union \n 5. Extract min \n 6. Decrease key \n 7.Delete node \n 8. print heap \n 9. exit \n enter operation_no = ");
    scanf("%d", &operation_no);

    switch (operation_no)
    {
    case 1:
      heap = make_fib_heap();
      break;

    case 2:
      if (heap == NULL)
      {
        heap = make_fib_heap();
      }
      printf(" enter number of nodes to be insert = ");
      scanf("%d", &no_of_nodes);
      for (i = 1; i <= no_of_nodes; i++)
      {
        printf("\n node %d and its key value = ", i);
        scanf("%d", &ele);
        insertion(heap, new_node, ele);
      }
      break;

    case 3:
      min_node = find_min_node(heap);
      if (min_node == NULL)
        printf("No minimum value");
      else
        printf("\n min value = %d", min_node->key);
      break;

    case 4:
      if (heap == NULL)
      {
        printf("\n no FIbonacci heap is created please create fibonacci heap \n ");
        break;
      }
      h1 = insertion_procedure();
      heap = unionHeap(heap, h1);
      printf("Unified Heap:\n");
      new_print_heap(heap->min);
      break;

    case 5:
      if (heap == NULL)
        printf("Fibonacci heap is empty");
      else
      {
        extracted_min = extract_min(heap);
        printf("\n min value = %d", extracted_min->key);
        printf("\n Updated heap: \n");
        new_print_heap(heap->min);
      }
      break;

    case 6:
      if (heap == NULL)
        printf("Fibonacci heap is empty");
      else
      {
        printf(" \n node to be decreased = ");
        scanf("%d", &dec_key);
        printf(" \n enter the new key = ");
        scanf("%d", &new_key);
        find_use = heap->min;
        find_node(heap, find_use, dec_key, new_key);
        printf("\n Key decreased- Corresponding heap:\n");
        new_print_heap(heap->min);
      }
      break;
    case 7:
      if (heap == NULL)
        printf("Fibonacci heap is empty");
      else
      {
        printf(" \n Enter node key to be deleted = ");
        scanf("%d", &dec_key);
        Delete_Node(heap, dec_key);
        printf("\n Node Deleted- Corresponding heap:\n");
        new_print_heap(heap->min);
        break;
      }
    case 8:
      new_print_heap(heap->min);
      break;

    case 9:
      free(new_node);
      free(heap);
      exit(0);

    default:
      printf("Invalid choice ");
    }
  }
}

```

</details>


#### Bounding the maximum degree

To prove that the amortized time of FIB-HEAP-EXTRACT-MIN and FIB-HEAP-DELETE is O(lg n), we must show that the upper bound D(n) on the degree of any node of an n-node Fibonacci heap is O(lg n). By Exercise 20.2-3, when all trees in the Fibonacci heap are unordered binomial trees, D(n) = ⌊lg n⌋. The cuts that occur in FIB-HEAP-DECREASE-KEY, however, may cause trees within the Fibonacci heap to violate the unordered binomial tree properties. In this section, we shall show that because we cut a node from its parent as soon as it loses two children, D(n) is O(lg n). In particular, we shall show that D(n) ≤ ⌊logφn⌋, where .

The key to the analysis is as follows. For each node x within a Fibonacci heap, define size(x) to be the number of nodes, including x itself, in the subtree rooted at x. (Note that x need not be in the root list-it can be any node at all.) We shall show that size(x) is exponential in degree[x]. Bear in mind that degree[x] is always maintained as an accurate count of the degree of x.


#### Code in c
 
 <details>
<summary>Answer</summary>
 
```
 
 
#include <math.h>
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>

typedef struct _NODE {
  int key;
  int degree;
  struct _NODE *left_sibling;
  struct _NODE *right_sibling;
  struct _NODE *parent;
  struct _NODE *child;
  bool mark;
  bool visited;
} NODE;

typedef struct fibanocci_heap {
  int n;
  NODE *min;
  int phi;
  int degree;
} FIB_HEAP;

FIB_HEAP *make_fib_heap();
void insertion(FIB_HEAP *H, NODE *new, int val);
NODE *extract_min(FIB_HEAP *H);
void consolidate(FIB_HEAP *H);
void fib_heap_link(FIB_HEAP *H, NODE *y, NODE *x);
NODE *find_min_node(FIB_HEAP *H);
void decrease_key(FIB_HEAP *H, NODE *node, int key);
void cut(FIB_HEAP *H, NODE *node_to_be_decrease, NODE *parent_node);
void cascading_cut(FIB_HEAP *H, NODE *parent_node);
void Delete_Node(FIB_HEAP *H, int dec_key);

FIB_HEAP *make_fib_heap() {
  FIB_HEAP *H;
  H = (FIB_HEAP *)malloc(sizeof(FIB_HEAP));
  H->n = 0;
  H->min = NULL;
  H->phi = 0;
  H->degree = 0;
  return H;
}

// Printing the heap
void print_heap(NODE *n) {
  NODE *x;
  for (x = n;; x = x->right_sibling) {
    if (x->child == NULL) {
      printf("node with no child (%d) \n", x->key);
    } else {
      printf("NODE(%d) with child (%d)\n", x->key, x->child->key);
      print_heap(x->child);
    }
    if (x->right_sibling == n) {
      break;
    }
  }
}

// Inserting nodes
void insertion(FIB_HEAP *H, NODE *new, int val) {
  new = (NODE *)malloc(sizeof(NODE));
  new->key = val;
  new->degree = 0;
  new->mark = false;
  new->parent = NULL;
  new->child = NULL;
  new->visited = false;
  new->left_sibling = new;
  new->right_sibling = new;
  if (H->min == NULL) {
    H->min = new;
  } else {
    H->min->left_sibling->right_sibling = new;
    new->right_sibling = H->min;
    new->left_sibling = H->min->left_sibling;
    H->min->left_sibling = new;
    if (new->key < H->min->key) {
      H->min = new;
    }
  }
  (H->n)++;
}

// Find min node
NODE *find_min_node(FIB_HEAP *H) {
  if (H == NULL) {
    printf(" \n Fibonacci heap not yet created \n");
    return NULL;
  } else
    return H->min;
}

// Union operation
FIB_HEAP *unionHeap(FIB_HEAP *H1, FIB_HEAP *H2) {
  FIB_HEAP *Hnew;
  Hnew = make_fib_heap();
  Hnew->min = H1->min;

  NODE *temp1, *temp2;
  temp1 = Hnew->min->right_sibling;
  temp2 = H2->min->left_sibling;

  Hnew->min->right_sibling->left_sibling = H2->min->left_sibling;
  Hnew->min->right_sibling = H2->min;
  H2->min->left_sibling = Hnew->min;
  temp2->right_sibling = temp1;

  if ((H1->min == NULL) || (H2->min != NULL && H2->min->key < H1->min->key))
    Hnew->min = H2->min;
  Hnew->n = H1->n + H2->n;
  return Hnew;
}

// Calculate the degree
int cal_degree(int n) {
  int count = 0;
  while (n > 0) {
    n = n / 2;
    count++;
  }
  return count;
}

// Consolidate function
void consolidate(FIB_HEAP *H) {
  int degree, i, d;
  degree = cal_degree(H->n);
  NODE *A[degree], *x, *y, *z;
  for (i = 0; i <= degree; i++) {
    A[i] = NULL;
  }
  x = H->min;
  do {
    d = x->degree;
    while (A[d] != NULL) {
      y = A[d];
      if (x->key > y->key) {
        NODE *exchange_help;
        exchange_help = x;
        x = y;
        y = exchange_help;
      }
      if (y == H->min)
        H->min = x;
      fib_heap_link(H, y, x);
      if (y->right_sibling == x)
        H->min = x;
      A[d] = NULL;
      d++;
    }
    A[d] = x;
    x = x->right_sibling;
  } while (x != H->min);

  H->min = NULL;
  for (i = 0; i < degree; i++) {
    if (A[i] != NULL) {
      A[i]->left_sibling = A[i];
      A[i]->right_sibling = A[i];
      if (H->min == NULL) {
        H->min = A[i];
      } else {
        H->min->left_sibling->right_sibling = A[i];
        A[i]->right_sibling = H->min;
        A[i]->left_sibling = H->min->left_sibling;
        H->min->left_sibling = A[i];
        if (A[i]->key < H->min->key) {
          H->min = A[i];
        }
      }
      if (H->min == NULL) {
        H->min = A[i];
      } else if (A[i]->key < H->min->key) {
        H->min = A[i];
      }
    }
  }
}

// Linking
void fib_heap_link(FIB_HEAP *H, NODE *y, NODE *x) {
  y->right_sibling->left_sibling = y->left_sibling;
  y->left_sibling->right_sibling = y->right_sibling;

  if (x->right_sibling == x)
    H->min = x;

  y->left_sibling = y;
  y->right_sibling = y;
  y->parent = x;

  if (x->child == NULL) {
    x->child = y;
  }
  y->right_sibling = x->child;
  y->left_sibling = x->child->left_sibling;
  x->child->left_sibling->right_sibling = y;
  x->child->left_sibling = y;
  if ((y->key) < (x->child->key))
    x->child = y;

  (x->degree)++;
}

// Extract min
NODE *extract_min(FIB_HEAP *H) {
  if (H->min == NULL)
    printf("\n The heap is empty");
  else {
    NODE *temp = H->min;
    NODE *pntr;
    pntr = temp;
    NODE *x = NULL;
    if (temp->child != NULL) {
      x = temp->child;
      do {
        pntr = x->right_sibling;
        (H->min->left_sibling)->right_sibling = x;
        x->right_sibling = H->min;
        x->left_sibling = H->min->left_sibling;
        H->min->left_sibling = x;
        if (x->key < H->min->key)
          H->min = x;
        x->parent = NULL;
        x = pntr;
      } while (pntr != temp->child);
    }

    (temp->left_sibling)->right_sibling = temp->right_sibling;
    (temp->right_sibling)->left_sibling = temp->left_sibling;
    H->min = temp->right_sibling;

    if (temp == temp->right_sibling && temp->child == NULL)
      H->min = NULL;
    else {
      H->min = temp->right_sibling;
      consolidate(H);
    }
    H->n = H->n - 1;
    return temp;
  }
  return H->min;
}

void cut(FIB_HEAP *H, NODE *node_to_be_decrease, NODE *parent_node) {
  NODE *temp_parent_check;

  if (node_to_be_decrease == node_to_be_decrease->right_sibling)
    parent_node->child = NULL;

  node_to_be_decrease->left_sibling->right_sibling = node_to_be_decrease->right_sibling;
  node_to_be_decrease->right_sibling->left_sibling = node_to_be_decrease->left_sibling;
  if (node_to_be_decrease == parent_node->child)
    parent_node->child = node_to_be_decrease->right_sibling;
  (parent_node->degree)--;

  node_to_be_decrease->left_sibling = node_to_be_decrease;
  node_to_be_decrease->right_sibling = node_to_be_decrease;
  H->min->left_sibling->right_sibling = node_to_be_decrease;
  node_to_be_decrease->right_sibling = H->min;
  node_to_be_decrease->left_sibling = H->min->left_sibling;
  H->min->left_sibling = node_to_be_decrease;

  node_to_be_decrease->parent = NULL;
  node_to_be_decrease->mark = false;
}

void cascading_cut(FIB_HEAP *H, NODE *parent_node) {
  NODE *aux;
  aux = parent_node->parent;
  if (aux != NULL) {
    if (parent_node->mark == false) {
      parent_node->mark = true;
    } else {
      cut(H, parent_node, aux);
      cascading_cut(H, aux);
    }
  }
}

void decrease_key(FIB_HEAP *H, NODE *node_to_be_decrease, int new_key) {
  NODE *parent_node;
  if (H == NULL) {
    printf("\n FIbonacci heap not created ");
    return;
  }
  if (node_to_be_decrease == NULL) {
    printf("Node is not in the heap");
  }

  else {
    if (node_to_be_decrease->key < new_key) {
      printf("\n Invalid new key for decrease key operation \n ");
    } else {
      node_to_be_decrease->key = new_key;
      parent_node = node_to_be_decrease->parent;
      if ((parent_node != NULL) && (node_to_be_decrease->key < parent_node->key)) {
        printf("\n cut called");
        cut(H, node_to_be_decrease, parent_node);
        printf("\n cascading cut called");
        cascading_cut(H, parent_node);
      }
      if (node_to_be_decrease->key < H->min->key) {
        H->min = node_to_be_decrease;
      }
    }
  }
}

void *find_node(FIB_HEAP *H, NODE *n, int key, int new_key) {
  NODE *find_use = n;
  NODE *f = NULL;
  find_use->visited = true;
  if (find_use->key == key) {
    find_use->visited = false;
    f = find_use;
    decrease_key(H, f, new_key);
  }
  if (find_use->child != NULL) {
    find_node(H, find_use->child, key, new_key);
  }
  if ((find_use->right_sibling->visited != true)) {
    find_node(H, find_use->right_sibling, key, new_key);
  }

  find_use->visited = false;
}

FIB_HEAP *insertion_procedure() {
  FIB_HEAP *temp;
  int no_of_nodes, ele, i;
  NODE *new_node;
  temp = (FIB_HEAP *)malloc(sizeof(FIB_HEAP));
  temp = NULL;
  if (temp == NULL) {
    temp = make_fib_heap();
  }
  printf(" \n enter number of nodes to be insert = ");
  scanf("%d", &no_of_nodes);
  for (i = 1; i <= no_of_nodes; i++) {
    printf("\n node %d and its key value = ", i);
    scanf("%d", &ele);
    insertion(temp, new_node, ele);
  }
  return temp;
}
void Delete_Node(FIB_HEAP *H, int dec_key) {
  NODE *p = NULL;
  find_node(H, H->min, dec_key, -5000);
  p = extract_min(H);
  if (p != NULL)
    printf("\n Node deleted");
  else
    printf("\n Node not deleted:some error");
}

int main(int argc, char **argv) {
  NODE *new_node, *min_node, *extracted_min, *node_to_be_decrease, *find_use;
  FIB_HEAP *heap, *h1, *h2;
  int operation_no, new_key, dec_key, ele, i, no_of_nodes;
  heap = (FIB_HEAP *)malloc(sizeof(FIB_HEAP));
  heap = NULL;
  while (1) {
    printf(" \n Operations \n 1. Create Fibonacci heap \n 2. Insert nodes into fibonacci heap \n 3. Find min \n 4. Union \n 5. Extract min \n 6. Decrease key \n 7.Delete node \n 8. print heap \n 9. exit \n enter operation_no = ");
    scanf("%d", &operation_no);

    switch (operation_no) {
      case 1:
        heap = make_fib_heap();
        break;

      case 2:
        if (heap == NULL) {
          heap = make_fib_heap();
        }
        printf(" enter number of nodes to be insert = ");
        scanf("%d", &no_of_nodes);
        for (i = 1; i <= no_of_nodes; i++) {
          printf("\n node %d and its key value = ", i);
          scanf("%d", &ele);
          insertion(heap, new_node, ele);
        }
        break;

      case 3:
        min_node = find_min_node(heap);
        if (min_node == NULL)
          printf("No minimum value");
        else
          printf("\n min value = %d", min_node->key);
        break;

      case 4:
        if (heap == NULL) {
          printf("\n no FIbonacci heap created \n ");
          break;
        }
        h1 = insertion_procedure();
        heap = unionHeap(heap, h1);
        printf("Unified Heap:\n");
        print_heap(heap->min);
        break;

      case 5:
        if (heap == NULL)
          printf("Empty Fibonacci heap");
        else {
          extracted_min = extract_min(heap);
          printf("\n min value = %d", extracted_min->key);
          printf("\n Updated heap: \n");
          print_heap(heap->min);
        }
        break;

      case 6:
        if (heap == NULL)
          printf("Fibonacci heap is empty");
        else {
          printf(" \n node to be decreased = ");
          scanf("%d", &dec_key);
          printf(" \n enter the new key = ");
          scanf("%d", &new_key);
          find_use = heap->min;
          find_node(heap, find_use, dec_key, new_key);
          printf("\n Key decreased- Corresponding heap:\n");
          print_heap(heap->min);
        }
        break;
      case 7:
        if (heap == NULL)
          printf("Fibonacci heap is empty");
        else {
          printf(" \n Enter node key to be deleted = ");
          scanf("%d", &dec_key);
          Delete_Node(heap, dec_key);
          printf("\n Node Deleted- Corresponding heap:\n");
          print_heap(heap->min);
          break;
        }
      case 8:
        print_heap(heap->min);
        break;

      case 9:
        free(new_node);
        free(heap);
        exit(0);

      default:
        printf("Invalid choice ");
    }
  }
}
```
</details>

### Van Emde Boas trees

Van Emde Boas tree (or Van Emde Boas priority queue or vEB tree) is a tree data structure which implements 
an associative array with m-bit integer keys. 
It performs all operations  in O(log log M) time, 
where M is the maximum number of elements that can be stored in the tree.


#### Preliminary approaches

#### A recursive structure

Van Emde Boas Tree is a recursively defined structure.

u: Number of keys present in the VEB Tree.
Minimum: Contains the minimum key present in the VEB Tree.
Maximum: Contains the maximum key present in the VEB Tree.
Summary: Points to new VEB(\sqrt{u}) Tree which contains overview of keys present in clusters array.
Clusters: An array of size \sqrt{u} each place in the array points to new VEB(\sqrt{u}) Tree.

#### The Van Emde Boas trees

Van Emde Boas Tree supports search, successor, predecessor, insert and delete operations in O(lglgN) time which is faster than any of related data structures like priority queue, binary search tree, etc. Van Emde Boas Tree works with O(1) time-complexity for minimum and maximum query. Here N is the size of the universe over which tree is defined and lg is log base 2.

Note: Van Emde Boas Data Structure’s key set must be defined over a range of 0 to n(n is positive integer of the form 2k) and it works when duplicate keys are not allowed.

Abbreviations:

VEB is an abbreviation of Van Emde Boas tree.
VEB(\sqrt{u}) is an abbreviation for VEB containing u number of keys.

#### Code in cpp
<details>
<summary>Answer</summary>

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
  
class Van_Emde_Boas {
  
public:
    int universe_size;
    int minimum;
    int maximum;
    Van_Emde_Boas* summary;
    vector<Van_Emde_Boas*> clusters;
  
    // Function to return cluster numbers
    // in which key is present
    int high(int x)
    {
        int div = ceil(sqrt(universe_size));
        return x / div;
    }
  
    // Function to return position of x in cluster
    int low(int x)
    {
        int mod = ceil(sqrt(universe_size));
        return x % mod;
    }
  
    // Function to return the index from
    // cluster number and position
    int generate_index(int x, int y)
    {
        int ru = ceil(sqrt(universe_size));
        return x * ru + y;
    }
  
    // Constructor
    Van_Emde_Boas(int size)
    {
        universe_size = size;
        minimum = -1;
        maximum = -1;
  
        // Base case
        if (size <= 2) {
            summary = nullptr;
            clusters = vector<Van_Emde_Boas*>(0, nullptr);
        }
        else {
            int no_clusters = ceil(sqrt(size));
  
            // Assigning VEB(sqrt(u)) to summary
            summary = new Van_Emde_Boas(no_clusters);
  
            // Creating array of VEB Tree pointers of size sqrt(u)
            clusters = vector<Van_Emde_Boas*>(no_clusters, nullptr);
  
            // Assigning VEB(sqrt(u)) to all of its clusters
            for (int i = 0; i < no_clusters; i++) {
                clusters[i] = new Van_Emde_Boas(ceil(sqrt(size)));
            }
        }
    }
};
  
// Driver code
int main()
{
    // New Van_Emde_Boas tree with u = 16
    Van_Emde_Boas* akp = new Van_Emde_Boas(4);
}

```
</details>


### Data structures for disjoint set

#### Disjoint set operation

Consider a situation with a number of persons and following tasks to be performed on them.

Add a new friendship relation, i.e., a person x becomes friend of another person y.
Find whether individual x is a friend of individual y (direct or indirect friend)
Example:

We are given 10 individuals say,
a, b, c, d, e, f, g, h, i, j

Following are relationships to be added.
a <-> b  
b <-> d
c <-> f
c <-> i
j <-> e
g <-> j

And given queries like whether a is a friend of d
or not.

We basically need to create following 4 groups
and maintain a quickly accessible connection
among group items:
G1 = {a, b, d}
G2 = {c, f, i}
G3 = {e, g, j}
G4 = {h}

#### Linked list representation of disjoint sets

<details>
<summary>Answer</summary>

```
// C++ program for implementation of disjoint
// set data structure using linked list
#include <bits/stdc++.h>
using namespace std;
  
// to represent linked list which is a set
struct Item;
  
// to represent Node of linked list. Every
// node has a pointer to representative
struct Node
{
    int val;
    Node *next;
    Item *itemPtr;
};
  
// A list has a pointer to head and tail
struct Item
{
    Node *hd, *tl;
};
  
// To represent union set
class ListSet
{
private:
  
    // Hash to store addresses of set representatives
    // for given values. It is made global for ease of
    // implementation. And second part of hash is actually
    // address of Nodes. We typecast addresses to long
    // before storing them.
    unordered_map<int, Node *> nodeAddress;
  
public:
    void makeset(int a);
    Item* find(int key);
    void Union(Item *i1, Item *i2);
};
  
// To make a set with one object
// with its representative
void ListSet::makeset(int a)
{
    // Create a new Set
    Item *newSet = new Item;
  
    // Create a new linked list node
    // to store given key
    newSet->hd = new Node;
  
    // Initialize head and tail
    newSet->tl = newSet->hd;
    nodeAddress[a] = newSet->hd;
  
    // Create a new set
    newSet->hd->val = a;
    newSet->hd->itemPtr = newSet;
    newSet->hd->next = NULL;
}
  
// To find representative address of a
// key
Item *ListSet::find(int key)
{
    Node *ptr = nodeAddress[key];
    return (ptr->itemPtr);
}
  
// union function for joining two subsets
// of a universe.  Mergese set2 into set1
// and deletes set1.
void ListSet::Union(Item *set1, Item *set2)
{
    Node *cur = set2->hd;
    while (cur != 0)
    {
        cur->itemPtr = set1;
        cur = cur->next;
    }
  
    // Join the tail of the set to head
    // of the input set
    (set1->tl)->next = set2->hd;
    set1->tl = set2->tl;
  
    delete set2;
}
  
// Driver code
int main()
{
    ListSet a;
    a.makeset(13);  //a new set is made with one object only
    a.makeset(25);
    a.makeset(45);
    a.makeset(65);
  
    cout << "find(13): " << a.find(13) << endl;
    cout << "find(25): "
         << a.find(25) << endl;
    cout << "find(65): "
         << a.find(65) << endl;
    cout << "find(45): "
         << a.find(45) << endl << endl;
    cout << "Union(find(65), find(45)) \n";
  
    a.Union(a.find(65), a.find(45));
  
    cout << "find(65]): "
         << a.find(65) << endl;
    cout << "find(45]): "
         << a.find(45) << endl;
    return 0;
}

```
</details>

#### Disjoint set forests

In a faster implementation of disjoint sets, we represent sets by rooted trees, with each node containing one member and each tree representing one set. In a disjoint-set forest, illustrated in Figure 21.4(a), each member points only to its parent. The root of each tree contains the representative and is its own parent. As we shall see, although the straightforward algorithms that use this representation are no faster than ones that use the linked-list representation, by introducing two heuristics-"union by rank" and "path compression"-we can achieve the asymptotically fastest disjoint-set data structure known.



#### Analysis of union by rank compression

Union by Rank: First of all, we need a new array of integers called rank[]. Size of this array is same as the parent array. If i is a representative of a set, rank[i] is the height of the tree representing the set.
Now recall that, in the Union operation, it doesn’t matter which of the two trees is moved under the other (see last two image examples above). Now what we want to do is minimize the height of the resulting tree. If we are uniting two trees (or sets), let’s call them left and right, then it all depends on the rank of left and the rank of right.

If the rank of left is less than the rank of right, then it’s best to move left under right, because that won’t change the rank of right (while moving right under left would increase the height). In the same way, if the rank of right is less than the rank of left, then we should move right under left.
If the ranks are equal, it doesn’t matter which tree goes under the other, but the rank of the result will always be one greater than the rank of the trees.
// Unites the set that includes i and the set 
// that includes j
void union(int i, int j) 
{
    // Find the representatives (or the root nodes) 
    // for the set that includes i
    int irep = this.find(i);

    // And do the same for the set that includes j
    int jrep = this.Find(j);

    // Elements are in same set, no need to 
    // unite anything.    
    if (irep == jrep)
        return;

    // Get the rank of i’s tree
    irank = Rank[irep],

    // Get the rank of j’s tree
    jrank = Rank[jrep];

    // If i’s rank is less than j’s rank
    if (irank < jrank) 
    {
        // Then move i under j
        this.parent[irep] = jrep;
    } 

    // Else if j’s rank is less than i’s rank
    else if (jrank < irank) 
    {
        // Then move j under i
        this.Parent[jrep] = irep;
    } 

    // Else if their ranks are the same
    else
    {

        // Then move i under j (doesn’t matter
        // which one goes where)
        this.Parent[irep] = jrep;

        // And increment the result tree’s 
        // rank by 1
        Rank[jrep]++;
    }
}

#### Code in cpp
<details>
<summary>Answer</summary>
 

```
// C++ implementation of disjoint set
#include <iostream>
using namespace std;
class DisjSet {
    int *rank, *parent, n;
  
public:
    // Constructor to create and
    // initialize sets of n items
    DisjSet(int n)
    {
        rank = new int[n];
        parent = new int[n];
        this->n = n;
        makeSet();
    }
  
    // Creates n single item sets
    void makeSet()
    {
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
  
    // Finds set of given item x
    int find(int x)
    {
        // Finds the representative of the set
        // that x is an element of
        if (parent[x] != x) {
  
            // if x is not the parent of itself
            // Then x is not the representative of
            // his set,
            parent[x] = find(parent[x]);
  
            // so we recursively call Find on its parent
            // and move i's node directly under the
            // representative of this set
        }
  
        return parent[x];
    }
  
    // Do union of two sets represented
    // by x and y.
    void Union(int x, int y)
    {
        // Find current sets of x and y
        int xset = find(x);
        int yset = find(y);
  
        // If they are already in same set
        if (xset == yset)
            return;
  
        // Put smaller ranked item under
        // bigger ranked item if ranks are
        // different
        if (rank[xset] < rank[yset]) {
            parent[xset] = yset;
        }
        else if (rank[xset] > rank[yset]) {
            parent[yset] = xset;
        }
  
        // If ranks are same, then increment
        // rank.
        else {
            parent[yset] = xset;
            rank[xset] = rank[xset] + 1;
        }
    }
};
  
int main()
{
    DisjSet obj(5);
    obj.Union(0, 2);
    obj.Union(4, 2);
    obj.Union(3, 1);
    if (obj.find(4) == obj.find(0))
        cout << "Yes\n";
    else
        cout << "No\n";
    if (obj.find(1) == obj.find(0))
        cout << "Yes\n";
    else
        cout << "No\n";
  
    return 0;
}
```
</details>


## Graph algorithm

In computational complexity theory, the potential method is a method used to analyze the amortized time and space complexity of a data structure, a measure of its performance over sequences of operations that smooths out the cost of infrequent but expensive operations.

### Elementary  graph algorithm

#### Representations of graph

In graph theory, a graph representation is a technique to store graph into the memory of computer.

To represent a graph, we just need the set of vertices, and for each vertex the neighbors of the vertex (vertices which is directly connected to it by an edge). If it is a weighted graph, then the weight will be associated with each edge.

There are different ways to optimally represent a graph, depending on the density of its edges, type of operations to be performed and ease of use.



#### Breadth first search

first we will visit the vertex,explore it and then MOVE ON to another vertex then explore it.
(level order on a binary tree.)
 
 #### Code in c
  
 <details>
<summary>Answer</summary>
 
```
 
 #include <stdio.h>
#include <stdlib.h>
#define SIZE 40

struct queue {
  int items[SIZE];
  int front;
  int rear;
};

struct queue* createQueue();
void enqueue(struct queue* q, int);
int dequeue(struct queue* q);
void display(struct queue* q);
int isEmpty(struct queue* q);
void printQueue(struct queue* q);

struct node {
  int vertex;
  struct node* next;
};

struct node* createNode(int);

struct Graph {
  int numVertices;
  struct node** adjLists;
  int* visited;
};

// BFS algorithm
void bfs(struct Graph* graph, int startVertex) {
  struct queue* q = createQueue();

  graph->visited[startVertex] = 1;
  enqueue(q, startVertex);

  while (!isEmpty(q)) {
    printQueue(q);
    int currentVertex = dequeue(q);
    printf("Visited %d\n", currentVertex);

    struct node* temp = graph->adjLists[currentVertex];

    while (temp) {
      int adjVertex = temp->vertex;

      if (graph->visited[adjVertex] == 0) {
        graph->visited[adjVertex] = 1;
        enqueue(q, adjVertex);
      }
      temp = temp->next;
    }
  }
}

// Creating a node
struct node* createNode(int v) {
  struct node* newNode = malloc(sizeof(struct node));
  newNode->vertex = v;
  newNode->next = NULL;
  return newNode;
}

// Creating a graph
struct Graph* createGraph(int vertices) {
  struct Graph* graph = malloc(sizeof(struct Graph));
  graph->numVertices = vertices;

  graph->adjLists = malloc(vertices * sizeof(struct node*));
  graph->visited = malloc(vertices * sizeof(int));

  int i;
  for (i = 0; i < vertices; i++) {
    graph->adjLists[i] = NULL;
    graph->visited[i] = 0;
  }

  return graph;
}

// Add edge
void addEdge(struct Graph* graph, int src, int dest) {
  // Add edge from src to dest
  struct node* newNode = createNode(dest);
  newNode->next = graph->adjLists[src];
  graph->adjLists[src] = newNode;

  // Add edge from dest to src
  newNode = createNode(src);
  newNode->next = graph->adjLists[dest];
  graph->adjLists[dest] = newNode;
}

// Create a queue
struct queue* createQueue() {
  struct queue* q = malloc(sizeof(struct queue));
  q->front = -1;
  q->rear = -1;
  return q;
}

// Check if the queue is empty
int isEmpty(struct queue* q) {
  if (q->rear == -1)
    return 1;
  else
    return 0;
}

// Adding elements into queue
void enqueue(struct queue* q, int value) {
  if (q->rear == SIZE - 1)
    printf("\nQueue is Full!!");
  else {
    if (q->front == -1)
      q->front = 0;
    q->rear++;
    q->items[q->rear] = value;
  }
}

// Removing elements from queue
int dequeue(struct queue* q) {
  int item;
  if (isEmpty(q)) {
    printf("Queue is empty");
    item = -1;
  } else {
    item = q->items[q->front];
    q->front++;
    if (q->front > q->rear) {
      printf("Resetting queue ");
      q->front = q->rear = -1;
    }
  }
  return item;
}

// Print the queue
void printQueue(struct queue* q) {
  int i = q->front;

  if (isEmpty(q)) {
    printf("Queue is empty");
  } else {
    printf("\nQueue contains \n");
    for (i = q->front; i < q->rear + 1; i++) {
      printf("%d ", q->items[i]);
    }
  }
}

int main() {
  struct Graph* graph = createGraph(6);
  addEdge(graph, 0, 1);
  addEdge(graph, 0, 2);
  addEdge(graph, 1, 2);
  addEdge(graph, 1, 4);
  addEdge(graph, 1, 3);
  addEdge(graph, 2, 4);
  addEdge(graph, 3, 4);

  bfs(graph, 0);

  return 0;
}
```
</details>

#### Depth first search
 
first visit all the vertex then explore it.
 (preorder traversal of the graph.)
 
#### Code in c
 <details>
<summary>Answer</summary>
 
```
#include<stdio.h>
#include<conio.h>
int a[20][20],reach[20],n;
void dfs(int v) {
	int i;
	reach[v]=1;
	for (i=1;i<=n;i++)
	  if(a[v][i] && !reach[i]) {
		printf("\n %d->%d",v,i);
		dfs(i);
	}
}
void main() {
	int i,j,count=0;
	clrscr();
	printf("\n Enter number of vertices:");
	scanf("%d",&n);
	for (i=1;i<=n;i++) {
		reach[i]=0;
		for (j=1;j<=n;j++)
		   a[i][j]=0;
	}
	printf("\n Enter the adjacency matrix:\n");
	for (i=1;i<=n;i++)
	  for (j=1;j<=n;j++)
	   scanf("%d",&a[i][j]);
	dfs(1);
	printf("\n");
	for (i=1;i<=n;i++) {
		if(reach[i])
		   count++;
	}
	if(count==n)
	  printf("\n Graph is connected"); else
	  printf("\n Graph is not connected");
	getch();
	
```
</details>

#### Topological sort

Topological sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge u v, vertex u comes before v in the ordering. Topological Sorting for a graph is not possible if the graph is not a DAG.

For example, a topological sorting of the following graph is “5 4 2 3 1 0”. There can be more than one topological sorting for a graph. For example, another topological sorting of the following graph is “4 5 2 3 1 0”. The first vertex in topological sorting is always a vertex with in-degree as 0 (a vertex with no incoming edges).


#### Code in cpp

 <details>
<summary>Answer</summary>

```
// A C++ program to print topological
// sorting of a DAG
#include <iostream>
#include <list>
#include <stack>
using namespace std;
 
// Class to represent a graph
class Graph {
    // No. of vertices'
    int V;
 
    // Pointer to an array containing adjacency listsList
    list<int>* adj;
 
    // A function used by topologicalSort
    void topologicalSortUtil(int v, bool visited[],
                             stack<int>& Stack);
 
public:
    // Constructor
    Graph(int V);
 
    // function to add an edge to graph
    void addEdge(int v, int w);
 
    // prints a Topological Sort of
    // the complete graph
    void topologicalSort();
};
 
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}
 
void Graph::addEdge(int v, int w)
{
    // Add w to v’s list.
    adj[v].push_back(w);
}
 
// A recursive function used by topologicalSort
void Graph::topologicalSortUtil(int v, bool visited[],
                                stack<int>& Stack)
{
    // Mark the current node as visited.
    visited[v] = true;
 
    // Recur for all the vertices
    // adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            topologicalSortUtil(*i, visited, Stack);
 
    // Push current vertex to stack
    // which stores result
    Stack.push(v);
}
 
// The function to do Topological Sort.
// It uses recursive topologicalSortUtil()
void Graph::topologicalSort()
{
    stack<int> Stack;
 
    // Mark all the vertices as not visited
    bool* visited = new bool[V];
    for (int i = 0; i < V; i++)
        visited[i] = false;
 
    // Call the recursive helper function
    // to store Topological
    // Sort starting from all
    // vertices one by one
    for (int i = 0; i < V; i++)
        if (visited[i] == false)
            topologicalSortUtil(i, visited, Stack);
 
    // Print contents of stack
    while (Stack.empty() == false) {
        cout << Stack.top() << " ";
        Stack.pop();
    }
}
 
// Driver Code
int main()
{
    // Create a graph given in the above diagram
    Graph g(6);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);
 
    cout << "Following is a Topological Sort of the given "
            "graph \n";
 
    // Function Call
    g.topologicalSort();
 
    return 0;
}

```
</details>

#### Strongly connected components


### Minimum spanning trees

Sub graph of graphs having n elements but {n-1} edges.

#### Growing a Minimum spanning trees

Sort the graph edges with respect to their weights.
Start adding edges to the MST from the edge with the smallest weight until the edge of the largest weight.
Only add edges which doesn't form a cycle , edges which connect only disconnected components.
 
 #### Kruskal algorithm
 
 Kruskal's algorithm finds a minimum spanning forest of an undirected edge-weighted graph. If the graph is connected, it finds a minimum spanning tree.
 It is a greedy algorithm in graph theory as in each step it adds the next lowest-weight edge that will not form a cycle to the minimum spanning forest.
 
 #### Code in c
 
  <details>
<summary>Answer</summary>
 
```
 
 #include<stdio.h>
#include<conio.h>
#include<stdlib.h>
int i,j,k,a,b,u,v,n,ne=1;
int min,mincost=0,cost[9][9],parent[9];
int find(int);
int uni(int,int);
void main()
{
	clrscr();
	printf("\n\tImplementation of Kruskal's algorithm\n");
	printf("\nEnter the no. of vertices:");
	scanf("%d",&n);
	printf("\nEnter the cost adjacency matrix:\n");
	for(i=1;i<=n;i++)
	{
		for(j=1;j<=n;j++)
		{
			scanf("%d",&cost[i][j]);
			if(cost[i][j]==0)
				cost[i][j]=999;
		}
	}
	printf("The edges of Minimum Cost Spanning Tree are\n");
	while(ne < n)
	{
		for(i=1,min=999;i<=n;i++)
		{
			for(j=1;j <= n;j++)
			{
				if(cost[i][j] < min)
				{
					min=cost[i][j];
					a=u=i;
					b=v=j;
				}
			}
		}
		u=find(u);
		v=find(v);
		if(uni(u,v))
		{
			printf("%d edge (%d,%d) =%d\n",ne++,a,b,min);
			mincost +=min;
		}
		cost[a][b]=cost[b][a]=999;
	}
	printf("\n\tMinimum cost = %d\n",mincost);
	getch();
}
int find(int i)
{
	while(parent[i])
	i=parent[i];
	return i;
}
int uni(int i,int j)
{
	if(i!=j)
	{
		parent[j]=i;
		return 1;
	}
	return 0;
}
 
```
</details>
 
 #### Prim's algorithm
 
 Prim's Algorithm is a famous greedy algorithm. It is used for finding the Minimum Spanning Tree (MST) of a given graph. To apply Prim's algorithm, the given graph must be weighted, connected and undirected.
 
 #### Code in c
  <details>
<summary>Answer</summary>
 
```
 
 
 #include<stdio.h>
 
#include<conio.h>
 
int a,b,u,v,n,i,j,ne=1;
 
int visited[10]={0},min,mincost=0,cost[10][10];
 
void main()
 
{
 
	clrscr();
 
	printf("\nEnter the number of nodes:");
 
	scanf("%d",&n);
 
	printf("\nEnter the adjacency matrix:\n");
 
	for(i=1;i<=n;i++)
 
	for(j=1;j<=n;j++)
 
	{
 
		scanf("%d",&cost[i][j]);
 
		if(cost[i][j]==0)
 
			cost[i][j]=999;
 
	}
 
	visited[1]=1;
 
	printf("\n");
 
	while(ne < n)
 
	{
 
		for(i=1,min=999;i<=n;i++)
 
		for(j=1;j<=n;j++)
 
		if(cost[i][j]< min)
 
		if(visited[i]!=0)
 
		{
 
			min=cost[i][j];
 
			a=u=i;
 
			b=v=j;
 
		}
 
		if(visited[u]==0 || visited[v]==0)
 
		{
 
			printf("\n Edge %d:(%d %d) cost:%d",ne++,a,b,min);
 
			mincost+=min;
 
			visited[b]=1;
 
		}
 
		cost[a][b]=cost[b][a]=999;
 
	}
 
	printf("\n Minimun cost=%d",mincost);
 
	getch();
 
}

 ```
</details>

### Single source shortest paths
 
#### The bellman ford algorithm
 
 gives shortest path from one node to all other nodes. works on negative edge weights.
 ( works by overestimating the length of the path from the starting vertex to all other vertices. )
 
 #### Code in c
 
   <details>
<summary>Answer</summary>
 
```
 
#include <stdio.h>
#include <stdlib.h>

#define INFINITY 99999

//struct for the edges of the graph
struct Edge {
  int u;  //start vertex of the edge
  int v;  //end vertex of the edge
  int w;  //weight of the edge (u,v)
};

//Graph - it consists of edges
struct Graph {
  int V;        //total number of vertices in the graph
  int E;        //total number of edges in the graph
  struct Edge *edge;  //array of edges
};

void bellmanford(struct Graph *g, int source);
void display(int arr[], int size);

int main(void) {
  //create graph
  struct Graph *g = (struct Graph *)malloc(sizeof(struct Graph));
  g->V = 4;  //total vertices
  g->E = 5;  //total edges

  //array of edges for graph
  g->edge = (struct Edge *)malloc(g->E * sizeof(struct Edge));

  //------- adding the edges of the graph
  /*
		edge(u, v)
		where 	u = start vertex of the edge (u,v)
				v = end vertex of the edge (u,v)
		
		w is the weight of the edge (u,v)
	*/

  //edge 0 --> 1
  g->edge[0].u = 0;
  g->edge[0].v = 1;
  g->edge[0].w = 5;

  //edge 0 --> 2
  g->edge[1].u = 0;
  g->edge[1].v = 2;
  g->edge[1].w = 4;

  //edge 1 --> 3
  g->edge[2].u = 1;
  g->edge[2].v = 3;
  g->edge[2].w = 3;

  //edge 2 --> 1
  g->edge[3].u = 2;
  g->edge[3].v = 1;
  g->edge[3].w = 6;

  //edge 3 --> 2
  g->edge[4].u = 3;
  g->edge[4].v = 2;
  g->edge[4].w = 2;

  bellmanford(g, 0);  //0 is the source vertex

  return 0;
}

void bellmanford(struct Graph *g, int source) {
  //variables
  int i, j, u, v, w;

  //total vertex in the graph g
  int tV = g->V;

  //total edge in the graph g
  int tE = g->E;

  //distance array
  //size equal to the number of vertices of the graph g
  int d[tV];

  //predecessor array
  //size equal to the number of vertices of the graph g
  int p[tV];

  //step 1: fill the distance array and predecessor array
  for (i = 0; i < tV; i++) {
    d[i] = INFINITY;
    p[i] = 0;
  }

  //mark the source vertex
  d[source] = 0;

  //step 2: relax edges |V| - 1 times
  for (i = 1; i <= tV - 1; i++) {
    for (j = 0; j < tE; j++) {
      //get the edge data
      u = g->edge[j].u;
      v = g->edge[j].v;
      w = g->edge[j].w;

      if (d[u] != INFINITY && d[v] > d[u] + w) {
        d[v] = d[u] + w;
        p[v] = u;
      }
    }
  }

  //step 3: detect negative cycle
  //if value changes then we have a negative cycle in the graph
  //and we cannot find the shortest distances
  for (i = 0; i < tE; i++) {
    u = g->edge[i].u;
    v = g->edge[i].v;
    w = g->edge[i].w;
    if (d[u] != INFINITY && d[v] > d[u] + w) {
      printf("Negative weight cycle detected!\n");
      return;
    }
  }

  //No negative weight cycle found!
  //print the distance and predecessor array
  printf("Distance array: ");
  display(d, tV);
  printf("Predecessor array: ");
  display(p, tV);
}

void display(int arr[], int size) {
  int i;
  for (i = 0; i < size; i++) {
    printf("%d ", arr[i]);
  }
  printf("\n");
}
 
```
</details>

#### Single source shortest paths in directed acyclic graphs

Given a Weighted Directed Acyclic Graph and a source vertex in the graph, find the shortest paths from given source to all other vertices.

For a general weighted graph, we can calculate single source shortest distances in O(VE) time using Bellman–Ford Algorithm. For a graph with no negative weights, we can do better and calculate single source shortest distances in O(E + VLogV) time using Dijkstra’s algorithm. Can we do even better for Directed Acyclic Graph (DAG)? We can calculate single source shortest distances in O(V+E) time for DAGs. The idea is to use Topological Sorting.

We initialize distances to all vertices as infinite and distance to source as 0, then we find a topological sorting of the graph. Topological Sorting of a graph represents a linear ordering of the graph (See below, figure (b) is a linear representation of figure (a) ). Once we have topological order (or linear representation), we one by one process all vertices in topological order. For every vertex being processed, we update distances of its adjacent using distance of current vertex.

#### Code in cpp
   <details>
<summary>Answer</summary>
 
```
// C++ program to find single source shortest paths for Directed Acyclic Graphs
#include<iostream>
#include <bits/stdc++.h>
#define INF INT_MAX
using namespace std;
  
// Graph is represented using adjacency list. Every node of adjacency list 
// contains vertex number of the vertex to which edge connects. It also 
// contains weight of the edge
class AdjListNode
{
    int v;
    int weight;
public:
    AdjListNode(int _v, int _w)  { v = _v;  weight = _w;}
    int getV()       {  return v;  }
    int getWeight()  {  return weight; }
};
  
// Class to represent a graph using adjacency list representation
class Graph
{
    int V;    // No. of vertices'
  
    // Pointer to an array containing adjacency lists
    list<AdjListNode> *adj;
  
    // A function used by shortestPath
    void topologicalSortUtil(int v, bool visited[], stack<int> &Stack);
public:
    Graph(int V);   // Constructor
  
    // function to add an edge to graph
    void addEdge(int u, int v, int weight);
  
    // Finds shortest paths from given source vertex
    void shortestPath(int s);
};
  
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<AdjListNode>[V];
}
  
void Graph::addEdge(int u, int v, int weight)
{
    AdjListNode node(v, weight);
    adj[u].push_back(node); // Add v to u's list
}
  
// A recursive function used by shortestPath. See below link for details
// https://www.geeksforgeeks.org/topological-sorting/
void Graph::topologicalSortUtil(int v, bool visited[], stack<int> &Stack)
{
    // Mark the current node as visited
    visited[v] = true;
  
    // Recur for all the vertices adjacent to this vertex
    list<AdjListNode>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
    {
        AdjListNode node = *i;
        if (!visited[node.getV()])
            topologicalSortUtil(node.getV(), visited, Stack);
    }
  
    // Push current vertex to stack which stores topological sort
    Stack.push(v);
}
  
// The function to find shortest paths from given vertex. It uses recursive 
// topologicalSortUtil() to get topological sorting of given graph.
void Graph::shortestPath(int s)
{
    stack<int> Stack;
    int dist[V];
  
    // Mark all the vertices as not visited
    bool *visited = new bool[V];
    for (int i = 0; i < V; i++)
        visited[i] = false;
  
    // Call the recursive helper function to store Topological Sort
    // starting from all vertices one by one
    for (int i = 0; i < V; i++)
        if (visited[i] == false)
            topologicalSortUtil(i, visited, Stack);
  
    // Initialize distances to all vertices as infinite and distance
    // to source as 0
    for (int i = 0; i < V; i++)
        dist[i] = INF;
    dist[s] = 0;
  
    // Process vertices in topological order
    while (Stack.empty() == false)
    {
        // Get the next vertex from topological order
        int u = Stack.top();
        Stack.pop();
  
        // Update distances of all adjacent vertices
        list<AdjListNode>::iterator i;
        if (dist[u] != INF)
        {
          for (i = adj[u].begin(); i != adj[u].end(); ++i)
             if (dist[i->getV()] > dist[u] + i->getWeight())
                dist[i->getV()] = dist[u] + i->getWeight();
        }
    }
  
    // Print the calculated shortest distances
    for (int i = 0; i < V; i++)
        (dist[i] == INF)? cout << "INF ": cout << dist[i] << " ";
}
  
// Driver program to test above functions
int main()
{
    // Create a graph given in the above diagram.  Here vertex numbers are
    // 0, 1, 2, 3, 4, 5 with following mappings:
    // 0=r, 1=s, 2=t, 3=x, 4=y, 5=z
    Graph g(6);
    g.addEdge(0, 1, 5);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 3, 6);
    g.addEdge(1, 2, 2);
    g.addEdge(2, 4, 4);
    g.addEdge(2, 5, 2);
    g.addEdge(2, 3, 7);
    g.addEdge(3, 4, -1);
    g.addEdge(4, 5, -2);
  
    int s = 1;
    cout << "Following are shortest distances from source " << s <<" n";
    g.shortestPath(s);
  
    return 0;
}

```
</details>
 
#### Dijkstra's algorithm

Single source shortest path algorithm. does not works on negative weights.
{minimization problem-optimization problem-greedy method-solved in stages by taking one step at a time and considering one input
at a time to get an optimal solution}

#### Code in c
   <details>
<summary>Answer</summary>
 
```
#include<stdio.h>
#include<conio.h>
#define INFINITY 9999
#define MAX 10
 
void dijikstra(int G[MAX][MAX], int n, int startnode);
 
void main(){
	int G[MAX][MAX], i, j, n, u;
	clrscr();
	printf("\nEnter the no. of vertices:: ");
	scanf("%d", &n);
	printf("\nEnter the adjacency matrix::\n");
	for(i=0;i < n;i++)
		for(j=0;j < n;j++)
			scanf("%d", &G[i][j]);
	printf("\nEnter the starting node:: ");
	scanf("%d", &u);
	dijikstra(G,n,u);
	getch();
}
 
void dijikstra(int G[MAX][MAX], int n, int startnode)
{
	int cost[MAX][MAX], distance[MAX], pred[MAX];
	int visited[MAX], count, mindistance, nextnode, i,j;
	for(i=0;i < n;i++)
		for(j=0;j < n;j++)
			if(G[i][j]==0)
				cost[i][j]=INFINITY;
			else
				cost[i][j]=G[i][j];
	
	for(i=0;i< n;i++)
	{
		distance[i]=cost[startnode][i];
		pred[i]=startnode;
		visited[i]=0;
	}
	distance[startnode]=0;
	visited[startnode]=1;
	count=1;
	while(count < n-1){
		mindistance=INFINITY;
		for(i=0;i < n;i++)
			if(distance[i] < mindistance&&!visited[i])
			{
				mindistance=distance[i];
				nextnode=i;
			}
		visited[nextnode]=1;
		for(i=0;i < n;i++)
			if(!visited[i])
				if(mindistance+cost[nextnode][i] < distance[i])
				{
					distance[i]=mindistance+cost[nextnode][i];
					pred[i]=nextnode;
				}
			count++;
	}
 
	for(i=0;i < n;i++)
		if(i!=startnode)
		{
			printf("\nDistance of %d = %d", i, distance[i]);
			printf("\nPath = %d", i);
			j=i;
			do
			{
				j=pred[j];
				printf(" <-%d", j);
			}
			while(j!=startnode);
		}
}
 
 ```
 </details>
 
 #### difference constraints and shortest paths
 
 Because there are edges from the source vertex v0 to all other vertices in the constraint graph, any negative-weight cycle in the constraint graph is reachable from v0. If the Bellman-Ford algorithm returns TRUE, then the shortest-path weights give a feasible solution to the system.
 
 #### Proofs of shortest paths
 
 The proof of this is based on the notion that if there was a shorter path than any sub-path, then the shorter path should replace that sub-path to make the whole path shorter. If s ->.. ... Denote the distance of the shortest path from s to u as delta(s,u).

 
 ### All pairs shotest paths
 
 #### Shortest path and matrix multiplication
 
 The algorithm is based on dynamic programming, in which each major loop will invoke an operation that is very similar to matrix multiplication. Following the DP strategy, the structure of this problem is, for any two vertices u and v,
if u=v, then the shortest path p from u to v is 0.
otherwise, decompose p into u→x→v, where p' is a path from u to x and contains at most k edges and it is the shortest path from u to x.
A recursive solution for the APSP problem is defined. Let dij (k) be the minimum weight of any path from i to j that contains at most k edges.
If k=0, then

dij (0) ={ 0 if i=j ∞ if i≠j

Otherwise, for k≥1, dij (k) can be computed from dij (k-1) and the adjacency matrix w.
dij (k) =min{ dij (k-1) , min1≤l≤n { dil (k-1) + wlj }}= min1≤l≤n { dil (k-1) + wlj }
SPECIAL-MATRIX-MULTIPLY (A,B)
 1     n ←  rows [A]
 2     C ← new n×n matrix
 3    for  i ←  1 to  n
 4             do for  j ←  1 to  n
 5                            do  cij ←  ∞
 6                                  for  k ←  1 to  n
 7                                           do  cij ←  min( cij , aik + bkj )
 .                                                    /* Here's where this algorithm */
 .                                                    /* differs from MATRIX-MULTIPLY. */
 8    return  C
The optimal solution can be computed by calling SPECIAL-MATRIX-MULTIPLY ( D(k) ,W) for 1≤k≤n-2. We only need to run to n-2 because that will give us D(n-1) giving us all the shortest path lengths of at most n-1 edges (you only need n-1 edges to connect n vertices). Since SPECIAL-MATRIX-MULTIPLY is called n-2 times, the total running time is O( n4 ).
 
 
 #### The Floyd Warshall Algorithm
 
The Floyd Warshall Algorithm is for solving the All Pairs Shortest Path problem. The problem is to find shortest distances between every pair of vertices in a given edge weighted directed Graph. 
Example: 

Input:
       graph[][] = { {0,   5,  INF, 10},
                    {INF,  0,  3,  INF},
                    {INF, INF, 0,   1},
                    {INF, INF, INF, 0} }
which represents the following graph
             10
       (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
       \|/         |
       (1)------->(2)
            3       
Note that the value of graph[i][j] is 0 if i is equal to j 
And graph[i][j] is INF (infinite) if there is no edge from vertex i to j.

Output:
Shortest distance matrix
      0      5      8      9
    INF      0      3      4
    INF    INF      0      1
    INF    INF    INF      0
 
 #### Code in c
   <details>
<summary>Answer</summary>
 
```
// C Program for Floyd Warshall Algorithm
#include<stdio.h>
 
// Number of vertices in the graph
#define V 4
 
/* Define Infinite as a large enough
  value. This value will be used
  for vertices not connected to each other */
#define INF 99999
 
// A function to print the solution matrix
void printSolution(int dist[][V]);
 
// Solves the all-pairs shortest path
// problem using Floyd Warshall algorithm
void floydWarshall (int graph[][V])
{
    /* dist[][] will be the output matrix
      that will finally have the shortest
      distances between every pair of vertices */
    int dist[V][V], i, j, k;
 
    /* Initialize the solution matrix
      same as input graph matrix. Or
       we can say the initial values of
       shortest distances are based
       on shortest paths considering no
       intermediate vertex. */
    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            dist[i][j] = graph[i][j];
 
    /* Add all vertices one by one to
      the set of intermediate vertices.
      ---> Before start of an iteration, we
      have shortest distances between all
      pairs of vertices such that the shortest
      distances consider only the
      vertices in set {0, 1, 2, .. k-1} as
      intermediate vertices.
      ----> After the end of an iteration,
      vertex no. k is added to the set of
      intermediate vertices and the set
      becomes {0, 1, 2, .. k} */
    for (k = 0; k < V; k++)
    {
        // Pick all vertices as source one by one
        for (i = 0; i < V; i++)
        {
            // Pick all vertices as destination for the
            // above picked source
            for (j = 0; j < V; j++)
            {
                // If vertex k is on the shortest path from
                // i to j, then update the value of dist[i][j]
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }
 
    // Print the shortest distance matrix
    printSolution(dist);
}
 
/* A utility function to print solution */
void printSolution(int dist[][V])
{
    printf ("The following matrix shows the shortest distances"
            " between every pair of vertices \n");
    for (int i = 0; i < V; i++)
    {
        for (int j = 0; j < V; j++)
        {
            if (dist[i][j] == INF)
                printf("%7s", "INF");
            else
                printf ("%7d", dist[i][j]);
        }
        printf("\n");
    }
}
 
// driver program to test above function
int main()
{
    /* Let us create the following weighted graph
            10
       (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
       \|/         |
       (1)------->(2)
            3           */
    int graph[V][V] = { {0,   5,  INF, 10},
                        {INF, 0,   3, INF},
                        {INF, INF, 0,   1},
                        {INF, INF, INF, 0}
                      };
 
    // Print the solution
    floydWarshall(graph);
    return 0;
}
```
</details>
 
 
 #### Johnson’s algorithm for sparse graphs
 
 The problem is to find shortest paths between every pair of vertices in a given weighted directed Graph and weights may be negative. We have discussed Floyd Warshall Algorithm for this problem. Time complexity of Floyd Warshall Algorithm is Θ(V3). Using Johnson’s algorithm, we can find all pair shortest paths in O(V2log V + VE) time. Johnson’s algorithm uses both Dijkstra and Bellman-Ford as subroutines.

If we apply Dijkstra’s Single Source shortest path algorithm for every vertex, considering every vertex as source, we can find all pair shortest paths in O(V*VLogV) time. So using Dijkstra’s single source shortest path seems to be a better option than Floyd Warshell, but the problem with Dijkstra’s algorithm is, it doesn’t work for negative weight edge.
The idea of Johnson’s algorithm is to re-weight all edges and make them all positive, then apply Dijkstra’s algorithm for every vertex.
 
 
 ### Maximum flow
 
 #### Flow networks
 
 In graph theory, a flow network (also known as a transportation network) is a directed graph where each edge has a capacity and each edge receives a flow. The amount of flow on an edge cannot exceed the capacity of the edge. Often in operations research, a directed graph is called a network, the vertices are called nodes and the edges are called arcs. A flow must satisfy the restriction that the amount of flow into a node equals the amount of flow out of it, unless it is a source, which has only outgoing flow, or sink, which has only incoming flow. A network can be used to model traffic in a computer network, circulation with demands, fluids in pipes, currents in an electrical circuit, or anything similar in which something travels through a network of nodes.
 
 
 #### The ford fulkerson algorithm
 
 Ford-Fulkerson algorithm is a greedy approach for calculating the maximum possible flow in a network or a graph.
 
 #### Code in c
 
  <details>
<summary>Answer</summary>
 
```

 
 #include <stdio.h>

#define A 0
#define B 1
#define C 2
#define MAX_NODES 1000
#define O 1000000000

int n;
int e;
int capacity[MAX_NODES][MAX_NODES];
int flow[MAX_NODES][MAX_NODES];
int color[MAX_NODES];
int pred[MAX_NODES];

int min(int x, int y) {
  return x < y ? x : y;
}

int head, tail;
int q[MAX_NODES + 2];

void enqueue(int x) {
  q[tail] = x;
  tail++;
  color[x] = B;
}

int dequeue() {
  int x = q[head];
  head++;
  color[x] = C;
  return x;
}

// Using BFS as a searching algorithm
int bfs(int start, int target) {
  int u, v;
  for (u = 0; u < n; u++) {
    color[u] = A;
  }
  head = tail = 0;
  enqueue(start);
  pred[start] = -1;
  while (head != tail) {
    u = dequeue();
    for (v = 0; v < n; v++) {
      if (color[v] == A && capacity[u][v] - flow[u][v] > 0) {
        enqueue(v);
        pred[v] = u;
      }
    }
  }
  return color[target] == C;
}

// Applying fordfulkerson algorithm
int fordFulkerson(int source, int sink) {
  int i, j, u;
  int max_flow = 0;
  for (i = 0; i < n; i++) {
    for (j = 0; j < n; j++) {
      flow[i][j] = 0;
    }
  }

  // Updating the residual values of edges
  while (bfs(source, sink)) {
    int increment = O;
    for (u = n - 1; pred[u] >= 0; u = pred[u]) {
      increment = min(increment, capacity[pred[u]][u] - flow[pred[u]][u]);
    }
    for (u = n - 1; pred[u] >= 0; u = pred[u]) {
      flow[pred[u]][u] += increment;
      flow[u][pred[u]] -= increment;
    }
    // Adding the path flows
    max_flow += increment;
  }
  return max_flow;
}

int main() {
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
      capacity[i][j] = 0;
    }
  }
  n = 6;
  e = 7;

  capacity[0][1] = 8;
  capacity[0][4] = 3;
  capacity[1][2] = 9;
  capacity[2][4] = 7;
  capacity[2][5] = 2;
  capacity[3][5] = 5;
  capacity[4][2] = 7;
  capacity[4][3] = 4;

  int s = 0, t = 5;
  printf("Max Flow: %d\n", fordFulkerson(s, t));
}
 ```
 </details>
 
 #### Maximum bipartite algorithm
 
 an undirected graph is bipartite if there exists partition into left and right such that every edge has one vertex in left and one in right.
(no odd length cycles,2 colors).


#### Push relable algorithm

Push-Relabel Algorithm 
1) Initialize PreFlow : Initialize Flows 
   and Heights 

2) While it is possible to perform a Push() or 
   Relablel() on a vertex
   // Or while there is a vertex that has excess flow
           Do Push() or Relabel()

// At this point all vertices have Excess Flow as 0 (Except source
// and sink)
3) Return flow.

#### Code in cpp
  <details>
<summary>Answer</summary>
 

```
// C++ program to implement push-relabel algorithm for
// getting maximum flow of graph
#include <bits/stdc++.h>
using namespace std;
  
struct Edge
{
    // To store current flow and capacity of edge
    int flow, capacity;
  
    // An edge u--->v has start vertex as u and end
    // vertex as v.
    int u, v;
  
    Edge(int flow, int capacity, int u, int v)
    {
        this->flow = flow;
        this->capacity = capacity;
        this->u = u;
        this->v = v;
    }
};
  
// Represent a Vertex
struct Vertex
{
    int h, e_flow;
  
    Vertex(int h, int e_flow)
    {
        this->h = h;
        this->e_flow = e_flow;
    }
};
  
// To represent a flow network
class Graph
{
    int V;    // No. of vertices
    vector<Vertex> ver;
    vector<Edge> edge;
  
    // Function to push excess flow from u
    bool push(int u);
  
    // Function to relabel a vertex u
    void relabel(int u);
  
    // This function is called to initialize
    // preflow
    void preflow(int s);
  
    // Function to reverse edge
    void updateReverseEdgeFlow(int i, int flow);
  
public:
    Graph(int V);  // Constructor
  
    // function to add an edge to graph
    void addEdge(int u, int v, int w);
  
    // returns maximum flow from s to t
    int getMaxFlow(int s, int t);
};
  
Graph::Graph(int V)
{
    this->V = V;
  
    // all vertices are initialized with 0 height
    // and 0 excess flow
    for (int i = 0; i < V; i++)
        ver.push_back(Vertex(0, 0));
}
  
void Graph::addEdge(int u, int v, int capacity)
{
    // flow is initialized with 0 for all edge
    edge.push_back(Edge(0, capacity, u, v));
}
  
void Graph::preflow(int s)
{
    // Making h of source Vertex equal to no. of vertices
    // Height of other vertices is 0.
    ver[s].h = ver.size();
  
    //
    for (int i = 0; i < edge.size(); i++)
    {
        // If current edge goes from source
        if (edge[i].u == s)
        {
            // Flow is equal to capacity
            edge[i].flow = edge[i].capacity;
  
            // Initialize excess flow for adjacent v
            ver[edge[i].v].e_flow += edge[i].flow;
  
            // Add an edge from v to s in residual graph with
            // capacity equal to 0
            edge.push_back(Edge(-edge[i].flow, 0, edge[i].v, s));
        }
    }
}
  
// returns index of overflowing Vertex
int overFlowVertex(vector<Vertex>& ver)
{
    for (int i = 1; i < ver.size() - 1; i++)
       if (ver[i].e_flow > 0)
            return i;
  
    // -1 if no overflowing Vertex
    return -1;
}
  
// Update reverse flow for flow added on ith Edge
void Graph::updateReverseEdgeFlow(int i, int flow)
{
    int u = edge[i].v, v = edge[i].u;
  
    for (int j = 0; j < edge.size(); j++)
    {
        if (edge[j].v == v && edge[j].u == u)
        {
            edge[j].flow -= flow;
            return;
        }
    }
  
    // adding reverse Edge in residual graph
    Edge e = Edge(0, flow, u, v);
    edge.push_back(e);
}
  
// To push flow from overflowing vertex u
bool Graph::push(int u)
{
    // Traverse through all edges to find an adjacent (of u)
    // to which flow can be pushed
    for (int i = 0; i < edge.size(); i++)
    {
        // Checks u of current edge is same as given
        // overflowing vertex
        if (edge[i].u == u)
        {
            // if flow is equal to capacity then no push
            // is possible
            if (edge[i].flow == edge[i].capacity)
                continue;
  
            // Push is only possible if height of adjacent
            // is smaller than height of overflowing vertex
            if (ver[u].h > ver[edge[i].v].h)
            {
                // Flow to be pushed is equal to minimum of
                // remaining flow on edge and excess flow.
                int flow = min(edge[i].capacity - edge[i].flow,
                               ver[u].e_flow);
  
                // Reduce excess flow for overflowing vertex
                ver[u].e_flow -= flow;
  
                // Increase excess flow for adjacent
                ver[edge[i].v].e_flow += flow;
  
                // Add residual flow (With capacity 0 and negative
                // flow)
                edge[i].flow += flow;
  
                updateReverseEdgeFlow(i, flow);
  
                return true;
            }
        }
    }
    return false;
}
  
// function to relabel vertex u
void Graph::relabel(int u)
{
    // Initialize minimum height of an adjacent
    int mh = INT_MAX;
  
    // Find the adjacent with minimum height
    for (int i = 0; i < edge.size(); i++)
    {
        if (edge[i].u == u)
        {
            // if flow is equal to capacity then no
            // relabeling
            if (edge[i].flow == edge[i].capacity)
                continue;
  
            // Update minimum height
            if (ver[edge[i].v].h < mh)
            {
                mh = ver[edge[i].v].h;
  
                // updating height of u
                ver[u].h = mh + 1;
            }
        }
    }
}
  
// main function for printing maximum flow of graph
int Graph::getMaxFlow(int s, int t)
{
    preflow(s);
  
    // loop untill none of the Vertex is in overflow
    while (overFlowVertex(ver) != -1)
    {
        int u = overFlowVertex(ver);
        if (!push(u))
            relabel(u);
    }
  
    // ver.back() returns last Vertex, whose
    // e_flow will be final maximum flow
    return ver.back().e_flow;
}
  
// Driver program to test above functions
int main()
{
    int V = 6;
    Graph g(V);
  
    // Creating above shown flow network
    g.addEdge(0, 1, 16);
    g.addEdge(0, 2, 13);
    g.addEdge(1, 2, 10);
    g.addEdge(2, 1, 4);
    g.addEdge(1, 3, 12);
    g.addEdge(2, 4, 14);
    g.addEdge(3, 2, 9);
    g.addEdge(3, 5, 20);
    g.addEdge(4, 3, 7);
    g.addEdge(4, 5, 4);
  
    // Initialize source and sink
    int s = 0, t = 5;
  
    cout << "Maximum flow is " << g.getMaxFlow(s, t);
    return 0;
}
```
</details>


#### The relable to front algorithm

The relabel-to-front algorithm is used to find the maximum flow in the network.
First, we need to understand the basic operations i.e. push and relabel:
Each vertex in the network has 2 variables associated with it which are height variable(h) and excess flow(e).

Push: If a vertex has excess flow and there is an adjacent node with lower height (in the residual graph) then we push flow from the vertex to the lower height node.
Relabel: If a vertex has excess flow and no adjacent node with lower height are available then we use relabel operation to increase the height of vertex so that it can perform push operation.
The relabel-to-front algorithm maintains a list of vertices in the network. It starts from the beginning of the list and repeatedly selects an overflowing vertex u and performs discharge operation on it.
Discharge operation is performing push and relabel operation until vertex u has no positive excess flow(e)
If a vertex is relabeled, it is moved to the front of the list and algorithm scans again.

Algorithm:

Initialize the preflow and heights to the same values as in the generic push-relabel algorithm.
Initialize list L which contains all vertices except source and sink.
Initialize current pointer of each vertex u to the first vertex in u’s neighbour list N. The neighbour list N contains those vertices for which there is a residual edge.
While algorithm reaches the end of list L.
Select the vertex u from list L and perform discharge operation.
If u was relabeled by discharge then move u to the front of the list.
If u was moved to the front of the list, the vertex in the next iteration is the one following u in its new position in the list.

#### Code in cpp

  <details>
<summary>Answer</summary>
 
```
// C++ program to implement push-relabel algorithm for
// getting maximum flow of graph
#include <bits/stdc++.h>
using namespace std;
  
struct Edge
{
    // To store current flow and capacity of edge
    int flow, capacity;
  
    // An edge u--->v has start vertex as u and end
    // vertex as v.
    int u, v;
  
    Edge(int flow, int capacity, int u, int v)
    {
        this->flow = flow;
        this->capacity = capacity;
        this->u = u;
        this->v = v;
    }
};
  
// Represent a Vertex
struct Vertex
{
    int h, e_flow;
  
    Vertex(int h, int e_flow)
    {
        this->h = h;
        this->e_flow = e_flow;
    }
};
  
// To represent a flow network
class Graph
{
    int V;    // No. of vertices
    vector<Vertex> ver;
    vector<Edge> edge;
  
    // Function to push excess flow from u
    bool push(int u);
  
    // Function to relabel a vertex u
    void relabel(int u);
  
    // This function is called to initialize
    // preflow
    void preflow(int s);
  
    // Function to reverse edge
    void updateReverseEdgeFlow(int i, int flow);
  
public:
    Graph(int V);  // Constructor
  
    // function to add an edge to graph
    void addEdge(int u, int v, int w);
  
    // returns maximum flow from s to t
    int getMaxFlow(int s, int t);
};
  
Graph::Graph(int V)
{
    this->V = V;
  
    // all vertices are initialized with 0 height
    // and 0 excess flow
    for (int i = 0; i < V; i++)
        ver.push_back(Vertex(0, 0));
}
  
void Graph::addEdge(int u, int v, int capacity)
{
    // flow is initialized with 0 for all edge
    edge.push_back(Edge(0, capacity, u, v));
}
  
void Graph::preflow(int s)
{
    // Making h of source Vertex equal to no. of vertices
    // Height of other vertices is 0.
    ver[s].h = ver.size();
  
    //
    for (int i = 0; i < edge.size(); i++)
    {
        // If current edge goes from source
        if (edge[i].u == s)
        {
            // Flow is equal to capacity
            edge[i].flow = edge[i].capacity;
  
            // Initialize excess flow for adjacent v
            ver[edge[i].v].e_flow += edge[i].flow;
  
            // Add an edge from v to s in residual graph with
            // capacity equal to 0
            edge.push_back(Edge(-edge[i].flow, 0, edge[i].v, s));
        }
    }
}
  
// returns index of overflowing Vertex
int overFlowVertex(vector<Vertex>& ver)
{
    for (int i = 1; i < ver.size() - 1; i++)
       if (ver[i].e_flow > 0)
            return i;
  
    // -1 if no overflowing Vertex
    return -1;
}
  
// Update reverse flow for flow added on ith Edge
void Graph::updateReverseEdgeFlow(int i, int flow)
{
    int u = edge[i].v, v = edge[i].u;
  
    for (int j = 0; j < edge.size(); j++)
    {
        if (edge[j].v == v && edge[j].u == u)
        {
            edge[j].flow -= flow;
            return;
        }
    }
  
    // adding reverse Edge in residual graph
    Edge e = Edge(0, flow, u, v);
    edge.push_back(e);
}
  
// To push flow from overflowing vertex u
bool Graph::push(int u)
{
    // Traverse through all edges to find an adjacent (of u)
    // to which flow can be pushed
    for (int i = 0; i < edge.size(); i++)
    {
        // Checks u of current edge is same as given
        // overflowing vertex
        if (edge[i].u == u)
        {
            // if flow is equal to capacity then no push
            // is possible
            if (edge[i].flow == edge[i].capacity)
                continue;
  
            // Push is only possible if height of adjacent
            // is smaller than height of overflowing vertex
            if (ver[u].h > ver[edge[i].v].h)
            {
                // Flow to be pushed is equal to minimum of
                // remaining flow on edge and excess flow.
                int flow = min(edge[i].capacity - edge[i].flow,
                               ver[u].e_flow);
  
                // Reduce excess flow for overflowing vertex
                ver[u].e_flow -= flow;
  
                // Increase excess flow for adjacent
                ver[edge[i].v].e_flow += flow;
  
                // Add residual flow (With capacity 0 and negative
                // flow)
                edge[i].flow += flow;
  
                updateReverseEdgeFlow(i, flow);
  
                return true;
            }
        }
    }
    return false;
}
  
// function to relabel vertex u
void Graph::relabel(int u)
{
    // Initialize minimum height of an adjacent
    int mh = INT_MAX;
  
    // Find the adjacent with minimum height
    for (int i = 0; i < edge.size(); i++)
    {
        if (edge[i].u == u)
        {
            // if flow is equal to capacity then no
            // relabeling
            if (edge[i].flow == edge[i].capacity)
                continue;
  
            // Update minimum height
            if (ver[edge[i].v].h < mh)
            {
                mh = ver[edge[i].v].h;
  
                // updating height of u
                ver[u].h = mh + 1;
            }
        }
    }
}
  
// main function for printing maximum flow of graph
int Graph::getMaxFlow(int s, int t)
{
    preflow(s);
  
    // loop untill none of the Vertex is in overflow
    while (overFlowVertex(ver) != -1)
    {
        int u = overFlowVertex(ver);
        if (!push(u))
            relabel(u);
    }
  
    // ver.back() returns last Vertex, whose
    // e_flow will be final maximum flow
    return ver.back().e_flow;
}
  
// Driver program to test above functions
int main()
{
    int V = 6;
    Graph g(V);
  
    // Creating above shown flow network
    g.addEdge(0, 1, 16);
    g.addEdge(0, 2, 13);
    g.addEdge(1, 2, 10);
    g.addEdge(2, 1, 4);
    g.addEdge(1, 3, 12);
    g.addEdge(2, 4, 14);
    g.addEdge(3, 2, 9);
    g.addEdge(3, 5, 20);
    g.addEdge(4, 3, 7);
    g.addEdge(4, 5, 4);
  
    // Initialize source and sink
    int s = 0, t = 5;
  
    cout << "Maximum flow is " << g.getMaxFlow(s, t);
    return 0;
}
```
</details>

### Multithreaded algorithm

Multithreading is a feature that allows concurrent execution of two or more parts of a program for maximum utilization of Resources.
 Each part of such program is called a thread. So, threads are light-weight processes within a process.

#### The basics of dynamic multithreading

Threads are popular way to improve application through parallelism. For example, in a browser, multiple tabs can be different threads. MS word uses multiple threads, one thread to format the text, other thread to process inputs, etc.
Threads operate faster than processes due to following reasons:
1) Thread creation is much faster.
2) Context switching between threads is much faster.
3) Threads can be terminated easily
4) Communication between threads is faster.

  <details>
<summary>Answer</summary>
 
```

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>  //Header file for sleep(). man 3 sleep for details.
#include <pthread.h>
  
// A normal C function that is executed as a thread 
// when its name is specified in pthread_create()
void *myThreadFun(void *vargp)
{
    sleep(1);
    printf("Printing GeeksQuiz from Thread \n");
    return NULL;
}
   
int main()
{
    pthread_t thread_id;
    printf("Before Thread\n");
    pthread_create(&thread_id, NULL, myThreadFun, NULL);
    pthread_join(thread_id, NULL);
    printf("After Thread\n");
    exit(0);
}
```
</details>

#### Multithreaded matrix multiplication

 In multi-threading, instead of utilizing a single core of your processor, we utilizes all or more core to solve the problem.

We create different threads, each thread evaluating some part of matrix multiplication.
Depending upon the number of cores your processor has, you can create the number of threads required. Although you can create as many threads as you need, a better way is to create each thread for one core.

In second approach,we create a separate thread for each element in resultant matrix. Using pthread_exit() we return computed value from each thread which is collected by pthread_join(). This approach does not make use of any global variables.

#### Code in c

  <details>
<summary>Answer</summary>
 
```
// C Program to multiply two matrix using pthreads without 
// use of global variables 
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>
#define MAX 4
  
  
//Each thread computes single element in the resultant matrix
void *mult(void* arg)
{
    int *data = (int *)arg;
    int k = 0, i = 0;
      
    int x = data[0];
    for (i = 1; i <= x; i++)
           k += data[i]*data[i+x];
      
    int *p = (int*)malloc(sizeof(int));
         *p = k;
      
//Used to terminate a thread and the return value is passed as a pointer
    pthread_exit(p);
}
  
//Driver code
int main()
{
  
    int matA[MAX][MAX]; 
    int matB[MAX][MAX]; 
      
      
    int r1=MAX,c1=MAX,r2=MAX,c2=MAX,i,j,k;
  
  
    // Generating random values in matA
    for (i = 0; i < r1; i++) 
            for (j = 0; j < c1; j++) 
                   matA[i][j] = rand() % 10; 
            
        // Generating random values in matB 
    for (i = 0; i < r1; i++) 
            for (j = 0; j < c1; j++) 
                   matB[i][j] = rand() % 10; 
     
    // Displaying matA         
    for (i = 0; i < r1; i++){
        for(j = 0; j < c1; j++)
            printf("%d ",matA[i][j]);
        printf("\n");
    }
              
    // Displaying matB                
    for (i = 0; i < r2; i++){
        for(j = 0; j < c2; j++)
            printf("%d ",matB[i][j]);
        printf("\n");    
    }
      
      
    int max = r1*c2;
      
      
    //declaring array of threads of size r1*c2        
    pthread_t *threads;
    threads = (pthread_t*)malloc(max*sizeof(pthread_t));
      
    int count = 0;
    int* data = NULL;
    for (i = 0; i < r1; i++)
        for (j = 0; j < c2; j++)
               {
                 
               //storing row and column elements in data 
            data = (int *)malloc((20)*sizeof(int));
            data[0] = c1;
      
            for (k = 0; k < c1; k++)
                data[k+1] = matA[i][k];
      
            for (k = 0; k < r2; k++)
                data[k+c1+1] = matB[k][j];
               
             //creating threads
                pthread_create(&threads[count++], NULL, 
                               mult, (void*)(data));
                  
                    }
      
    printf("RESULTANT MATRIX IS :- \n");
    for (i = 0; i < max; i++) 
    {
      void *k;
        
      //Joining all threads and collecting return value 
      pthread_join(threads[i], &k);
             
            
          int *p = (int *)k;
      printf("%d ",*p);
      if ((i + 1) % c2 == 0)
          printf("\n");
    }
  
      
  
  return 0;
}
```
</details>



#### Multithreaded merge sort

Merge Sort is a popular sorting technique which divides an array or list into two halves and then start merging them when sufficient depth is reached. Time complexity of merge sort is O(nlogn).

Threads are lightweight processes and threads shares with other threads their code section, data section and OS resources like open files and signals. But, like process, a thread has its own program counter (PC), a register set, and a stack space.

Multi-threading is way to improve parallelism by running the threads simultaneously in different cores of your processor. In this program, we’ll use 4 threads but you may change it according to the number of cores your processor has.

Examples:

Input :  83, 86, 77, 15, 93, 35, 86, 92, 49, 21, 
         62, 27, 90, 59, 63, 26, 40, 26, 72, 36
Output : 15, 21, 26, 26, 27, 35, 36, 40, 49, 59, 
         62, 63, 72, 77, 83, 86, 86, 90, 92, 93

Input :  6, 5, 4, 3, 2, 1
Output : 1, 2, 3, 4, 5, 6

#### Code in c
   <details>
<summary>Answer</summary>
 
```
#include <pthread.h>
#include <time.h>
#include <stdlib.h>

// number of elements in array
#define MAX 15

// number of threads
#define THREAD_MAX 4

//using namespace std;

// array of size MAX
int a[MAX];
int part = 0;

// merge function for merging two parts
void merge(int low, int mid, int high)
{   
    int* left = (int*) malloc( (mid - low + 1) * sizeof(int));
    int* right = (int*) malloc( (high - mid) * sizeof(int));


    // n1 is size of left part and n2 is size
    // of right part
    int n1 = mid - low + 1,
    n2 = high - mid,
    i, j;

    // storing values in left part
    for (i = 0; i < n1; i++)
        left[i] = a[i + low];

    // storing values in right part
    for (i = 0; i < n2; i++)
        right[i] = a[i + mid + 1];

    int k = low;
    i = j = 0;

    // merge left and right in ascending order
    while (i < n1 && j < n2) {
        if (left[i] <= right[j])
            a[k++] = left[i++];
        else
            a[k++] = right[j++];
    }

    // insert remaining values from left
    while (i < n1) {
        a[k++] = left[i++];
    }

    // insert remaining values from right
    while (j < n2) {
        a[k++] = right[j++];
    }

    free(left);
    free(right);
}

// merge sort function
void merge_sort(int low, int high)
{
    // calculating mid point of array
    int mid = low + (high - low) / 2;
    if (low < high) {

        // calling first half
        merge_sort(low, mid);

        // calling second half
        merge_sort(mid + 1, high);

        // merging the two halves
        merge(low, mid, high);
    }
}

// thread function for multi-threading
void* merge_sort123(void* arg)
{
    // which part out of 4 parts
    int thread_part = part++;

    // calculating low and high
    int low = thread_part * (MAX / THREAD_MAX);
    int high = (thread_part + 1) * (MAX / THREAD_MAX) - 1;

    // evaluating mid point
    int mid = low + (high - low) / 2;
    if (low < high) {
        merge_sort(low, mid);
        merge_sort(mid + 1, high);
        merge(low, mid, high);
    }
    return 0;
}



// Driver Code
int main()
{
    // generating random values in array
    for (int i = 0; i < MAX; i++){
        a[i] = rand() % 100;
    //        printf("%d ", a[i]);
    }


    pthread_t threads[THREAD_MAX];

    // creating 4 threads
    for (int i = 0; i < THREAD_MAX; i++)
        pthread_create(&threads[i], NULL, merge_sort123,
                       (void*)NULL);

    // joining all 4 threads
    for (int i = 0; i < THREAD_MAX; i++)
        pthread_join(threads[i], NULL);


    ///////////////////////////////////////////////////////////////
    // --- THIS MAY BE THE PART WHERE THE MERGING IS INVALID --- //
    ///////////////////////////////////////////////////////////////
    // merging the final 4 parts
    merge(0, (MAX / 2 - 1) / 2, MAX / 2 - 1);
    merge(MAX / 2, MAX/2 + (MAX-1-MAX/2)/2, MAX - 1);
    merge(0, (MAX - 1)/2, MAX - 1);


    // displaying sorted array
    printf("\n\nSorted array: ");
    for (int i = 0; i < MAX; i++)
        printf ("%d ", a[i]);


    printf("\n");
    return 0;
}

```
</details>

### Matrix operation

#### Solving systems of linear equation

  <details>
<summary>Answer</summary>
 
```
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    char var[] = { 'x', 'y', 'z', 'w' };
    printf("Enter the number of variables in the equations: ");
    int n;
    scanf("%d", &n);
    printf("\nEnter the coefficients of each variable for each equations");
    printf("\nax + by + cz + ... = d");
    int mat[n][n];
    int constants[n][1];
    int i,j;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &mat[i][j]);
        }
        scanf("%d", &constants[i][0]);
    }
 
    printf("Matrix representation is: ");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            printf(" %f", mat[i][j]);
        }
        printf(" %f", var[i]);
        printf(" = %f", constants[i][0]);
        printf("\n");
    }
    return 0;
}
```
</details>

####  Inverting matrices

steps to find the inverse of a matrix using Gauss-Jordan method:
Interchange any two row.
Multiply each element of row by a non-zero integer.
Replace a row by the sum of itself and a constant multiple of another row of the matrix.

#### Code in cpp

<details>
<summary>Answer</summary>
	
 ```
 // C++ program to find the inverse of Matrix.
 
#include <iostream>
#include <vector>
using namespace std;
 
// Function to Print matrix.
void PrintMatrix(float** ar, int n, int m)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cout << ar[i][j] << "  ";
        }
        printf("\n");
    }
    return;
}
 
// Function to Print inverse matrix
void PrintInverse(float** ar, int n, int m)
{
    for (int i = 0; i < n; i++) {
        for (int j = n; j < m; j++) {
            printf("%.3f  ", ar[i][j]);
        }
        printf("\n");
    }
    return;
}
 
// Function to perform the inverse operation on the matrix.
void InverseOfMatrix(float** matrix, int order)
{
    // Matrix Declaration.
 
    float temp;
 
    // PrintMatrix function to print the element
    // of the matrix.
    printf("=== Matrix ===\n");
    PrintMatrix(matrix, order, order);
 
    // Create the augmented matrix
    // Add the identity matrix
    // of order at the end of original matrix.
    for (int i = 0; i < order; i++) {
 
        for (int j = 0; j < 2 * order; j++) {
 
            // Add '1' at the diagonal places of
            // the matrix to create a identity matirx
            if (j == (i + order))
                matrix[i][j] = 1;
        }
    }
 
    // Interchange the row of matrix,
    // interchanging of row will start from the last row
    for (int i = order - 1; i > 0; i--) {
 
        // Swapping each and every element of the two rows
        // if (matrix[i - 1][0] < matrix[i][0])
        // for (int j = 0; j < 2 * order; j++) {
        //
        //        // Swapping of the row, if above
        //        // condition satisfied.
        // temp = matrix[i][j];
        // matrix[i][j] = matrix[i - 1][j];
        // matrix[i - 1][j] = temp;
        //    }
 
        // Directly swapping the rows using pointers saves
        // time
 
        if (matrix[i - 1][0] < matrix[i][0]) {
            float* temp = matrix[i];
            matrix[i] = matrix[i - 1];
            matrix[i - 1] = temp;
        }
    }
 
    // Print matrix after interchange operations.
    printf("\n=== Augmented Matrix ===\n");
    PrintMatrix(matrix, order, order * 2);
 
    // Replace a row by sum of itself and a
    // constant multiple of another row of the matrix
    for (int i = 0; i < order; i++) {
 
        for (int j = 0; j < order; j++) {
 
            if (j != i) {
 
                temp = matrix[j][i] / matrix[i][i];
                for (int k = 0; k < 2 * order; k++) {
 
                    matrix[j][k] -= matrix[i][k] * temp;
                }
            }
        }
    }
 
    // Multiply each row by a nonzero integer.
    // Divide row element by the diagonal element
    for (int i = 0; i < order; i++) {
 
        temp = matrix[i][i];
        for (int j = 0; j < 2 * order; j++) {
 
            matrix[i][j] = matrix[i][j] / temp;
        }
    }
 
    // print the resultant Inverse matrix.
    printf("\n=== Inverse Matrix ===\n");
    PrintInverse(matrix, order, 2 * order);
 
    return;
}
 
// Driver code
int main()
{
    int order;
 
    // Order of the matrix
    // The matrix must be a square a matrix
    order = 3;
    /*
float matrix[20][20] = { { 5, 7, 9 },
                         { 4, 3, 8 },
                         { 7, 5, 6 },
                         { 0 } };
*/
    float** matrix = new float*[20];
    for (int i = 0; i < 20; i++)
        matrix[i] = new float[20];
 
    matrix[0][0] = 5;
    matrix[0][1] = 7;
    matrix[0][2] = 9;
    matrix[1][0] = 4;
    matrix[1][1] = 3;
    matrix[1][2] = 8;
    matrix[2][0] = 7;
    matrix[2][1] = 5;
    matrix[2][2] = 6;
 
    // Get the inverse of matrix
    InverseOfMatrix(matrix, order);
 
    return 0;
}
 ```
 </details>
	


#### Symmetric positive definite matrices and least squares approximation

Symmetric positive-definite matrices have many interesting and desirable properties. For example, they are nonsingular, and LU decomposition can be performed on them without our having to worry about dividing by 0. In this section, we shall prove several other important properties of symmetric positive-definite matrices and show an interesting application to curve fitting by a least-squares approximation.

### Linear programming
 
#### Standard and slack forms

In standard form, all the constraints are inequalities, whereas in slack form, the constraints are equalities. means that each entry of the vector x must be nonnegative.


#### Formulating problems as linear programs

You will recall from the Two Mines example that the conditions for a mathematical model to be a linear program (LP) were:

all variables continuous (i.e. can take fractional values)
a single objective (minimise or maximise)
the objective and constraints are linear i.e. any term is either a constant or a constant multiplied by an unknown.
LP's are important - this is because:

many practical problems can be formulated as LP's
there exists an algorithm (called the simplex algorithm) which enables us to solve LP's numerically relatively easily.
We will return later to the simplex algorithm for solving LP's but for the moment we will concentrate upon formulating LP's.

Some of the major application areas to which LP can be applied are:

Blending
Production planning
Oil refinery management
Distribution
Financial and economic planning
Manpower planning
Blast furnace burdening
Farm planning


#### The simplex algorithm

 To find the maximum solution of the linear program.
linear program-standard form-slack form-simplex algorithm-solution.
 
### Code in c
   <details>
<summary>Answer</summary>
 
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>
#include <assert.h>

#define M 20
#define N 20

static const double epsilon   = 1.0e-8;
int equal(double a, double b) { return fabs(a-b) < epsilon; }

typedef struct {
  int m, n; // m=rows, n=columns, mat[m x n]
  double mat[M][N];
} Tableau;

void nl(int k){ int j; for(j=0;j<k;j++) putchar('-'); putchar('\n'); }

void print_tableau(Tableau *tab, const char* mes) {
  static int counter=0;
  int i, j;
  printf("\n%d. Tableau %s:\n", ++counter, mes);
  nl(70);

  printf("%-6s%5s", "col:", "b[i]");
  for(j=1;j<tab->n; j++) { printf("    x%d,", j); } printf("\n");

  for(i=0;i<tab->m; i++) {
    if (i==0) printf("max:"); else
    printf("b%d: ", i);
    for(j=0;j<tab->n; j++) {
      if (equal((int)tab->mat[i][j], tab->mat[i][j]))
        printf(" %6d", (int)tab->mat[i][j]);
      else
        printf(" %6.2lf", tab->mat[i][j]);
      }
    printf("\n");
  }
  nl(70);
}
void read_tableau(Tableau *tab, const char * filename) {
  int err, i, j;
  FILE * fp;

  fp  = fopen(filename, "r" );
  if( !fp ) {
    printf("Cannot read %s\n", filename); exit(1);
  }
  memset(tab, 0, sizeof(*tab));
  err = fscanf(fp, "%d %d", &tab->m, &tab->n);
  if (err == 0 || err == EOF) {
    printf("Cannot read m or n\n"); exit(1);
  }
  for(i=0;i<tab->m; i++) {
    for(j=0;j<tab->n; j++) {
      err = fscanf(fp, "%lf", &tab->mat[i][j]);
      if (err == 0 || err == EOF) {
        printf("Cannot read A[%d][%d]\n", i, j); exit(1);
      }
    }
  }
  printf("Read tableau [%d rows x %d columns] from file '%s'.\n",
    tab->m, tab->n, filename);
  fclose(fp);
}

void pivot_on(Tableau *tab, int row, int col) {
  int i, j;
  double pivot;

  pivot = tab->mat[row][col];
  assert(pivot>0);
  for(j=0;j<tab->n;j++)
    tab->mat[row][j] /= pivot;
  assert( equal(tab->mat[row][col], 1. ));

  for(i=0; i<tab->m; i++) { // foreach remaining row i do
    double multiplier = tab->mat[i][col];
    if(i==row) continue;
    for(j=0; j<tab->n; j++) { // r[i] = r[i] - z * r[row];
      tab->mat[i][j] -= multiplier * tab->mat[row][j];
    }
  }
}

// Find pivot_col = most negative column in mat[0][1..n]
int find_pivot_column(Tableau *tab) {
  int j, pivot_col = 1;
  double lowest = tab->mat[0][pivot_col];
  for(j=1; j<tab->n; j++) {
    if (tab->mat[0][j] < lowest) {
      lowest = tab->mat[0][j];
      pivot_col = j;
    }
  }
  printf("Most negative column in row[0] is col %d = %g.\n", pivot_col, lowest);
  if( lowest >= 0 ) {
    return -1; // All positive columns in row[0], this is optimal.
  }
  return pivot_col;
}

// Find the pivot_row, with smallest positive ratio = col[0] / col[pivot]
int find_pivot_row(Tableau *tab, int pivot_col) {
  int i, pivot_row = 0;
  double min_ratio = -1;
  printf("Ratios A[row_i,0]/A[row_i,%d] = [",pivot_col);
  for(i=1;i<tab->m;i++){
    double ratio = tab->mat[i][0] / tab->mat[i][pivot_col];
    printf("%3.2lf, ", ratio);
    if ( (ratio > 0  && ratio < min_ratio ) || min_ratio < 0 ) {
      min_ratio = ratio;
      pivot_row = i;
    }
  }
  printf("].\n");
  if (min_ratio == -1)
    return -1; // Unbounded.
  printf("Found pivot A[%d,%d], min positive ratio=%g in row=%d.\n",
      pivot_row, pivot_col, min_ratio, pivot_row);
  return pivot_row;
}

void add_slack_variables(Tableau *tab) {
  int i, j;
  for(i=1; i<tab->m; i++) {
    for(j=1; j<tab->m; j++)
      tab->mat[i][j + tab->n -1] = (i==j);
  }
  tab->n += tab->m -1;
}

void check_b_positive(Tableau *tab) {
  int i;
  for(i=1; i<tab->m; i++)
    assert(tab->mat[i][0] >= 0);
}

// Given a column of identity matrix, find the row containing 1.
// return -1, if the column as not from an identity matrix.
int find_basis_variable(Tableau *tab, int col) {
  int i, xi=-1;
  for(i=1; i < tab->m; i++) {
    if (equal( tab->mat[i][col],1) ) {
      if (xi == -1)
        xi=i;   // found first '1', save this row number.
      else
        return -1; // found second '1', not an identity matrix.

    } else if (!equal( tab->mat[i][col],0) ) {
      return -1; // not an identity matrix column.
    }
  }
  return xi;
}

void print_optimal_vector(Tableau *tab, char *message) {
  int j, xi;
  printf("%s at ", message);
  for(j=1;j<tab->n;j++) { // for each column.
    xi = find_basis_variable(tab, j);
    if (xi != -1)
      printf("x%d=%3.2lf, ", j, tab->mat[xi][0] );
    else
      printf("x%d=0, ", j);
  }
  printf("\n");
} 

void simplex(Tableau *tab) {
  int loop=0;
  add_slack_variables(tab);
  check_b_positive(tab);
  print_tableau(tab,"Padded with slack variables");
  while( ++loop ) {
    int pivot_col, pivot_row;

    pivot_col = find_pivot_column(tab);
    if( pivot_col < 0 ) {
      printf("Found optimal value=A[0,0]=%3.2lf (no negatives in row 0).\n",
        tab->mat[0][0]);
      print_optimal_vector(tab, "Optimal vector");
      break;
    }
    printf("Entering variable x%d to be made basic, so pivot_col=%d.\n",
      pivot_col, pivot_col);

    pivot_row = find_pivot_row(tab, pivot_col);
    if (pivot_row < 0) {
      printf("unbounded (no pivot_row).\n");
      break;
    }
    printf("Leaving variable x%d, so pivot_row=%d\n", pivot_row, pivot_row);

    pivot_on(tab, pivot_row, pivot_col);
    print_tableau(tab,"After pivoting");
    print_optimal_vector(tab, "Basic feasible solution");

    if(loop > 20) {
      printf("Too many iterations > %d.\n", loop);
      break;
    }
  }
}

Tableau tab  = { 4, 5, {                     // Size of tableau [4 rows x 5 columns ]
    {  0.0 , -0.5 , -3.0 ,-1.0 , -4.0,   },  // Max: z = 0.5*x + 3*y + z + 4*w,
    { 40.0 ,  1.0 ,  1.0 , 1.0 ,  1.0,   },  //    x + y + z + w <= 40 .. b1
    { 10.0 , -2.0 , -1.0 , 1.0 ,  1.0,   },  //  -2x - y + z + w <= 10 .. b2
    { 10.0 ,  0.0 ,  1.0 , 0.0 , -1.0,   },  //        y     - w <= 10 .. b3
  }
};

int main(int argc, char *argv[]){
  if (argc > 1) { // usage: cmd datafile
    read_tableau(&tab, argv[1]);
  }
  print_tableau(&tab,"Initial");
  simplex(&tab);
  return 0;
}
 ```
 </details>
 
 #### Duality
 
 #### The intial basic feasibe solution
 
 ### Polynomials and the fft
 
 #### Representing polynomials
 
 The simple way is to represent a polynomial with degree 'n' and store the coefficient of n+1 terms of the polynomial in the array. So every array element will consist of two values: Coefficient and. Exponent.
 
 
 #### The dft and fft
 
 The discrete Fourier transform (DFT) converts a finite list of equally spaced samples of a function into the list of coefficients of a finite combination of complex sinusoids, ordered by their frequencies, that has those same sample values. It can be said to convert the sampled function from its original domain (often time or position along a line) to the frequency domain.
 
 #### Code in c (naive approach)
  <details>
<summary>Answer</summary>
 
```
 
 
 #include<stdio.h>
#include<math.h>
#define PI 3.14159265
int k = 20;
 
struct DFT_Coefficient {
    double real, img;
};
 
int main(int argc, char **argv) {
    int N = 10;
    float a, b, c;
    int i, j;
    struct DFT_Coefficient dft_val[k];
    double cosine[N];
    double sine[N];
 
    printf("Discrete Fourier Transform using naive method\n");
    printf("Enter the coefficient of simple linear function:\n");
    printf("ax + by = c\n");
    scanf("%f", &a);
    scanf("%f", &b);
    scanf("%f", &c);
    double function[N];
    for (i = 0; i < N; i++) {
        function[i] = (((a * (double) i) + (b * (double) i)) - c);
        //System.out.print( "  "+function[i] + "  ");
    }
    for (i = 0; i < N; i++) {
        cosine[i] = cos((2 * i * k * PI) / N);
        sine[i] = sin((2 * i * k * PI) / N);
    }
 
    printf("The coefficients are: ");
    for (j = 0; j < k; j++) {
        for (i = 0; i < N; i++) {
            dft_val[j].real += function[i] * cosine[i];
            dft_val[j].img += function[i] * sine[i];
        }
        printf("( %e ) - ( %e i)\n", dft_val[j].real, dft_val[j].img);
    }
    return 0;
}
 ```
 </details>
 
 #### Efficient fft implementations
 
 ### Number-therotic algorithms
 
 #### Elementric number theoritic notions
 
 Divisibility and divisors.
Prime and composite numbers.
The division theorem, remainders, and modular equivalence.
Common divisors and greatest common divisors.
Relatively prime integers.
Unique factorization.
Exercises.
Euclid's algorithm.
 
 
 #### Greatest common divisor
 
 The HCF or GCD of two integers is the largest integer that can exactly divide both numbers (without a remainder).
 
 #### Code in c
 
   <details>
<summary>Answer</summary>
 
```
#include <stdio.h>
int main()
{
    int n1, n2, i, gcd;

    printf("Enter two integers: ");
    scanf("%d %d", &n1, &n2);

    for(i=1; i <= n1 && i <= n2; ++i)
    {
        // Checks if i is factor of both integers
        if(n1%i==0 && n2%i==0)
            gcd = i;
    }

    printf("G.C.D of %d and %d is %d", n1, n2, gcd);

    return 0;
}
 ```
 </details>
 
 #### Modular arithmatic
 
 Informally, we can think of modular arithmetic as arithmetic as usual over the integers, except that if we are working modulo n, then every result x is replaced by the element of {0, 1, . . . , n - 1} that is equivalent to x, modulo n (that is, x is replaced by x mod n). This informal model is sufficient if we stick to the operations of addition, subtraction, and multiplication. A more formal model for modular arithmetic, which we now give, is best described within the framework of group theory.
 
 #### Solving modular linear equations
 
 #### The chinese remainder theoram
 
 In number theory, the Chinese remainder theorem states that if one knows the remainders of the Euclidean division of an integer n by several integers, then one can determine uniquely the remainder of the division of n by the product of these integers, under the condition that the divisors are pairwise coprime.
 
 Around A.D. 100, the Chinese mathematician  solved the problem of finding those integers x that leave remainders 2, 3, and 2 when divided by 3, 5, and 7 respectively. One such solution is x = 23; all solutions are of the form 23 + 105k for arbitrary integers k. The "Chinese remainder theorem" provides a correspondence between a system of equations modulo a set of pairwise relatively prime moduli (for example, 3, 5, and 7) and an equation modulo their product (for example, 105).

The Chinese remainder theorem has two major uses. Let the integer n = nl n2 . . . nk, where the factors ni are pairwise relatively prime. First, the Chinese remainder theorem is a descriptive "structure theorem" that describes the structure of Zn as identical to that of the Cartesian product Zn1 XZn2 X . . . X Znk with componentwise addition and multiplication modulo ni in the ith component. Second, this description can often be used to yield efficient algorithms, since working in each of the systems Zni can be more efficient (in terms of bit operations) than working modulo n.

#### Code in cpp

  <details>
<summary>Answer</summary>

```
// A C++ program to demonstrate working of Chinise remainder
// Theorem
#include<bits/stdc++.h>
using namespace std;
 
// k is size of num[] and rem[].  Returns the smallest
// number x such that:
//  x % num[0] = rem[0],
//  x % num[1] = rem[1],
//  ..................
//  x % num[k-2] = rem[k-1]
// Assumption: Numbers in num[] are pairwise coprime
// (gcd for every pair is 1)
int findMinX(int num[], int rem[], int k)
{
    int x = 1; // Initialize result
 
    // As per the Chinese remainder theorem,
    // this loop will always break.
    while (true)
    {
        // Check if remainder of x % num[j] is
        // rem[j] or not (for all j from 0 to k-1)
        int j;
        for (j=0; j<k; j++ )
            if (x%num[j] != rem[j])
               break;
 
        // If all remainders matched, we found x
        if (j == k)
            return x;
 
        // Else try next numner
        x++;
    }
 
    return x;
}
 
// Driver method
int main(void)
{
    int num[] = {3, 4, 5};
    int rem[] = {2, 3, 1};
    int k = sizeof(num)/sizeof(num[0]);
    cout << "x is " << findMinX(num, rem, k);
    return 0;
}

```
</details>
 
 #### Powers of an element
  
 #### The rsa public key cryptosystem
 
Unlike symmetric key cryptography, we do not find historical use of public-key cryptography. It is a relatively new concept.

Symmetric cryptography was well suited for organizations such as governments, military, and big financial corporations were involved in the classified communication.

With the spread of more unsecure computer networks in last few decades, a genuine need was felt to use cryptography at larger scale. The symmetric key was found to be non-practical due to challenges it faced for key management. This gave rise to the public key cryptosystems.

 #### Primality testing
 
 #### Integer factorization
 
 ### String matching
 
 #### The naive string matching algorithm
 
 Given a text txt[0..n-1] and a pattern pat[0..m-1], write a function search(char pat[], char txt[]) that prints all occurrences of pat[] in txt[]. You may assume that n > m.

Examples:

Input:  txt[] = "THIS IS A TEST TEXT"
        pat[] = "TEST"
Output: Pattern found at index 10

Input:  txt[] =  "AABAACAADAABAABA"
        pat[] =  "AABA"
Output: Pattern found at index 0
        Pattern found at index 9
        Pattern found at index 12

 
 #### Code in c
  <details>
<summary>Answer</summary>
 
```
// C program for Naive Pattern Searching algorithm
#include <stdio.h>
#include <string.h>
  
void search(char* pat, char* txt)
{
    int M = strlen(pat);
    int N = strlen(txt);
  
    /* A loop to slide pat[] one by one */
    for (int i = 0; i <= N - M; i++) {
        int j;
  
        /* For current index i, check for pattern match */
        for (j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;
  
        if (j == M) // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
            printf("Pattern found at index %d \n", i);
    }
}
  
/* Driver program to test above function */
int main()
{
    char txt[] = "AABAACAADAABAAABAA";
    char pat[] = "AABA";
    search(pat, txt);
    return 0;
}
```
</details>

 #### The rabin karp algorithm
 
 The Rabin-Karp algorithm is a string-searching algorithm that uses hashing to find patterns in strings.
 
#### CODE IN C
  <details>
<summary>Answer</summary>
 
```
#include<stdio.h>
#include<string.h>
  
// d is the number of characters in the input alphabet
#define d 256
  
/* pat -> pattern
    txt -> text
    q -> A prime number
*/
void search(char pat[], char txt[], int q)
{
    int M = strlen(pat);
    int N = strlen(txt);
    int i, j;
    int p = 0; // hash value for pattern
    int t = 0; // hash value for txt
    int h = 1;
  
    // The value of h would be "pow(d, M-1)%q"
    for (i = 0; i < M-1; i++)
        h = (h*d)%q;
  
    // Calculate the hash value of pattern and first
    // window of text
    for (i = 0; i < M; i++)
    {
        p = (d*p + pat[i])%q;
        t = (d*t + txt[i])%q;
    }
  
    // Slide the pattern over text one by one
    for (i = 0; i <= N - M; i++)
    {
  
        // Check the hash values of current window of text
        // and pattern. If the hash values match then only
        // check for characters on by one
        if ( p == t )
        {
            /* Check for characters one by one */
            for (j = 0; j < M; j++)
            {
                if (txt[i+j] != pat[j])
                    break;
            }
  
            // if p == t and pat[0...M-1] = txt[i, i+1, ...i+M-1]
            if (j == M)
                printf("Pattern found at index %d \n", i);
        }
  
        // Calculate hash value for next window of text: Remove
        // leading digit, add trailing digit
        if ( i < N-M )
        {
            t = (d*(t - txt[i]*h) + txt[i+M])%q;
  
            // We might get negative value of t, converting it
            // to positive
            if (t < 0)
            t = (t + q);
        }
    }
}
  
/* Driver Code */
int main()
{
    char txt[] = "GEEKS FOR GEEKS";
    char pat[] = "GEEK";
    
      // A prime number
    int q = 101; 
    
      // function call
    search(pat, txt, q);
    return 0;
}

```
</details>

#### String matching with finite automata

In this post, we will discuss Finite Automata (FA) based pattern searching algorithm. In FA based algorithm, we preprocess the pattern and build a 2D array that represents a Finite Automata. Construction of the FA is the main tricky part of this algorithm. Once the FA is built, the searching is simple. In search, we simply need to start from the first state of the automata and the first character of the text. At every step, we consider next character of text, look for the next state in the built FA and move to a new state. If we reach the final state, then the pattern is found in the text. The time complexity of the search process is O(n).

#### Code in c
  <details>
<summary>Answer</summary>


````
// C program for Finite Automata Pattern searching
// Algorithm
#include<stdio.h>
#include<string.h>
#define NO_OF_CHARS 256
  
int getNextState(char *pat, int M, int state, int x)
{
    // If the character c is same as next character
    // in pattern,then simply increment state
    if (state < M && x == pat[state])
        return state+1;
  
    // ns stores the result which is next state
    int ns, i;
  
    // ns finally contains the longest prefix
    // which is also suffix in "pat[0..state-1]c"
  
    // Start from the largest possible value
    // and stop when you find a prefix which
    // is also suffix
    for (ns = state; ns > 0; ns--)
    {
        if (pat[ns-1] == x)
        {
            for (i = 0; i < ns-1; i++)
                if (pat[i] != pat[state-ns+1+i])
                    break;
            if (i == ns-1)
                return ns;
        }
    }
  
    return 0;
}
  
/* This function builds the TF table which represents4
    Finite Automata for a given pattern */
void computeTF(char *pat, int M, int TF[][NO_OF_CHARS])
{
    int state, x;
    for (state = 0; state <= M; ++state)
        for (x = 0; x < NO_OF_CHARS; ++x)
            TF[state][x] = getNextState(pat, M, state, x);
}
  
/* Prints all occurrences of pat in txt */
void search(char *pat, char *txt)
{
    int M = strlen(pat);
    int N = strlen(txt);
  
    int TF[M+1][NO_OF_CHARS];
  
    computeTF(pat, M, TF);
  
    // Process txt over FA.
    int i, state=0;
    for (i = 0; i < N; i++)
    {
        state = TF[state][txt[i]];
        if (state == M)
            printf ("\n Pattern found at index %d",
                                           i-M+1);
    }
}
  
// Driver program to test above function
int main()
{
    char *txt = "AABAACAADAABAAABAA";
    char *pat = "AABA";
    search(pat, txt);
    return 0;
}
````
</details>

#### The knuth morris pratt algorithm

It is based on pattern search. if given a string  and a Pattern, we need to find the presence of pattern in
the string and hence find its indices. 

### CODE IN C
  <details>
<summary>Answer</summary>
 
```
#include<string.h>
void prefixSuffixArray(char* pat, int M, int* pps) {
   int length = 0;
   pps[0] = 0;
   int i = 1;
   while (i < M) {
      if (pat[i] == pat[length]) {
         length++;
         pps[i] = length;
         i++;
      } else {
         if (length != 0)
         length = pps[length - 1];
         else {
            pps[i] = 0;
            i++;
         }
      }
   }
}
void KMPAlgorithm(char* text, char* pattern) {
   int M = strlen(pattern);
   int N = strlen(text);
   int pps[M];
   prefixSuffixArray(pattern, M, pps);
   int i = 0;
   int j = 0;
   while (i < N) {
      if (pattern[j] == text[i]) {
         j++;
         i++;
      }
      if (j == M) {
         printf("Found pattern at index %d\n", i - j);
         j = pps[j - 1];
      }
      else if (i < N && pattern[j] != text[i]) {
         if (j != 0)
         j = pps[j - 1];
         else
         i = i + 1;
      }
   }
}
int main() {
   char text[] = "xyztrwqxyzfg";
   char pattern[] = "xyz";
   printf("The pattern is found in the text at the following index : \n");
   KMPAlgorithm(text, pattern);
   return 0;
}

```
</details>

### Computational geometry

Computational geometry is a branch of computer science devoted to the study of algorithms which can be stated in terms of geometry. ... Combinatorial computational geometry, also called algorithmic geometry, which deals with geometric objects as discrete entities.

#### Line segment propeties


#### Determining whether any pair of segment intersects

Given two line segments (p1, q1) and (p2, q2), find if the given line segments intersect with each other.

#### Code in cpp
  <details>
<summary>Answer</summary>

```
// A C++ program to check if two given line segments intersect
#include <iostream>
using namespace std;
  
struct Point
{
    int x;
    int y;
};
  
// Given three colinear points p, q, r, the function checks if
// point q lies on line segment 'pr'
bool onSegment(Point p, Point q, Point r)
{
    if (q.x <= max(p.x, r.x) && q.x >= min(p.x, r.x) &&
        q.y <= max(p.y, r.y) && q.y >= min(p.y, r.y))
       return true;
  
    return false;
}
  
// To find orientation of ordered triplet (p, q, r).
// The function returns following values
// 0 --> p, q and r are colinear
// 1 --> Clockwise
// 2 --> Counterclockwise
int orientation(Point p, Point q, Point r)
{
    // See https://www.geeksforgeeks.org/orientation-3-ordered-points/
    // for details of below formula.
    int val = (q.y - p.y) * (r.x - q.x) -
              (q.x - p.x) * (r.y - q.y);
  
    if (val == 0) return 0;  // colinear
  
    return (val > 0)? 1: 2; // clock or counterclock wise
}
  
// The main function that returns true if line segment 'p1q1'
// and 'p2q2' intersect.
bool doIntersect(Point p1, Point q1, Point p2, Point q2)
{
    // Find the four orientations needed for general and
    // special cases
    int o1 = orientation(p1, q1, p2);
    int o2 = orientation(p1, q1, q2);
    int o3 = orientation(p2, q2, p1);
    int o4 = orientation(p2, q2, q1);
  
    // General case
    if (o1 != o2 && o3 != o4)
        return true;
  
    // Special Cases
    // p1, q1 and p2 are colinear and p2 lies on segment p1q1
    if (o1 == 0 && onSegment(p1, p2, q1)) return true;
  
    // p1, q1 and q2 are colinear and q2 lies on segment p1q1
    if (o2 == 0 && onSegment(p1, q2, q1)) return true;
  
    // p2, q2 and p1 are colinear and p1 lies on segment p2q2
    if (o3 == 0 && onSegment(p2, p1, q2)) return true;
  
     // p2, q2 and q1 are colinear and q1 lies on segment p2q2
    if (o4 == 0 && onSegment(p2, q1, q2)) return true;
  
    return false; // Doesn't fall in any of the above cases
}
  
// Driver program to test above functions
int main()
{
    struct Point p1 = {1, 1}, q1 = {10, 1};
    struct Point p2 = {1, 2}, q2 = {10, 2};
  
    doIntersect(p1, q1, p2, q2)? cout << "Yes\n": cout << "No\n";
  
    p1 = {10, 0}, q1 = {0, 10};
    p2 = {0, 0}, q2 = {10, 10};
    doIntersect(p1, q1, p2, q2)? cout << "Yes\n": cout << "No\n";
  
    p1 = {-5, -5}, q1 = {0, 0};
    p2 = {1, 1}, q2 = {10, 10};
    doIntersect(p1, q1, p2, q2)? cout << "Yes\n": cout << "No\n";
  
    return 0;
}
```
</details>

#### Finding a convex hull

Given a set of points in the plane. the convex hull of the set is the smallest convex polygon that contains all the points of it.

#### Code in cpp

  <details>
<summary>Answer</summary>

```
// A C++ program to find convex hull of a set of points. Refer
// https://www.geeksforgeeks.org/orientation-3-ordered-points/
// for explanation of orientation()
#include <bits/stdc++.h>
using namespace std;
  
struct Point
{
    int x, y;
};
  
// To find orientation of ordered triplet (p, q, r).
// The function returns following values
// 0 --> p, q and r are colinear
// 1 --> Clockwise
// 2 --> Counterclockwise
int orientation(Point p, Point q, Point r)
{
    int val = (q.y - p.y) * (r.x - q.x) -
              (q.x - p.x) * (r.y - q.y);
  
    if (val == 0) return 0;  // colinear
    return (val > 0)? 1: 2; // clock or counterclock wise
}
  
// Prints convex hull of a set of n points.
void convexHull(Point points[], int n)
{
    // There must be at least 3 points
    if (n < 3) return;
  
    // Initialize Result
    vector<Point> hull;
  
    // Find the leftmost point
    int l = 0;
    for (int i = 1; i < n; i++)
        if (points[i].x < points[l].x)
            l = i;
  
    // Start from leftmost point, keep moving counterclockwise
    // until reach the start point again.  This loop runs O(h)
    // times where h is number of points in result or output.
    int p = l, q;
    do
    {
        // Add current point to result
        hull.push_back(points[p]);
  
        // Search for a point 'q' such that orientation(p, q,
        // x) is counterclockwise for all points 'x'. The idea
        // is to keep track of last visited most counterclock-
        // wise point in q. If any point 'i' is more counterclock-
        // wise than q, then update q.
        q = (p+1)%n;
        for (int i = 0; i < n; i++)
        {
           // If i is more counterclockwise than current q, then
           // update q
           if (orientation(points[p], points[i], points[q]) == 2)
               q = i;
        }
  
        // Now q is the most counterclockwise with respect to p
        // Set p as q for next iteration, so that q is added to
        // result 'hull'
        p = q;
  
    } while (p != l);  // While we don't come to first point
  
    // Print Result
    for (int i = 0; i < hull.size(); i++)
        cout << "(" << hull[i].x << ", "
              << hull[i].y << ")\n";
}
  
// Driver program to test above functions
int main()
{
    Point points[] = {{0, 3}, {2, 2}, {1, 1}, {2, 1},
                      {3, 0}, {0, 0}, {3, 3}};
    int n = sizeof(points)/sizeof(points[0]);
    convexHull(points, n);
    return 0;
}

Output: The output is points of the convex hull.
(0, 3)
(0, 0)
(3, 0)
(3, 3)


```
</details>


#### Finding the closest pair of points

We are given an array of n points in the plane, and the problem is to find out the closest pair of points in the array. This problem arises in a number of applications. For example, in air-traffic control, you may want to monitor planes that come too close together, since this may indicate a possible collision. Recall the following formula for distance between two points p and q.

 \left \|pq  \right \| = \sqrt{(p_{x}-q_{x})^{2}+ (p_{y}-q_{y})^{2}} 

The Brute force solution is O(n^2), compute the distance between each pair and return the smallest. We can calculate the smallest distance in O(nLogn) time using Divide and Conquer strategy. In this post, a O(n x (Logn)^2) approach is discussed. We will be discussing a O(nLogn) approach in a separate post.

Algorithm
Following are the detailed steps of a O(n (Logn)^2) algortihm.
Input: An array of n points P[]
Output: The smallest distance between two points in the given array.

As a pre-processing step, the input array is sorted according to x coordinates.

1) Find the middle point in the sorted array, we can take P[n/2] as middle point.

2) Divide the given array in two halves. The first subarray contains points from P[0] to P[n/2]. The second subarray contains points from P[n/2+1] to P[n-1].

3) Recursively find the smallest distances in both subarrays. Let the distances be dl and dr. Find the minimum of dl and dr. Let the minimum be d.

4) From the above 3 steps, we have an upper bound d of minimum distance. Now we need to consider the pairs such that one point in pair is from the left half and the other is from the right half. Consider the vertical line passing through P[n/2] and find all points whose x coordinate is closer than d to the middle vertical line. Build an array strip[] of all such points.

5) Sort the array strip[] according to y coordinates. This step is O(nLogn). It can be optimized to O(n) by recursively sorting and merging.

6) Find the smallest distance in strip[]. This is tricky. From the first look, it seems to be a O(n^2) step, but it is actually O(n). It can be proved geometrically that for every point in the strip, we only need to check at most 7 points after it (note that strip is sorted according to Y coordinate). See this for more analysis.
7) Finally return the minimum of d and distance calculated in the above step (step 6).

#### Code in c

  <details>
<summary>Answer</summary>
 
```
// A divide and conquer program in C/C++ to find the smallest distance from a
// given set of points.
  
#include <stdio.h>
#include <float.h>
#include <stdlib.h>
#include <math.h>
  
// A structure to represent a Point in 2D plane
struct Point
{
    int x, y;
};
  
/* Following two functions are needed for library function qsort().
   Refer: http://www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
  
// Needed to sort array of points according to X coordinate
int compareX(const void* a, const void* b)
{
    Point *p1 = (Point *)a,  *p2 = (Point *)b;
    return (p1->x - p2->x);
}
// Needed to sort array of points according to Y coordinate
int compareY(const void* a, const void* b)
{
    Point *p1 = (Point *)a,   *p2 = (Point *)b;
    return (p1->y - p2->y);
}
  
// A utility function to find the distance between two points
float dist(Point p1, Point p2)
{
    return sqrt( (p1.x - p2.x)*(p1.x - p2.x) +
                 (p1.y - p2.y)*(p1.y - p2.y)
               );
}
  
// A Brute Force method to return the smallest distance between two points
// in P[] of size n
float bruteForce(Point P[], int n)
{
    float min = FLT_MAX;
    for (int i = 0; i < n; ++i)
        for (int j = i+1; j < n; ++j)
            if (dist(P[i], P[j]) < min)
                min = dist(P[i], P[j]);
    return min;
}
  
// A utility function to find a minimum of two float values
float min(float x, float y)
{
    return (x < y)? x : y;
}
  
  
// A utility function to find the distance between the closest points of
// strip of a given size. All points in strip[] are sorted according to
// y coordinate. They all have an upper bound on minimum distance as d.
// Note that this method seems to be a O(n^2) method, but it's a O(n)
// method as the inner loop runs at most 6 times
float stripClosest(Point strip[], int size, float d)
{
    float min = d;  // Initialize the minimum distance as d
  
    qsort(strip, size, sizeof(Point), compareY); 
  
    // Pick all points one by one and try the next points till the difference
    // between y coordinates is smaller than d.
    // This is a proven fact that this loop runs at most 6 times
    for (int i = 0; i < size; ++i)
        for (int j = i+1; j < size && (strip[j].y - strip[i].y) < min; ++j)
            if (dist(strip[i],strip[j]) < min)
                min = dist(strip[i], strip[j]);
  
    return min;
}
  
// A recursive function to find the smallest distance. The array P contains
// all points sorted according to x coordinate
float closestUtil(Point P[], int n)
{
    // If there are 2 or 3 points, then use brute force
    if (n <= 3)
        return bruteForce(P, n);
  
    // Find the middle point
    int mid = n/2;
    Point midPoint = P[mid];
  
    // Consider the vertical line passing through the middle point
    // calculate the smallest distance dl on left of middle point and
    // dr on right side
    float dl = closestUtil(P, mid);
    float dr = closestUtil(P + mid, n-mid);
  
    // Find the smaller of two distances
    float d = min(dl, dr);
  
    // Build an array strip[] that contains points close (closer than d)
    // to the line passing through the middle point
    Point strip[n];
    int j = 0;
    for (int i = 0; i < n; i++)
        if (abs(P[i].x - midPoint.x) < d)
            strip[j] = P[i], j++;
  
    // Find the closest points in strip.  Return the minimum of d and closest
    // distance is strip[]
    return min(d, stripClosest(strip, j, d) );
}
  
// The main function that finds the smallest distance
// This method mainly uses closestUtil()
float closest(Point P[], int n)
{
    qsort(P, n, sizeof(Point), compareX);
  
    // Use recursive function closestUtil() to find the smallest distance
    return closestUtil(P, n);
}
  
// Driver program to test above functions
int main()
{
    Point P[] = {{2, 3}, {12, 30}, {40, 50}, {5, 1}, {12, 10}, {3, 4}};
    int n = sizeof(P) / sizeof(P[0]);
    printf("The smallest distance is %f ", closest(P, n));
    return 0;
}

```
</details>

### Np completeness

 a problem is NP-complete when: a brute-force search algorithm can solve it, 
and the correctness of each solution can be verified quickly.


#### Polynomial time

An algorithm is said to be of polynomial time if its running time is upper bounded by a polynomial expression in the size of the input for the algorithm.


#### Polynomial time verification

We now look at algorithms that "verify" membership in languages. For example, suppose that for a given instance <G, u, v, k> of the decision problem PATH, we are also given a path p from u to v. We can easily check whether the length of p is at most k, and if so, we can view p as a "certificate" that the instance indeed belongs to PATH. For the decision problem PATH, this certificate doesn't seem to buy us much. After all, PATH belongs to P- in fact, PATH can be solved in linear time-and so verifying membership from a given certificate takes as long as solving the problem from scratch. We shall now examine a problem for which we know of no polynomial-time decision algorithm yet, given a certificate, verification is easy.


#### Np completeness and reducibility

P is set of problems that can be solved by a deterministic Turing machine in Polynomial time.

NP is set of decision problems that can be solved by a Non-deterministic Turing Machine in Polynomial time. P is subset of NP (any problem that can be solved by deterministic machine in polynomial time can also be solved by non-deterministic machine in polynomial time).
Informally, NP is set of decision problems which can be solved by a polynomial time via a “Lucky Algorithm”, a magical algorithm that always makes a right guess among the given set of choices (Source Ref 1).

NP-complete problems are the hardest problems in NP set.  A decision problem L is NP-complete if:
1) L is in NP (Any given solution for NP-complete problems can be verified quickly, but there is no efficient known solution).
2) Every problem in NP is reducible to L in polynomial time (Reduction is defined below).

A problem is NP-Hard if it follows property 2 mentioned above, doesn’t need to follow property 1. Therefore, NP-Complete set is also a subset of NP-Hard set.

Let L1 and L2 be two decision problems. Suppose algorithm A2 solves L2. That is, if y is an input for L2 then algorithm A2 will answer Yes or No depending upon whether y belongs to L2 or not.
The idea is to find a transformation from L1 to L2 so that the algorithm A2 can be part of an algorithm A1 to solve L1.
Learning reduction in general is very important. For example, if we have library functions to solve certain problem and if we can reduce a new problem to one of the solved problems, we save a lot of time. Consider the example of a problem where we have to find minimum product path in a given directed graph where product of path is multiplication of weights of edges along the path. If we have code for Dijkstra’s algorithm to find shortest path, we can take log of all weights and use Dijkstra’s algorithm to find the minimum product path rather than writing a fresh code for this new problem.


#### Np completeness proofs

From the definition of NP-complete, it appears impossible to prove that a problem L is NP-Complete.  By definition, it requires us to that show every problem in NP is polynomial time reducible to L.   Fortunately, there is an alternate way to prove it.   The idea is to take a known NP-Complete problem and reduce it to L.  If polynomial time reduction is possible, we can prove that L is NP-Complete by transitivity of reduction (If a NP-Complete problem is reducible to L in polynomial time, then all problems are reducible to L in polynomial time).

#### Np complete problems

NP-complete problem, any of a class of computational problems for which no efficient solution algorithm has been found. Many significant computer-science problems belong to this class—e.g., the traveling salesman problem, satisfiability problems, and graph-covering problems.

### Approximation algorithms


#### The vertex cover problem

to find minimum subset of vertices that covers all the edges. 
(remove maximum degree vertices and all its associated edges.)
The Vertex Cover Problem is to find a subset of the vertices of a graph that contains an endpoint of every edge.

#### Code in c
  <details>
<summary>Answer</summary>
 
```
#include <stdio.h>
#include <stdlib.h>
 
/* Connect two edges */
void edge_connect(edge *edges, unsigned int first, unsigned int second, 
        unsigned int *pos)
{
    edges[*pos].first = first;
    edges[*pos].second = second;
    (*pos)++;
}
 
int main(void)
{
    const unsigned int size = 4; /* Edges */
    const unsigned int order = 5; /* Vertices */
    edge *edges = malloc(size * sizeof(edge));
    unsigned int i = 0;
    edge_connect(edges, 0, 1, &i);
    edge_connect(edges, 0, 2, &i);
    edge_connect(edges, 0, 3, &i);
    edge_connect(edges, 1, 4, &i);
    unsigned int *cover;
    unsigned int c = vertex_cover(edges, size, order, &cover);
    printf("Cover size is %u\n", c);
    printf("Vertices in cover:\n");
    for (i = 0; i < order; i++) {
        if (cover[i]) {
            printf("%u ", i);
        }
    }
    putchar('\n');
    free(edges);
    free(cover);
    return 0;
}

```
</details>

#### The travelling salesman problem

given cities and distance between them.we have to find the shortest route to visit every city only once
and return to the starting point.

#### Code in c
  <details>
<summary>Answer</summary>
 
```
#include<stdio.h>
 
int ary[10][10],completed[10],n,cost=0;
 
void takeInput()
{
	int i,j;
 
	printf("Enter the number of villages: ");
	scanf("%d",&n);
 
	printf("\nEnter the Cost Matrix\n");
 
	for(i=0;i < n;i++)
	{
		printf("\nEnter Elements of Row: %d\n",i+1);
 
		for( j=0;j < n;j++)
			scanf("%d",&ary[i][j]);
 
		completed[i]=0;
	}
 
	printf("\n\nThe cost list is:");
 
	for( i=0;i < n;i++)
	{
		printf("\n");
 
		for(j=0;j < n;j++)
			printf("\t%d",ary[i][j]);
	}
}
 
void mincost(int city)
{
	int i,ncity;
 
	completed[city]=1;
 
	printf("%d--->",city+1);
	ncity=least(city);
 
	if(ncity==999)
	{
		ncity=0;
		printf("%d",ncity+1);
		cost+=ary[city][ncity];
 
		return;
	}
 
	mincost(ncity);
}
 
int least(int c)
{
	int i,nc=999;
	int min=999,kmin;
 
	for(i=0;i < n;i++)
	{
		if((ary[c][i]!=0)&&(completed[i]==0))
			if(ary[c][i]+ary[i][c] < min)
			{
				min=ary[i][0]+ary[c][i];
				kmin=ary[c][i];
				nc=i;
			}
	}
 
	if(min!=999)
		cost+=kmin;
 
	return nc;
}
 
int main()
{
	takeInput();
 
	printf("\n\nThe Path is:\n");
	mincost(0); //passing 0 because starting vertex
 
	printf("\n\nMinimum cost is %d\n ",cost);
 
	return 0;
}

```
</details>

#### The set covering problem

the set cover problem is to identify the smallest sub-collection of S whose union equals the universe.
 For example, consider the universe U={1,2,3,4,5} and the collection of set S={{1,2,3},{2,4},{3,4},{4,5}. Clearly the union of S is U.


#### Code in c
  <details>
<summary>Answer</summary>
 
```
#include <stdio.h>
#include <stdlib.h>
#include <assert.h>
#include <string.h>
#include <stdbool.h>
#include <signal.h>

//buffer used by input statements
char inbuf[1024];
char _file[1024];

typedef struct Set Set;

struct Set /* the state of the game at each possible move */
{
	int nGlobalSetSize;
	int nSubSets;
	int* originalOrder;
	int* nSubSetSizes;
	int** subsets;
	int** subSetsSizesSum;
};

typedef struct Solution Solution;
struct Solution
{
	int nSolutionSize;
	int* subSets;
	int* boolIncluded;
};

Set* set;
Solution* solution;
Solution* bestSolution;

bool GetALine(FILE *f, char buf[]);
void readGameFile(const char *s);
void init_args(int argc, char **argv);
void echoInit();
void printSubSet(int nSubSetIndex);
void printSolution(Solution* solution);
bool checkSolution(Solution* solution);
bool containsSubSet(Solution* solution, int subSetIndex);
void addSubSet(Solution* solution, int subSetIndex);
void removeSubSet(Solution* solution, int subSetIndex);
void backTrack(Solution* solution);
void backTrack3(Solution* solution, int last);
void backTrack4(Solution* solution, int last, int sum);
void createSolutionStruct();
void copySolutionToBest();
void sortSubSets();
void greedy();
int numberOfUncoveredElements(int subSetIndex);

void intHandler(int dummy) {
	printSolution(bestSolution);
    exit(0);
}

int main(int argc, char *argv[]) {

	signal(SIGINT, intHandler);

	init_args(argc, argv);
	readGameFile(_file);
	sortSubSets();
	//echoInit();
	createSolutionStruct();

	greedy();

	backTrack4(solution, 0, 0);

	printSolution(bestSolution);
	printf("\n");

	return 0;
}

void greedy() {
	int i;
	int temp;
	bestSolution->nSolutionSize = 0;
	addSubSet(bestSolution, 0);
	int addIndex = 0;
	int addNumber = 0;

	while(!checkSolution(bestSolution)) {
		addIndex = 0;
		addNumber = 0;
		for(i=0; i<set->nSubSets; i++) {
			if(!containsSubSet(bestSolution, i)) {
				temp = numberOfUncoveredElements(i);
				if(temp > addNumber) {
					addNumber = temp;
					addIndex = i;
				}
			}
		}
		addSubSet(bestSolution, addIndex);
	}
	//printSolution(bestSolution);
}

int numberOfUncoveredElements(int subSetIndex) {
	int i;
	int count=0;

	for(i=0; i<set->nSubSetSizes[subSetIndex]; i++) {
		if(!bestSolution->boolIncluded[set->subsets[subSetIndex][i] - 1])
			count++;
	}

	return count;
}

//This sorts the subsets by size
void sortSubSets() {
	int i,j;
	int tempInt;
	int* tempIntP;
	for(i=0; i<set->nSubSets;++i) {
		for(j=i+1; j<set->nSubSets; ++j) {
			if(set->nSubSetSizes[i] < set->nSubSetSizes[j]) {
				tempInt = set->nSubSetSizes[i];
				tempIntP = set->subsets[i];
				set->subsets[i] = set->subsets[j];
				set->subsets[j] = tempIntP;
				set->nSubSetSizes[i] = set->nSubSetSizes[j];
				set->nSubSetSizes[j] = tempInt;
				tempInt = set->originalOrder[i];
				set->originalOrder[i] = set->originalOrder[j];
				set->originalOrder[j] = tempInt;
			}
		}
	}
	//Get Memory for sizes table
	set->subSetsSizesSum = (int **) malloc(sizeof(int *) * set->nSubSets);
	for(i=0; i<set->nSubSets; i++) {
		set->subSetsSizesSum[i] = (int *) malloc(sizeof(int) * set->nSubSets);
		memset(set->subSetsSizesSum[i], 0, set->nSubSets);
	}

	for(i=0; i<set->nSubSets; i++) {
		tempInt = 0;
		for(j=i; j<set->nSubSets; j++) {
			tempInt += set->nSubSetSizes[j];
			set->subSetsSizesSum[i][j-i] = tempInt;
		}
	}

	//Check
	/*for(i=0; i<set->nSubSets; i++) {
		for(j=0; j<set->nSubSets; j++) {
			printf("%u ", set->subSetsSizesSum[i][j]);
		}
		printf("\n");
	}*/
}

void createSolutionStruct() {
	int i;
	solution = malloc(sizeof(Solution));
	solution->subSets = malloc(sizeof(int) * (set->nSubSets));
	for(i=0; i<(set->nSubSets); i++)
		solution->subSets[i] = -1;
	solution->boolIncluded = malloc(sizeof(int) * set->nGlobalSetSize);
	memset(solution->boolIncluded, 0, set->nGlobalSetSize);

	bestSolution = malloc(sizeof(Solution));
	bestSolution->subSets = malloc(sizeof(int) * (set->nSubSets));
	for (i = 0; i < (set->nSubSets); i++)
		bestSolution->subSets[i] = -1;
	bestSolution->boolIncluded = malloc(sizeof(int) * set->nGlobalSetSize);
	memset(bestSolution->boolIncluded, 0, set->nGlobalSetSize);
	bestSolution->nSolutionSize = set->nSubSets-1;
}

void copySolutionToBest() {
	int i;
	bestSolution->nSolutionSize = solution->nSolutionSize;
	for(i=0;i<solution->nSolutionSize;i++)
		bestSolution->subSets[i] = solution->subSets[i];
}

int depth = 0;

void backTrack(Solution* solution) {
	int i;

	if(solution->nSolutionSize >= bestSolution->nSolutionSize)
		return;

	if(checkSolution(solution)) {
		if(solution->nSolutionSize < bestSolution->nSolutionSize)
			copySolutionToBest();
	}

	for(i=0; i<set->nSubSets; i++) {
		if(!containsSubSet(solution, i)) {
			//add subset to solution
			addSubSet(solution, i);
			//recure
			depth++;
			backTrack(solution);
			depth--;
			//remove solution
			removeSubSet(solution, i);
		}
	}
}

void backTrack2(Solution* solution) {
	int i;

	if(solution->nSolutionSize >= bestSolution->nSolutionSize)
		return;

	if(checkSolution(solution)) {
		if(solution->nSolutionSize < bestSolution->nSolutionSize)
			copySolutionToBest();
	}

	for(i=depth; i<set->nSubSets; i++) {
		//if(!containsSubSet(solution, i)) {
			//add subset to solution
			addSubSet(solution, i);
			//recure
			depth++;
			backTrack2(solution);
			depth--;
			//remove solution
			removeSubSet(solution, i);
		//}
	}
}

void backTrack3(Solution* solution, int last) {
	int i;

	if(solution->nSolutionSize >= bestSolution->nSolutionSize)
		return;

	if(checkSolution(solution)) {
		if(solution->nSolutionSize < bestSolution->nSolutionSize) {
			copySolutionToBest();
		}
		return;
	}

	for(i=last; i<set->nSubSets; i++) {
		//add subset to solution
		addSubSet(solution, i);
		//recure
		backTrack3(solution, i + 1);
		//remove solution
		removeSubSet(solution, i);
	}
}

void backTrack4(Solution* solution, int last, int sum) {
	int i;

	if(solution->nSolutionSize >= bestSolution->nSolutionSize)
		return;

	if(checkSolution(solution)) {
		if(solution->nSolutionSize < bestSolution->nSolutionSize) {
			copySolutionToBest();
			printf("New Solution Size : %u\n",bestSolution->nSolutionSize);
		}
		return;
	}

	for(i=last; i<set->nSubSets; i++) {
		if(sum+set->subSetsSizesSum[i][(bestSolution->nSolutionSize-1)-solution->nSolutionSize] < set->nGlobalSetSize)
			return;
		//add subset to solution
		addSubSet(solution, i);
		sum+=set->nSubSetSizes[i];
		//recure
		backTrack4(solution, i + 1, sum);
		sum-=set->nSubSetSizes[i];
		//remove solution
		removeSubSet(solution, i);
	}
}

void addSubSet(Solution* solution, int subSetIndex) {
	int i;
	solution->nSolutionSize++;
	solution->subSets[solution->nSolutionSize-1] = subSetIndex;

	for(i=0; i<set->nSubSetSizes[subSetIndex]; i++) {
		solution->boolIncluded[set->subsets[subSetIndex][i] - 1] += 1;
	}

	/*for(i=0; i<set->nSubSetSizes[subSetIndex]; i++) {
		printf("%u ",solution->boolIncluded[i]);
	}
	printf("\n");*/
}

void removeSubSet(Solution* solution, int subSetIndex) {
	int i;
	solution->subSets[solution->nSolutionSize-1] = -1;
	solution->nSolutionSize--;

	for(i=0; i<set->nSubSetSizes[subSetIndex]; i++) {
		solution->boolIncluded[set->subsets[subSetIndex][i] - 1] -= 1;
	}
}

bool containsSubSet(Solution* solution, int subSetIndex) {
	int i;

	for(i=0; i<solution->nSolutionSize; i++) {
		if(solution->subSets[i] == subSetIndex) {
			return true;
		}
	}

	return false;
}

bool checkSolution(Solution* solution) {
	int i;
	bool allDone = true;
	for(i=0; i<set->nGlobalSetSize; i++) {
		int boolInc = solution->boolIncluded[i];
		if(boolInc == 0) {
			return false;
		}
	}
	return allDone;
}

void printSolution(Solution* solution) {
	int i;
	printf("(%u)\n",solution->nSolutionSize);

	for(i=0; i<solution->nSolutionSize; i++) {
		printf("(%u) ", set->originalOrder[solution->subSets[i]]);
		printSubSet(solution->subSets[i]);
	}
}

void echoInit() {
	int i;
	printf("Universal Set 1-%u\n",set->nGlobalSetSize);
	printf("Number of subsets %u\n",set->nSubSets);
	for(i=0; i<set->nSubSets; i++) {
		printSubSet(i);
	}
}

void printSubSet(int nSubSetIndex) {
	int j;
	for (j = 0; j < set->nSubSetSizes[nSubSetIndex]; j++) {
		printf("%u ", set->subsets[nSubSetIndex][j]);
	}
	printf("\n");
}

bool GetALine(FILE *f, char buf[]) {
	/* Read a line of possibly commented input from the file *f.*/
	char *p;
	bool not_eof = false;
	while ( fgets(buf, 1024, f) != NULL) {
		p=strchr(buf, (int) '\n');
		if ( p != NULL )
			*p = '\0';

		if (*buf != '\0') {
			not_eof = true;
			break;
		}
	}
	return (not_eof);
}

void readGameFile(const char *s) {
	FILE *f;
	int lineno=0, i=0;
	int subSetSize=0;
	int nCurrSubSet=0;
	char * pch;
	char buf[1024];

	if(s==NULL)
		exit(1);

	f = fopen(s, "r");
	if(f == NULL) {
		printf("Could not open file");
		exit(1);
	}

	set = malloc(sizeof(Set));

	while(GetALine(f, inbuf)) {

		switch(lineno) {
		case 0:
			set->nGlobalSetSize = atoi(inbuf);
			break;
		case 1:
			set->nSubSets = atoi(inbuf);
			set->nSubSetSizes = (int *) malloc(sizeof(int) * set->nSubSets);
			set->originalOrder = (int *) malloc(sizeof(int) * set->nSubSets);
			for(i=0; i<set->nSubSets; i++) {
				set->originalOrder[i] = i+1;
			}
			set->subsets = (int**) malloc(sizeof(int*) * set->nSubSets);
			break;
		default:
			subSetSize = 0;
			strcpy(buf, inbuf);

			pch = strtok(inbuf, " ");
			while (pch != NULL) {
				subSetSize++;
				pch = strtok(NULL, " ");
			}

			set->nSubSetSizes[nCurrSubSet] = subSetSize;
			set->subsets[nCurrSubSet] = (int *) malloc(sizeof(int) * subSetSize);

			i = 0;
			pch = strtok(buf, " ");
			while (pch != NULL) {
				set->subsets[nCurrSubSet][i] = atoi(pch);
				i++;
				pch = strtok(NULL, " ");
			}

			nCurrSubSet++;
		}

		lineno++;
	}
}

void init_args(int argc, char **argv) {

	char str[1024], *opts[] = { "-f" }; /* valid options */
	int valopts[] = { 1 }; /* indicates options with values */
	/* 0=none, 1=required, -1=optional */
	int i, /* looper through all cmdline arguments */
	a, /* current valid argument-value position */
	op, /* position number of found option */
	nopts = sizeof(opts) / sizeof(char *);

	a = 1;
	for (i = 1; i <= nopts; i++) {
		if (a >= argc)
			break;

		/* figure out which option by its position 0-(nopts-1) */
		for (op = 0; op < nopts; op++) {
			if (strncmp(opts[op], argv[a], 2) == 0)
				break; /* found it, move on */
		}
		if (op == nopts) {
			fprintf(stderr, "Invalid option %s\n", argv[a]);
			printf("%s", "Pancake requires an input file. Use -f filename.txt");
			exit(-1);
		}

		*str = '\0';
		/* extract value part of option-value pair */
		if (valopts[op]) {
			if ('\0' != argv[a][2]) { /* no space betw opt-value */
				strcpy(str, (argv[a] + 2));
			} else if ('-' != *argv[a + 1]) { /* space betw opt-value */
				strcpy(str, argv[++a]);
			} else if (0 < valopts[op]) { /* required opt-val not found */
				fprintf(stderr, "Incomplete option %s\n", opts[op]);
				printf("%s", "Pancake requires an input file. Use -f filename.txt");
				exit(-1);
			} /* opt-val not required */
		}

		/* tell us what to do here                   */
		/* set indicators/variables based on results */
		switch (op) {
		case 0: /* -d */
			strcpy(_file, str);
			break; /* -f */
		default:
			fprintf(stderr, "Programmer: bad option in main:init_args:switch");
		}

		a++; /* move to next valid arg-value position */

	} /* end for(i) */
}

```
</details>

#### The subset-sum problem

to find the subset of given set whose sum is equal to given number.

#### Code in c
<details>
<summary>Answer</summary>
	
```
#include < stdio.h >

void sumOfSub(int,int,int);
static int m=0;
int*w;
int*x;
void main()
{ int i=0,sum=0,n=0;
 printf("Enter size of array: ");
 scanf("%d",&n);
 w=(int*)malloc(sizeof(int)*n+1);
 x=(int*)malloc(sizeof(int)*n+1);
 printf("Enter %d elements: ",n);
 for(i=1;i < =n;i++)
 {
  scanf("%d",&w[i]);
  sum+=w[i];
  x[i]=0;
 }
 printf("Enter the sum to be obtained: ");
 scanf("%d",&m);
 if(sum < m)
 {
 printf("Not possible to obtain any subset !!! ");
 exit(1);
 }
 printf("Possible Subsets are( 0 indicates exclusion and 1 indicates inclusion) : ");
 sumOfSub(0,1,sum);
}

void sumOfSub(int s,int k,int r)
{ int i=0;
 x[k]=1;
 if(s+w[k]==m)
 { printf("\n");
  for(i=1;i < =k;i++)
  printf("\t%d",x[i]);
 }
 else if((s+w[k]+w[k+1]) < =m)
 {
  sumOfSub(s+w[k],k+1,r-w[k]);
 }
 if((s+r-w[k]) > =m && (s+w[k+1]) < =m)
 {
  x[k]=0;
  sumOfSub(s,k+1,r-w[k]);
 }
}
	
```
</details>	

####  Randomization and linear programming

In this section, we study two techniques that are useful in designing approximation algorithms: randomization and linear programming. We will give a simple randomized algorithm
for an optimization version of 3-CNF satisfiability, and then we will use linear programming to help design an approximation algorithm for a weighted version of the vertex
cover problem. This section only scratches the surface of these two powerful techniques. The chapter notes give references for further study of these areas.



























