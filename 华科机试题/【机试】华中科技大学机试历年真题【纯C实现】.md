传送门：<https://www.nowcoder.com/kaoyan/retest/11002?page=0>

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <memory.h>
#include <limits.h>
#define MAXN 100+5
#define ll long long
#define mem(a, n) memset(a, n, sizeof(a))

/// pro29 农夫、羊、菜和狼的故事
int main() {
    printf("sheep_go\nnothing_come\nvegetable_go\nsheep_come\nwolf_go\nnothing_come\nsheep_go\nsucceed\n");
    return 0;
}

/// pro28 最长&最短文本

typedef struct Node {
    int len;
    char str[1005];
} Node;
Node s[MAXN];
int main() {
//    freopen("dataIn.txt", "r", stdin);
    int i=0;
    while(gets(s[i].str)!=NULL)
        s[i].len = strlen(s[i].str), i++;
    int minLen = INT_MAX, maxLen = INT_MIN;
    int k;
    for(k=0; k<i; k++) {
        int len = s[k].len;
        if(len < minLen) minLen = len;
        if(len > maxLen) maxLen = len;
    }
    for(k=0; k<i; k++) {
        if(s[k].len == minLen) puts(s[k].str);
    }
    for(k=0; k<i; k++) {
        if(s[k].len == maxLen) puts(s[k].str);
    }
    return 0;
}


/// pro27 八进制

void solve(int n, int k) {
    char ans[MAXN];
    int cnt=0;
    while(n) {
        while(n) {
            ans[cnt++]=(n%k+'0');
            n/=k;
        }
    }
    int i;
    for(i=--cnt; i>=0; i--) {
        putchar(ans[i]);
    }
    puts("");
}

int main() {
    int n;
    while(~scanf("%d", &n)) {
        solve(n, 8);
    }
    return 0;
}


/// pro26 阶乘

int main() {
    int n;
    while(~scanf("%d", &n)) {
        int y1=0,y2=0, j=1, i;
        for(i=1; i<=n; i++) {
            j*=i;
            if(i&1) y1+=j;
            else y2+=j;
        }
        printf("%d %d\n", y1, y2);
    }
    return 0;
}


/// pro25 找位置
//这里可能用C++或Python写代码要精简些
int main() {
    char str[MAXN];
    while(~(scanf("%s", str))) {
        int len = strlen(str), flag=0;///flag标记是否有输出
        int i, j;
        for(i=0; i<len; i++) {
            flag=0;
            for(j=i+1; j<len; j++) {
                // str[j]='*' 为输出位置的标记避免重复输出
                if(str[i] == str[j] && str[j]!='*') {
                    if(flag == 0) {
                        printf("%c:%d,%c:%d",str[i],i,str[j],j);
                        flag=1;
                    } else {
                        printf(",%c:%d",str[j], j);
                    }
                    str[j]='*';
                }
            }
            if(flag==1) puts("");
        }
    }
    return 0;
}


/// pro24 回文字符串
int main()  {
    char str[1005];
    while(gets(str)!=NULL) {
        int flag=0, i;
        int len=strlen(str);
        for(i=0; i<len/2; ++i) {
            if(str[i] != str[len-i-1]) {
                flag=1;
                break;
            }
        }
        printf("%s!\n", flag ? "No" : "Yes");
    }
    return 0;
}


/// pro23 a+b

/// pro22 N阶楼梯上楼问题
// 思路：多种方法，如1）迭代；2）打表 3）递归（题目要求非递归）
// 打表
int ans[MAXN];
void fun() {
    ans[1]=1,ans[2]=2;
    int i;
    for(i=3; i<91; i++) {
        ans[i] = ans[i-1] + ans[i-2];
    }
}
// 迭代
int solve(int n) {
    int k=3, ans;
    int p=1, q=2;
    if(n==1) return p;
    if(n==2) return q;
    while(k++ <= n) {
        ans = p+q;
        int tmp = p;
        p = q;
        q = ans;
    }
    return ans;
}

int main() {
    int n;
//    fun();
    while(~scanf("%d", &n)) {
        printf("%d\n", solve(n));
    }
    return 0;
}

/// pro21 大整数排序
// 思路：先按照字符串长度排序，长度一致再比较大小
typedef struct Node{
    int len;
    char str[1005];
} Node;
Node node[MAXN];

int cmp(const void* a, const void* b) {
    struct Node *str1 = (Node *)a;
    struct Node *str2 = (Node *)b;
    if(str1->len != str2->len) return str1->len - str2->len;
    return strcmp(str1->str, str2->str);
}

