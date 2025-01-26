# TO-DO-LIST
i made this to do list using C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_TASKS 100
#define MAX_LENGTH 100

typedef struct {
    char description[MAX_LENGTH];
    int isDone; // 0 = not done, 1 = done
} Task;

Task tasks[MAX_TASKS];
int taskCount = 0;
