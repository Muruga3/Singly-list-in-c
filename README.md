# Singly-list-in-c
#include <stdio.h>
#include<stdlib.h>
struct Node {
    int data;
    struct Node* next;
};
typedef struct Node node;
node* head = NULL;
void insert(int d) { // d = 30
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    
    if(head==NULL) {
        head = newNode;
    }
    else {
        node* temp = head;
        while(temp->next!=NULL) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}
void insertbeg(int d) { // d  = 40
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = head;
    
    head = newNode;
}
void insertafter(int x, int d) { // x = 20, d = 50
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    
    node* temp = head;
    while(temp->data != x) {
        temp = temp->next;
    }
    newNode->next = temp->next;
    temp->next = newNode;
}
void insertbefore(int x, int d) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->data = d;
    newNode->next = NULL;
    
    node* prev = NULL;
    node* temp = head;
    
    while(temp->data!=x) {
        prev = temp;
        temp = temp->next;
    }
    
    newNode->next = temp;
    prev->next = newNode;
}
void deletebeg() {
    if(head==NULL) {
        printf("\nList is Empty");
        return;
    }
    node* temp = head;
    head = temp->next;
    free(temp);
}
void deleteEnd() {
    if(head==NULL)  {
        printf("\nList is Empty");
        return;
    }
    if(head->next == NULL) {
        free(head);
        head = NULL;
        return;
    }
    
    node* temp = head;
    node* prev = NULL;
    
    while(temp->next != NULL) {
        prev = temp;
        temp = temp->next;
    }
    free(temp);
    prev->next = NULL;
}
void deletePosition(int Position) {
    if(head==NULL) {
        printf("\nList is Empty");
    }
    if(Position == 0) {
        deletebeg();
        return;
    }
    
    node* temp = head;
    node* prev = NULL;
    int CurrentPosition = 0;
    
    while(temp!=NULL && CurrentPosition != Position) {
        prev = temp;
        temp = temp->next;
        CurrentPosition++;
    }
    
    if(temp==NULL) {
        printf("\nInvalid Position");
    }
    prev->next = temp->next;
    free(temp);
}
void display() {
    node* temp = head;
    while(temp!=NULL) {
        printf("\nNode = %d", temp->data);
        // printf("\nAddress = %d", temp->next);
        temp = temp->next;
    }
    printf("\nNode = NULL");
}

int main() {
    insert(10);
    insert(20);
    insert(30);
    insertbeg(40);
    insertafter(20, 50);
    insertbefore(20, 60);
    display();
    printf("\n---------------------------");
    deletebeg();
    deleteEnd();
    deletePosition(2);
    display();

    return 0;
}