int main() {
    int n;
    while(~scanf("%d", &n)) {
        int i;
        getchar();
        for(i=0; i<n; i++) {
            scanf("%s", node[i].str);
            node[i].len = strlen(node[i].str);
        }
        qsort(node, n, sizeof(node[0]), cmp);
        for(i=0; i<n; i++) {
            printf("%s\n", node[i].str);
        }
    }
    return 0;
}

/// pro20 二叉排序树
typedef struct BTNode {
    int data;
    struct BTNode* lchild;
    struct BTNode* rchild;
} BTNode;

///建立二叉排序树
BTNode* create(BTNode *T, int data) {
    if(T == NULL) {
        T = (BTNode*) malloc(sizeof(BTNode));
        T->data = data;
        T->lchild = T->rchild = NULL;
        return T;
    } else if(data < T->data) {
        T->lchild = create(T->lchild, data);
    } else if(data > T->data) {
        T->rchild = create(T->rchild, data);
    }
    return T;
}
//前序遍历
void travelPre(BTNode *T) {
    if(T==NULL) return;
    printf("%d ", T->data);
    travelPre(T->lchild);
    travelPre(T->rchild);
}

//中序遍历
void travelIn(BTNode *T) {
    if(T==NULL) return;
    travelIn(T->lchild);
    printf("%d ", T->data);
    travelIn(T->rchild);
}

//后序遍历
void travelPost(BTNode *T) {
    if(T==NULL) return ;
    travelPost(T->lchild);
    travelPost(T->rchild);
    printf("%d ", T->data);
}

int main() {
    int n;
    while(~scanf("%d", &n)) {
        BTNode *T=NULL;
        while(n--) {
            int data;
            scanf("%d", &data);
            T = create(T, data);
        }
        travelPre(T);
        puts("");
        travelIn(T);
        puts("");
        travelPost(T);
        puts("");
    }
    return 0;
}


/// pro19 打印日期
int month[12] = {31,28,31,30,31,30,31,31,30,31,30,31};
/// 判断是否闰年
int isLeapYear(int year) {
    if(year%4==0&&year%100!=0 || (year%400==0)) return 1;
    return 0;
}

int main() {
    int year, d;
    while(~scanf("%d%d", &year, &d)) {
        int flag=isLeapYear(year);
        int m, i;
        for(i=0; i<12; i++) {
            if(flag&&i==1) {///若是闰年的二月
                if(d-month[i]-1>=1) d=d-month[i]-1;
                else break;
            } else {
                if(d-month[i]>=1) d-=month[i];
                else break;
            }
        }
        printf("%d-%02d-%02d\n", year, i+1, d);

    }
    return 0;
}


/// pro18 A+B
char stra[MAXN];
int main() {
    while(gets(stra)!=NULL) {
        ll a=0, b=0;
        int flag1=0, flag2=0;/// flag1, flag2分别表示两个数的符号位，若为1则为负数，反之则正数
        int flag=0;/// flag=0时计算第一个数，flag=1时计算第二个数
        for(int i=0; stra[i]; i++) {
            if(!flag) {
                if(stra[i]=='-')
                    flag1=1;
                else if(stra[i]>='0'&&stra[i]<='9') {
                    a=a*10+stra[i]-'0';
                } else if(stra[i]==',')
                    continue;
                else if(stra[i]==' ')
                    flag=1;
            } else {
                if(stra[i]=='-')
                    flag2=1;
                else if(stra[i]>='0'&&stra[i]<='9') {
                    b=b*10+stra[i]-'0';
                } else if(stra[i]==',')
                    continue;
            }
        }
        if(flag1)   a=-a;
        if(flag2)   b=-b;
        printf("%lld\n", a+b);
    }
    return 0;
}

/// pro17 对称矩阵
int a[MAXN][MAXN];
int main() {
    int n, i ,j;
    while(~scanf("%d", &n)) {
        for(i=0; i<n; i++) {
            for(j=0; j<n; j++) {
                scanf("%d", &a[i][j]);
            }
        }
        int flag=0;
        for(i=0; i<n; i++) {
            for(j=0; j<n; j++) {
                if(a[i][j] != a[j][i]) {
                    flag=1;
                    break;
                }
            }
            if(flag) break;
        }
        printf("%s\n", flag ? "No!" : "Yes!");
    }
    return 0;
}

/// pro16 最小年龄的三个职工
/// 结构体排序
typedef struct Employee {
    int number, age;
    char name[15];
} Employee;
Employee emp[MAXN];

