# Assessed Coursework 2

This is an Eclipse project in Maven for the implementation of the Page Ranking algorithm to define the page rank of articles(nodes). In this project,we are using Spark framework for implementing the Page Rank which is defined as PR(u) = 0.15 + 0.85* sum(PR(v)/L(v)), ∀v:∃(v,u) ∈ S, where L(v) is the number of outlinks of page v.

## **Compilation and Testing**

For this purpose, we need to give three arguments in command line. First, we specify the input_filename. Second, is the no_of_iterations. Third, is the ISO8601-formatted date. From the command line, in this directory, type : 
mvn package
The above command will create a jar file and this can be used to set HADOOP_CLASSPATH

The class with the main() method is "PageRank" and output. 

## **Requirements**
Eclipse, Maven, HDFS, spark

## **Assessed Coursework 2**

Following is the detailed description of all the map-reduce jobs : 

###### **JavaPair RDD 1**
Here, we used newAPIHadoopFile method to read all the Revision at once. We used a map method to separate all the Revision in the input text file(which is separated by "\n"). Now, we used mapToPair to get all the outlinks and the timestamp related to that specific Revision. And, we send distinct outlinks and timestamp as value and thier respective article title as the key.

Next, we used the reduceByKey method to get the maximum Revision Based on the timestamp. Furthermore, we used another mapToPair method to remove the value of timestamp in the received input. 

###### **JavaPair RDD 2**
Here, we used one map method in which we receive the article title as key and outlinks as value. In this methode we will assign a page rank score of 1 to all the articles.

###### **JavaPair RDD 3**
This receives all the articles and their score assigned as 1. Here, we used maptopair to assign the contribution to each outlink and later also assign the original article with a score 0.0. This will run till the number of iterations specified in the command line.
Now, in the reduceByKey method, we will implement the page rank formula, and we will receive the page rank score of all the aritcles which is then sorted based on score by a map method.

Result is stored in a output file whose name is given in args[1] through command line.
