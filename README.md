//Q1 
#include <stdio.h>
#include<stdlib.h>
int main(){
    int* ptr;
    ptr=(int*)malloc(sizeof(int));
    if(ptr==NULL){
        printf("Memory allocation failed.");
        exit(1);
    }
    printf("Enter a number: ");
    scanf("%d", ptr);
    printf("You Entered: %d\n", *ptr);
    free(ptr);
}

//Q2
#include <stdio.h>
#include<stdlib.h>
int main(){
    int n;
    printf("Enter number of integers.");
    scanf("%d", &n);
    int* ptr;
    ptr=(int*)calloc(n, sizeof(int));
    if(ptr==NULL){
        printf("Memory allocation failed.");
        exit(1);
    }
    for(int i=0;i<n;i++){
        scanf("%d", &ptr[i]);
    }
    printf("Stored integers are: ");
    
    for(int i=0;i<n;i++){
        printf("%d, ", ptr[i]);
    }
    free(ptr);
}
//Q4
#include <stdio.h>
#include<stdlib.h>
int main(){
    int n, top=-1, value, choice;
    printf("Enter the size of stack: ");
    scanf("%d", &n);
    int* stack= (int*)malloc(n*sizeof(int));
    if(stack==NULL){
        printf("Memory allocation failed.");     
    }

    do{
        printf("Stack Menu: \n");
        printf("1. Push\n");
        printf("2. Pop\n");
        printf("3. Display\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice){
            case 1: if(top==n-1){
                printf("Stack overfload.\n");
            }
            else{
                printf("Enter value to push: ");
                scanf("%d", &value);
                top++;
                stack[top]=value;
            }
            break;
            case 2: if(top==-1){
                printf("Stack underflowed.\n");
            }
            else{
                printf("Popped element: %d\n", stack[top]);
                top--;
            }
            break;
            case 3: if(top==-1){
                printf("Stack is empty.\n");
            }
            else{
                printf("Stack elements: \n");
                for(int i=top;i>=0;i--){
                    printf("%d\n", stack[i]);
                }
            }
            break;
            case 4 :
            printf("Exiting programme.\n");
            break;

            default: printf("Invalid Choice...Try again.");
        }
    }
    while(choice !=4);
    free(stack);
}

//Q3
#include <stdio.h>
#include<stdlib.h>
int main(){
    int n;
    float sum=0;
    printf("Enter how many numbers: ");
    scanf("%d", &n);
    float*ptr=(float*)malloc(n*sizeof(float));
    if(ptr==NULL){
        printf("Memory allocation failed.");
        exit(1);
    }
    for(int i=0;i<n;i++){
        scanf("%f", &ptr[i]);
        sum+=ptr[i];
    }
    
    printf("The average is: %.2f", sum/n);
    free(ptr);
}

//Q5
#include <stdio.h>

int main(){
    FILE* fp;
    char ch;
    fp = fopen("text.txt", "r");

    if(fp==NULL){
        printf("File not found.");
    }

    printf("File contents: ");

    ch=fgetc(fp);
    while(ch != EOF){
        printf("%c", ch);
        ch=fgetc(fp);
    }

    fclose(fp);
    return 0;
}

//Q6
#include <stdio.h>
#include<string.h>
int main(){
    FILE* fp;
    char ch;
    fp = fopen("text.txt", "a");

    if(fp==NULL){
        printf("File not found.");
    }

    printf("Enter text to append: ");
    char str[100];
    fgets(str,100,stdin);
    

    fputs(str, fp);

    fclose(fp); 
    return 0;
}



//Q7
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    char name[50];
    int roll;
    float marks;
};

int main() {
    struct Student student[100], temp;
    int n, count = 0, i, j;
    FILE *fp;

    printf("Enter number of students: ");
    scanf("%d", &n);
  
    fp = fopen("students.txt", "w");
    if (fp == NULL) {
        printf("File cannot be opened for writing.\n");
        exit(1);
    }

    for (i = 0; i < n; i++) {
        printf("\nEnter details for student %d\n", i + 1);
        printf("Name: ");
        scanf("%s", student[i].name);

        printf("Roll number: ");
        scanf("%d", &student[i].roll);
        printf("Marks: ");
        scanf("%f", &student[i].marks);
     
        fprintf(fp, "%s %d %.2f\n", student[i].name, student[i].roll, student[i].marks);
    }

    fclose(fp);

    fp = fopen("students.txt", "r");
    if (fp == NULL) {
        printf("File cannot be opened for reading.\n");
        exit(1);
    }

    while (fscanf(fp, "%s %d %f", student[count].name, &student[count].roll, &student[count].marks) == 3) {
        count++;
    }
    fclose(fp);

    for (i = 0; i < count - 1; i++) {
        for (j = i + 1; j < count; j++) {
            if (student[i].marks < student[j].marks) {
                temp = student[i];
                student[i] = student[j];
                student[j] = temp;
            }
        }
    }


    printf("Rank-wise Student List:\n");
    for (i = 0; i < count; i++) {
        printf("Rank %d  Name: %s  Roll: %d  Marks: %.2f\n",
               i + 1, student[i].name, student[i].roll, student[i].marks);
    }
}
