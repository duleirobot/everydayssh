# 剑指Offer

## 数组中重复的数字

###　题目链接：



### 题目描述：

在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组[2,3,1,0,2,5,3]，那么对应的输出是2或者3。存在不合法的输入的话输出-1



数据范围：0≤*n*≤10000 

进阶：时间复杂度O(n) ，空间复杂度O(n)



输入：

```
[2,3,1,0,2,5,3]
```

返回值：

```
2
```

说明：

```
2或3都是对的  
```

### 解题思路：

输入＼输出

算法：法一：遍历整个数组，将数组当前指向的元素依次与之前的元素比较，若相同则循环结束，返回当前值。

点评：如果机器没有视觉的话，这在数组里面已经是最简便的基本方法来“比较是否为同一个数”



```ｃ＋＋
class Solution {
public:
int duplicate(vector<int>& numbers) {
for(int i=0;i<numbers.size();i++)
{
    int j=0;
    while(i>j)
    {if(numbers[i]==numbers[j]&&i>0)
　　　　　return numbers[i];
　　　　　　　　　j++;
   }
    return -1;
}
};
```


## 二维数组的查找

### 题目链接

### 题目描述

在一个二维数组array中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

[

[1,2,8,9],
[2,4,9,12],
[4,7,10,13],
[6,8,11,15]

]

给定 target = 7，返回 true。

给定 target = 3，返回 false。

数据范围：矩阵的长宽满足 0 ≤*n*,*m*≤500 ， 矩阵中的值满0≤*v**a**l*≤10^9
进阶：空间复杂度 O(1) ，时间复杂度 O(n+m)

**示例1**

输入：

```
7,[[1,2,8,9],[2,4,9,12],[4,7,10,13],[6,8,11,15]]
```

返回值：

```
true
```

说明：

```
存在7，返回true    
```

**示例2**

输入：

```
1,[[2]]
```

返回值：

```
false

```

**示例3**

输入：

```
3,[[1,2,8,9],[2,4,9,12],[4,7,10,13],[6,8,11,15]]
```

返回值：

```
false
```

说明：

```
不存在3，返回false    
```

### 解题思路

思路：题目有特殊条件，递增性局部有序性。横向看，可以将输入的数用二分法查找；纵向看，也可以将输入的数二分查找；能不能结合横纵，最终经过探索发现可以。通过矩阵对角线为分界点的形式将图慢慢扩大，发现这样走的路程最短，即比较次数最少。

```c++
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        int m=array.size();
        if(m==0) return false;
        
     for(int i=0,j=0;i<array[0].size();i++,j++) 
    {
        if(target==array[i][j])
            return true;
        if(target<array[i][j])
        {
            for(int hang=j-1;hang>0;hang--)
            {
                if(target==array[i][hang]||target==array[hang][j]) return true;
                else return false;
                
            }
        };
        
         
    }; 
          return false;  //没有这一行，编译无法通过
    }
    
};
```

点评：此方法只适合方阵;

## 替换空格

### 题目链接

### 题目描述

请实现一个函数，将一个字符串s中的每个空格替换成“%20”。

例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

数据范围：0≤*l**e**n*(*s*)≤1000 。保证字符串中的字符为大写英文字母、小写英文字母和空格中的一种。

示例：

输入：

```
"We Are Happy"
```

返回值：

```
"We%20Are%20Happy"
```



输入：

```
" "
```

返回值：

```
"%20"
```

### 解题思路

思路：直接替换，注意遍历字符串的方式

``` c++
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param s string字符串 
     * @return string字符串
     */
    string replaceSpace(string s) {
        // write code here
        string res = "";
        //遍历字符串
        for(int i = 0; i < s.length(); i++){
            //非空格直接复制
            if(s[i] == ' ') res += "%20";
                
            //空格就替换
            else
                res += s[i];
        }
        return res;
    }
};
```

## 从尾巴到头打印链表

### 题目链接

### 题目描述

输入一个链表的头节点，按链表从尾到头的顺序返回每个节点的值（用数组返回）。

如输入{1,2,3}的链表如下图:

