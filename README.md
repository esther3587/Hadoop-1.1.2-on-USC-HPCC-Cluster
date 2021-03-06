# Hadoop-1.1.2-on-USC-HPCC-Cluster
This project is meant to suppport Hadoop-1.1.2 on USC HPCC clusters. The current version of Hadoop provided by HPCC relies on /scratch filesystem rather than HDFS. In this case, the HPC users execute their Hadoop programs by putting their files into /scratch, and then Hadoop will access the data files in /scratch when running the map-reduce. Here shows how Hadoop-1.1.2 can successfully launch up HDFS on HPCC cluster. We provide two different tutorials as options to run Hadoop. 

<Option 1> **Interactive mode**

1. Copy hadoop repository to your working directory.

            git clone https://github.com/JackMing/Hadoop-1.1.2-on-USC-HPCC-Cluster.git

2. In `launch-up-hadoop-on-hpcc`, change line 8 `HADOOP_TEMPLATE_DIR` to your working directory, specifically where your conf/ folder is.

            HADOOP_TEMPLATE_DIR=${HADOOP_TEMPLATE_DIR:-/path/to/configuration/template/dir/}

3. You need to request nodes by **qsub** and run it in the interactive mode by adding option **-I**. If you need more options, please check the main page of qsub.

            qsub -d . -l 'walltime=00:30:00' -l 'nodes=3:ppn=6' -l 'pmem=2g' -I

4. Before you start your hadoop program, you should run the following setup commands first to launch up the HDFS.

            source setup.sh
            ./launch-up-hadoop-on-hpcc

5. After the setup, you can submit your hadoop job as you want. You can also manage the HDFS by the command `hdfs`

6. You can run the following example to verify your hadoop is working properly.

            hadoop jar /usr/usc/hadoop/1.1.2/hadoop-examples-1.1.2.jar pi 250 1000

7. Please remember to copy your output file out from the HDFS each time you finish your operation. The HDFS will be erased after you leave the cluster or the running time exceeds the walltime limit you set up before.

<Option 2> **Submit PBS script**

1. Copy hadoop repository to your working directory. 

            git clone https://github.com/JackMing/Hadoop-1.1.2-on-USC-HPCC-Cluster.git

2. In PBS script `hadoop-example.pbs`, modify your WORK_HOME path. 
3. The current PBS script will run the hadoop example (wordcount). If you want to run other examples, modify the corresponding paths.
4. In `launch-up-hadoop-on-hpcc`, change line 8 `HADOOP_TEMPLATE_DIR` to your working directory, specifically where your conf/ folder is.

            HADOOP_TEMPLATE_DIR=${HADOOP_TEMPLATE_DIR:-/path/to/configuration/template/dir/} 

5. Submit PBS script.

            qsub hadoop-example.pbs


 
