# 力扣好题记录
## 15.三数之和
使用双指针法，用指针标定需要相加的数字
## 18.四数之和
与三数之和思路相似

## 96.不同搜索树
关键是在于轮询所有的动归数组

## 150.逆波兰表达式求值
其中用到了stoi函数LeetCode貌似不支持我自己实现了一个
```c++
long long StringToIntCore(const char *str,bool minus);
int  my_stoi(const char *str)
{
    int num=0;
    if(str!=NULL&&*str!='\0')
    {
        bool minus = false;
        if(*str=='+')
        {
            str++;
        }
        else if(*str=='-')
        {
            str++;
            minus = true;
        }
        if(*str!='\0')
        {
            num = StringToIntCore(str,minus);
        }
    }
    return (int)num;
}
long long StringToIntCore(const char *str,bool minus)
{
    long long num=0;
    while(*str!='\0')
    {
        if(*str>='0'&&*str<='9')
        {
            int flag = minus?-1:1;
            
            
            num = num*10+flag*(*str-'0');
            
            //判断num溢出分别判断正负
            if((!minus&&num>0x7FFFFFFF)||(minus&&num<(signed int)0x80000000))
            {
                num = 0;
                break;
            }
            str++;
        }
        else
        {
            num = 0;
            break;
        }
    }
    return num;
}

```
## 559.N叉树的最大深度
树形结构DFS计算深度
return深度，并且在函数体内判断深度是否为最深或者最浅
```C++
class Solution {
public:
    int CountDepth(Node *root){
        if(root==NULL)return 0;
        int depth  = 0;
        for(auto i:root->children)
        {
            depth = max(depth,CountDepth(i));
        }

        return depth+1;
    }
    int maxDepth(Node* root) {
        return CountDepth(root);
    }
};
```


## BFS广搜
```
#广搜的核心
void BFS()
{
    定义队列;
    定义备忘录，用于记录已经访问的位置；

    判断边界条件，是否能直接返回结果的。

    将起始位置加入到队列中，同时更新备忘录。

    while (队列不为空) {
        获取当前队列中的元素个数。
        for (元素个数) {
            取出一个位置节点。
            判断是否到达终点位置。
            获取它对应的下一个所有的节点。
            条件判断，过滤掉不符合条件的位置。
            新位置重新加入队列。
        }
    }

}
```
- ## 1091.二进制矩阵中的最短路径
```cpp
class Solution {
public:
    struct Node{
        int x;
        int y;
    };
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        queue<Node>Que;
        int total=0;
        int X=grid.size();
        int Y=grid[0].size();
        vector<vector<int>> visit(X,vector<int>(Y,0));
        if(grid[0][0]==1||grid[X-1][Y-1]==1){
            return -1;
        }
        Que.push({0,0});
        visit[0][0]=1;
        while(!Que.empty())
        {
            int size=Que.size();
            for(int i=0;i<size;i++)
            {
                Node currentNode = Que.front();
                int x=currentNode.x;
                int y=currentNode.y;
                if(x==X-1&&y==Y-1)
                    return total+1;
                vector<Node> nextNode={{x + 1, y}, {x - 1, y}, {x + 1, y - 1}, {x + 1, y + 1},{x, y + 1}, {x, y - 1}, {x - 1, y - 1}, {x - 1, y + 1}};

                for(auto& n:nextNode)
                {
                    if(n.x<0||n.x>=X||n.y<0||n.y>=Y)
                        continue;
                    if(visit[n.x][n.y]==1)
                        continue;
                    if(grid[n.x][n.y]==1)
                        continue;
                    visit[n.x][n.y]=1;
                    Que.push(n);
                }
                Que.pop();                      
            }
            total++;
        }
        return -1;
    }
};

```

## 剑指Offer05 替换空格
移动字符串数组的时候，从后面开始遍历比从头开始要好
