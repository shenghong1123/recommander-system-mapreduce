# recommander-system-mapreduce
Use collaborative filtering algorithms to predict rating matrix

```
install Docker

mkdir bigdata-class

cd bigdata-class #create a working directory on localhost

sudo docker pull joway/hadoop-cluster #download cluster image from docker hub

git clone https://github.com/joway/hadoop-cluster-docker #download code from github

sudo docker network create --driver=bridge hadoop #build a bride for communication between hadoop nodes

cd hadoop-cluster-docker

sudo ./start-container.sh #enter the docker container

./start-hadoop.sh #start hadoop

cd src #Enter src directory

wget https://s3-us-west-2.amazonaws.com/jiuzhang-bigdata/RecommenderSystem.tar #download the code

tar -xvf  RecommenderSystem.tar #uncompress

cd RecommenderSystem #enter uncompressed directory

hdfs dfs -mkdir /input

hdfs dfs -put input/* /input  #upload user's rating data to HDFS

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

hdfs dfs -ls / #you should see the result if everything is correct
```
