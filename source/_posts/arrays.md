---
title: Arrays
date: 2023-11-19 16:45:08
tags: 
 - Arrays
 - Note
category: Java
mathjax: true
---

# 关于java的Arrays类使用方法

## 介绍 
 Arrays类位于 java.util 包中，主要包含了操作数组的各种方法。  

```java
 import java.util.Arrays;
```

---

## 填充数组 fill
 ```java
 int num = scanner.nextInt();
        int a= scanner.nextInt();
        int [] arr= new int[num];//建立一个名为arr的数组,大小为num
        Arrays.fill(arr,a);//给所有赋值为a
        String string_a = Arrays.toString(arr);//将数组中的内容全部打印出来
        System.out.println(string_a);

        int m =scanner.nextInt();
        int n =scanner.nextInt();
        int q =scanner.nextInt();
        Arrays.fill(arr,m,n,q);//给第m位到第n位(不包括n位)赋值q
        String string_mnq = Arrays.toString(arr);
        System.out.println(string_mnq);
 ```

---

## 数组排序 sort

 ### 数字排序
 ```java
 int[] intArray = new int[] {4,89,-11,88};
        Arrays.sort(intArray);
        String intArray_sort = Arrays.toString(intArray);
        System.out.println(intArray_sort);
 ```

 ### 字符串排序，先大写后小写
 ```java
 String[] strArray = new String[] { "x", "b", "M" };
        Arrays.sort(strArray);
        String strArray_sort = Arrays.toString(strArray);
        System.out.println(strArray_sort);
 ```
 ### 忽略大小写排序
 ```java
 Arrays.sort(strArray, String.CASE_INSENSITIVE_ORDER);
        //输出： [b, M ,x]
 ```
 ### 反向排序 使用时注意引入
 ```import java.util.Collections;```  
 ```java
 Arrays.sort(strArray, Collections.reverseOrder());
        //输出： [x, b ,M]
 ```
 ### 忽略大小写的反向排序
 ```java
 Arrays.sort(strArray, String.CASE_INSENSITIVE_ORDER);
        Collections.reverse(Arrays.asList(strArray));
        //输出： [x, M ,b]
 ```
 ### 选择数组指定位置排序
 ```java
 int[] arr_c = {8,7,2,4,6,0};
        Arrays.sort(arr_c,0,3);//给第0位（0开始）到第3位（不包括）排序
        String str = Arrays.toString(arr_c); // Arrays类的toString()方法能将数组中的内容全部打印出来
        System.out.print(str);
        //输出: [2, 7, 8, 4, 6, 0]
 ```

---

## 比较数组元素是否相等 equals
 ```java
 int[] arr1 = {1,2,3};
        int[] arr2 = {1,2,3};
        System.out.println(Arrays.equals(arr1,arr2));
        //输出：true
        //如果是arr1.equals(arr2),则返回false，因为equals比较的是两个对象的地址，不是里面的数，而Arrays.equals重写了equals，所以，这里能比较元素是否相等。
 ```

---

## 二分查找法找指定元素的索引值(下标) binarySearch
 ```java
 int[] arr_b = {10,20,30,40,50};
        System.out.println(Arrays.binarySearch(arr_b, 30));
        //输出：2 （下标索引值从0开始）
 ```

---

## 截取数组 copyOf copy OfRange
 ```java
 int[] arr_o = {10,20,30,40,50};
        int[] arr1_o = Arrays.copyOf(arr_o, 3);
        String str1_o = Arrays.toString(arr1_o);
        System.out.print(str1_o);
        //输出：[10, 20, 30] （截取arr数组的3个元素赋值给新数组arr1）

        int []arr_co = {10,20,30,40,50};
        int []arr1_co = Arrays.copyOfRange(arr,1,3);
        String str1_co = Arrays.toString(arr1_co);
        System.out.print(str1_co);
        //输出：[20, 30] （从第1位（0开始）截取到第3位（不包括））
 ```

---

## 总结
常用的主要是
```java
Arrays.fill//填充数组内容
Arrays.sort//排序
Arrays.equals//比较大小
Arrays.binarySearch//二分法查找
Arrays.copyOf Arrays.copyOfRange//截取数组组成新数组
```

### 参考资料
[二分法](https://blog.csdn.net/u012194956/article/details/79103843)  
[数组](https://blog.csdn.net/JianZuoGuang/article/details/104280654)
