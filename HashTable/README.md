
哈希表就是一种以键-值(key-indexed) 存储数据的结构，我们只要输入待查找的值即 key，即可查找到其对应的值。例如若关键字为k，则其值存放在 f(k) 的存储位置上，由此不需比较便可直接取得所查记录。称这个对应关系 f 为散列函数，按这个思想建立的表为哈希表（散列表）。

哈希查找第一步就是使用哈希函数将键映射成索引，这种映射函数就是`哈希（散列）函数`。哈希函数需要易于计算并且能够均匀分布所有键。一个好的哈希函数必须在理论上非常的快、稳定并且是可确定的。常用的哈希函数一般基于常见的运算，比如加法、乘法和移位运算，如以下方法：

1. 直接定址法：取关键字或关键字的某个线性函数值为散列地址。即或hash(k) = k 或者 hash(k) = a*k +b，其中a, b为常数（这种散列函数叫做自身函数）
2. 数字分析法：假设关键字是以r为基的数，并且哈希表中可能出现的关键字都是事先知道的，则可取关键字的若干数位组成哈希地址。
3. 平方取中法：取关键字平方后的中间几位为哈希地址。通常在选定哈希函数时不一定能知道关键字的全部情况，取其中的哪几位也不一定合适，而一个数平方后的中间几位数和数的每一位都相关，由此使随机分布的关键字得到的哈希地址也是随机的。取的位数由表长决定。
4. 折叠法：将关键字分割成位数相同的几部分（最后一部分的位数可以不同），然后取这几部分的叠加和（舍去进位）作为哈希地址。
5. 除留余数法：取关键字被某个不大于散列表表长m的数p除后所得的余数为散列地址。对p的选择很重要，一般取素数或m，若p选择不好，容易产生冲突。
	
DEK：Knuth在《编程的艺术 第三卷》的第六章排序和搜索中给出一个 Hash 函数如下：

    long DEKHash(string str)
    {     long hash = str.length();
        for(int i = 0; i < str.length(); i++)
        {
            hash = ((hash << 5) ^ (hash >> 27)) ^ str[i];
        }
        return hash;
    } 
对不同的关键字可能得到同一散列地址，即k1 != k2，而f(k1)=f(k2)，这种现象称为冲突（Collision），避免hash碰撞碰撞的方法有：

* `拉链法`：将大小为M的数组的每一个元素指向一个条链表，链表中的每一个节点都存储散列值为该索引的键值对。
* `开放定址法`：使用大小为M的数组来保存N个键值对，其中M>N，使用数组中的空位解决碰撞冲突。其中最简单的是线性探测法，当碰撞发生时即一个键的散列值被另外一个键占用时，直接检查散列表中的下一个位置即将索引值加1。
* `再散列`：在上次散列计算发生冲突时，利用该次冲突的散列函数地址产生新的散列函数地址，直到冲突不再发生。
* 建立一个公共溢出区。

为什么一般hashtable的桶数会取一个`素数`？

首先来说假如关键字是随机分布的，那么无所谓一定要模质数。但在实际中往往关键字有某种规律，例如大量的等差数列，那么公差和模数不互质的时候发生碰撞的概率会变大，而用质数就可以很大程度上回避这个问题。


