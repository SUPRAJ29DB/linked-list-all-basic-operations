# linked-list-all-basic-operations
```
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *next;
};

struct node* createnode(int data) {
    struct node *temp = (struct node*)malloc(sizeof(struct node));
    if(!temp) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    temp->data = data;
    temp->next = NULL;
    return temp;
}

void insertbegin(int data, struct node **head) {
    struct node *newnode = createnode(data);
    newnode->next = *head;
    *head = newnode;
}

void insertend(int data, struct node **head) {
    struct node *newnode = createnode(data);
    if(*head == NULL) {
        *head = newnode;
    } else {
        struct node *temp = *head;
        while(temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = newnode;
    }
}

void insertmiddle(int data, int pos, struct node **head) {
    if(pos < 1) {
        printf("Invalid position\n");
        return;
    }
    if(pos == 1) {
        insertbegin(data, head);
        return;
    }

    struct node *newnode = createnode(data);
    struct node *temp = *head;
    for(int i = 1; i < pos-1 && temp != NULL; i++) {
        temp = temp->next;
    }

    if(temp == NULL) {
        printf("Position out of range\n");
        free(newnode);
        return;
    }

    newnode->next = temp->next;
    temp->next = newnode;
}

void deletebegin(struct node **head) {
    if(*head == NULL) {
        printf("List is empty\n");
        return;
    }
    struct node *temp = *head;
    *head = (*head)->next;
    free(temp);
}

void deleteend(struct node **head) {
    if(*head == NULL) {
        printf("List is empty\n");
        return;
    }
    if((*head)->next == NULL) {
        free(*head);
        *head = NULL;
        return;
    }

    struct node *temp = *head;
    while(temp->next->next != NULL) {
        temp = temp->next;
    }
    free(temp->next);
    temp->next = NULL;
}

void deletemiddle(int pos, struct node **head) {
    if(*head == NULL) {
        printf("List is empty\n");
        return;
    }
    if(pos < 1) {
        printf("Invalid position\n");
        return;
    }
    if(pos == 1) {
        deletebegin(head);
        return;
    }

    struct node *temp = *head;
    struct node *prev = NULL;
    
    for(int i = 1; i < pos && temp != NULL; i++) {
        prev = temp;
        temp = temp->next;
    }

    if(temp == NULL) {
        printf("Position out of range\n");
        return;
    }

    prev->next = temp->next;
    free(temp);
}

void display(struct node *head) {
    struct node *temp = head;
    while(temp != NULL) {
        printf("%d->", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    struct node *head = NULL;

    // Insertion examples
    insertbegin(10, &head);
    insertend(30, &head);
    insertmiddle(20, 2, &head);
    insertbegin(5, &head);
    insertend(40, &head);
    insertmiddle(25, 4, &head);

    printf("List after insertions: ");
    display(head);

    // Deletion examples
    deletebegin(&head);
    deleteend(&head);
    deletemiddle(3, &head);

    printf("List after deletions: ");
    display(head);

    // Free memory
    while(head != NULL) {
        deletebegin(&head);
    }

    return 0;
}
```
//
// Created By Suprakash Ghosh 14/08/25
//
 
