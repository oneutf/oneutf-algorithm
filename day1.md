## 算法笔记-oneutf

### 两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

示例：
```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

解题思路：
1. 暴力破解法为双重循环，时间复杂度为O(n^2)，在此不做示例
2. 需要采用Map，将数组值和下标以键对值方式存入Map中，利用Map原生方法判断所需差值是否存在，存在则根据键值下标，不存在则将当前数值值以及下标存入Map集合

代码：
``` javaScript
const map = new Map();
for(let i = 0; i < nums.length; i ++){
  const diff = target - nums[i]; // 取出当前元素所需要的数
  if(map.has(diff)){ // 判断是否存在于Map
    return [map.get(diff), i]; // 存在则返回Map对应值，和下标
  }else{
    map.set(nums[i], i); // 不存在则将当前元素存入Map
  }
}
```

代码分析：
一次遍历即可完成，时间复杂度为O(n)


### 两数相加

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：
```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

解题思路：


代码：
``` javaScript
var addTwoNumbers = function (l1, l2) {
    const head = new ListNode("head");
    let temp = head;
    let add = 0, sum = 0;
    let p = l1, q = l2;
    while (p || q) {
        sum = (p ? p.val : 0) + (q ? q.val : 0) + add;
        temp.next = new ListNode(sum % 10);
        temp = temp.next;
        add = sum >= 10 ? 1 : 0;
        p && (p = p.next);
        q && (q = q.next);
    }
    add && (temp.next = new ListNode(add));
    return head.next;
};
```

代码分析：

