#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct book {
    int id;
    char title[100];
    char author[100];
    struct book* next;
};

struct book* createBook(int id, char title[], char author[]) {
    struct book* newBook = (struct book*)malloc(sizeof(struct book));
    newBook->id = id;
    strcpy(newBook->title, title);
    strcpy(newBook->author, author);
    newBook->next = NULL;
    return newBook;
}

void addBook(struct book** head, int id, char title[], char author[]) {
    struct book* newBook = createBook(id, title, author);
    if (*head == NULL) {
        *head = newBook;
        return;
    }
    struct book* temp = *head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newBook;
}

void displayBooks(struct book* head) {
    if (head == NULL) {
        printf("No books in the library.\n");
        return;
    }
    printf("\nLibrary Books:\n");
    struct book* temp = head;
    while (temp != NULL) {
        printf("ID: %d, Title: %s, Author: %s\n", temp->id, temp->title, temp->author);
        temp = temp->next;
    }
}

struct book* searchBook(struct book* head, int id) {
    struct book* temp = head;
    while (temp != NULL) {
        if (temp->id == id) {
            return temp;
        }
        temp = temp->next;
    }
    return NULL;
}

void deleteBook(struct book** head, int id) {
    struct book* temp = *head;
    struct book* prev = NULL;

    if (temp != NULL && temp->id == id) {
        *head = temp->next;
        free(temp);
        printf("Book with ID %d deleted.\n", id);
        return;
    }

    while (temp != NULL && temp->id != id) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) {
        printf("Book with ID %d not found.\n", id);
        return;
    }

    prev->next = temp->next;
    free(temp);
    printf("Book with ID %d deleted.\n", id);
}

int main() {
    struct book* library = NULL;
    int choice, id;
    char title[100], author[100];

    while (1) {
        printf("\nLibrary Management System\n");
        printf("1. Add Book\n2. Display Books\n3. Search Book\n4. Delete Book\n5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar();

        switch (choice) {
            case 1:
                printf("Enter the book ID: ");
                scanf("%d", &id);
                getchar();
                printf("Enter the book title: ");
                fgets(title, sizeof(title), stdin);
                title[strcspn(title, "\n")] = '\0';
                printf("Enter the book author: ");
                fgets(author, sizeof(author), stdin);
                author[strcspn(author, "\n")] = '\0';
                addBook(&library, id, title, author);
                break;
            case 2:
                displayBooks(library);
                break;
            case 3:
                printf("Enter book ID to search: ");
                scanf("%d", &id);
                struct book* found = searchBook(library, id);
                if (found) {
                    printf("Book found - ID: %d, Title: %s, Author: %s\n", found->id, found->title, found->author);
                } else {
                    printf("Book with ID %d not found.\n", id);
                }
                break;
            case 4:
                printf("Enter book ID to delete: ");
                scanf("%d", &id);
                deleteBook(&library, id);
                break;
            case 5:
                printf("Exiting program.\n");
                return 0;
            default:
                printf("Invalid choice! Try again.\n");
        }
    }

    return 0;
}
