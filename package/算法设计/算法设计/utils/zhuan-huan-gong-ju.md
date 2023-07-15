---
description: 一般是Array转List，List转Array。
---

# 🕎 转换工具

## Array => List

{% tabs %}
{% tab title="Arrays.asList" %}
{% code title="长度不可变" overflow="wrap" lineNumbers="true" %}
```java
Integer[] array = new Integer[]{2, 1, 3, 4};
List<Integer> list = Arrays.asList(array);
```
{% endcode %}
{% endtab %}

{% tab title="构造器" %}
{% code title="数据量大时效率低" overflow="wrap" lineNumbers="true" %}
```java
Integer[] array = new Integer[]{2, 1, 3, 4};
List<Integer> list = new ArrayList<>(Arrays.asList(array));
```
{% endcode %}
{% endtab %}

{% tab title="Collections.addAll" %}
{% code title="高效率" overflow="wrap" lineNumbers="true" %}
```java
Integer[] array = new Integer[]{2, 1, 3, 4};
List<Integer> list = new ArrayList<>(array.length);
Collections.addAll(list, array);
```
{% endcode %}
{% endtab %}

{% tab title="Stream流" %}
<pre class="language-java" data-title="方便" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-java">// 注意Stream.of方法不行
int[] array = new int[]{2, 1, 3, 4};
<strong>List&#x3C;Integer> list = Arrays.stream(array).boxed().collect(Collectors.toList());
</strong></code></pre>
{% endtab %}
{% endtabs %}

## List => Array

{% tabs %}
{% tab title="List.toArray" %}
{% code title="只能转为包装类型Array" overflow="wrap" lineNumbers="true" %}
```java
List<Integer> list = Stream.of(1, 2, 4, 3).collect(Collectors.toList());
Integer[] array = list.toArray(new Integer[0]);
```
{% endcode %}
{% endtab %}

{% tab title="Stream流" %}
{% code title="可以转为int[]，简洁" overflow="wrap" lineNumbers="true" %}
```java
List<Integer> list = Stream.of(1, 2, 4, 3).collect(Collectors.toList());
int[] array = list.stream().mapToInt(Integer::intValue).toArray();
```
{% endcode %}
{% endtab %}
{% endtabs %}

## int\[] => Integer\[]

{% tabs %}
{% tab title="Stream流" %}
{% code title="转为流，再装箱" overflow="wrap" lineNumbers="true" %}
```java
int[] array = new int[]{1, 2, 4, 3};
Integer[] wrapArray = Arrays.stream(array).boxed().toArray(Integer[]::new);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Integer\[] => int\[]

{% tabs %}
{% tab title="Stream流" %}
{% code title="转为IntStream，再转Array" overflow="wrap" lineNumbers="true" %}
```java
Integer[] wrapArray = new Integer[]{1, 2, 4, 3};
int[] array = Arrays.stream(wrapArray).mapToInt(Integer::intValue).toArray();
```
{% endcode %}
{% endtab %}
{% endtabs %}
