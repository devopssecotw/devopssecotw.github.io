# dsa data structure. algorithm 數據結構 算法
## 常见数据结构与算法
### 搜索中常见数据结构与算法探究
#### 一
##### 前言
ES现在已经被广泛的使用在日常的搜索中，Lucene作为它的内核值得深入研究，比如FST，下面就用两篇分享来介绍一些本文的主题：

第一篇主要介绍数据结构和算法基础和分析方法，以及一些常用的典型的数据结构；

第二篇主要介绍图论，以及自动机，KMP，FST等算法；

下面开始第一篇：
##### 提出问题
“算法是计算机科学领域最重要的基石之一“

“编程语言虽然该学，但是学习计算机算法和理论更重要，因为计算机算法和理论更重要，因为计算机语言和开发平台日新月异，但万变不离其宗的是那些算法和理论，例如数据结构、算法、编译原理、计算机体系结构、关系型数据库原理等等。“

——《算法的力量》



2.1.1 案例一
设有一组N个数而要确定其中第k个最大者，称之为选择问题。常规的解法如下：

该问题的一种解法就是将这N个数读进一个数组中，在通过某种简单的算法，比如冒泡排序法，以递减顺序将数组排序，然后返回位置k上的元素。

稍微好一点的算法可以先把前k个元素读入数组并对其排序。接着，将剩下的元素再逐个读入。当新元素被读到时，如果它小于数组中的第k个元素则忽略之，否则就将其放到数组中正确的位置上，同时将数组中的一个元素挤出数组。当算法终止时，位于第k个位置上的元素作为答案返回。

这两种算法编码都很简单，但是自然要问：哪个算法更好？哪个算法更重要？还是两个算法都足够好？使用N=30000000和k=15000000进行模拟将发现，两个算法在合理的时间量内均不能结束；每一种算法都需要计算机处理若干时间才能完成。



其实还有很多可以解决这个问题，比如二叉堆，归并算法等等。



2.2.2案例二

输入是由一些字母构成的一个二维数组以及一组单词组成。目标是要找出字谜中的单词，这些单词可能是水平、垂直、或沿对角线上任何方向放置。下图所示的字谜由单词this、two、fat和that组成。

Image

图1 字谜单词字符排列示意图

现在至少也有两种直观的算法来求解这个问题：



对单词表中的每个单词，检查每一个有序三元组（行，列，方向）验证是否有单词存在。这需要大量嵌套的for循环，但它基本上是直观的算法。

对于每一个尚未越出迷板边缘的有序四元组（行，列，方向，字符数）可以测试是否所指的单词在单词表中。这也导致使用大量嵌套的for循环。



上述两种方法相对来说都不难编码，但如果增加行和列的数量，则上面提出的两种解法均需要相当长的时间。



以上两个案例中，可以看到要写一个工作程序并不够。如果这个程序在巨大的数据集上运行，那么运行时间就变成了重要问题。



那么，使用自动机理论可以快速的解决这个问题，下一篇中给大家详细的分析。
##### 数据结构与算法基础
3.1 数据结构基础


3.1.1 什么是数据结构
在计算机领域中，数据是信息的载体，是能够输入到计算机中并且能被计算机识别、存储和处理的符号的总称。数据结构是指数据元素和数据元素之间的相互关系或数据的组织形式。数据元素是数据的的基本单位，数据元素有若干基本项组成。

3.1.2 数据之间的关系
数据之间的关系分为两类：

·      逻辑关系

表示数据之间的抽象关系，按每个元素可能具有的前趋数和直接后继数将逻辑结构分为线性结构和非线性结构。

逻辑关系或逻辑结构有如下特点：

只是描述数据结构中数据元素之间的联系规律；

是从具体问题中抽象出来的数学模型，是独立于计算机存储器的（与硬件无关）

逻辑结构的分类如下：

线性结构

树形结构

图状结构

其他结构


·      物理关系

逻辑关系在计算中的具体实现方法，分为顺序存储方法、链式存储方法、索引存储方法、散列存储方法。

