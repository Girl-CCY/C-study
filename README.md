#include<iostream>
#include<malloc.h>
using namespace std;
#define OK 1
#define ERROR 0
#define OVERFLOW -2
typedef int Status;
typedef int Elemtype;
typedef struct LNode
{
    int data;
    struct LNode* next;
}
LNode, * LinkList;
void ListTraverse(LinkList L)
{
    LinkList p;
    p = L->next;
    printf("当前链表为：");
    while (p != NULL) {
        printf("%d", p->data);
        p = p->next;
    }
    printf("\n");
    return;
}
void CreateList_H(LinkList& L, int n)
{
    L = new LNode;
    L->next = NULL;
    LNode* p = (LNode*)malloc(sizeof(LNode));
    LNode* temp = p;
    int i = 0;
    for (i = 0; i < n; ++i)
    {
        p = new LNode;
        cin >> p->data;
        p->next = L->next;
        L->next = p;
    }
}

Status ListInsert(LinkList& L, int i, int e)
{
    LinkList p = L; int j = 0;
    while(p&&(j<i-1))
    {
        p = p->next; ++j;
    }
    if (!p || j > i - 1)
        return ERROR;
    LinkList s = new LNode;
    s->data = e;
    s->next = p->next;
    p->next = s;
    return OK;
}

Status ListDelete(LinkList& L, int i)
{
    LinkList p = L; int j = 0;
    while((p->next)&&(j<i-1))
    {
        p == p->next; ++j;
    }
    if (!(p->next) || (j > i - 1))
        return ERROR;
    LinkList q = p->next;
    p->next = q->next;
    delete q;
    return OK;
}
LNode* LocateElem(LinkList L, int e)
{
    LinkList p = L->next;
    while (p && p->data != e)
        p = p->next;
    cout << "你要查找的元素是:" << p->data << endl;
    return p;
}
void MergeList_L(LinkList LA, LinkList LB, LinkList &LC)
{
    LinkList pa, pb, pc;
    LC = new LNode;
    LC->next = NULL;
    pa = LA->next; pb = LB->next;  
    LC = LA;   
    pc = LC;
    while (pa && pb)
    {
        if (pa->data <= pb->data)
        {
            pc->next = pa;
            pc - pa;
            pa = pa->next;
        }
        else
        {
            pc->next = pb;
            pc = pb;
            pb = pb->next;
        }
    }
    pc->next = pa ? pa:pb;
    delete LB;
}

    int main(){  
        LinkList L, p;
        int n;
        cout << "输入创建的链表个数：";
        cin >> n;
        CreateList_H(L, n);
        cout << "输出创建链表：";
        p = L->next;
        while (p)
        {
            cout << p->data << ' ';
            p = p->next;
        }
        cout << endl;
        ListInsert(L, 3, 6);
        cout << "插入一个元素后，";
        ListTraverse(L);
        ListDelete(L, 3);
        cout << "删除一个元素后，";
        ListTraverse(L);
        LocateElem(L, 3);
        LinkList L2, x;
        int k;
        cout << "输入创建的链表个数：";
        cin >> k;
        CreateList_H(L2, k);
        cout << "输出创建链表：";
        x = L2->next;
        while (x)
        {
            cout << x->data << ' ';
            x = x->next;
        }
        cout << endl;
        LinkList L3;
        MergeList_L(L, L2, L3);
        ListTraverse(L3);
        
}

