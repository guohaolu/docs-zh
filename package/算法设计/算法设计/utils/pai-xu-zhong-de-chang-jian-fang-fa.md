# 📹 排序工具

## Array

### 排序

#### 基本类型排序

算法：Dual-Pivot Quicksort

```java
// 场景1：升序排序
int[] ls = {1, 2, 3, 7, 6};
Arrays.sort(ls);
// 场景2：降序排序（此处不能为基础类型）
Integer[] ls = {1, 2, 3, 7, 6};
Arrays.sort(ls, Collections.reverseOrder());
```

#### 对象排序

要求对象是可比较的（实现了Comparable接口）

```java
// x.compareTo(y), x < y 返回-1；x = y 返回0；x > y 返回1
public interface Comparable<T> {
    public int compareTo(T o);
}
```

算法：TimSort（稳定排序）

**二维数组自定义排序**

{% code overflow="wrap" %}
```java
// int[][]看成元素为int[]的Array，要求按照第一个元素升序，若第一个元素相同，则按照第三个元素降序，若第三个元素也相同，按照第二个元素升序。
```
{% endcode %}

```java
public class SortTest {
    private static final Comparator<int[]> COMPARATOR = (o1, o2) -> {
        if (o1[0] != o2[0]) {
            return o1[0] - o2[0];
        }
        if (o1[2] != o2[2]) {
            return o2[2] - o1[2];
        }
        return Integer.compare(o1[1], o2[1]);
    };

    @Test
    void testArraySort() {
        int[][] array = new int[4][3]; // 4个元素，每个元素为int[3]
        array[0] = new int[]{5, 2, 3};
        array[1] = new int[]{6, 8, 3};
        array[2] = new int[]{6, 9, 10};
        array[3] = new int[]{6, 8, 10};
        Arrays.sort(array, COMPARATOR);
        for (int[] ls : array) {
            System.out.println(Arrays.toString(ls));
        }
    }
}
```

#### NOTE

`Arrays.asList()`方法返回的List是长度不可变的，若违反则抛出异常：（如：`UnsupportedOperationException at java.util.AbstractList.add`）

## Comparator比较器

### 介绍

> `Comparator`是一个函数式接口，常被用在排序（`Collections.sort` or `Arrays.sort`）。

### 非静态方法

#### compare

方法契约`int compare(T o1, T o2)`

若T为`Integer`，`return o1 - o2`即为升序，`return o2 - o1`为降序。

#### thenComparing

将比较器组合在一起。

1. c1.thenComparing(c2)：c1比较后为0，则再通过c2排序。
2. c1.thenComparing(Function keyExtractor)：通过转换后的值进行自然排序，一般转换为Integer之类的值（如：Student::getAge）。注意，转换后不允许为null，不然空指针异常。
3. c1.thenComparing(Function keyExtractor, Comparator keyComparator)：同上，只是自然排序变为了keyComparator指定排序。

#### reversed

对排序进行反转。

#### thenComparingXxx

将对象转为数值后进行自然排序。

### 静态方法

1. reverseOrder和naturalOrder属于直接提供比较器。
2. nullsFirst和nullsLast相当于对你本身的比较器做了一下封装，定义了null值的位置。
3. comparing方法比较常用，但需要注意null值。

### 排序规则工具方法
