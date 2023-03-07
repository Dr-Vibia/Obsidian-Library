贝尔曼-福特算法与迪科斯彻算法类似，都以松弛操作为基础，即估计的最短路径值渐渐地被更加准确的值替代，直至得到最优解。在两个算法中，计算时每个边之间的估计距离值都比真实值大，并且被新找到路径的最小长度替代。 然而，迪科斯彻算法以贪心法选取未被处理的具有最小权值的节点，然后对其的出边进行松弛操作；而贝尔曼-福特算法简单地对所有边进行松弛操作，共 $\displaystyle |V|-1$ 次，其中 $\displaystyle |V|$ 是图的点的数量。在重复地计算中，已计算得到正确的距离的边的数量不断增加，直到所有边都计算得到了正确的路径。这样的策略使得贝尔曼-福特算法比迪科斯彻算法适用于更多种类的输入。

贝尔曼-福特算法的最多运行 $\displaystyle O(|V|\cdot |E|)$ 次，$\displaystyle |V|$ 和 $\displaystyle |E|$ 分别是节点和边的数量。
> 边权非负：Dijkstra
> 边权可以为负但没有负环：Bellman-Ford

```pseudocode
procedure BellmanFord(list vertices, list edges, vertex source)
   // 讀入邊和節點的列表並對distance和predecessor寫入最短路徑

   // 初始化圖
   for each vertex v in vertices:
       if v is source then distance[v] := 0
       else distance[v] := infinity
       predecessor[v] := null

   // 對每一條邊重複操作
   for i from 1 to size(vertices)-1:
       for each edge (u, v) with weight w in edges:
           if distance[u] + w < distance[v]:
               distance[v] := distance[u] + w
               predecessor[v] := u

   // 檢查是否有負權重的回路
   for each edge (u, v) with weight w in edges:
       if distance[u] + w < distance[v]:
           error "圖包含負權重的回路"
```

