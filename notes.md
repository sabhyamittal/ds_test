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
 #### GREEDY ALGORITHM
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
FIBONACCI HEAPS:
 
 

