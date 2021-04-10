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

HEAP SORT:Heap sort can be understood as the improved version of the binary search tree. It does not create a node as in case of binary search tree instead it builds the heap by adjusting the position of elements within the array itself.
### CODE IN C:
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
 
 QUICK SORT:follows divide and conquer strategy.
starting from the first element(pivot);
It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, 
according to whether they are less than or greater than the pivot. ... The sub-arrays are then sorted recursively.
### CODE IN C
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
 
## BINARY SEARCH TREE
it is a binary tree in which each node is having value lesser than itself at left side and greater
than itself at right hand side.

### CODE IN C
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
 
RED BLACK TREES: A red-black tree is a kind of self-balancing binary search tree where each node has an extra bit, and that bit is often interpreted as the colour (red or black). These colours are used to ensure that the tree remains balanced during insertions and deletions. Although the balance of the tree is not perfect, it is good enough to reduce the searching time and maintain it around O(log n) time, where n is the total number of elements in the tree. This tree was invented in 1972 by Rudolf Bayer. 

It must be noted that as each node requires only 1 bit of space to store the colour information. 

Rules That Every Red-Black Tree Follows: 
Every node has a colour either red or black.
The root of the tree is always black.
There are no two adjacent red nodes (A red node cannot have a red parent or red child).
Every path from a node (including root) to any of its descendants NULL nodes has the same number of black nodes.
 
 
### CODE IN C(INSERTION)

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
 
 ## DYNAMIC PROGRAMMING
 storing intermediate results and using it for solving further sub problems.ex: fibonacci series.
 
 ROD CUTTING:Given a rod of length n inches and an array of prices that contains prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces
 
 ### CODE IN C
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
 
 LONGEST COMMON SUBSEQUENCE:given two sequenceS, find the longest common terms between them.
 Example: ABCDEF & ABC
 Answer: ABC
 
 ### CODE IN C
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
 ## GREEDY ALGORITHM
 Used for solving optimizing problems which either require max result or min result.
1.AN ACTIVITY SELECTION PROBLEM:You are given n activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time.
  ### CODE IN C:
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

## B-TREES
Balanced tree: guidelines to make m-way search trees are known as b-trees.(dynamic multilevel index).
{B-tree is a special type of self-balancing search tree in which each node can contain more than one key and can have more than two children. It is a generalized form of the binary search tree.}
### CODE IN C
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
FIBONACCI HEAPS:linked list of heap ordered trees.(min heap)
Fibonacci Heap is a collection of trees with min-heap or max-heap property. In Fibonacci Heap, trees can can have any shape even all trees can be single nodes.
 ### CODE IN C
 
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
 
 ## ELEMENTARY GRAPH ALGORITHMS
 BREADTH FIRST SEARCH:first we will visit the vertex,explore it and then MOVE ON to another vertex then explore it.
(level order on a binary tree.)
 
 ### CODE IN  C
  
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
 
 DEPTH FIRST SEARCH:first visit all the vertex then explore it.
 (preorder traversal of the graph.)
### CODE IN C
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
 
 MINIMUM SPANNING TREE: Sub graph of graphs having n elements but {n-1} edges.
 
 KRUSKAL ALGORITHM:Kruskal's algorithm finds a minimum spanning forest of an undirected edge-weighted graph. If the graph is connected, it finds a minimum spanning tree.
 It is a greedy algorithm in graph theory as in each step it adds the next lowest-weight edge that will not form a cycle to the minimum spanning forest.
 ### CODE IN C
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
 
 PRIM'S ALGORITHM:Prim's Algorithm is a famous greedy algorithm. It is used for finding the Minimum Spanning Tree (MST) of a given graph. To apply Prim's algorithm, the given graph must be weighted, connected and undirected.
 ### CODE IN C
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
 
 THE BELLMAN-FORD ALGORITHM:gives shortest path from one node to all other nodes. works on negative edge weights.
 ( works by overestimating the length of the path from the starting vertex to all other vertices. )
 ### CODE IN C
 
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
 
 DIJKSTRA'S ALGORITHM: Single source shortest path algorithm. does not works on negative weights.
{minimization problem-optimization problem-greedy method-solved in stages by taking one step at a time and considering one input
at a time to get an optimal solution}
### CODE IN  C
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
 
 MAXIMUM BIPARTITE ALGORITHM:
 an undirected graph is bipartite if there exists partition into left and right such that every edge has one vertex in left and one in right.
(no odd length cycles,2 colors).
 
 SIMPLEX ALGORITHM:To find the maximum solution of the linear program.
linear program-standard form-slack form-simplex algorithm-solution.
 
### CODE IN C 
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
 THE RABIN-KARP ALGORITHM:The Rabin-Karp algorithm is a string-searching algorithm that uses hashing to find patterns in strings.
 
### CODE IN C
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
KNUTH-MORRIS-PRATT ALGORITHM: It is based on pattern search. if given a string  and a Pattern, we need to find the presence of pattern in
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

THE VERTEX COVER PROBLEM:to find minimum subset of vertices that covers all the edges. 
(remove maximum degree vertices and all its associated edges.)
The Vertex Cover Problem is to find a subset of the vertices of a graph that contains an endpoint of every edge.

### CODE IN C
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
THE TRAVELLING SALESMAN PROBLEM:given cities and distance between them.we have to find the shortest route to visit every city only once
and return to the starting point.

### CODE IN C
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
THE SET COVERING PROBLEM:the set cover problem is to identify the smallest sub-collection of S whose union equals the universe.
 For example, consider the universe U={1,2,3,4,5} and the collection of set S={{1,2,3},{2,4},{3,4},{4,5}. Clearly the union of S is U.


### CODE IN C
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

THE SUBSET SUM PROBLEM:to find the subset of given set whose sum is equal to given number.

### CODE IN C
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
</details.	


























