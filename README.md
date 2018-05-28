# recommander-system-mapreduce
Use collaborative filtering algorithms to predict rating matrix

```
cd src # 进入src 目录

wget https://s3-us-west-2.amazonaws.com/jiuzhang-bigdata/RecommenderSystem.tar # 下载代码

tar -xvf  RecommenderSystem.tar # 解压缩

cd RecommenderSystem # 进入解压出的目录

hdfs dfs -mkdir /input

hdfs dfs -put input/* /input  # 把user 相关的rating 文件上传

hdfs dfs -rm -r /dataDividedByUser

hdfs dfs -rm -r /coOccurrenceMatrix

hdfs dfs -rm -r /Normalize

hdfs dfs -rm -r /Multiplication

hdfs dfs -rm -r /Sum

cd src/main/java/

hadoop com.sun.tools.javac.Main *.java

jar cf recommender.jar *.class

hadoop jar recommender.jar Driver /input /dataDividedByUser /coOccurrenceMatrix /Normalize /Multiplication /Sum

hdfs dfs -cat /Sum/*

#args0: original dataset

#args1: output directory for DividerByUser job

#args2: output directory for coOccurrenceMatrixBuilder job

#args3: output directory for Normalize job

#args4: output directory for Multiplication job

#args5: output directory for Sum job

hdfs dfs -ls / #如果结果正确你可以看到下面这些文件里面有相应的结果输出
```
