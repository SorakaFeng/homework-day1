## 判断题

1、 ABCD  
AB 说的可以极大提高 没说一定; C 看起来也没毛病; D 说的是事实;

2、 D
用注释 '!'清空, 用空字符串应该也可以代替吧

## 简答题

先调用钩子函数

然后就进行判断
text children 的相互对比
做些是不是特殊值 字段存不存在的判断

新的有 text 老的也有 text 不一样就更新 text
新的有 text 老的是 children 清掉老的 加上新的
新的啥都没有 老的有东西 清空老的
新的是 children 老的是 text 清空 text, 加上 children
新的是 children 老的也是 children 看下内存地址是不是一样的 不一样 递归进去，遍历里面的子节点
children 和 text 互斥

```if (新的有text) {
    if(老的也有text && text不同) {
        替换text;
    } else if(老的是children) {
        清空老的, 加上text;
    } else if(老的没有) {
        加上新的;
    }
} else if (新的有children){
    if (老的也有children) {
        if (新的children地址 !== 老的children) {
            递归调用;
        }
    } else if (老的有text) {
        清空text; 添加新的children;
    } else if (老的没有) {
        添加新的children;
    }
} else if(新的没有) {
    if(老的有text 或者 children) {
        清空;
    }
}
```

调用 postpatch 钩子函数