int cmp(const void* a, const void* b){
    struct Employee* emp1 = (Employee*)a;
    struct Employee* emp2 = (Employee*)b;
    if(emp1->age != emp2->age) return emp1->age - emp2->age;
    else if(emp1->number != emp2->number) return emp1->number - emp2->number;
    return strcmp(emp1->name, emp2->name);
}

int main() {

    int n;
    scanf("%d", &n);
    int i;
    for(i=0; i<n; i++) {
        scanf("%d %s %d", &emp[i].number, emp[i].name, &emp[i].age);
    }
    qsort(emp, n, sizeof(emp[0]), cmp);
    for(i=0; i<3; i++) {
        printf("%d %s %d\n", emp[i].number, emp[i].name, emp[i].age);
    }
    return 0;
}

/// pro15 矩阵最大值
int a[MAXN][MAXN];
int main() {

    int n,m;
    while(~scanf("%d%d", &n, &m)) {
        int i,j,maxVal,indexOfMaxVal;
        for(i=0; i<n; i++) {
            scanf("%d",&a[i][0]);
            int sum = a[i][0];
            maxVal = a[i][0], indexOfMaxVal = 0;
            for(j=1; j<m; j++) {
                scanf("%d",&a[i][j]);
                sum += a[i][j];
                if(maxVal < a[i][j]) {
                    maxVal = a[i][j];
                    indexOfMaxVal = j;
                }
            }
            a[i][indexOfMaxVal] = sum;
        }
        for(i=0; i<n; i++) {
            for(j=0; j<m; j++) {
                printf("%d ", a[i][j]);
            }
            puts("");
        }
    }
    return 0;
}

/// pro14 守形数
/// 思路：先计算输入值n的位数，然后判断n*n%t == n是否成立
int main() {
    int n;
    while(~scanf("%d", &n)) {
        int t=1;
        while(n/t) t*=10;
        printf("%s\n", (n*n%t == n) ? "Yes!": "No!");
    }
    return 0;
}