物理关系或物理结构有如下特点：

是数据的逻辑结构在计算机存储其中的映像；

存储结构是通过计算机程序来实现，因而是依赖于具体的计算机语言的；

物理结构分类如下：

顺序结构

链式结构

索引结构


3.2 算法基础


3.2.1 基础概念
算法是为求解一个问题需要遵循的、被清楚指定的简单指令的集合。对于一个问题，一旦某种算法给定并且被确定是正确的，那么重要的一步就是确定该算法将需要多少诸如时间或空间等资源量的问题。如果一个问题的求解算法竟然需要长达一年时间，那么这种算法就很难能有什么用处。同样，一个需要若干个GB的内存的算法在当前的大多数机器上也是无法使用的。


3.2.2 数学基础
一般来说，估算算法资源消耗所需的分析是一个理论问题，因此需要一套数学分析法，先从数学定义开始。



定理1：如果存在正常数c和n0，使得当N>= n0时，T(N) <= cf(N)，则记为T(N) = O(f(N))。



定理2：如果存在正常数c和n0，使得当N>=n0时，T(N) <= cg(N)，则记为T(N) = Ω(g(N))。



定理3：T(N) = θ(h(N))当且仅当T(N) = O(h(N)) 和 T(N) = Ω(h(N))。



定理4：如果对每一个正常数c都存在常数n0使得当N>n0时，T(N) < cp(N)，则T(N) = o(p(N))。



这些定义的目的是要在函数间建立一种相对的级别。给定两个函数，通常存在一些点，在这些点上一个函数的值小于另一个函数的值，因此，一般宣称f(N)<g(N)，是没有什么意义的。于是，比较他们的相对增长率。当将相对增长率应用到算法分析时，会明白它是重要的度量。



如果用传统的不等式来计算增长率，那么第一个定义T(N) = O(f(N))是说T(N)的增长率小于或者等于f(N)的增长率。第二个定义T(N) = Ω(g(N))是说T(N)增长率大于或者等于g(N)的增长率。第三个定义T(N) = θ(h(N))是说T(N)的增长率等于h(N)的增长率。最后一个定义T(N) = o(p(N))说的则是T(N)的增长率小于p(N)的增长率。他不同于大O，因为大O包含增长率相同的可能性。



要证明某个函数T(N) =O(f(N))，通常不是形式的使用这些定义，而是使用一些已知的结果（比如说T(N) = O(log(N))）。一般来说，这就意味着证明是非常简单的计算而不应涉及微积分，除非遇到特殊情况。如下是常见的已知函数结果

c（常数函数）

logN（对数函数）

logN^2（对数平方函数）

N（线性函数）

NlogN

N^2（二次函数）

N^3（三次函数）

2^N（指数函数）



在使用已知函数结果时，有几点需要注意：



首先，将常数或低阶项放进大O是非常坏的习惯。不要写成T(N) = O(2*N^2)或T(N) = O(N^2 + N)。这两种情形下，正确的形式是T(N) = O(N^2)。也就是说低阶项一般可以被忽略，而常数也可以弃掉。

其次，总能够通过计算极限limN→∞f(N)/g(N)（极限公式）来确定两个函数f(N)和g(N)的相对增长率。该极限可以有四种可能的值：

极限是0：这意味着f(N) = o(g(N))。

极限是c != 0：这意味着f(N) = θ(g(N))。

极限是∞：这意味着g(N) = o(f(N))。

极限摆动：二者无关。


3.2.3 复杂度函数
正常情况下的复杂度函数包含如下两种：

时间复杂度

空间复杂度

时间和空间的度量并没有一个固定的标准，但是在正常情况下，时间复杂度的单位基本上是以一次内存访问或者一次IO来决定。空间复杂度是指在算法执行过程中需要占用的存储空间。对于一个算法来说，时间复杂度和空间复杂度往往是相互影响，当追求一个好的时间复杂度时，可能会使空间复杂度变差，即可能占用更多的存储空间；反之，当追求一个较好的空间复杂度时，可能会使时间复杂度变差，即可能占用较长的运算时间。



