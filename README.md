# Databricks - ETL Project

 This project is part of Databricks - Developer Foundations Badge. The idea behind this project is to ingest data from a purchasing system and load it into a data lake for further analysis.

* The main objective of this project is to use raw data to perform **ETL** (Extract, Transform and Load) using  **Azure Databricks**.

### The below image represents the solution architechture for this project :

![image](https://user-images.githubusercontent.com/79434863/180215332-81f17092-91fa-4ffe-928a-5f71f0294c47.png)

### Step 1: 
In this step you three batches of orders will be ingested, one for 2017, 2018 and 2019.

Each year, different individuals and different standards were used resulting in datasets that vary slightly:
* In 2017 the backup was written as fixed-width text files
![image](https://user-images.githubusercontent.com/79434863/180590852-4da05768-61ce-4bb2-8917-8d61457823ae.png)

* In 2018 the backup was written a tab-separated text files
![image](https://user-images.githubusercontent.com/79434863/180591399-49950b46-26ca-43a5-8b2b-fe7664c5e7cb.png)

* In 2019 the backup was written as a "standard" comma-separted text files but the format of the column names was changed
![image](https://user-images.githubusercontent.com/79434863/180591570-3f6e2b66-0f2f-452f-a421-cf529ce2277d.png)

### Step 2:
Now that the three years of orders are ingested, we will create a temp view unifying all the datasets into one single dataset.
![image](https://user-images.githubusercontent.com/79434863/180592309-a2005e6a-2fcd-4aeb-87c2-b624ecad338d.png)

Now that the three years of orders are combined into a single dataset, we can begin the processes of transforming the data. What we want to do next, is to extract all that data into their respective datasets. In other words, we want to normalize the data, in this case, to reduce data duplication.

In the one record, there are actually four sub-datasets:
* The order itself which is the aggregator of the other three datasets.
* ![image](https://user-images.githubusercontent.com/79434863/180592418-b135331e-72ef-4dc8-b1d3-3d73498bb462.png)

* The line items of each order which includes the price and quantity of each specific item.
![image](https://user-images.githubusercontent.com/79434863/180592433-5d46a06e-daec-4ae1-a407-a53eb7d7a06e.png)

* The sales rep placing the order.
![image](https://user-images.githubusercontent.com/79434863/180592383-6f8791cb-70de-4503-a640-60cdc00d4ff4.png)



### Step 3: 
The products being sold by our sales reps are itemized in an XML document which we will need to load. With the help of we spark-xml library we can load the products table.
![image](https://user-images.githubusercontent.com/79434863/180592589-8b063fd6-d33b-4da8-9ba9-9a5b49d54d12.png)

### Step 4: 
With our four historical datasets properly loaded, we can now begin to process the "current" orders.
We can process these JSON files as a stream of orders that are continually added to this dataset.

* The orders
![image](https://user-images.githubusercontent.com/79434863/180592812-a91d9288-029f-409e-a71d-9e21bf31aa4c.png)

* The line items
![image](https://user-images.githubusercontent.com/79434863/180592846-46dedace-4ee4-4803-9dde-0c6c0c220659.png)
