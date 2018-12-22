#TensorFlow Schoolwork

#### 任务一：将鸢尾花数据集按照8:2的比例划分成训练集和验证集

导入数据集：

> from sklearn.datasets import load_iris    
> iris = load_iris()  
>
> x = iris.data
> y = iris.target

数据集划分：

> from sklearn.model_selection import train_test_split
> Xtrain, Xtest, Ytrain, Ytest = train_test_split(x, y, test_size = 0.2,shuffle=True)

####任务二：设计模型

我选用了加权投票的方式，距离越近权重越大

>             for i in range(K):
>                 m=int(idx[0,i])
>                 if(Ytrain[m]==0):
>                     classes[0] += (1-idx[1,i]/100)*1
>                 elif(Ytrain[m]==1):
>                     classes[1] +=(1-idx[1,i]/100)* 1
>                 else:
>                     classes[2] +=(1-idx[1,i]/100)* 1

####任务三：训练模型

已完成

####任务四：验证模型

让K分别等于1~10，看模型预测的正确率，发现K等于9时正确率约等于0.96

####任务五

已完成