3.3 知识储备


3.3.1 质数分辨定理（HashTree的理论基础）
简单的说就是，n个不同的质数可以分辨的连续数的个数和他们的乘机相同。分辨是指这些连续的整数不可能有相同的余数序列。



3.3.2 Hash算法

1）Hash

Hash一般翻译成散列，也可以直接音译成哈希，就是把任意长度的输入，通过散列算法变换成固定长度的输出，该输入就是散列值。不同的输入可能散列成相同的值，确定的散列值不可能确定一个输入。

2）常见的Hash算法

MD4：消息摘要算法；

MD5：消息摘要算法，MD4的升级版本；

SHA-1：SHA-1的设计和MD4相同原理，并模仿该算法；

自定义HASH算法：程序设计者可以自定义HASH算法，比如java中重写的hashCode()方法。

3）Hash碰撞

解决Hash碰撞常见的方法有一下几种：

分离链接法（链表法）：做法是将散列到同一个值的所有元素保留在一个表中，例如JDK中的HashMap；

探测散列表：当发生Hash碰撞时，尝试寻找另外一个单元格，直到知道到空的单元为止。包括：线性探测法，平方探测法，双散列。

3.3.2树结构的基本概念

树的递归定义：一棵树是一些节点的集合。这个集合可以是空集；若不是空集，则树由根节点root以及0个或多个非空的子树组成，这些子树中每一棵的根都被来自根root的一条有向的边所连接；

树叶节点：没有儿子节点称为树叶；

深度：对于任意节点ni，ni的深度为从根到ni的唯一路径的长；

高度：对于任意节点ni，ni的高度为从ni到一片树叶的最长路径的长；

树的遍历：树的遍历分为两种，先序遍历和后续遍历。



3.3.4二叉搜索树

二叉搜索树是一棵二叉树，其中每个节点都不能有多于两个子节点。

对于二叉查找树的每一个节点X，它的左子树中所有项的值都小于X节点中的项，而它的右子树中所有项的值大于X中的项。
##### 常见数据结构与算法分析
4.1 线性数据结构

4.1.1 HashMap


·      总述

HashMap是开发中最常用的数据结构之一，数据常驻于内存中，对于小的数据量来说，HashMap的增删改查的效率都非常高，复杂度接近于O(1)。

·      数据结构和算法

o   HashMap由一个hash函数和一个数组组成；

o   数据插入，当<key,value>进入到map的时候，根据hash(key)找到对应点位置，如果位置为空，直接保存，如果位置不为空，则使用链表的方式处理；为了解决遍历链表所增加的时间，JDK中的链表在大小增大到8时，将会演变成红黑树以降低时间复杂度。为什么开始使用链表，后面使用红黑树：

§  数据量较小的时候，链表的查询效率相对来说也比较高，使用红黑树占用空间比链表要大；

§  为什么选择8，请参考泊松分布；

o   查找和删除的过程，同插入的过程类似；

o  HashMap可以支持自动扩容，扩容机制需要看具体的实现；

Image

图2 HashMap的构建过程示意图

优缺点

优点：动态可变长存储数据，快速的查询速度，查询复杂度接近O(1);

缺点：只支持小数据量的内存查询；

使用场景

在内存中小数据量的数据保存和快速查找。



4.1.2 Bloom Filter（布隆过滤器）
·      总述

布隆过滤器算法为大数据量的查找提供了快速的方法，时间复杂度为O(k)，布隆过滤器的语义为：

布隆过滤器的输出为否定的结果一定为真；

布隆过滤器的输出为肯定的结果不一定为真；

·      数据结构和算法

布隆过滤器的具体结构和算法为：

布隆过滤器包含k个hash函数，每个函数可以把key散列成一个整数（下标）；

布隆过滤器包含了一个长度为n的bit数组（向量数组），每个bit的初始值为0；

当某个key加入的时候，用k个hash函数计算出k个散列值，并把数组中对应的比特置为1；

