> mkdir input
> cp etc/hadoo;/* input/
> ./bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input output 'dfs[a-z.]+'


get java home dir on mac

> /usr/libexec/java_home

> vim etc/hadoop/hadoop-env.sh

change JAVA_HOME

> export JAVA_HOME=/Users/yaojack/Library/Java/JavaVirtualMachines/openjdk-20.0.1/Contents/Home

add HADOOP_PREFIX

> export HADOOP_PREFIX=/Users/yaojack/bigdata/hadoop-2.10.2

edit config

> vim etc/hadoop/core-site.xml
> vim etc/hadoop/hdfs-site.xml
> vim etc/hadoop/mapred-site.xml
> vim etc/hadoop/yarn-site.xml

format the name node

> ./bin/hdfs namenode -format

> ./sbin/start-dfs.sh

see node status 

> localhost:50070

create user dir

> ./bin/hdfs dfs -mkdir -p /user/yaojack

start yarn

./sbin/start-yarn.sh

monitor clusters

localhost;8088


hdfs  dfs -mkdir input
hdfs  dfs -put  etc/hadoop/* input/

>  hadoop jar   share/hadoop/mapreduce/hadoop-mapreduce-examples-2.10.2.jar grep input output 'dfs[a-z.]+'


## Replication

+ Replication blocks based on the replication factor
+ Store replicas in different locations

Choosing Replica Locations

Maximize redundancy 
Minimize write bandwidth

Block cache


Metadata Files
    fsimage  - A snapshot of the complete file system at start up, load into memory

    edits
	
default backup location  on Name node local file system

Configure the Backup Location

Set the property 
dfs.namenode.name.dir in hdfs-site.xml

$path1, $path2,$path3
A comma separated list of paths

Merging these files is very compute heavy
Bringing a system back online could take a long time
SecondNameNode


Configure the checkpoint Frequency


Set properties in hdfs-site.xml

 specified the Number of seconds between each checkpointo

dfs.namenode.checkpoint.period

specified the period when the secondary name node polls the name node for uncheckpointed transactions

dfs.namenode.checkpoint.check.period 

specified the number of transactions(edits to the file system) before checkpointingo
dfs.namenode.checkpoint.txns 
