
# Dynamic Memory Allocation in C

## Demonstrate dynamic memory allocation using `malloc()`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = (int *)malloc(sizeof(int));
    if (ptr == NULL) {
        printf("Memory not allocated.\n");
        return 1;
    }
    *ptr = 42;
    printf("Value: %d\n", *ptr);
    free(ptr);
    return 0;
}
```

---

## Allocate memory for an array using `calloc()`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 5;
    int *arr = (int *)calloc(n, sizeof(int));
    if (arr == NULL) {
        printf("Memory not allocated.\n");
        return 1;
    }

    for (int i = 0; i < n; i++)
        printf("arr[%d] = %d\n", i, arr[i]); // Initialized to 0

    free(arr);
    return 0;
}
```

---

## Resize memory using `realloc()`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr = (int *)malloc(2 * sizeof(int));
    if (arr == NULL) return 1;

    arr[0] = 1; arr[1] = 2;

    arr = (int *)realloc(arr, 4 * sizeof(int));
    if (arr == NULL) return 1;

    arr[2] = 3; arr[3] = 4;

    for (int i = 0; i < 4; i++)
        printf("arr[%d] = %d\n", i, arr[i]);

    free(arr);
    return 0;
}
```

---

## Allocate memory for a linked list node

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

int main() {
    struct Node* head = (struct Node *)malloc(sizeof(struct Node));
    if (head == NULL) {
        printf("Memory not allocated.\n");
        return 1;
    }

    head->data = 10;
    head->next = NULL;

    printf("Node data: %d\n", head->data);
    free(head);
    return 0;
}
```