判断某个key是否在集合时，用k个hash函数算出k个值，并查询数组中对应的比特位，如果所有的bit位都为1，认为在集合中；

布隆过滤器的大小需要提前评估，并且不能扩容；


布隆过滤器的插入过程如下：

Image

图3 布隆过滤器的构建过程示意图

判断某个key是否在集合时，用k个hash函数算出k个值，并查询数组中对应的比特位，如果所有的bit位都为1，认为在集合中

布隆过滤器无法删除数据；

布隆过滤器查询的时间复杂度为O(k)；

布隆过滤器空间的占用在初始化的时候已经固定不能扩容。

·      优缺点

优点：布隆过滤器在时间和空间上都有巨大的优势。布隆过滤器存储空间和插入/查找时间都是常数。布隆过滤器不需要存储数据本身，节省空间。

缺点：布隆过滤器的缺点是有误差。元素越多误差越高。可以通过提高hash函数的个数和扩大bit数组的长度来降低误差率；

·      场景

使用场景：缓存击穿，判断有无。


4.1.3 SkipList（跳表）
·      总述

跳表是一种特殊的链表，相比一般的链表有更高的查找效率，可比拟二差查找树，平均期望的插入，查找，删除的时间复杂度都是O(logN);

·      数据结构和算法

跳表可视为水平排列（Level）、垂直排列（Row）的位置（Position）的二维集合。每个Level是一个列表Si，每个Row包含存储连续列表中相同Entry的位置，跳表的各个位置可以通过以下方式进行遍历。

After(P)：返回和P在同一Level的后面的一个位置，若不存在则返回NULL；

Before(P)：返回和P在同一Level的前面的一个位置，若不存在则返回NULL；

Below(P)：返回和P在同一Row的下面的一个位置，若不存在则返回NULL；

Above(P)：返回和P在同一Row的上面的一个位置，若不存在则返回NULL。

Image

图4 跳跃列表结构示意图

有顺序关系的多个Entry(K,V)集合M可以由跳表实现，跳表S由一系列列表{S0，S1，S2，......，Sh}组成，其中h代表的跳表的高度。每个列表Si按照Key顺序存储M项的子集，此外S中的列表满足如下要求：

列表S0中包含了集合M的每个一个Entry；

对于i = 1 ，...... ，h-1列表Si包含列表Si-1中Entry的随机子集；

Si中的Entry是从Si-1中的Entry集合中随机选择的，对于Si-1中的每一个Entry，以1/2的概率来决定是否需要拷贝到Si中，我们期望S1有大约n/2个Entry，S2中有大约n/4个Entry，Si中有n/2^i。跳表的高度h大约是logn。从一个列表到下一个列表的Entry数减半并不是跳表的强制要求；

插入的过程描述，以上图为例，插入Entry58：

找到底层列表S0中55的位置，在其后插入Entry58；

假设随机函数取值为1，紧着回到20的位置，在其后插入58，并和底层列表S0的Entry58链接起来形成Entry58的Row；

假设随机函数取值为0，则插入过程终止；



下图为随机数为1的结果图：
Image



图5 插入一个元素的过程示意图

删除过程：同查找过程。



时间复杂度

o   查找包括两个循环，外层循环是从上层Level到底层Level，内层循环是在同一个Level，从左到右;

o   跳表的高度大概率为O(logn)，所以外层循环的次数大概率为O(logn);

o   在上层查找比对过的key，不会再下层再次查找比对，任意一个key被查找比对的概率为1/2，因此内存循环比对的期望次数是2也就是O(1);

o   因此最终的时间复杂度函数O(n) = O(1)*O(logn)也就是O(logn)；

空间复杂度

o   Level i期望的元素个数为 n/2^i；

o   跳表中所有的Entry（包含同一个Entry的Row中的元素） Σn/2^i = nΣ1/2^i，其中有级数公式得到Σ1/2^i < 2；

o   期望的列表空间为O(n)；

·      优缺点

优点：快速查找，算法实现简单；

缺点：跳表在链表的基础上增加了多级索引以提升查询效率，使用空间来换取时间，必然会增加存储的负担。

