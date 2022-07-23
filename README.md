# Databricks - ETL Project

 This project is part of Databricks - Developer Foundations Badge. The idea behind this project is to ingest data from a purchasing system and load it into a data lake for further analysis.

* The main objective of this project is to use raw data to perform **ETL** (Extract, Transform and Load) using  **Azure Databricks**.

### The below image represents the solution architechture for this project :

![image](https://user-images.githubusercontent.com/79434863/180215332-81f17092-91fa-4ffe-928a-5f71f0294c47.png)

### Step 1: 
In this step you three batches of orders will be ingested, one for 2017, 2018 and 2019.

As each batch is ingested, we are going to append it to a new Delta table, unifying all the datasets into one single dataset.

Each year, different individuals and different standards were used resulting in datasets that vary slightly:
* In 2017 the backup was written as fixed-width text files
![image](https://user-images.githubusercontent.com/79434863/180590852-4da05768-61ce-4bb2-8917-8d61457823ae.png)
* In 2018 the backup was written a tab-separated text files
![image](https://user-images.githubusercontent.com/79434863/180591399-49950b46-26ca-43a5-8b2b-fe7664c5e7cb.png)
* In 2019 the backup was written as a "standard" comma-separted text files but the format of the column names was changed
![image](https://user-images.githubusercontent.com/79434863/180591570-3f6e2b66-0f2f-452f-a421-cf529ce2277d.png)

### Step 2:
Now that the three years of orders are ingested, we can begin the processes of transforming the data.

In the one record, there are actually four sub-datasets:
* The order itself which is the aggregator of the other three datasets.
* The line items of each order which includes the price and quantity of each specific item.
* The sales rep placing the order.
* The customer placing the order - for the sake of simplicity, we will not break this dataset out and leave it as part of the order.

What we want to do next, is to extract all that data into their respective datasets (except the customer data). In other words, we want to normalize the data, in this case, to reduce data duplication.




### Step 4: 
* Since we did transformation according to the project requirement, the data in the new container in ADLS storage can be used for Machine Learning and Data Science purpose. Filly one more time we are going to use ADF to load the data into the SQL database, so that Data Analysts can query  data directly from the database by using PowerBi/Tableau or any other data visualization tool for analysis purpose.

![](./Slides_and_Screenshots(Media)/PowerBi_ss.png)


![](./Slides_and_Screenshots(Media)/tests_vs_new_cases_1.png)

![](./Slides_and_Screenshots(Media)/tests_vs_new_cases_2.png)

![](./Slides_and_Screenshots(Media)/tests_map.png)

* I have also used **Schedule Triggers** at the time of Ingesting the data into the ADLS storage from different storage and also used **Event Triggers** which triggers when the data reaches into the ADLS storage.
* I basically categorized the data into 3 types. i.e ***Brozne --> Silver --> Gold*** which basically means when the data moves from bronze to gold, the quality and the value of the data improves.

* This project has been taken inspiration from one of the course in Udemy: https://www.udemy.com/course/learn-azure-data-factory-from-scratch/



![](./Slides_and_Screenshots(Media)/giphy.gif)




