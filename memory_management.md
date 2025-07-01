
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

## First-Fit Memory Allocation

```c
#include <stdio.h>
#define SIZE 5

void firstFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[n];
    for (int i = 0; i < n; i++) allocation[i] = -1;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (blockSize[j] >= processSize[i]) {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                break;
            }
        }
    }

    for (int i = 0; i < n; i++) {
        printf("Process %d -> Block ", i + 1);
        if (allocation[i] != -1) printf("%d\n", allocation[i] + 1);
        else printf("Not Allocated\n");
    }
}
```

---

## Best-Fit Memory Allocation

```c
#include <stdio.h>
#define SIZE 5

void bestFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[n];
    for (int i = 0; i < n; i++) allocation[i] = -1;

    for (int i = 0; i < n; i++) {
        int bestIdx = -1;
        for (int j = 0; j < m; j++) {
            if (blockSize[j] >= processSize[i]) {
                if (bestIdx == -1 || blockSize[j] < blockSize[bestIdx])
                    bestIdx = j;
            }
        }
        if (bestIdx != -1) {
            allocation[i] = bestIdx;
            blockSize[bestIdx] -= processSize[i];
        }
    }

    for (int i = 0; i < n; i++) {
        printf("Process %d -> Block ", i + 1);
        if (allocation[i] != -1) printf("%d\n", allocation[i] + 1);
        else printf("Not Allocated\n");
    }
}
```

---

## Worst-Fit Memory Allocation

```c
#include <stdio.h>
#define SIZE 5

void worstFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[n];
    for (int i = 0; i < n; i++) allocation[i] = -1;

    for (int i = 0; i < n; i++) {
        int worstIdx = -1;
        for (int j = 0; j < m; j++) {
            if (blockSize[j] >= processSize[i]) {
                if (worstIdx == -1 || blockSize[j] > blockSize[worstIdx])
                    worstIdx = j;
            }
        }
        if (worstIdx != -1) {
            allocation[i] = worstIdx;
            blockSize[worstIdx] -= processSize[i];
        }
    }

    for (int i = 0; i < n; i++) {
        printf("Process %d -> Block ", i + 1);
        if (allocation[i] != -1) printf("%d\n", allocation[i] + 1);
        else printf("Not Allocated\n");
    }
}
```

---

## Next-Fit Memory Allocation

```c
#include <stdio.h>
#define SIZE 5

void nextFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[n];
    for (int i = 0; i < n; i++) allocation[i] = -1;
    int j = 0;

    for (int i = 0; i < n; i++) {
        int count = 0;
        while (count < m) {
            if (blockSize[j] >= processSize[i]) {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                break;
            }
            j = (j + 1) % m;
            count++;
        }
    }

    for (int i = 0; i < n; i++) {
        printf("Process %d -> Block ", i + 1);
        if (allocation[i] != -1) printf("%d\n", allocation[i] + 1);
        else printf("Not Allocated\n");
    }
}
```
