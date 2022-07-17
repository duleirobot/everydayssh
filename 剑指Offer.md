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

