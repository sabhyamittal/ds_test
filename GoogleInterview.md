### Most Asked topics:
- Sorting, searching, divide-and-conquer, dynamic 
 programming/memoization or algorithms linked 
 to a specific data structure. 
 
- Big-O notations (e.g. run time complexity). We 
 recommend discussing or outlining the 
 algorithm you have in mind before writing code.
 
- Algorithm Complexity, Design, & Analysis: It's 
 fairly critical that you understand big-O 
 complexity analysis. Again run some practice 
 problems to get this down in application.
 
- Recursion and using it to find more elegant 
 solutions to problems that can be solved 
 iteratively.
 
- Know how hashtables work. Be able to 
 implement one using only arrays in your favorite 
 language, in about the space of one interview.
 
- Common sorting functions; what kind of input 
 data they’re efficient on. Think about what 
 efficiency means in terms of runtime/space 
 used. (ie. In exceptional cases insertion-sort or 
 radix-sort are better than generic QuickSort 
 /MergeSort/HeapSort. Don't do bubble-sort. You 
 should know the details of at least one n*log(n) 
 sorting algorithm, preferably two (ie. quicksort & 
 merge sort).
 
- Trees: Know about trees; basic tree 
 construction, traversal and manipulation 
 algorithms. Familiarize yourself with binary 
 trees, n-ary trees, and trie-trees. Be familiar with 
 at least one type of balanced binary tree, 
 whether it's a red/black tree, a splay tree or an 
 AVL tree, and know how it's implemented. 
 Understand tree traversal algorithms: BFS and 
 DFS, and know the difference between inorder, 
 postorder and preorder.
 #### Quick sort
 follows divide and conquer strategy
Best Case Complexity [Big-omega]: O(nlog n) It occurs when the pivot element is always the middle element or near to the middle element. Average Case Complexity [Big-theta]: O(nlog n) It occurs when the above conditions do not occur. 2. Space Complexity The space complexity for quicksort is O(log n).
 <details>
 <summary>code in c++ </summary>
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
 
 <details>
  <summary>code in python</summary>
  ```
  def partition(arr, low, high):
    i = (low-1)         # index of smaller element
    pivot = arr[high]     # pivot
 
    for j in range(low, high):
 
        # If current element is smaller than or
        # equal to pivot
        if arr[j] <= pivot:
 
            # increment index of smaller element
            i = i+1
            arr[i], arr[j] = arr[j], arr[i]
 
    arr[i+1], arr[high] = arr[high], arr[i+1]
    return (i+1)
 
# The main function that implements QuickSort
# arr[] --> Array to be sorted,
# low  --> Starting index,
# high  --> Ending index
 
# Function to do Quick sort
 
 
def quickSort(arr, low, high):
    if len(arr) == 1:
        return arr
    if low < high:
 
        # pi is partitioning index, arr[p] is now
        # at right place
        pi = partition(arr, low, high)
 
        # Separately sort elements before
        # partition and after partition
        quickSort(arr, low, pi-1)
        quickSort(arr, pi+1, high)
 
 
# Driver code to test above
arr = [10, 7, 8, 9, 1, 5]
n = len(arr)
quickSort(arr, 0, n-1)
print("Sorted array is:")
for i in range(n):
    print("%d" % arr[i])
                  
```
</details>                  
 
 #### Merge sort
 
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### Heap sort
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### Insertion sort
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### Radix sort
 
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 #### Binary Tree
 
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### Binary search tree
 
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### AVL tree
 
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### BFS
 
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
 
 #### DFS
 <details>
 <summary>code in c++ </summary>
 ```
 ```
 </details>
