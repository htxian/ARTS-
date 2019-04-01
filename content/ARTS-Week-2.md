



## Algorithm

>[442.Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/)
>
> Medium
>
> Given an array of integers, 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear **twice** and others appear **once**.
>
> Find all the elements that appear **twice** in this array.
>
> Could you do it without extra space and in O(*n*) runtime?
>
> **Example:**
>
> ```
> Input:
> [4,3,2,7,8,2,3,1]
>
> Output:
> [2,3]
>
> ```

Python3 的答案：

```Python
def findDuplicates(nums:[int]):
    reslut = []
    for index in range(len(nums)):
        #取出列表的值的绝对值，作为下标
        a = int(abs(nums[index]))
        #将通过新下标的获取的数值改成它的相反数
        nums[a - 1] = nums[a - 1] * -1
        #因为一个数据重复的数据只会出现两次，所以如果新下标取的数值是正的，那么这个下标就是重复的数据
        if nums[a - 1] > 0:
            reslut.append(a)
    return reslut
```

swift 的答案：

```Swift
func findDuplicates(_ nums:inout [Int]) -> [Int] {
    var result:[Int] = []
    for index in nums {
        let a = abs(index)
        if nums[a - 1] > 0 {
            nums[a-1] = nums[a-1] * -1
        } else {
            result.append(a)
        }
    }
    
    return result
}
```

这题的要求是不能增加额外的内存且只能遍历数组一次，一开始我是想不到怎么实现的。想了半天之后，决定看一下答案，看了答案之后有种豁然开朗的感觉。之前处理数组时，除了增删改查，从来没想过能把数组元素中改成它的相反数，通过是否修改过相反数来判断这个元素是否出现过一次。这种解法只有在这题中合适，因为数组中的元素必须是整数，且题目中说的重复数字只出现2次。

做完上面那题，再做 [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array) 就会发现这道理也可以参考上面的方法，把出现的元素设置为相反数，遍历完后，数组元素为正的对应下标+1就是原来数组中没有出现的元素。

## Review

这是看 leetcode 的题目讨论时，发现的一个新大陆：[GeeksForGeeks](https://www.geeksforgeeks.org/) 是计算机科学百科，涵盖了所有计算机科学核心课程。

## Tips

## Share

这周尝试了写一个爬虫，学到不少工作之外的东西。之前自学的 python 终于又有练手的机会了。

写了个简单的总结: [一次简单的爬虫经历](https://htxian.github.io/%E4%B8%80%E6%AC%A1%E7%AE%80%E5%8D%95%E7%9A%84%E7%88%AC%E8%99%AB%E7%BB%8F%E5%8E%86/)





