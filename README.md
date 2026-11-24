#include <stdio.h>
#include <string.h>

// Macro defined as 6
#define MAX 6

// Global Queue Arrays and Pointers
char queue[MAX][50]; // Queue can hold 6 items, up to 50 characters each
int front = -1;
int rear = -1;

// Function Prototypes
void insert(char item[]);
void delete();
void update(int position, char newValue[]);
void display();

int main() {
    printf("--- C QUEUE OPERATIONS DEMO (Max Size: %d) --- \n\n", MAX);

    // 1. Test Insert (Enqueue)
    insert("Task A");
    insert("Task B");
    insert("Task C");
    display();

    // 2. Test Update
    update(1, "Task B - Priority updated");
    display();

    // 3. Test Delete (Dequeue)
    delete();
    display();

    // Fill up the queue to test macro limit overflow
    insert("Task D");
    insert("Task E");
    insert("Task F");
    insert("Task G"); // This will prompt an overflow error
    display();

    return 0;
}

// --- 1. INSERT OPERATION (Enqueue) ---
void insert(char item[]) {
    // Check if queue is full
    if (rear == MAX - 1) {
        printf("[ERROR] Cannot insert '%s'. Queue Overflow!\n", item);
        return;
    }

    // If inserting the very first element
    if (front == -1) {
        front = 0;
    }
 
    rear++;
    strcpy(queue[rear], item); // Copy string into the queue slot
    printf("[INSERT] Added: '%s' at position %d\n", item, rear);

}

// --- 2. DELETE OPERATION (Dequeue) ---
void delete() {
    // Check if queue is empty
    if (front == -1 || front > rear) {
        printf("[ERROR] Cannot delete. Queue Underflow!\n");
        return;
    }

    printf("[DELETE] Removed: '%s' from position %d\n", queue[front], front);
    
    front++;

    // Reset queue pointers if it becomes completely empty
    if (front > rear) {
        front = -1;
        rear = -1;
    }
}

// --- 3. UPDATE OPERATION ---
void update(int position, char newValue[]) {
    // Check if the queue is empty
    if (front == -1) {
        printf("[ERROR] Queue is empty. Nothing to update.\n");
        return;
    }

    // Validate if the requested index currently holds an active item
    if (position < front || position > rear) {
        printf("[ERROR] Position %d is invalid or empty.\n", position);
        return;
    }

    printf("[UPDATE] Position %d changed from '%s' to '%s'\n", position, queue[position], newValue);
    strcpy(queue[position], newValue); // Copy the new string over the old one
}

// --- HELPER FUNCTION: DISPLAY ---
void display() {
    printf("\n--- Current Queue Status ---\n");
    if (front == -1 || front > rear) {
        printf("[Empty]\n");
    } else {
        for (int i = 0; i < MAX; i++) {
            if (i >= front && i <= rear) {
                printf("Index %d: %s <-- (Active)\n", i, queue[i]);
            } else {
                printf("Index %d: [Empty Slot]\n", i);
            }
        }
    }
    printf("-----------------------------\n\n");
}# Data-Structure-
