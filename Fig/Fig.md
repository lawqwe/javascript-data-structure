什么是图？
图也是一种非常常见的数据结构，是一种与树有点相似的数据结构。
图论是数学的一个分支，在数学概念上，树是图的一种
它以图为研究对象，研究定点和边组成的数学理论和方法
主要研究的目的是事物之间的关系，定点代表事物，边代表两个事物之间的关系
比如地铁线路图，人际交际网，村与村之间的关系等。

图的特点：
一组顶点：通常用V（Vertex）表示顶点集合
一组边：通常用E（Edge）表示边的集
边是顶点与顶点之间的连线
边也可与是有向的，也可以是无向的
比如A----B,通常表示无向；A--->B，通常表示有向


图的常见术语：
顶点：表示图中的一个节点
边：边是顶点与顶点之间的连线
相邻顶点：两个由一条线连接在一起的顶点称之为相邻顶点
度：一个顶点相邻的顶点个数
路径：路径是顶点v1,v2...vn的一个连续系列。
简单路径：路径中不能包含重复的顶点
回路：第一个顶点和最后一个顶点相同的路径称之为回路 比如0 1 5 6 3 0
无向图：所有的边都没有方向的图
有向图：图中的边具有方向性
无权图：图中的边不带权重的图
带权图：带权图表示边有一定的权重。这里的权重可以是任意你希望表示的数据

图的常见表示方式：邻接矩阵
什么是邻接矩阵？
邻接矩阵让每一个节点和一个整数相关联，该整数作为数组的一个下标值
我们用一个二维数组来表示顶点之间的连接
邻接矩阵的问题：
如果图是一个稀疏图的话矩阵中会存在大量的0，这意味着我们浪费了很多内存空间来表示这些不存在的边

图的常见表示方式二：邻接表
什么是邻接表？
邻接表由图中的每个顶点以及和顶点相邻的顶点列表组成
这个列表有很多存储方式：素组，链表，字典（哈希表）都可以
邻接表的问题： 
邻接表计算出度非常简单（出度就是指向别人的数量，入度就是别人指向自己的数量）
邻接表如果计算入度的话非常麻烦，它必须的构建一个‘逆邻接表’。这样子才能有效的计算入度，
但是一般开发中很少会使用到入度。

图的遍历：
图的遍历思想和树的一样，图的遍历意味着将图中的每个顶点都访问一遍，而且不能有重复的访问。
一般有两种方式来进行遍历：
广度优先遍历（Breadth-First Search;简称BFS）
深度优先遍历（Depth-First Search；简称DFS）
两种算法都需要制定第一个被访问的顶点




















