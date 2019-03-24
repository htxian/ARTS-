## Algorithm

> 19.Remove Nth Node From End of List
>
>  Given a linked list, remove the n-th node from the end of list and return its head.
>
>  Example:
>
>  Given linked list: 1->2->3->4->5, and n = 2.
>
>  After removing the second node from the end, the linked list becomes 1->2->3->5.
>
>  Note:
>
>  Given n will always be valid.

实现方式是使用两个指针，一个快指针，先按顺序执行到第n个节点，然后慢指针就开始执行，

当快指针执行完最后一个节点时，慢指针所指的下一个节点就是待删除节点。使用的swift语言来写的

```Swift
class Solution {
    func removeNthFromEnd(_ head: ListNode?, _ n: Int) -> ListNode? {

        let temp = ListNode(0)
        temp.next = head
        var fast: ListNode? = temp
        var slow: ListNode? = temp
        
        for _ in 0 ..< n {
            if fast == nil {
                break
            }
            fast = fast!.next
        }
        while fast != nil && fast!.next != nil {
            slow = slow!.next
            fast = fast!.next
        }
        slow!.next = slow!.next!.next

        return temp.next
    }
}
```

## Review

最近重新学习了一下 iOS 的相关知识，看了一下官方的文档。

这个是一个关于响应链的文档：[Using Responders and the Responder Chain to Handle Events](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/using_responders_and_the_responder_chain_to_handle_events?language=objc)

##### 结论如下：

1.只有继承 UIResponder 的对象才能处理事件。

2.事件的响应过程分为3个阶段：事件的产生，事件的传递，事件的响应

3.事件的传递是根据以下步骤找到最合适的view：产生触摸事件->UIApplication事件队列->[UIWindow hitTest:withEvent:]->返回**更合适**的view->[子控件 hitTest:withEvent:]->返回**最合适**的view

4.找到合适的view后，执行toches方法。将事件顺着响应者链往上传递，将事件交给上一个响应者进行处理 。

## Tips

这周工作中遇到一个算是比较简单的问题，因为我们知道 ```UICollectionView``` 没有和 ```UITableView``` 一样有 ```tableHeaderView``` ，所以我的处理办法是往 ```UICollectionView``` 上增加一个View，然后设置 ```UICollectionView``` 的contentInset 。

具体代码如下：

```objective-c
    UICollectionViewFlowLayout *layout = [[UICollectionViewFlowLayout alloc] init];
    layout.scrollDirection = UICollectionViewScrollDirectionVertical;
    layout.itemSize = CGSizeMake([UIScreen mainScreen].bounds.size.width, 100);
    UICollectionView *collection = [[UICollectionView alloc] initWithFrame:CGRectZero collectionViewLayout:layout];
    [self.view addSubview:collection];
    [collection mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.mas_equalTo(0);
    }];
    
    UIView *headerView = [[UIView alloc] init];
    [collection addSubview:headerView];
    //通过 Masonry 设置 headerView 会存在设置的尺寸不对
    headerView.frame = CGRectMake(0, 0, self.collection.frame.size.width, 200);
    self.collection.contentInset = UIEdgeInsetsMake(200, 0, 0, 0);
```

## Share

待完成