/// pro13 遍历链表
typedef struct LinkNode {
    int data;
    struct LinkNode *next;
} LinkNode, *LinkList;
//链表初始化
LinkList init() {
    LinkList L = (LinkNode*) malloc(sizeof(LinkNode));
    L->next = NULL;
    return L;
}
//插入
void insert(LinkList L, int x) {
    LinkList pre=L;
    LinkList cur=L->next;
    while(cur) { ///寻找插入x使链表还是升序的位置
        if(cur->data >= x) break;
        pre = cur, cur = cur->next;
    }
    /// tmp指向即将插入的节点
    LinkNode *tmp = (LinkNode*) malloc(sizeof(LinkNode));
    tmp->data = x;
    pre->next = tmp;
    tmp->next = cur;
}
void print(LinkList L) {
    LinkList p=L->next;
    while(p->next != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    printf("%d\n", p->data);
}
int main() {
    int n;
    scanf("%d", &n);
    int i, data;
    LinkList L = init();
    for(i=0; i<n; i++) {
        scanf("%d", &data);
        insert(L, data);
    }
    print(L);
    free(L);
    return 0;
}

/// pro12成绩排序
typedef struct Student {
    char name[MAXN];
    int age, grade;
} Student;
Student stu[1005];

int cmp(const void *a, const void *b) {
    struct Student *stu1 = (Student*)a;///强制转换为Student指针类型
    struct Student *stu2 = (Student*)b;
    if(stu1->grade != stu2->grade) return stu1->grade - stu2->grade;
    else if(strcmp(stu1->name, stu2->name)) return strcmp(stu1->name, stu2->name);
    return stu1->age - stu2->age;
}

int main() {
    int n, i;
    while(~scanf("%d", &n)) {
        for(i=0; i<n; i++) {
            scanf("%s %d %d", stu[i].name, &stu[i].age, &stu[i].grade);
        }
        qsort(stu, n, sizeof(stu[0]), cmp);
        for(i=0; i<n; i++) {
            printf("%s %d %d\n",stu[i].name, stu[i].age, stu[i].grade);
        }
    }
    return 0;
}


/// pro11 最大的两个数
/// 思路：按列查找，主要是记得按照列的顺序输出两个最大数，这里采用一个索引保存前面最大的
int main() {

#ifdef ONLINE_JUDGE
#else
    freopen("dataIn.txt", "r", stdin);
    freopen("dataOut.txt", "w", stdout);
#endif
    int i,j;
    int a[4][5];
    for(i=0; i<4; i++) {
        for(j=0; j<5; j++) {
            scanf("%d", &a[i][j]);
        }
    }
    int maxTwoValue[2][5];
    int maxVal, theSecMaxVal, indexOfMaxVal, indexOfTheSecVal;
    for(j=0; j<5; j++) {
        int val1=a[0][j], val2=a[1][j];
        if(val1 < val2) {
            maxVal = val2, theSecMaxVal = val1;
            indexOfMaxVal = 1, indexOfTheSecVal = 0;
        } else {
            maxVal = val1, theSecMaxVal = val2;
            indexOfMaxVal = 0, indexOfTheSecVal = 1;
        }
        for(i=2; i<4; i++) {
            if(a[i][j] > maxVal) {
                theSecMaxVal = maxVal, maxVal = a[i][j];
                indexOfTheSecVal = indexOfMaxVal;
                indexOfMaxVal = i;
            } else if(a[i][j] > theSecMaxVal) {
                theSecMaxVal = a[i][j], indexOfTheSecVal = i;
            }
        }
        if(indexOfMaxVal < indexOfTheSecVal) {
            maxTwoValue[0][j] = maxVal, maxTwoValue[1][j] = theSecMaxVal;
        } else {
            maxTwoValue[0][j] = theSecMaxVal, maxTwoValue[1][j] = maxVal;
        }
    }
    for(i=0; i<2; i++) {
        for(j=0; j<5; j++) {
            printf("%d ", maxTwoValue[i][j]);
        }
        puts("");
    }
    return 0;
}


/// pro10 奇偶校验
int ans[8];
void solve(char ch) {
    int num=ch,k=8, t=0;
    while(num) {
        ans[--k]=num%2;
        if(num%2) t++;
        num/=2;
    }
    ans[0]=t%2 ? 0 : 1;
}
int main() {
    char str[MAXN];
    while(~scanf("%s", str)){
        for(int i=0; str[i]; i++) {
            memset(ans, 0, sizeof(ans));
            solve(str[i]);
            for(int j=0; j<8; j++) printf("%d", ans[j]);
            puts("");
        }
    }
    return 0;
}

/// pro09 二叉树的遍历
char pre[MAXN], in[MAXN], post[MAXN];
void create(int preL, int preR, int inL, int inR, int postL, int postR) {
    if(postL > postR)
        return;
    char root = pre[preL];
    post[postR] = root; /// 根据二叉树前序遍历与中序遍历的特点
    int k=0;
    while(in[inL+k] != root) { //从当前中序序列中找根
        k++;
    }
    // 分别创建左子树与右子树
    create(preL+1, preL+k, inL, inL+k-1, postL, postL+k-1);
    create(preL+k+1, preR, inL+k+1, inR, postL+k, postR-1); //已插入根节点到post[postR]中
    return ;
}
int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("dataIn.txt", "r", stdin);
    freopen("dataOut.txt", "w", stdout);
#endif
    while(~scanf("%s %s", &pre, &in)) {
        int len = strlen(pre);
        create(0, len-1, 0, len-1, 0, len-1);
        int i;
        for(i=0; i<len; i++) {
            putchar(post[i]);
        }
        puts("");
    }
    return 0;
}


/// pro08 特殊排序
int cmp(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

int a[MAXN];
int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("dataIn.txt", "r", stdin);
    freopen("dataOut.txt", "w", stdout);
#endif
    int n,i;
    while(~scanf("%d", &n)) {
        for(i=0; i<n; i++) {
            scanf("%d", &a[i]);
        }
        qsort(a, n, sizeof(int), cmp);
        printf("%d\n", a[n-1]);
        if(n == 1) { //数据中n==1即只有一个数时
            printf("-1\n");
            continue;
        }
        for(i=0; i<n-1; i++) {
            printf("%d ",a[i]);
        }
    }
    return 0;
}

/// pro07 排序
int cmp(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

int a[MAXN];
int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("dataIn.txt", "r", stdin);
    freopen("dataOut.txt", "w", stdout);
#endif
    int n,i;
    while(~scanf("%d", &n)) {
        for(i=0; i<n; i++) {
            scanf("%d", &a[i]);
        }
        qsort(a, n, sizeof(int), cmp);
        for(i=0; i<n; i++) {
            printf("%d ",a[i]);
        }
    }
    return 0;
}

