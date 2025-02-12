# MapReduce : Movie Script Analysis

The purpose of this assignment is to implement and execute a Hadoop MapReduce program for movie script analysis.

## **Learning Outcomes**  

By completing this activity, students will gain hands-on experience with:  

1. **Hadoop Architecture & Data Processing** – Understanding how Hadoop’s Distributed File System (HDFS) and the MapReduce programming model collaborate to process large-scale datasets.  
2. **Developing & Running MapReduce Jobs** – Writing, compiling, and executing Java-based MapReduce applications on a Hadoop cluster using Docker.  
3. **Interacting with the Hadoop Ecosystem** – Utilizing Hadoop commands to manage data in HDFS, monitor job execution, and retrieve results.  
4. **Containerized Hadoop Deployment** – Setting up and running Hadoop components within Docker containers for efficient and isolated processing.  
5. **Interpreting MapReduce Outputs** – Extracting meaningful insights from job results by analyzing word frequencies, dialogue lengths, and unique words.  
6. **Implementing Text Processing in Java** – Using Java-based Mapper and Reducer classes to parse, process, and manipulate textual data effectively.  
7. **Leveraging Hadoop Counters for Insights** – Tracking and measuring key statistics such as the number of processed lines, words, unique terms, and character dialogues.  

This activity will equip students with the foundational skills needed to work with large-scale data processing in distributed computing environments. 🚀

## Setup and Execution

### 1. **Start the Hadoop Cluster**

Run the following command to start the Hadoop cluster:

```bash
docker compose up -d
```

### 2. **Build the Code**

Build the code using Maven:

```bash
mvn install
```

### 3. **Move JAR File to Shared Folder**

Move the generated JAR file to a shared folder for easy access:

```bash
mv target/*.jar input/
```

### 4. **Copy JAR to Docker Container**

Copy the JAR file to the Hadoop ResourceManager container:

```bash
docker cp input/hands-on2-movie-script-analysis-1.0-SNAPSHOT.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 5. **Move Dataset to Docker Container**

Copy the dataset to the Hadoop ResourceManager container:

```bash
docker cp input/movie_dialogues.txt resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 6. **Connect to Docker Container**

Access the Hadoop ResourceManager container:

```bash
docker exec -it resourcemanager /bin/bash
```

Navigate to the Hadoop directory:

```bash
cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 7. **Set Up HDFS**

Create a folder in HDFS for the input dataset:

```bash
hadoop fs -mkdir -p /input/dataset
```

Copy the input dataset to the HDFS folder:

```bash
hadoop fs -put ./movie_dialogues.txt /input/dataset
```

### 8. **Execute the MapReduce Job**

Run your MapReduce job using the following command:

```bash
hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreduce/hands-on2-movie-script-analysis-1.0-SNAPSHOT.jar com.example.controller.Controller /input/dataset/input.txt /output
```

### 9. **View the Outputs**

To view the outputs of your MapReduce job, use:

```bash
hadoop fs -cat /output/*
```

  ```bash
  hadoop fs -cat /output/task1/*
  ```
  
  ```bash
  hadoop fs -cat /output/task2/*
  ```
  
  ```bash
  hadoop fs -cat /output/task3/*
  ```


### 10. **Copy Output from HDFS to Local OS**

To copy the output from HDFS to your local machine:

1. Use the following command to copy from HDFS:
    ```bash
    hdfs dfs -get /output /opt/hadoop-3.2.1/share/hadoop/mapreduce/
    ```

2. use Docker to copy from the container to your local machine:
   ```bash
   exit 
   ```
    ```bash
    docker cp resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/output/ output/
    ```
3. Commit and push to your repo so that we can able to see your output