·      使用场景

许多开源的软件都在使用跳表：

Redis中的有序集合zset；

LevelDB Hbase中的memtable；

Lucene中的Posting List。


4.2 简单非线性数据结构


4.2.1 AVL
·      总述

AVL树是带有平衡条件的二叉查找树，这个平衡条件必须要容易保持，而且它保证树的深度必须是O(logN)。在AVL树中任何节点的两个子树的高度最大差别为1。

·      数据结构和算法

AVL树本质上还是一棵二叉查找树，有以下特点：

AVL首先是一棵二叉搜索树；

带有平衡条件：每个节点的左右子树的高度之差的绝对值最多为1；

当插入节点或者删除节点时，树的结构发生变化导致破坏特点二时，就要进行旋转保证树的平衡。

针对旋转做详细分析如下：

把必须重新平衡的节点叫做a，由于任意节点最多有两个儿子，因此出现高度不平衡就需要a点的两棵子树的高度差2。可以看出，这种不平衡可能出现一下四种情况：

对a的左儿子的左子树进行一次插入；

对a的左儿子的右子树进行一次插入；

对a的右儿子的左子树进行一次插入；

对a的右儿子的柚子树进行一次插入。

情形1和4是关于a的对称，而2和3是关于a点的对称。因此理论上解决两种情况。

第一种情况是插入发生在外侧的情况，该情况通过对树的一次单旋转而完成调整。第二种情况是插入发生在内侧的情况，这种情况通过稍微复杂些的双旋转来处理。



单旋转的简单示意图如下：

Image

图6 单旋转示意图


双旋转的简单示意图如下：

Image

图7 双旋转示意图

·      优缺点

优点：使用二叉查找算法时间复杂度为O(logN)，结构清晰简单；

缺点：插入和删除都需要进行再平衡，浪费CPU资源；

·      使用场景

少量数据的查找和保存；



4.2.2 Red Black Tree
·      总述

红黑树是一种自平衡的二叉查找树，是2-3-4树的一种等同，它可以在O(logN)内做查找，插入和删除。

·      数据结构和算法

在AVL的基础之上，红黑树又增加了如下特点：

每个节点或者是红色，或者是黑色；

根节点是黑色；

如果一个节点时红色的，那么它的子节点必须是黑色的；

从一个节点到一个null引用的每一条路径必须包含相同数目的黑色节点。

红黑树的示意图如下（图片来源于网络）：

Image

图8  红黑树结构示意图

那么将一个节点插入到红黑树中，需要执行哪些步骤呢？

将红黑树当做一棵二叉搜索树，将节点插入；

将插入的节点着色为红色；

通过一系列的旋转和着色等操作，使之重新成为一棵红黑树。

在第二步中，被插入的节点被着为红色之后，他会违背哪些特性呢

对于特性1，显然是不会违背；

对于特性2，显然也是不会违背；

对于特性4，显然也是不会违背；

对于特性3，有可能会违背，我们将情况描述如下：

被插入的节点是根节点：直接把此节点涂为黑色；

被插入的节点的父节点是黑色：什么也不需要做。节点被插入后，仍然是红黑树；

被插入的节点的父节点是红色：此种情况下与特性3违背，所以将情况分析如下：

当前节点的父节点是红色，且当前节点的祖父节点的另一个子节点也是红色。处理策略为：将父节点置为黑色、将叔叔节点置为黑色、将祖父节点置为红色；

当前节点的父节点是红色，叔叔节点时黑色，且当前节点是其父节点的右子节点。将父节点作为新的当前节点、以新的当前节点作为支点进行左旋；

当前节点的父节点是红色，叔叔节点时黑色，且当前节点时父节点的左子节点。将父节点置为黑色、将祖父节点置为红色、以祖父节点为支点进行右旋。

定理：一棵含有n个节点的红黑树的高度至多为2log(N+1)，证明过程请查看参考资料。

由此定理可推论红黑树的时间复杂度为log(N)；

·      优缺点