/// pro06 a+b
char a[1005], b[1005];
void add(char* s1,char* s2) {
    char s[1005]={};
	int cnt=0;
    int len1=strlen(s1)-1;
    int len2=strlen(s2)-1;
    int ca=0;///ca表示进位
    while(len1!=-1&&len2!=-1) {
        int sum=ca+(s1[len1--]-'0')+(s2[len2--]-'0');
        s[cnt++]=((sum)%10+'0');
        ca=sum/10;
    }
    while(len1!=-1) { ///若len1!=-1
        int sum=ca+(s1[len1--]-'0');
        s[cnt++]=((sum)%10+'0');
        ca=sum/10;
    }
    while(len2!=-1) { ///若len2!=-1
        int sum=ca+(s2[len2--]-'0');
        s[cnt++]+=((sum)%10+'0');
        ca=sum/10;
    }
    if(ca)
        s[cnt++]+=(ca+'0');
	int i;
	for(i=cnt-1; i>=0; i--) {
		putchar(s[i]);
	}
	puts("");
}
int main() {
    while(~scanf("%s %s", a, b)) {
        add(a, b);
    }
    return 0;
}

/// pro05 字符串连接
int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("dataIn.txt", "r", stdin);
    freopen("dataOut.txt", "w", stdout);
#endif
    char ch;
    char ans[MAXN];
    int i, t=0;
    while((ch=getchar())!='\n') {
        if(ch!=' ')
            ans[t++] = ch;
    }
    for(i=0; i<t; i++) {
        putchar(ans[i]);
    }
    return 0;
}

/// pro04 二叉排序树
typedef struct BNode {
    // data
    int data;
    struct BNode *lchild;
    struct BNode *rchild;
} BNode;

// T: 二叉树根节点的地址，data：当前需要插入二叉排序树的节点数据，fa：当前结点的父节点指针
BNode* create(BNode* T, int data, int *fa) {
    if(T == NULL) {
        T = (BNode*) malloc (sizeof(BNode));
        T->data = data;
        T->lchild = T->rchild = NULL;
        return T;
    } else if(data < T->data) {
        *fa = T->data;
        T->lchild = create(T->lchild, data, fa);
    } else if(data > T->data){
        *fa = T->data;
        T->rchild = create(T->rchild, data, fa);
    }
    return T;
}

int main() {
    int n;
    while(~scanf("%d", &n)) {
        BNode* T=NULL;
        while(n--) {
            int data, fa=-1;
            scanf("%d", &data);
            T = create(T, data, &fa);
            printf("%d\n", fa);
        }
    }
    return 0;
}

/// pro03 IP地址
int main() {
#ifdef ONLINE_JUDGE
#else
    freopen("dataIn.txt", "r", stdin);
    freopen("dataOut.txt", "w", stdout);
#endif
    char s[MAXN];
    while(fgets(s, MAXN, stdin)!=NULL) {
        int i, flag=0;
        for(i=0; i<15; i++) {
            char ch=s[i];
            if(ch>='0' && ch<='9') {
                int sum=0;
                while(ch>='0' && ch<='9') {
                    sum=sum*10+(ch-'0');
                    ch=s[++i];
                }
                if(sum<0||sum>255) {
                    flag=1;
                    break;
                }
            }
        }
        if(flag)
            puts("No!");
        else
            puts("Yes!");
    }
    return 0;
}


/// pro02 统计单词
int num[MAXN];
int main() {
    char s[MAXN];
    mem(num, 0);
    int index=0; //字母索引
    while(fgets(s, MAXN, stdin)!=NULL) {
        int i,len = strlen(s);
        for(i=0; i<len; i++) {
            char ch=s[i];
//            printf("ch=%c\n", ch);
            if(isalpha(ch)) {
                for( ; isalpha(s[i]) ; i++) {
                    num[index]++;
                }
//                printf("num[%d] = %d\n",index, num[index]);
                if(s[i]==' ')
                    index++;
                if(s[i]=='.')
                    break;
            } else if(ch==' ') {
                index++;
            } else if(ch=='.')
                break;
        }
        for(i=0; i<=index; i++) {
            printf("%d",num[i]);
            printf("%c", i==index ? '\n' : ' ');
        }
    }
    return 0;
}

/// pro01 矩阵转置
int a[MAXN][MAXN];
int main() {
    int i,j, n;
    scanf("%d", &n);
    for(i=0; i<n; i++) {
        for(j=0; j<n; j++)
            scanf("%d",&a[i][j]);
    }
    for(j=0; j<n; j++) {
        for(i=0; i<n; i++) {
            printf("%d", a[i][j]);
            if(i==n-1)
                printf("\n");
            else
                printf(" ");
        }
    }
    return 0;
}

```

