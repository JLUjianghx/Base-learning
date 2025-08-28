# Base-learning
The repository is used to record my learning during the foundation stage.






# stack code
#include <stdio.h>
#include<stdlib.h>

#define MaxSize 6
typedef struct{
    int data[MaxSize];
    int top;

}sqStack;
//初始化栈
void init_stack(sqStack &s){
    s.top=-1;//代表栈为空
}

//判断是否初始化
bool stack_empty(sqStack s){
    if(s.top==-1){
        return true;
    }
    return false;
}

//入栈
bool inStack(sqStack &s,int x){
    if(s.top==MaxSize-1){
        return false;
    }
    s.data[++s.top]=x;
    return true;

}

//出栈
bool outStack(sqStack &s,int &x){

    if(s.top==-1){
        return false;
    }
    x=s.data[s.top--];
    return true;

}

//获取栈顶元素
bool getTop(sqStack s,int &x){
    if(s.top==-1){
        return false;
    }
    x=s.data[s.top];
    return true;

}


int main() {
    sqStack s;
    init_stack(s);
    bool ret_isEmpty= stack_empty(s);
    if(ret_isEmpty){
        printf("stack is empty\n");
    }
    inStack(s,1);
    inStack(s,2);
    inStack(s,3);
    inStack(s,4);

    int x;
    bool flag= getTop(s,x);
    if(flag){
        printf("top is %d",x);
    }

    return 0;
}


# sqQueue code
#include <stdio.h>
#include<stdlib.h>

//循环队列
#define Maxsize 6
typedef struct{
    int data[Maxsize];
    int front,rear;

}sqQueue;

//初始化
void init_queue(sqQueue &s){
    s.front=s.rear=0;
}

//判断是否空
bool isEmpty(sqQueue s){
    if(s.rear==s.front){
        return true;
    }
    return false;
}

//入队
bool enQueue(sqQueue &s,int x){
    if((s.rear+1)%Maxsize==s.front){
        return false;
    }
    s.data[s.rear]=x;
    s.rear=(s.rear+1)%Maxsize;
    return true;
}

//出队
bool deQueue(sqQueue &s,int &x){
    if(isEmpty(s)){
        return false;
    }
    x=s.data[s.front];
    s.front=(s.front+1)%Maxsize;
    return true;

}

int main() {
    sqQueue s;
    bool ret;
    init_queue(s);
    bool ret_empty= isEmpty(s);
    if(ret_empty){
        printf("queue is empty\n");
    }

    enQueue(s,1);
    enQueue(s,2);
    enQueue(s,3);
    enQueue(s,4);
    ret=enQueue(s,5);
     ret=enQueue(s,6);
    if(ret){
        printf("enter queue success\n");
    }else{
        printf("enter queue fail\n");
    }

    int x;
    deQueue(s,x);

    return 0;
}



