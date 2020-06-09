前面我们已经说过了数组的缺点：
1、删除元素的第一个时会非常消耗性能，因为需要把所有元素都得移动一个位置。
2、数组在插入一个元素的时候也是如此
3、数组还有不方便的缺点就是当我们不知道里面元素的下标值时我们需要对整个数组进行遍历比较。
效率非常低（当然这里如果使用二分查找的话会相对高些）
那么有没有一种数据结构能直接根据关键字KEY就能快速找到对应的元素呢？这时就有了散列列表查找（哈希表）

一、什么是哈希表？
散列技术是指在记录的存储位置和它的关键字之间建立一个确定的对应关系f，使每一个关键字都对应一个存储位置。
即：存储位置=f（关键字）。这样，在查找的过程中，只需要通过这个对应关系f 找到给定值key的映射f（key）。
只要集合中存在关键字和key相等的记录，则必在存储位置f（key）处。我们把这种对应关系f 称为散列函数或哈希函数。
按照这个思想，采用散列技术将记录存储在一块连续的存储空间中，这块连续的存储空间称为哈希表。所得的存储地址称为哈希地址或散列地址。
（JS大多数的哈希表是基于数组实现的，其实简单点讲就是把key关键字变成了数组的下标值。）

二、如果构建哈希表？
1、哈希函数：把要存储的数据的key转换成大数字（这里的方式很多，可以根据情况来制定），然后再把大数字哈希化
2、哈希化：将大数字转换为数组范围内的下标值的过程就是哈希化
3、哈希表：最终将这个数据插入到数组，最整个数组进行封装，我们就称这个为哈希表


三、哈希冲突
何为哈希冲突？就是你在把key转换成数组下标时肯定会有相同的怎么办？难道是覆盖前面一个么？
当然不是，这种冲突时不可能避免的，只能解决冲突。
那么如何解决冲突？
常见的四种方案：
1、开放地址法: 核心就是寻找空白的位置来存放重复的数据。
怎么查找空白的位置呢？
a、线性探测：一个一个的查找空白位置，散列是一定会有空白位置，满的话再扩容数组，后面代码实现的时候再说。
但是得遵循一些规则，比如你是用线性查找的空白位置时你取值得时候也要用线性查找的方式，当查找到第一个空白的位置时就代表没有这个值。
因为你放的时候就是一步一步的去找空白位置，如果发现第一个空白位置为空时就插入这个空白位置。
但是线性探测会有一个严重的问题，那就是聚集：
比如22-23-24-25-26，那么意味着2-3-4-5-6下标值都有元。那么在查询或者删除、插入的时候性能会很差，因为你需要找很多个才能找到一个空的位置。
所以二次探测可以减轻下这个问题。
b、二次探测：二次探测是在线性探测的步长上面进行改进，扩大探测时的步长；线性探测的步长为1，比如从x位置开始探测，那么依次就是X+1,X+2...
二次探测步长步长大概就是比如从x位置开始探测，依次就是X+1^2，X+2^2，X+3^2...
但是二线探测也有一个小问题，如何32-112-82-2-192，这些元素的步长插入时的步长相同。这种可能会造成步长隔得很远的一种聚集。
这种解决方案就是再哈希法

2、再哈希法：
当繁盛冲突时，使用不同的哈希函数计算地址，直到不冲突为止。这种方法不易产生堆积，但是耗费时间。
核心：就是把地址值再使用哈希函数进行一次哈希化，把这次哈希化的结果作为步长。
但是不能使用跟上次一样的哈希函数，不然结果还是上次同样的位置。
还有不能输出0，否则将没有步长，每次探测都是原地踏步，算法会进入死循环。
前面的人已经帮我们想好一个很好的哈希函数了：
setpSiez = constant - (key % constant)
其中constant是质素，而且小于数组的容量
例如：setpSiez = 5 - (key % 5)

3、链地址法：核心就是每个数组单元中存储的不再是一个单数据，而是一个链条。
这个链条可以是数组或者是链表（把相同的放在一个数组内，查找的时候进行线性查找比较）


四、哈希化的效率
哈希表中执行插入和搜索的操作效率是非常高的，如果没有冲突效率可能会更高。
如果有冲突，存取的时间就依赖后来的探测长度了
平均探测长度以及平均存取时间，取决于填装因子，随着填装因子变大，探测长度也越来越大
随着填装因子变大，效率下降的情况，在不同开放地址法方案中比链地值法更严重，当然也得根据具体业务来选择使用哪个
在分析效率前，我们先知道什么是填装因子：
填装因子表示当前哈希表中已经包含的数据项和整个哈希表长度的比值
填装因子 = 总数据项 / 哈希表长度
开放地址法的填装因子最大是1，因为它必须找到空白的单元才能将元素放入
链地址法的填装因子可以大于1，因为链条可以无限的延长下去，只要你愿意，效率可能就不太行了


五、如何构建一个优秀的哈希函数？
1、尽可能的让计算的过程变得简单，提高计算效率（尽量少有乘法和除法，因为他们的性能都比较低）
2、优秀的哈希函数应该具备哪些优点：
   快速计算：快速计算得到元素相应的hashCode
   均匀分布：在哈希表中。无论是链地址法还是开放地法，当多个元素映射到同一个位置的时候，都会影响效率
   所以优秀的哈希函数能让元素映射到不同的位置。让元素在哈希表中均匀分布。

快速计算：霍顿法则（数学公式提取）
均匀分布：尽量使用质数（这里是数学的知识），哈希表长度使用质数，N次幂的底数使用质数




