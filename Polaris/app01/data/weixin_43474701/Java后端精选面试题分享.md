
--- 
title:  Java后端精选面试题分享 
tags: []
categories: [] 

---
### Java后端精选面试题分享

**一、选择题**
1.  在Linux系统中，使用vi编辑文件时，命令模式下删除光标所在位置的后面一个字符的命令是（B） A、z B、x C、c D、v 1.  在Linux系统中，查看IP的命令是（D） A、cat B、vi C、ipconfig D、ifconfig 1.  Linux查看文件的命令，若希望在查看文件内容过程中可以用光标上下移动来查看文件内容，应使用的命令是（D） A、cat B、more C、tail D、less 1.  Linux文件权限一共10位长度，分成四段，第三段表示的内容是（B） A、文件所有者的权限 B、文件所有者所在组的权限 C、其他用户的权限 D、文件类型 1.  数据库事务有四个特性，下列哪个不属于（A） A、回归性 B、原子性 C、隔离性 D、持久性 1.  一个MySQL的表，有F1、F2、F3、F4、F5、F6 这6个字段，建立一个联合索引包含三个字段F2、F4、F5，搜索条件包含哪些字段是不能使用这个联合索引（A） A、F2 B、F2、F4 C、F2、F5 D、F2、F4、F5 1.  在SQL语句中，删除表结构的命令是（A） A、DROP TABLE B、DELETE TABLE B、ALTER TABLE D、REMOVE TABLE 1.  在数据库系统中，产生不一致的根本原因是（D） A数据存储量太大 B没有严格保护数据 C未对数据进行完整性控制 D数据冗余 1.  小张用十六进制、八进制和十进制写了如下的一个等式：52-19=33。式中三个数是各不相同进位制的数，试问52、19、33，分别是（B） A、八进制，十进制，十六进制 B、十进制，十六进制，八进制 C、八进制，十六进制，十进制 D、十进制，八进制，十六进制 1.  咖啡店销售系统具体需求为：咖啡店店员在卖咖啡时，可以根据顾客的要求加入各种配料，并根据加入配料价格的不同来计算总价。若要设计该系统可以应该采用（A）进行设计 A、装饰模式 B、单例模式 C、原型模式 D、组合模式 
11.HTTP返回码中表示”页面永久性移走“的是（C） A、401 B、400 C、302 D、301

12.用CIDR表示16.158.165.91/22，则这个网络的子网掩码为（B） A、255.255.251.0 B、255.255.252.0 C、255.255.253.0 D、255.255.254.0
1.  测试网络是否有问题的ping命令所使用的报文是（C） A、TCP B、UDP C、ICMP D、HTTP 1.  基于比较的排序算法是（A） A、快速排序 B、桶排序 C、基数排序 D、计数排序 1.  在下面的程序段中，对x的赋值语句的频度为（C） For（k=1；k&lt;=n；k++） For（j=1；j&lt;=n；j++） x=x＋1 A、O(n) B、O(2n) C、O(n²) D、O(log2n) 1.  下列步骤中，不属于动态规划算法基本步骤的是（D） A、算出最优解 B、构造最优解 C、定义最优解 D、比较最优解 1.  非线性结构是数据元素之间存在一种（D） A、一对多关系 B、一对一关系  C、多对一关系 D、多对多关系 
18.若某线性表中最常用的操作是取第i个元素和找第i个元素的前趋元素,则采用（C）存储方式最节省时间。 A、单链表 B、双链表 C、顺序表 D、单循环链表

19.设有100个元素,用二分法查找时,最大比较次数是（B） A、2 B、7 C、8 D、9

20.链表具有的特点不包括（A） A、可随机访问任一元素 B、插入删除不需要移动元素 C、不必事先估计存储空间 D、所需空间与线性表长度成正比

**二.简答题** 老板一共需要给某个员工发奖金n元，可以选择一次发1元，也可以选择一次发2元，也可以选择一次发3元。请问老板给这位员工发放完n元奖金共有多少种不同的方法？

数据范围：1 &lt;= n &lt;= 10

输入例子1: 2

输出例子1: 2

例子说明1: 一共有2元奖金，有两种发放方法；第一中：分别每次发放1元，两次发放完，第二种一次全部发放完

输入例子2: 3

输出例子2: 4

例子说明2: 一共有3元奖金，有4种发放方法；第一种：分别每次发放1元，3次发放完，第二种先第一次发2元，第二次发1元； 第三种第一次发1元，第二次发2元； 第四种方法一次全部发放完 **答案：** 分析：可以这样想，发5元怎么发？ 1：先发1块的情况下，剩下4块是不是就和发4块的方法一样了？ 2：先发2块的情况下，剩下3块是不是就和发3块的方法一样了？ 3：先发3块的情况下，剩下2块是不是就和发2块的方法一样了？ 4：先发4块的情况下，剩下1块是不是就和发1块的方法一样了？ 5：5块一次性发完，唯一方法 这很递归嘛~ 即符合 f(n) = f(n-1) + f(n-2) + … + f(1) + 1

```
public class GiveMoney {<!-- -->
    public static void main(String[] args) {<!-- -->
        Scanner scanner = new Scanner (System.in);
        System.out.print ("输入要发的奖金:");
        int number = scanner.nextInt ();
        System.out.println ("您有" + f (number) + "种方法发完" + number + "元奖金!!");
    }

    /**
     * 获取 发奖金可用的总方法 的方法
     *
     * @param number 要发的钱数
     * @return 总方法数
     */
    public static int f(Integer number) {<!-- -->
        // 设置递归结束条件
        if (number == 1) {<!-- -->
            return 1;
        }
        // 实现 f(n) = f(n-1) + f(n-2) + ... + f(1) + 1
        int count = 0;
        for (int i = number - 1; i &gt;= 1; i--) {<!-- -->
            count = f (i) + count;
        }
        return count + 1;
    }
}

```
1. 一张学生成绩表score，部分内容如下： name course grade 张三 操作系统 67 陈四 数据结构 86 刘五 软件工程 89 用一条SQL 语句查询出每门课都大于80 分的学生姓名。（20分） select distinct name from score where name not in(select distinct name from score where sorce&gt;=80)