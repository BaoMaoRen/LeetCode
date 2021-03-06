#### 给你一个 n x n 矩阵 matrix ，其中每行和每列元素均按升序排序，找到矩阵中第 k 小的元素。请注意，它是 排序后 的第 k 小元素，而不是第 k 个 不同 的元素。
1     5      9 

10  11    13

12   13   15

第8小的元素：13



题解：

way1（*）：二分查找思想，通过题目可知第一个数为矩阵的最小值，最后一个值为矩阵的最大值，在此值域内通过二分查找，二分查找的条件是，每次比较在矩阵中比值域mid值小的数据个数，通过个数判断下一个值域的边界；改题涉及到了二分查找变种思想（多个符合条件的值中找第一个，第一个符合条件的即数组中存在的值）；

 大概的意思：在数组的数据比它小的个数，小于等于8个的第一个数（因为这个数在数组中存在，所以他是满足条件的第一个数）



way2：利用归并排序的思想，将多个有序的数组合并为一个，当合并到第K个值时，即为原解；



```c++
bool check(char* matrix, int mid, int n)
{
    int i = n - 1, j = 0;
    int count = 0;
  	while( i >= 0 || y < n )
    {
        if(matrix[i][j] <= mid)
        {
            cout += i + 1;
            j++
        }
        else
        {
            i--;
        }
    }
    return cout;
}

bool find_matrix_number(char* matrix, int n, int num, int &retval)
{
   	if(!matrix || num < 0) return false; 
   	int max = matrix[n-1][n-1], min = matrix[0][0];
    int mid = -1;
    while(min < max)
    {
        mid = min + ((max - min) >> 1);
        if(check(matrix, mid , n) >= num)
        {
            max = mid;
        }
        else
        {
            min = mid + 1;
        }
    }
   	retval = mid;
    return true;
}
```



二分查找的思路：

1.确定初始左值、右值及中值；

2.将问题转化为二分问题模型（二分模型有普通模型和变种模型两种：普通模型查找具体值；变种模型查找范围边界值，例如大于等于某值）；

3.通过分析模型结果获取下一次边界值，重复以上步骤。