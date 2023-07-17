---
description: 区间划分（Interval Partitioning Problem）也被称为区间着色（Interval Coloring Problem）
---

# 🦽 区间划分

## 题目描述

给定 `n` 个请求的集合 `{1， 2， ...， n}`，其中`i`请求在时间 `s（i）` 开始，在时间 `f（i）` 结束，找到调度所有请求所需的最小资源数，以便不会同时将两个请求分配给同一资源。

```java
public int intervalPartitioning(int[][] intvs) {
    // TODO
}
```

教室调度：寻找最少的教室数目能安排完所有讲座，保证没有两个讲座在同一时间出现在同一教室。如下图，表示10个讲座被安排在了4间教室中：

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>第一种划分</p></figcaption></figure>

实际更好的安排方案是，将10个讲座按照下图的方式分配到3间教室中：

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>更好的划分</p></figcaption></figure>

## 解题思路

1. 按开始时间升序排列
2. 第一个区间占用第一个资源
3. 维护一个存储资源的优先级队列`resources`，存放每个相容集
4. 对余下的区间逐个判断，若找到与之相容的（且结束时间最小的）资源，则放入
5. 没有的话，就另外创资源

## 算法实现

<details>

<summary>算法的抽象描述</summary>

{% code overflow="wrap" lineNumbers="true" %}
```java
Let R be the set of all requests
Let d = 0 be the number of resources
while !R.empty():
  Choose a request i ∈ R that has the earliest start time
  if i can be assigned to some resource k <= d:
    assign request i to resource k
  else:
    allocate a new resouparce d+1
    assign request i to resource d+1
    d = d + 1java
return d
```
{% endcode %}

</details>

<details>

<summary>java语言描述</summary>

{% code overflow="wrap" %}
```java
private static final Comparator<int[]> COMPARATOR = Comparator.comparingInt(ls -> ls[0]);

public int intervalPartition(int[][] intvs) {
    if (intvs == null || intvs.length == 0) {
        return 0;
    }
    Arrays.sort(intvs, COMPARATOR);
    Queue<Integer> resources = new PriorityQueue<>();
    resources.add(intvs[0][1]);
    for (int i = 1; i < intvs.length; i++) {
        if (intvs[i][0] >= resources.element()) {
            resources.remove();
        }
        resources.add(intvs[i][1]);
    }
    return resources.size();
}
```
{% endcode %}

</details>
