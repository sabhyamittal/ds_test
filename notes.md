# Introduction to Algorithms

## The role of algorithm in computing
 Algorithms are definite number of steps to solve a given problem in definite amount of time.For example:The travelling salesman problem,
 which finds out the shortest path /route between two cities hence it is used by GPS which is used all over globe.

### Getting Started
INSERTION SORT:Efficient algorithm for sorting small number of elements.EX: sorting a deck of cards.

#### CODE FOR INSERTION SORT IN C
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

## DIVIDE AND CONQUER
### THE MAXIMUM SUBARRAY PROBLEM
To find a subarray of the given array whose sum is maximum.
By divide and conquer->find the center indices->max on the LHS and RHS->sum of max.

### CODE IN C
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
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

