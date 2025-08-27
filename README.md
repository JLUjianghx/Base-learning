# Base-learning
The repository is used to record my learning during the foundation stage.
# SqList code
#include <stdio.h>

#define Maxsize 50
typedef int elem_type;

typedef  struct{
    elem_type data[Maxsize];
    int length;//顺序表长度
}sqList;
bool elem_insert(sqList &s,int i,elem_type element){
    if(i<1 || i>s.length+1){
        return false;
    }
    if(Maxsize==s.length){
        printf("no free space\n");
        return false;
    }
    for(int j=s.length;j>=i;j--){

        s.data[j]=s.data[j-1];

    }
    s.length++;
    s.data[i-1]=element;
    return true;
}
void Print(sqList s){
    for(int i =0;i<s.length;i++){
        printf("%3d ",s.data[i]);

    }
    printf("\n");
}
int main() {

    sqList s;
    int ret;//判断
    s.data[0]=10;//设置
    s.data[1]=20;
    s.data[2]=30;
    s.length=3;
    ret = elem_insert(s,2,60);//插入函数
    if(ret){
        printf("insert is successful\n");
        Print(s);
    }else{
        printf("insert is not successful");
    }
    return 0;
}


# LinkList code
#include <stdio.h>
#include<stdlib.h>

typedef int Elem_type;
typedef struct LNode{
    Elem_type data;
    struct LNode *next;

}LNODE,*link_list;


//头插
void list_head_insert(LNode* &l){
    l=(link_list)malloc(sizeof(LNODE));//申请节点空间，头指针指向头节点
    Elem_type x;
    scanf("%d",&x);
    link_list s;
    l->next= nullptr;
//    s=(link_list) malloc(sizeof (LNODE));
//    s->data=x;
//    s->next= nullptr;
//    l->next=s;
    while(x!=99){

        s=(link_list) malloc(sizeof (LNODE));
        s->data=x;
        s->next=l->next;
        l->next=s;
        scanf("%d",&x);


    }

}

//尾插
void list_tail_insert(LNODE* &l){
    l=(link_list) malloc(sizeof (LNode));
    link_list s,r=l;
    Elem_type x;
    scanf("%d",&x);
    s= (link_list )malloc(sizeof(LNODE));
    while(x!=99){
        s=(link_list) malloc(sizeof (LNode));
        s->data=x;
        r->next=s;
        r=s;
        scanf("%d",&x);
    }
    r->next= nullptr;

}


//按位置查找
link_list get_elem(LNode *l,int pos){
    LNode *p=l->next;
    int i=1;
    if(pos==0){
        return l;
    }
    if(pos<1){

        return nullptr;
    }


    while(p && i<pos){
        p=p->next;
        i++;

    }
    return p;

}


//按值查找
link_list locate_elem(LNode *l,Elem_type elem){

    link_list p=l->next;
    while(p && p->data!=elem){
    p=p->next;
    }
    return p;

}


//第i个位置插元素
bool list_front_insert(link_list l,int pos,Elem_type e){
    link_list p= get_elem(l,pos-1);
    if(p== nullptr){
        return false;
    }
    link_list s=(link_list)malloc(sizeof(LNode));
    s->data=e;
    s->next=p->next;
    p->next=s;

    return true;
}

//删除函数
bool list_delete(link_list l,int pos){
    link_list p= get_elem(l,pos-1);
    link_list q=p->next;
    if(p== nullptr || q== nullptr){

        return false;
    }
    p->next=q->next;
    free(q);
    return true;
}



//输出函数
void PrintLinkList(link_list l){
    l=l->next;
    while(l!= nullptr){

        printf("%3d",l->data);
        l=l->next;
    }
    printf("\n");


}



int main() {
    link_list l,search;//l是头指针
    list_tail_insert(l);
    //list_head_insert(l);
    PrintLinkList(l);


    //位置查询
    search=get_elem(l,2);
    if(search){
        printf("search by position succeed\n");
        printf("%d\n",search->data);
    }


    //值查询
    search= locate_elem(l,3);
    if(search){

        printf("search by value succeed\n");
        printf("%d\n",search->data);
    }



//第i个位置插入
    bool ret;
    ret = list_front_insert(l,2,66);
    if(ret){
        printf("list position i succeed\n");
        PrintLinkList(l);
    }

    //删除
    list_delete(l,2);
    PrintLinkList(l);



    return 0;
}


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



