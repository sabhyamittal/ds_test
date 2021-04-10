# Introduction to Algorithms

## The role of algorithm in computing
 Algorithms are definite number of steps to solve a given problem in definite amount of time.For example:The travelling salesman problem,
 which finds out the shortest path /route between two cities hence it is used by GPS which is used all over globe.

### Getting Started
INSERTION SORT:Efficient algorithm for sorting small number of elements.EX: sorting a deck of cards.

#### CODE FOR INSERTION SORT IN C
<details>
<summary>Answer</summary>
void insertionSort(int arr[], int n)
{
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
 
        /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
 
// A utility function to print an array of size n
void printArray(int arr[], int n)
{
    int i;
    for (i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}
 
/* Driver program to test insertion sort */
int main()
{
    int arr[] = { 12, 11, 13, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
 
    insertionSort(arr, n);
    printArray(arr, n);
 
    return 0;
}

</details>

