

### 三目运算符

1、三目运算符：又称之为三元运算符

2、格式：(关系表达式)?表达式1:表达式2;

3、如果关系表达式的结果为true，运算后的结果是表达式1；

4、如果关系表达式的结果为false，运算后的结果是表达式2；

```
int a =15;
int b =30;
int c =(a>b)?a:b;
System.out.println(c);
c的结果为30.
```

### 快速打印

```
public class 循环打印 {
    public static void main(String[] args) {
        //遍历数组的元素
        for (int x:number){
            System.out.println(x);
        }
    }
}
```



```java
Integer i = 10;  //装箱
int n = i;   //拆箱
Integer i = Integer.valueOf(10)
int n = i.intValue(); 
```