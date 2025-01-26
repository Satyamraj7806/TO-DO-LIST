# TO-DO-LIST
i made this to do list using C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_TASKS 100
#define MAX_LENGTH 100

typedef struct {
    char description[MAX_LENGTH];
    int isDone; 
} Task;

Task tasks[MAX_TASKS];
int taskCount = 0;
void loadTasks() {
    FILE *file = fopen("tasks.txt", "r");
    if (file == NULL) {
        return;
    }
    taskCount = 0;
    while (fscanf(file, "\n%d\n", tasks[taskCount].description, &tasks[taskCount].isDone) == 2) {
        taskCount++;
    }
    fclose(file);
}

void saveTasks() {
    FILE *file = fopen("tasks.txt", "w");
    if (file == NULL) {
        printf("Error saving tasks!\n");
        return;
    }
    for (int i = 0; i < taskCount; i++) {
        fprintf(file, "%s\n%d\n", tasks[i].description, tasks[i].isDone);
    }
    fclose(file);
}

void addTask() {
    if (taskCount >= MAX_TASKS) {
        printf("Task limit reached!\n");
        return;
    }
    printf("Enter task description: ");
    getchar(); 
    fgets(tasks[taskCount].description, MAX_LENGTH, stdin);
     taskCount++;
     }
     void viewTasks() {
    if (taskCount == 0) {
        printf("No tasks available.\n");
        return;
    }
    printf("\nTo-Do List:\n");
    for (int i = 0; i < taskCount; i++) {
        printf("%d. [%c] %s\n", i + 1, tasks[i].isDone ? 'X' : ' ', tasks[i].description);
    }
}

void markTaskDone() {
    int taskNum;
    viewTasks();
    if (taskCount == 0) return;
    printf("\nEnter task number to mark as done: ");
    scanf("%d", &taskNum);
    if (taskNum < 1 || taskNum > taskCount) {
        printf("Invalid task number!\n");
    } else {
        tasks[taskNum - 1].isDone = 1;
        printf("Task marked as done!\n");
    }
}

void deleteTask() {
    int taskNum;
    viewTasks();
    if (taskCount == 0) return;
    printf("\nEnter task number to delete: ");
    scanf("%d", &taskNum);
    if (taskNum < 1 || taskNum > taskCount) {
        printf("Invalid task number!\n");
    } else {
        for (int i = taskNum - 1; i < taskCount - 1; i++) {
            tasks[i] = tasks[i + 1];
        }
        taskCount--;
        printf("Task deleted successfully!\n");
    }
}

int main() {
    int choice;
    while (1) {
        printf("\n--- Badmoshi nhi mittar. ye rhi tumhari to do list ---\n");
        printf("1. Add Task\n");
        printf("2. View Tasks\n");
        printf("3. Mark Task as Done\n");
        printf("4. Delete Task\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                addTask();
                saveTasks();
                break;
            case 2:
                viewTasks();
                break;
            case 3:
                markTaskDone();
                saveTasks();
                break;
            case 4:
                deleteTask();
                saveTasks();
                break;
            case 5:
                saveTasks();
                printf("Ram ram laddar!\n");
                exit(0);
            default:
                printf("badmoshi nhi chhote. invalid option\n");
        }
    }
}

   
    
