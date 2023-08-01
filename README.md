# C-p66-5-
C语言学习笔记 p66 动态内存分配(5)
#include<stdio.h>
#include<stdlib.h>
struct S
{
    int n;
    int arr[];//未知大小-柔性数组成员-数组的大小是可以调整的
};
int main()
{
    int S s;
    printf("%d\n",sizeof(s));//输出为4，它并没包含这个数组成员
    struct S* ps=(struct S*)malloc(sizeof(struct S)+5*sizeof(int));
    ps->n=100;
    int i=0;
    for(i=0;i<5;i++)
    {
        ps->arr[i]=i;//0 1 2 3 4
    }
    struct S* ptr=realloc(ps,44);
    if(ptr!=NULL)
    {
        ps=ptr;
    }
    for(i=5;i<10;i++)
    {
        ps->arr[i]=i;
    }
    for(i=0;i<10;i++)
    {
        printf("%d\n",ps->arr[i]);
    }
    free(ps);
    ps=NULL;
    return 0;
}//这个是使用柔性数组数组，一般配合malloc和celloc一起使用，优点是内存是连续的，内存访问速度加快

struct S
{
    int n;
    int* arr;
};
int main()
{
    struct S*ps=malloc(sizeof(struct S));
    ps->arr=malloc(5*sizeo(int));
    int i=0;
    for(i=0;i<5;i++)
    {
        ps->arr[i]=i;
    }
    for(i=0;i<5;i++)
    {
        printf("%d\n",ps->arr[i]);
    }
    //调整大小
    int* ptr=realloc(ps->arr,10*sizeof(int));
    if(ptr!=NULL)
    {
        ps->arr=ptr;
    }
    for(i=5;i<10;i++)
    {
        ps->arr[i]=i;
    }
    for(i=0;i<10;i++)
    {
        printf("%d ",ps->arr[i]);
    }
    //释放内存
    free(ps->arr);
    ps->arr=NULL;
    free(ps);
    ps=NULL;
    return 0;
}//这个是双malloc，容易出错
