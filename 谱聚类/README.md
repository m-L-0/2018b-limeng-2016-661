#README

##Clustering Schoolwork

#### 任务一：将鸢尾花数据集画成图的形式

* 先算出数据集的相似度矩阵，这里用的是余弦相似度（余弦相似度计算出的数据尾数比较多，调节两点之间是否连线的时候，精度比较大，好调节）。
* 确定一个合适的**阈值**，只有两个样本之间的相似度大于该阈值时，这两个样本之间才有一条边。
* 可以看见数据集分成了几块，第一类之间更加聚集

####任务三：求取带权邻接矩阵

* 将余弦相似度矩阵对角线上的元素改为零，作为邻接矩阵

#### 任务四：根据邻接矩阵进行聚类

* 根据邻接矩阵求取度数矩阵
* 度数矩阵减去邻接矩阵，计算拉普拉斯矩阵
* 求除零之外的三个最小的特征值，并计算列出特征值对应的特征向量
* 完成K均值聚类算法:

>     def kmeans(dataSet, k):
>      numSamples,dim= dataSet.shape
>      clusterAssment = mat(zeros((numSamples, 2)))  #得到一个N*2的零矩阵,保存第i个样本的类别标号以及到质心的距离
>      clusterChanged = True   
>      
>     #初始化质心，从样本中随机选取K个作为初始质心
>     centroids = zeros((k, dim))
>     for i in range(k):  
>         index = int(random.uniform(0, numSamples))#随机产生一个数，作为质心的索引号
>         centroids[i, :] = dataSet[index, :]
>
>
> ​    
>     while clusterChanged:  
>         clusterChanged = False  
>         for i in range(numSamples): 
>             minDist  = 100000.0  
>             minIndex = 0  
>             #计算每个样本点与质点之间的距离，将其归内到距离最小的那一簇
>             for j in range(k):  
>                 distance = euclDistance(centroids[j, :], dataSet[i, :])  
>                 if distance < minDist:  
>                     minDist  = distance  
>                     minIndex = j  
>     
>             #若所有的样本不在变化，则退出while循环
>             if clusterAssment[i, 0] != minIndex:  
>                 clusterChanged = True  
>                 clusterAssment[i, :] = minIndex, minDist**2 
>     
>         #更新质心
>         for j in range(k):  
>             pointsInCluster = dataSet[nonzero(clusterAssment[:, 0].A ==j)[0]] #将dataSet矩阵中相对应的样本提取出来 
>             centroids[j, :] = mean(pointsInCluster, axis = 0)
>     return centroids, clusterAssment 

* 将特征向量传入K均值算法进行聚类

####任务五：将聚类结果可视化

* 根据聚类的结果将第一、二、三类分别画成红绿蓝三种颜色

> for i in range(150):
>     if(a[i]==0):
>         color = 'r'
>         node_color0.append(color)
>     elif(a[i]==1):
>         color = 'g'
>         node_color1.append(color)
>     else:
>         color = 'b'
>         node_color1.append(color)

####任务六：求分簇正确率

> centroids,clustAssment = kmeans(k,3)
> a=clustAssment.A[:,0]
> print(accuracy_score(y,a))  #打印聚类的正确率
>
> 0.9666666666666667 





正确率和初始质心的选取有很大的关联。