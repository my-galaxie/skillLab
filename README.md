# C Program to Remove Duplicates from a Sorted Linked List (User Input)

## 📘 Description

This C program allows the user to input a sorted linked list and removes duplicate elements. The user specifies the number of elements and provides values in sorted order. The program then processes the list and removes adjacent duplicates.

## 🧠 Algorithm

1. Input the number of nodes from the user.
2. Input node values in **sorted order**.
3. Create a linked list using the input.
4. Traverse the list:
    - If a node has the same value as the next node, remove the next node.
5. Print the final list without duplicates.

## 📦 Code

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

// Create a new node
struct Node* newNode(int data) {
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->next = NULL;
    return node;
}

// Append a node to the end of the list
void append(struct Node** head_ref, int new_data) {
    struct Node* new_node = newNode(new_data);
    struct Node* last = *head_ref;

    if (*head_ref == NULL) {
        *head_ref = new_node;
        return;
    }

    while (last->next != NULL)
        last = last->next;

    last->next = new_node;
}

// Remove duplicates from a sorted linked list
void removeDuplicates(struct Node* head) {
    struct Node* current = head;

    while (current != NULL && current->next != NULL) {
        if (current->data == current->next->data) {
            struct Node* next_next = current->next->next;
            free(current->next);
            current->next = next_next;
        } else {
            current = current->next;
        }
    }
}

// Print the linked list
void printList(struct Node* node) {
    while (node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;
    int n, value;

    printf("Enter the number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements in sorted order:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &value);
        append(&head, value);
    }

    printf("\nOriginal Linked List:\n");
    printList(head);

    removeDuplicates(head);

    printf("\nLinked List after removing duplicates:\n");
    printList(head);

    return 0;
}
