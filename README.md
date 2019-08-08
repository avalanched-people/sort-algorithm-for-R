# Data-analysis-written-examination
#几个常考的算法题目
# 1.冒泡排序
 具体描述：
 比较相邻的元素。如果第一个比第二个大，就交换它们两个；
 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数；
 针对所有的元素重复以上的步骤，除了最后一个；
 重复步骤1~3，直到排序完成。
![image](https://github.com/avalanched-people/Data-analysis-written-examination/bubble.gif)

```r
bubble_sort <- function(x){
  len <- length(x)
  for (i in 1:(len)){
    for (j in 1:ifelse((len-i)>0, len-i, 1)){
      if (x[j] > x[j+1]){
        temp <- x[j]
        x[j] <- x[j+1]
        x[j+1] <- temp
      }
    }
  }
  x
}
```