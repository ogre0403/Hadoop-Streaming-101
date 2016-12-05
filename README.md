# Hadoop Streaming 101

1. 下載範例程式至Linux家目錄
```bash
$ cd ~
$ git clone https://github.com/ogre0403/Hadoop-Streaming-101
$ cd ~/Hadoop-Streaming-101
```

2. 將測試資料上傳至HDFS
```bash
$ cd ~/Hadoop-Streaming-101/data
$ hadoop fs -put word.txt
```

3. 本範例提供 **R/Python/bash** 三種不同Hadoop Streaming的範例
>* 這步示範使用**R script**執行word count範例程式
```bash
$ cd ~/Hadoop-Streaming-101/R_script
$ hadoop jar ../hadoop-streaming-2.6.0-cdh5.5.1.jar \
-file ./mapper.r \
-file ./reducer.r \
-mapper ./mapper.r \
-reducer ./reducer.r \
-numReduceTasks 1 \
-input word.txt \
-output output
```
>>執行過程如下：
```bash
16/12/05 13:41:57 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [./mapper.r, ./reducer.r] [/opt/cloudera/parcels/CDH-5.5.1-1.cdh5.5.1.p0.11/jars/hadoop-streaming-2.6.0-cdh5.5.1.jar] /tmp/streamjob8712971123088099109.jar tmpDir=null
16/12/05 13:42:01 INFO mapred.FileInputFormat: Total input paths to process : 1
...
...
File Input Format Counters
Bytes Read=36
File Output Format Counters
Bytes Written=24
16/12/05 13:42:19 INFO streaming.StreamJob: Output directory: output
```
* 這步示範使用**Python script**執行word count範例程式
```bash
$ cd ~/Hadoop-Streaming-101/python_script
$ hadoop jar ../hadoop-streaming-2.6.0-cdh5.5.1.jar \
-file ./map.py \
-file ./reduce.py \
-mapper ./map.py \
-reducer ./reduce.py \
-numReduceTasks 1 \
-input word.txt \
-output output
```
>>執行過程如下：
```
16/12/05 13:47:37 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [./map.py, ./reduce.py] [/opt/cloudera/parcels/CDH-5.5.1-1.cdh5.5.1.p0.11/jars/hadoop-streaming-2.6.0-cdh5.5.1.jar] /tmp/streamjob8233069967197807642.jar tmpDir=null
16/12/05 13:47:40 INFO mapred.FileInputFormat: Total input paths to process : 1
...
...
WRONG_REDUCE=0
File Input Format Counters
Bytes Read=36
File Output Format Counters
Bytes Written=24
16/12/05 13:47:57 INFO streaming.StreamJob: Output directory: output
```
* 這步示範使用**Bash script**執行word count範例程式
```bash
$ cd ~/Hadoop-Streaming-101/bash_script
$ hadoop jar ../hadoop-streaming-2.6.0-cdh5.5.1.jar \
-file ./map.sh \
-file ./reduce.sh \
-mapper ./map.sh \
-reducer ./reduce.sh \
-numReduceTasks 1 \
-input word.txt \
-output output
```
>>執行過程如下：
```bash
16/12/05 13:46:42 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [./map.sh, ./reduce.sh] [/opt/cloudera/parcels/CDH-5.5.1-1.cdh5.5.1.p0.11/jars/hadoop-streaming-2.6.0-cdh5.5.1.jar] /tmp/streamjob2850544900133705954.jar tmpDir=null
16/12/05 13:46:46 INFO mapred.FileInputFormat: Total input paths to process : 1
...
...
File Input Format Counters
Bytes Read=36
File Output Format Counters
Bytes Written=24
16/12/05 13:47:03 INFO streaming.StreamJob: Output directory: output
```
4. 檢查執行結果
```bash
$ hadoop fs -cat output/part-00000
```
```bash
aaa 2
bbb 1
ccc 2
ddd 1
```

5. 更多Hadoop Streaming命令列所支援參數請參考
[Hadoop Streaming 官方文件](https://hadoop.apache.org/docs/r2.6.0/hadoop-mapreduce-client/hadoop-mapreduce-client-core/HadoopStreaming.html)


