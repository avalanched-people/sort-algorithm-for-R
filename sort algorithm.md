# ***几个常考的排序算法题目***  
# ***重在其中的思想***  
# 1.冒泡排序  
 具体描述：  
 比较相邻的元素。如果第一个比第二个大，就交换它们两个；  
 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数；  
 针对所有的元素重复以上的步骤，除了最后一个；  
 重复步骤1~3，直到排序完成
![image](https://github.com/avalanched-people/Data-analysis-written-examination/blob/master/bubble.gif)  
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
# 2.选择排序  
 具体描述：  
初始状态：无序区为R[1..n]，有序区为空；  
第i趟排序(i=1,2,3…n-1)开始时，当前有序区和无序区分别为R[1..i-1]和R(i..n）。该趟排序从当前无序区中-选出关键字最小的记录 R[k]，将它与无序区的第1个记录R交换，使R[1..i]和R[i+1..n)分别变为记录个数增加1个的新有序区和记录个数减少1个的新无序区;
n-1趟结束，数组有序化了。  
![image](https://github.com/avalanched-people/Data-analysis-written-examination/blob/master/selection.gif)  
```r
selection_sort <- function(x){
  len <- length(x)
  for (i in 1:(len-1)){
    min_index <- i
    for (j in (i+1):(len)){
      if (x[j] < x[min_index]){
        min_index <- j
      }
    }
    temp <- x[i]
    x[i] <- x[min_index]
    x[min_index] <- temp
    
  }
  x
}
```
# 3.插入排序  
插入排序  
从第一个元素开始，该元素可以认为已经被排序；  
取出下一个元素，在已经排序的元素序列中从后向前扫描；  
如果该元素（已排序）大于新元素，将该元素移到下一位置；  
重复步骤3，直到找到已排序的元素小于或者等于新元素的位置；  
将新元素插入到该位置后；  
重复步骤2~5。  
![image](https://github.com/avalanched-people/Data-analysis-written-examination/blob/master/insertion.gif)  
```r
insertion_sort <- function(x){
  len <- length(x)
  for (i in 2:len){
    current <- x[i]
    preIndex <- i-1
    while ((preIndex >= 1) & isTRUE(current < x[preIndex])){
      x[preIndex + 1] <- x[preIndex]
      preIndex <- preIndex - 1
    }
    preIndex <- ifelse(preIndex > 0, preIndex, preIndex + 1)
    x[preIndex] <- current
  }
  x
}
```

# 4.归并排序  
该算法是采用分治法（Divide and Conquer）的一个非常典型的应用  
将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序  
![image](https://github.com/avalanched-people/sort-algorithm-for-R/blob/master/merge_sort.gif)  
![image](https://github.com/avalanched-people/sort-algorithm-for-R/blob/master/归并排序演示.png)  
```r
merge_sort <- function(items) {
  browser()
  if (length(items) < 2) {
    return(items)
  }
  mid <- length(items) %/% 2
  left <- merge_sort(items[1:mid])
  right <- merge_sort(items[(mid+1):length(items)])
  return(merge(left, right))
}

merge <- function(item1, item2) {
  i <- 1; j <- 1; k <- 1
  len1 <- length(item1)
  len2 <- length(item2)
  len <- len1 + len2
  result <- numeric()
  
  while (i <= len1 && j <= len2) {
    if (item1[i] <= item2[j]) {
      result[k] <- item1[i]
      i <- i + 1
    }else {
      result[k] <- item2[j]
      j <- j + 1
    }
    k <- k + 1
  }
  # 对item2剩余的进行处理
  if (i > len1 && j <= len2) {
    result <- c(result[-k], item2[j:len2])
  }
  # 对item1剩余的进行处理
  if (i <= len1 && j > len2) {
    result <- c(result[-k], item1[i:len1])
  }
  return(result)
}
```

# 5.快速排序  
思想就是，选一个数作为基数（这里我选的是第一个数），大于这个基数的放到右边，小于这个基数的放到左边，等于这个基数的数可以放到左边或右边,看自己习惯，这里我是放到了左边.  
一趟结束后，将基数放到中间分隔的位置，第二趟将数组从基数的位置分成两半，分割后的两个的数组继续重复以上步骤，选基数，将小数放在基数左边，将大数放到基数的右边，再分割数组，，，直到数组不能再分为止，排序结束。  
![image](https://github.com/avalanched-people/sort-algorithm-for-R/blob/master/quick_sort.jpg)  
```r
# 本代码大幅使用了R语言内置的糖~
quick_sort <- function(x) {
  if (length(x) < 2 || length(unique(x)) == 1) {  # 此处迭代终止有两种可能：一是分割到一个数了；二是分割到的数组只有一种数字。
    return(x)                                     # 此时，数组都是自动排好序了的！
  }

  left <- quick_sort(c(x[which(x < x[1])], x[which(x == x[1])]))  # 以第一个数为基数，取出全部小于等于基数的数，注意：必须将所有基数放在最右边
  right <- quick_sort(x[which(x > x[1])])       # 取出全部大于基数的数
  return(c(left, right))
}
```

