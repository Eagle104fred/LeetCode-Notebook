# 力扣好题记录
## 15.三数之和
使用双指针法，用指针标定需要相加的数字
## 18.四数之和
与三数之和思路相似

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

## 剑指Offer05 替换空格
移动字符串数组的时候，从后面开始遍历比从头开始要好
