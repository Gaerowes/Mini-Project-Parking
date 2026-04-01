# Mini-Project-Parking
Simple parking system simulation using:
- Queue (Antrian mobil masuk)
- Stack (Parkiran)
- Deque (Opsional dua arah)

##  Features
- Tambah mobil ke antrian
- Parkir mobil (Queue → Stack)
- Mobil keluar (Stack)
- Deque depan & belakang
- Tampilkan semua data

##  Data Structures Used
- Queue (FIFO)
- Stack (LIFO)
- Deque (Double-ended queue)

##  Compile & Run

```bash
#include <stdio.h>
#include <string.h>

#define MAX 10

typedef struct{
        char data[MAX][10];
        int front, rear;
    } Queue;
    
typedef struct{
        char data[MAX][10];
        int top;
    } Stack;
    
typedef struct{
    char data[MAX][10];
    int front, rear;
} Deque;
    
int main(){
    Queue q;
    Stack s;
    Deque d;
    
    q.front = 0;
    q.rear = -1;
    s.top = -1;
    d.front = -1;
    d.rear = -1;
    
    int pilih;
    char plat[10];
    
    do {
        printf("\n=== Menu ===\n");
        printf("1. Tambah mobil\n");
        printf("2. Parkir mobil(Queue)\n");
        printf("3. Mobil keluar\n");
        printf("4. Tampilakan\n");
        printf("5. Masuk depan\n");
        printf("6. Masuk belakang\n");
        printf("7. Parkir dari depan\n");
        printf("8. Parkir dari belakang\n");
        printf("0. Exit\n");
        printf("Pilih: ");
        scanf("%d", &pilih);
        
        if (pilih == 1) {
            if (q.rear < MAX - 1) {
                printf("Plat: ");
                scanf("%s", plat);
                strcpy(q.data[++q.rear], plat);
            } else {
                printf("Queue penuh\n");
            }
        }
        else if (pilih == 2) {
            if (q.front <= q.rear) {
                if (s.top < MAX - 1) {
                    strcpy(s.data[++s.top], q.data[q.front]);
                    q.front++;
                    printf("Mobil diparkir\n");
                }
                else {
                    printf("Parkiran penuh\n");
                }
            }
            else {
                printf("Queue kosong\n");
            }
        }
        else if (pilih == 3) {
            if (s.top >= 0) {
                printf("Mobil keluar: %s\n", s.data[s.top]);
                s.top--;
            }
            else {
                printf("Parkiran kosong\n");
            }
        }
        else if (pilih == 4) {
            printf("Queue: ");
            if (q.front > q.rear) printf("kosong");
            for (int i = q.front;i <= q.rear;i++){
                printf("%s ", q.data[i]);
            }
            
            printf("\nParkiran: ");
                if (s.top < 0) printf("kosong");
                for(int i = 0;i <= s.top;i++){
                    printf("%s ", s.data[i]);
                }
                printf("\n");   
            
            printf("\nDeque: ");
                if (d.front == -1) printf("kosong");
                else {
                    for (int i = d.front; i <= d.rear; i++) {
                    printf("%s ", d.data[i]);
                    }
                }
                    printf("\n");
                
        }
        else if (pilih == 5) {
            printf("Plat: ");
            scanf("%s", plat);
            
            if(d.front == -1){
                d.front = d.rear = 0;
            } else if (d.front > 0){
                d.front--;
            } else {
                printf("deque penuh depan\n");
                continue;
            } strcpy (d.data[d.front], plat);
        }
        else if (pilih == 6) {
            printf("Plat: ");
            scanf("%s", plat);
            if (d.rear < MAX - 1){
                if (d.front == -1) d.front = 0;
                strcpy(d.data[++d.rear], plat);
            }
            else {
                printf("Deque penuh belakang\n");
            }
        }
        else if (pilih == 7) {
            if (d.front == -1){
                printf("Deque kosong\n");
            }
            else if (s.top < MAX - 1){
                strcpy(s.data[++s.top], d.data[d.front]);
                d.front++;
                
                if (d.front > d.rear){
                    d.front = d.rear = -1;
                }
                
                printf("Mobil dari depan diparkir\n");
            }
            else {
                printf("Parkir penuh\n");
            }
        }
        else if (pilih == 8){
            if (d.rear == -1){
                printf("Deque kosong\n");
            }
            else if (s.top < MAX - 1){
                strcpy(s.data[++s.top], d.data[d.rear]);
                d.rear--;
                
                if (d.front > d.rear){
                    d.front = d.rear = -1;
                }
                
                printf("Mobil dari belakang diparkir\n");
            }
            else {
                printf("Parkir penuh\n");
            }
        }
    } 
    while (pilih != 0);
    
    return 0;
}
