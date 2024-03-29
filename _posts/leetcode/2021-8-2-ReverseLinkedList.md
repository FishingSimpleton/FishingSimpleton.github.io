---
layout: blog
book: true
title:  "leetcode[反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)]by DylanChou 刷leetcode心得"
background-image: http://ot1cc1u9t.bkt.clouddn.com/17-7-15/82431810.jpg
date:   2021-8-2 16:04:21
category: LeetCode
tags:
- LeetCode
- 链表
---


#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

难度简单1908收藏分享切换为英文接收动态反馈

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
```

**示例 3：**

```
输入：head = []
输出：[]
```



### 1、迭代反转链表

该算法的实现思想非常直接，就是从当前链表的首元节点开始，一直遍历至链表的最后一个节点，这期间会逐个改变所遍历到的节点的指针域，另其指向前一个节点。

具体的实现方法也很简单，借助 3 个指针即可。以图 1 中建立的链表为例，首先我们定义 3 个指针并分别命名为 beg、mid、end。它们的初始指向如图 3 所示：



![迭代反转链表的初始状态](http://c.biancheng.net/uploads/allimg/200713/0U23460R-2.gif)
图 3 迭代反转链表的初始状态


在上图的基础上，遍历链表的过程就等价为：3 个指针每次各向后移动一个节点，直至 mid 指向链表中最后一个节点（此时 end 为 NULL ）。需要注意的是，这 3 个指针每移动之前，都需要做一步操作，即改变 mid 所指节点的指针域，另其指向和 beg 相同。

1) 在图 3 的基础上，我们先改变 mid 所指节点的指针域指向，另其和 beg 相同（即改为 NULL），然后再将 3 个指针整体各向后移动一个节点。整个过程如图 4 所示：



![迭代反转链表过程一](http://c.biancheng.net/uploads/allimg/200713/0U2345228-3.gif)
图 4 迭代反转链表过程一



2) 在图 4 基础上，先改变 mid 所指节点的指针域指向，另其和 beg 相同（指向节点 1 ），再将 3 个指针整体各向后移动一个节点。整个过程如图 5 所示：



![迭代反转链表过程二](http://c.biancheng.net/uploads/allimg/200713/0U2343502-4.gif)
图 5 迭代反转链表过程二



3) 在图 5 基础上，先改变 mid 所指节点的指针域指向，另其和 beg 相同（指向节点 2 ），再将 3 个指针整体各向后移动一个节点。整个过程如图 6 所示：



![迭代反转链表过程三](http://c.biancheng.net/uploads/allimg/200713/0U2345331-5.gif)
图 6 迭代反转链表过程三



4) 图 6 中，虽然 mid 指向了原链表最后一个节点，但显然整个反转的操作还差一步，即需要最后修改一次 mid 所指节点的指针域指向，另其和 beg 相同（指向节点 3）。如图 7 所示：



![迭代反转链表过程四](http://c.biancheng.net/uploads/allimg/200713/0U23460G-6.gif)
图 7 迭代反转链表过程四

> 注意，这里只需改变 mid 所指节点的指向即可，不用修改 3 个指针的指向。

5) 最后只需改变 head 头指针的指向，另其和 mid 同向，就实现了链表的反转。

如下是实现整个过程的代码：

```c++
//迭代反转法，head 为无头节点链表的头指针
link * iteration_reverse(link* head) {
    if (head == NULL || head->next == NULL) {
        return head;
    }
    else {
        link * beg = NULL;
        link * mid = head;
        link * end = head->next;
        //一直遍历
        while (1)
        {
            //修改 mid 所指节点的指向
            mid->next = beg;
            //此时判断 end 是否为 NULL，如果成立则退出循环
            if (end == NULL) {
                break;
            }
            //整体向后移动 3 个指针
            beg = mid;
            mid = end;
            end = end->next;
        }
        //最后修改 head 头指针的指向
        head = mid;
        return head;
    }
}
```

### 2、递归反转链表

和迭代反转法的思想恰好相反，递归反转法的实现思想是从链表的尾节点开始，依次向前遍历，遍历过程依次改变各节点的指向，即另其指向前一个节点。

鉴于该方法的实现用到了递归算法，不易理解，因此和讲解其他实现方法不同，这里先给读者具体的实现代码，然后再给大家分析具体的实现过程：

```c++
link* recursive_reverse(link* head) {
    //递归的出口
    if (head == NULL || head->next == NULL)     // 空链或只有一个结点，直接返回头指针
    {
        return head;
    }

    else
    {
        //一直递归，找到链表中最后一个节点
        link *new_head = recursive_reverse(head->next);

        //当逐层退出时，new_head 的指向都不变，一直指向原链表中最后一个节点；
        //递归每退出一层，函数中 head 指针的指向都会发生改变，都指向上一个节点。

        //每退出一层，都需要改变 head->next 节点指针域的指向，同时令 head 所指节点的指针域为 NULL。
        head->next->next = head;
        head->next = NULL;
        //每一层递归结束，都要将新的头指针返回给上一层。由此，即可保证整个递归过程中，能够一直找得到新链表的表头。
        return new_head;
    }
}
```

仍以图 1 中的链表为例，则整个递归实现反转的过程如下：

1) 由于 head 不为 NULL，因此函数每执行到第 11 行时，递归都会深入一层，并依次将指向节点 2、3、4 的指针作为实参（head_next 的指向）参与递归。而根据递归出口的判断条件，当函数参数 head 指向的是节点 4 时满足 head->next == NULL，递归过程不再深入，并返回指向节点 4 的指针，这就是反转链表的新头指针。

因此，当递归首次退出一层时，new_head 指向的是节点 4 ，而 head 由于退出一层，指向的是节点 3，如图 8 所示。



![递归反转链表过程一](http://c.biancheng.net/uploads/allimg/200713/0U2343055-7.gif)
图 8 递归反转链表过程一



2) 在此基础上，开始执行 17、18 行代码，整个操作过程如图 9 所示，最后将 new_head 的指向继续作为函数的返回值，传给上一层的 new_head。



![递归反转链表过程二](http://c.biancheng.net/uploads/allimg/200713/0U23413F-8.gif)
图 9 递归反转链表过程二

> 注意，图中节点 3 的 next 指针域`∧`表示为 NULL。

3) 再退一层，此时 new_head 仍指向节点 4，而 head 退出一层后，指向的是节点 2。在此基础上执行 17、18 行代码，并最终将 new_head 的指向作为函数返回值，继续传给上一层的 new_head。整个操作过程如图 10 所示：



![递归反转链表过程三](http://c.biancheng.net/uploads/allimg/200713/0U234D49-9.gif)
图 10 递归反转链表过程三



4) 再退一层，此时 new_head 仍指向节点 4，而 head 退出一层后，指向的是节点 1。在此基础上执行 17、18 行代码，并返回 new_head。整个操作过程如图 11 所示：


![递归反转链表过程四](http://c.biancheng.net/uploads/allimg/200713/0U2345454-10.gif)
图 11 递归反转链表过程四


head 由节点 1 进入递归，此时 head 的指向又返回到节点 1，整个递归过程结束。显然，以上过程已经实现了链表的反转，新反转链表的头指针为 new_head。

### 3、头插法反转链表

所谓头插法，是指在原有链表的基础上，依次将位于链表头部的节点摘下，然后采用从头部插入的方式生成一个新链表，则此链表即为原链表的反转版。

仍以图 1 所示的链表为例，接下来为大家演示头插反转法的具体实现过程：

1) 创建一个新的空链表，如图 12 所示：


![创建一个空链表](http://c.biancheng.net/uploads/allimg/200713/0U2342546-11.gif)
图 12 创建一个空链表



2) 从原链表中摘除头部节点 1，并以头部插入的方式将该节点添加到新链表中，如图 13 所示：


![从原链表摘除节点 1，再添加到新链表中](http://c.biancheng.net/uploads/allimg/200713/0U2342R3-12.gif)
图 13 从原链表摘除节点 1，再添加到新链表中



3) 从原链表中摘除头部节点 2，以头部插入的方式将该节点添加到新链表中，如图 14 所示：


![从原链表摘除节点 2，再添加到新链表中](http://c.biancheng.net/uploads/allimg/200713/0U23451H-13.gif)
图 14 从原链表摘除节点 2，再添加到新链表中



4) 继续重复以上工作，先后将节点 3、4 从原链表中摘除，并以头部插入的方式添加到新链表中，如图 15 所示：


![从原链表摘除节点 3、4，再添加到新链表中](http://c.biancheng.net/uploads/allimg/200713/0U234C44-14.gif)
图 15 从原链表摘除节点 3、4，再添加到新链表中


由此，就实现了对原链表的反转，新反转链表的头指针为 new_head。

如下为以头插法实现链表反转的代码：

```c++
link * head_reverse(link * head) {
    link * new_head = NULL;
    link * temp = NULL;
    if (head == NULL || head->next == NULL) {
        return head;
    }
    while (head != NULL)
    {
        temp = head;
        //将 temp 从 head 中摘除
        head = head->next;

        //将 temp 插入到 new_head 的头部
        temp->next = new_head;
        new_head = temp;
    }
    return new_head;
}
```

### 4、就地逆置法反转链表

就地逆置法和头插法的实现思想类似，唯一的区别在于，头插法是通过建立一个新链表实现的，而就地逆置法则是直接对原链表做修改，从而实现将原链表反转。

值得一提的是，在原链表的基础上做修改，需要额外借助 2 个指针（假设分别为 beg 和 end）。仍以图 1 所示的链表为例，接下来用就地逆置法实现对该链表的反转：

1) 初始状态下，令 beg 指向第一个节点，end 指向 beg->next，如图 16 所示：


![就地反转链表的初始状态](http://c.biancheng.net/uploads/allimg/200713/0U2342L7-15.gif)
图 16 就地反转链表的初始状态

```
beg=head;
end=head->next;
```



2) 将 end 所指节点 2 从链表上摘除，然后再添加至当前链表的头部。如图 17 所示：


![反转节点2](http://c.biancheng.net/uploads/allimg/200713/0U2341592-16.gif)
图 17 反转节点 2

```
 //将 end 从链表中摘除
 beg->next = end->next;
 //将 end 移动至链表头
 end->next = head;
 head = end;
 //调整 end 的指向，另其指向 beg 后的一个节点，为反转下一个节点做准备
 end = beg->next;
```



3) 将 end 指向 beg->next，然后将 end 所指节点 3 从链表摘除，再添加到当前链表的头部，如图 18 所示：


![反转节点3](http://c.biancheng.net/uploads/allimg/200713/0U2343N4-17.gif)
图 18 反转节点 3



4) 将 end 指向 beg->next，再将 end 所示节点 4 从链表摘除，并添加到当前链表的头部，如图 19 所示：


![反转节点 4](http://c.biancheng.net/uploads/allimg/200713/0U2342259-18.gif)
图 19 反转节点 4


由此，就实现了对图 1 链表的反转。 

具体实现代码如下：

```c++
link * local_reverse(link * head) {
    link * beg = NULL;
    link * end = NULL;
    if (head == NULL || head->next == NULL) {
        return head;
    }
    beg = head;
    end = head->next;
    while (end != NULL) {
        //将 end 从链表中摘除
        beg->next = end->next;
        //将 end 移动至链表头
        end->next = head;
        head = end;
        //调整 end 的指向，另其指向 beg 后的一个节点，为反转下一个节点做准备
        end = beg->next;
    }
    return head;
}
```