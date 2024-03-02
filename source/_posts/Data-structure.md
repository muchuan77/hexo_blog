---

title: Data structure
date: 2024-03-02 17:12:05
tags:
  -data structure
  -note
category: java
mathjax: true
---

# 关于数据结构的学习记录

## 1.二分查找

在有序数组A内，查找值target

---

### (1)基础版
```java
/*
二分查找基础版
Params： a -待查找的升序数组
        target - 待查找的目标值
Returns：
        找到则返回索引
        找不到返回 -1
 */
public static int binarySearchBasic(int[] a, int target){
    int i = 0, j=a.length - 1;//指针
    while (i<=j){//在范围内
        int m = (i+j)/2;
        if (target < a[m]){//目标值在左边
            j = m-1;
        } else if (a[m] < target){//右边
            i = m + 1;
        } else {//找到
            return m;
        }
    }
    return -1;
}
```

---

### (2)查找改动版

```java
/*
二分查找改动版
Params： a -待查找的升序数组
        target - 待查找的目标值
Returns：
        找到则返回索引
        找不到返回 -1
 */

public static int binarySearchAlternative(int[] a, int target){
    int i = 0, j=a.length;//指针
    while (i < j){//在范围内
        int m = (i + j) >>> 1;
        if (target < a[m]){//目标值在左边
            j = m;
        } else if (a[m] < target){//右边
            i = m + 1;
        } else {//找到
            return m;
        }
    }
    return -1;
}
```

---

## 2.动态数组

```java
import java.util.Iterator;
import java.util.function.Consumer;

public class DynamicArray implements Iterable<Integer> {

    private int size = 0;// 逻辑大小
    private int capacity = 8;// 容量
    private int[] array = {};
    
    //插入
    //遍历
    //删除
    //扩容
    
}
```

---

### （1）插入

```java
/*
向最后位置[size]添加元素
Params：element - 待添加元素
*/
public  void  addLast(int element) {
   //array[size] = element;
   //size ++;
    add(size,element);
}

/*
向 [0 ... size]位置添加元素
Params：index - 索引位置
        element - 待添加元素
*/
public void add(int index, int element){
    if (index >=0 && index < size) {
        System.arraycopy(array, index, array, index + 1, size - index);
    }
    array[index] = element;
    size ++;
}


//查询
/*
查询元素
   Params： index - 索引位置，在[0，size)区间内
   Returns：该索引位置的元素
 */
 public int get(int index) {//[0..size)
      return array[index];
 }
```

---

### (2) 遍历

```java
/*
遍历方法1
Params：consumer - 遍历要执行的操作，入参：每个元素
 */
public void foreach(Consumer<Integer> consumer){
    for (int i=0;i<size-1;i++){
        //System.out.println(array[i]);
        //提供 array[i]
        // 返回 void
        consumer.accept(array[i]);
    }
}
/*
遍历方法2 - 迭代器遍历
 */
@Override
public Iterator<Integer> iterator() {
    return new Iterator<Integer>() {
        int i = 0;
        @Override
        public boolean hasNext() {// 有没有下一个元素
            return i<size;
        }

        @Override
        public Integer next() { // 返回当前元素，并移向下一个元素
            return array[i++];
        }
    };
}


/*
遍历方法3 - stream流遍历
 */
public IntStream stream(){
    return IntStream.of(Arrays.copyOfRange(array, 0, size));
}
```

---

### （3）删除

```java
public int remove(int index) {// [0..size)
    int removed = array[index];
    if (index <size -1) {
        System.arraycopy(array, index + 1, array,
                index, size - index - 1);
    }
    size--;
    return removed;
}
```

---

### （4）扩容

```java
private void checkAndGrow() {
    //容量检查
    if (size == 0){
        array = new int[capacity];
    }else if (size == capacity){
        // 进行扩容,1.5 1.618 2
        capacity += capacity >> 1;
        int[] newArray = new int[capacity];
        System.arraycopy(array, 0,
                newArray, 0, size);
        array = newArray;
    }
}
```