优点：查询效率高，插入和删除的失衡的代销比AVL要小很多。

缺点：红黑树不追求完全平衡。

·      使用场景

红黑树的应用很广泛，主要用来存储有序的数据，时间复杂度为log(N)，效率非常高。例如java中的TreeSet、TreeMap、HashMap等。



4.2.3 B+Tree
·      总述

提起B+Tree都会想到大名鼎鼎的MySql的InnoDB引擎，该引擎使用的数据结构就是B+Tree。B+Tree是B-Tree（平衡多路查找树）的一种改良，使得更适合实现存储索引结构，也是该篇分享中唯一一个与磁盘有关系的数据结构。首先我们先了解一下磁盘的相关东西。

系统从磁盘读取数据到内存时是以磁盘块（block）为基本单位，位于同一块磁盘块中的数据会被一次性读取出来。InnoDB存储引擎中有页（Page）的概念，页是引擎管理磁盘的基本单位。

·      数据结构和算法

首先，先了解一下一棵m阶B-Tree的特性：

每个节点最多有m个子节点；

除了根节点和叶子结点外，其他每个节点至少有m/2个子节点；

若根节点不是叶子节点，则至少有两个子节点；

所有的叶子结点都是同一深度；

每个非叶子节点都包含n个关键字

关键字的个数的关系为 m/2-1 < n < m-1

B-Tree很适合作为搜索来使用，但是B-Tree有一个缺点就是针对范围查找支持的不太友好，所以才有了B+Tree；

那么B+Tree的特性在B-Tree的基础上又增加了如下几点：

非叶子节点只存储键值信息；

所有的叶子节点之间都有一个链指针（方便范围查找）；

数据记录都存放在叶子节点中；


将上述特点描述整理成下图（假设一个页（Page）只能写四个数据）：

Image

图9 B+Tree结构示意图



这样的数据结构可以进行两种运算，一种是针对主键的范围查找和分页查找，另外一种是从根节点开始，进行随机查找；

·      优缺点

优点：利用磁盘可以存储大量的数据，简单的表结构在深度为3的B+Tree上可以保存大概上亿条数据；B+Tree的深度大概也就是2~4，深度少就意味这IO会减少；B+Tree的时间复杂度log(m)N

缺点：插入或者删除数据有可能会导致数据页分裂；即使主键是递增的也无法避免随机写，这点LSM-Tree很好的解决了；无法支持全文索引；

·      使用场景

使用场景大多数数据库的引擎，例如MySql,MongoDB等。



4.2.4 HashTree


·      总述

HashTree是一种特殊的树状结构，根据质数分辨定理，树每层的个数为1、2、3、5、7、11、13、17、19、23、29.....

·      数据结构和算法

从2起的连续质数，连续10个质数接可以分辨大约6464693230个数，而按照目前CPU的计算水平，100次取余的整数除法操作几乎不算什么难事。


我们选择质数分辨算法来构建一颗哈希树。选择从2开始的连续质数来构建一个10层的哈希树。第一层节点为根节点，根节点先有2个节点，第二层的每个节点包含3个子节点；以此类推，即每层节点的数据都是连续的质数。对质数进行取余操作得到的数据决定了处理的路径。下面我们以随机插入10个数（442 9041 3460 3164 2997 3663 8250 9088906 4005）为例，来图解HashTree的插入过程，如下：

Image

图10 HashTree构建过程示意图

HashTree的节点查找过程和节点插入过程类似，就是对关键字用质数取余，根据余数确定下一节点的分叉路径，知道找到目标节点。如上图，在从对象中查找所匹配的对象，比较次数不超过10次，也就是说时间复杂度最多是o(1).

删除的过程和查找类似。

·      优缺点：

优点：结构简单，查找迅速，结构不变。

缺点：非有序性。



4.2.5 其他数据结构
鉴于篇幅有限，余下重要数据结构将在下一篇文章中再来一起讨论，敬请期待！




### references
#### links
- <https://mp.weixin.qq.com/s/5O4qDVP48jI5AFYGnAfKEw>