![img](https://uploadfiles.nowcoder.com/images/20210717/557336_1626506480516/103D87B58E565E87DEFA9DD0B822C55F)

返回一个数组为[3,2,1]

0 <= 链表长度 <= 10000

示例1

输入：

```
{1,2,3}
```

返回值：

```
[3,2,1]
```

示例2

输入：

```
{67,0,24,58}
```

返回值：

```
[58,24,0,67]
```

### 解题思路

思路：先输出然后倒序

``` c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> ans;
        while(head){
            ans.push_back(head->val);
            head=head->next;
        }
        reverse(ans.begin(),ans.end());
        return ans;
        
    }
};
```

点评：还有其他方法，如：栈

## 重建二叉树

### 题目链接

### 题目描述

给定节点数为 n 的二叉树的前序遍历和中序遍历结果，请重建出该二叉树并返回它的头结点。

例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建出如下图所示。

![img](https://uploadfiles.nowcoder.com/images/20210717/557336_1626504921458/776B0E5E0FAD11A6F15004B29DA5E628)

提示:

1.vin.length == pre.length

2.pre 和 vin 均无重复元素

3.vin出现的元素均出现在 pre里

4.只需要返回根结点，系统会自动输出整颗树做答案对比

数据范围：2000*n*≤2000，节点的值 −10000≤*v**a**l*≤10000

要求：空间复杂度 O(n)，时间复杂度 O(n)

示例1

输入：

```
[1,2,4,7,3,5,6,8],[4,7,2,1,5,3,8,6]
```

返回值：

```
{1,2,3,4,#,5,6,#,7,#,#,8}
```

说明：

```
返回根节点，系统会输出整颗二叉树对比结果，重建结果如题面图示    
```

示例2

输入：

```
[1],[1]
```

返回值：

```
{1}
```

示例3

输入：

```
[1,2,3,4,5,6,7],[3,2,4,1,6,5,7]
```

返回值：

```
{1,2,5,3,4,6,7}
```

### 解题思路

一定要用递归，先决条件：序列不能为零，先构建根节点使其初值为先序序列第一个值；找到中序中前序的第一个元素后得到左子树和右子树的先序和中序；根节点左子节点又可以仿照上面的逻辑，直接递归终止条件：

``` c++
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
        int n = pre.size();
        int m = vin.size();
        //每个遍历都不能为0
        if(n == 0 || m == 0)
            return NULL;
        //构建根节点
        TreeNode *root = new TreeNode(pre[0]);
        for(int i = 0; i < vin.size(); i++){
            //找到中序遍历中的前序第一个元素
            if(pre[0] == vin[i]){
                //左子树的前序遍历
                vector<int> leftpre(pre.begin() + 1, pre.begin() + i + 1); 
                //左子树的中序遍历
                vector<int> leftvin(vin.begin(), vin.begin() + i);
                //构建左子树
                root->left = reConstructBinaryTree(leftpre, leftvin);
                //右子树的前序遍历
                vector<int> rightpre(pre.begin() + i + 1, pre.end());
                //右子树的中序遍历
                vector<int> rightvin(vin.begin() + i + 1, vin.end());
                //构建右子树
                root->right = reConstructBinaryTree(rightpre, rightvin);
                break;
            }
        }
        return root; 

    }
};
```

点评：掌握递归很重要

## 二叉树的下一个结点

### 题目链接

### 题目描述

给定一个二叉树其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的next指针。下图为一棵有9个节点的二叉树。树中从父节点指向子节点的指针用实线表示，从子节点指向父节点的用虚线表示

![img](https://uploadfiles.nowcoder.com/images/20210616/557336_1623844408327/D03B8D5BB902D4516BB92CB216E58EC4)

示例:

输入:{8,6,10,5,7,9,11},8

返回:9

解析:这个组装传入的子树根节点，其实就是整颗树，中序遍历{5,6,7,8,9,10,11}，根节点8的下一个节点就是9，应该返回{9,10,11}，后台只打印子树的下一个节点，所以只会打印9，如下图，其实都有指向左右孩子的指针，还有指向父节点的指针，下图没有画出来

![img](https://uploadfiles.nowcoder.com/images/20210616/557336_1623845692021/E647707AEF2A4AE2C40F0FCCB549B6A5)

数据范围：节点数满足 1≤*n*≤50 ，节点上的值满足 1≤*v**a**l*≤100 

要求：空间复杂度 O(1) ，时间复杂度 O(n)

输入描述：

输入分为2段，第一段是整体的二叉树，第二段是给定二叉树节点的值，后台会将这2个参数组装为一个二叉树局部的子树传入到函数GetNext里面，用户得到的输入只有一个子树根节点

返回值描述：

返回传入的子树根节点的下一个节点，后台会打印输出这个节点

示例1

输入：

```
{8,6,10,5,7,9,11},8
```

返回值：

```
9
```

示例2

输入：

```
{8,6,10,5,7,9,11},6
```

返回值：

```
7
```

示例3

输入：

```
{1,2,#,#,3,#,4},4
```

返回值：

```
1
```

示例4

输入：

```
{5},5
```

返回值：

```
"null"
```

说明：

```
不存在，后台打印"null"   
```

### 解题思路

思路：创建一个存放结构体指针的动态数组，想办法获取根节点【利用next指针指向上一级】，然后再中序遍历结果存入存放结构体指针的动态数组,遍历数组返回结果否则结果为空



``` c++
class Solution {
public:
    vector<TreeLinkNode*> nodes;
    TreeLinkNode* GetNext(TreeLinkNode* pNode) {
        TreeLinkNode* root = pNode;
        // 获取根节点
        while(root->next) root = root->next;    
        
        // 中序遍历用nodes储存所有节点指针
        InOrder(root);                          
        int n = nodes.size();
        
        for(int i = 0; i < n - 1; i++) {
            TreeLinkNode* cur = nodes[i];
            // 将结点进行匹配       
            if(pNode == cur) {
                // 如果有匹配到给出的结点，则下一个结点即返回结果                  
                return nodes[i+1];              
            }
        }
        // 否则如果没有下一个结点则返回NULL
        return NULL;                            
    }
    // 中序遍历
    void InOrder(TreeLinkNode* root) {          
        if(root == NULL) return;
        InOrder(root->left);
        nodes.push_back(root);
        InOrder(root->right);
    }
};

```

点评：关键是中序遍历的算法

## 用两个栈来实现一个队列

### 题目链接

### 题目描述

用两个栈来实现一个队列，使用n个元素来完成 n 次在队列尾部插入整数(push)和n次在队列头部删除整数(pop)的功能。 队列中的元素为int类型。保证操作合法，即保证pop操作时队列内已有元素。

数据范围： n*≤1000

要求：存储n个元素的空间复杂度为 O(n) ，插入与删除的时间复杂度都是 O(1）

示例1

输入：

```
["PSH1","PSH2","POP","POP"]
```

返回值：

```
1,2
```

说明：

```
"PSH1":代表将1插入队列尾部
"PSH2":代表将2插入队列尾部
"POP“:代表删除一个元素，先进先出=>返回1
"POP“:代表删除一个元素，先进先出=>返回2    
```

示例2

输入：

```
["PSH2","POP","PSH1","POP"]
```

返回值：

```
2,1
```

###　解题思路

思路：两栈两用，一个管进，一个管出

``` c++
class Solution
{
public:
    //入队列就正常入栈
    void push(int node) { 
        stack1.push(node);
    }

    int pop() {
        //将第一个栈中内容弹出放入第二个栈中
        while(!stack1.empty()){ 
            stack2.push(stack1.top()); 
            stack1.pop();
        }
        //第二个栈栈顶就是最先进来的元素，即队首
        int res = stack2.top(); 
        stack2.pop(); 
        //再将第二个栈的元素放回第一个栈
        while(!stack2.empty()){ 
            stack1.push(stack2.top());
            stack2.pop();
        }
        return res;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};

```

点评：角度有了，就有逻辑，逻辑有了，再细节化处理

## 斐波拉契数列

### 题目链接

### 题目描述

大家都知道斐波那契数列，现在要求输入一个正整数 n ，请你输出斐波那契数列的第 n 项。

斐波那契数列是一个满足 

*f**i**b*(*x*)=1   *x*=1,2

*f**i**b*(*x*)=*f**i**b*(*x*−1)+*f**i**b*(*x*−2）  *x*>2

的数列

数据范围：1≤*n*≤40

要求：空间复杂度 O(1)，时间复杂度 O(n) ，本题也有时间复杂度 O(logn)的解法

输入描述：

一个正整数n

返回值描述：

输出一个正整数。

输入：

```
4
```

返回值：

```
3
```

说明：

```
根据斐波那契数列的定义可知，fib(1)=1,fib(2)=1,fib(3)=fib(3-1)+fib(3-2)=2,fib(4)=fib(4-1)+fib(4-2)=3，所以答案为3。   
```

输入：

```
1
```

返回值：

```
1
```



输入：

```
2
```

返回值：

```
1
```

### 解题思路

思路：递归。尽头条件：n=1和2时；递归逻辑：递推式

``` c++
class Solution {
public:
    int Fibonacci(int n) {
        if(n==1||n==2) return 1;
        return Fibonacci(n-1)+Fibonacci(n-2);

    }
};
```

点评：递归好

## 矩阵中的路径

### 题目链接

### 题目描述



请设计一个函数，用来判断在一个n乘m的矩阵中是否存在一条包含某长度为len的字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 例如
$$
\begin{pmatrix}
a&b&c&e\\
s&f&c&s\\
a&d&e&e

\end{pmatrix}
$$
矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

数据范围：0≤*n*,*m*≤20 ,1≤*l**e**n*≤25 

示例1

输入：

```
[[a,b,c,e],[s,f,c,s],[a,d,e,e]],"abcced"
```

返回值：

```
true
```

示例2

输入：

```
[[a,b,c,e],[s,f,c,s],[a,d,e,e]],"abcb"
```

返回值：

```
false
```



### 解题思路

思路:
