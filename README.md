# Apache Spark - Realtime Data Analystics Course - UOIT

[![N|Solid](https://spark.apache.org/images/spark-logo-trademark.png)](https://spark.apache.org/)

Apache Spark™ is a unified analytics engine for large-scale data processing.

This is a tutorial for installing apache spark and providng hands on spark RDDs, DataFrames and Datasets.

All the following instructions are installed on a Linux machine (Ubunutu)

# Step 1: Download 

![N|Solid](https://user-images.githubusercontent.com/9883712/54505838-1c067380-4910-11e9-9acb-c3b13a376eb4.PNG)
Choose:
  - Spark release: 2.4.0 (Nov 02 2018) or the most recent version at that time.
  - Package type: Pre-built for Apache Hadoop 2.7 and later (standalone version doesn't require hadoop installation).
  - Then copy using the provided link and use the following command to download the ".tgz" file into your working space.

```sh
$ cd /home/$User
$ wget http://apache.mirror.colo-serv.net/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz
$ tar xvf spark-2.4.0-bin-hadoop2.7.tgz 
$ sudo mv spark-2.4.0-bin-hadoop2.7 /usr/local/spark
```
Setting up the environment for Spark
Add the following line to ~/.bashrc file. It means adding the location, where the spark software file are located to the PATH variable.
```sh
$ sudo nano ~/.bashrc
$ SPARK_HOME=/usr/local/spark
$ export PATH=$SPARK_HOME/bin:$PATH
```
Then save the updates into the file by typing Ctrl + X then Y then Enter

Use the following command for sourcing the ~/.bashrc file.
```sh
$ source ~/.bashrc
```

# Step 2: Verifying Java Installation
Java installation is one of the mandatory things in installing Spark. Try the following command to verify the JAVA version.
```sh
$ java -version
```
If Java is already, installed on your system, you get to see the following response:
```sh
java version "1.7.0_71" 
Java(TM) SE Runtime Environment (build 1.7.0_71-b13) 
Java HotSpot(TM) Client VM (build 25.0-b02, mixed mode)
```
In case you do not have Java installed on your system, then Install Java before proceeding to next step.
```sh
$ sudo apt-get update
$ sudo apt-get install default-jre
```
# Step 3: Verifying Scala installation
You should Scala language to implement Spark. So let us verify Scala installation using following command.
```sh
$ scala -version
```
If Scala is already installed on your system, you get to see the following response:
```sh
Scala code runner version 2.11.6 -- Copyright 2002-2013, LAMP/EPFL
```
In case you don’t have Scala installed on your system, then proceed to next step for Scala installation.
```sh
$ sudo apt-get install scala
```
# Step 4: Verifying the Spark Installation
```sh
$ spark-shell
```
If spark is installed successfully then you will find the following output.

![Capture](https://user-images.githubusercontent.com/9883712/54507466-de0d4d80-4917-11e9-886c-727eda76203f.PNG)

To access the UI of the running spark cluster open the following  [http://192.168.56.1:4040](http://192.168.56.1:4040) or  [localhost:4040](localhost:4040)

![Capture](https://user-images.githubusercontent.com/9883712/54507541-347a8c00-4918-11e9-8ce9-422cf940ff62.PNG)

**Optional** To make the UI accessable from other machines on the same network we have to update spark-env configuation file. And add the IP of network interface used to connect to the network.
```sh
$ ifconfig
```
```sh
$ cd /usr/local/spark/conf
$ sudo cp spark-env.sh.template spark-env.sh
$ sudo nano spark-env.sh
SPARK_LOCAL_IP=ip_address
SPARK_MASTER_HOST=ip_address
```
Then save the updates into the file by typing Ctrl + X then Y then Enter.

# Step 5: Start the Apache Spark Cluster

![Capture](https://spark.apache.org/docs/latest/img/cluster-overview.png)

>1- Start the cluster manager (master) by executing the following line:
```sh
$ spark-class org.apache.spark.deploy.master.Master
```
>> Then notice the output it should give you the following:
```sh
2019-03-13 16:06:17 INFO  Master:54 - Starting Spark master at spark://192.168.56.1:7077
...
2019-03-13 16:06:17 INFO  MasterWebUI:54 - Bound MasterWebUI to 0.0.0.0, and started at http://localhost:8080
...
2019-03-13 16:06:17 INFO  Master:54 - I have been elected leader! New state: ALIVE
```
>2- Start the worker nodes by executing the following line:
>Notice you need to specify the master location (url), which you will get from the output of the first step
```sh
$ spark-class org.apache.spark.deploy.worker.Worker spark://192.168.56.1:7077
```
>Then you will get the following output if successful
```sh
2019-03-13 16:08:03 INFO  Utils:54 - Successfully started service 'WorkerUI' on port 8081.
....
2019-03-13 16:08:03 INFO  TransportClientFactory:267 - Successfully created connection to /192.168.56.1:7077 after 42 ms (0 ms spent in bootstraps)
....
2019-03-13 16:08:04 INFO  Worker:54 - Successfully registered with master spark://192.168.56.1:7077
```
>3- You can run as much worker nodes as you want using the same command in step two.

>4- Start the driver node using the following command:
```sh
$ spark-shell --master spark://192.168.56.1:7077
```
Note we specified the master attribute in the previous command to ask the driver node to connect to the created topology of the master and the worker nodes (refere to the apache spark componentes)

>If sucessful the output should return the following: **Look at Step 4**

# Step 6: Perform basic Scala 
