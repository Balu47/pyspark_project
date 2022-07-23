# Databricks - ETL Project

 This project is part of Databricks - Developer Foundations Badge. The idea behind this project is to ingest data from a purchasing system and load it into a data lake for further analysis.

* The main objective of this project is to use raw data to perform **ETL** (Extract, Transform and Load) using  **Azure Databricks**.

### The below image represents the solution architechture for this project :

![image](https://user-images.githubusercontent.com/79434863/180215332-81f17092-91fa-4ffe-928a-5f71f0294c47.png)

### Step 1: 
* I have uploaded the *population_by_age.tsv.gz (zipped_file)* into the Azure Blob Storage manually. After that I initialized the Azure Data Factory and created the **Linked Service** which connects to the Blob Storage and created **DataSet** points for the particular file. Along with that I created the **Pipeline** which has a **Copy Activity** that helps to Copy the Population Data from Blob storage to the **ADLS gen2**


![](./Slides_and_Screenshots(Media)/population_data_blob_ingestion.png)


### Step 2: 
In this step you three batches of orders will be ingested, one for 2017, 2018 and 2019.

As each batch is ingested, we are going to append it to a new Delta table, unifying all the datasets into one single dataset.

Each year, different individuals and different standards were used resulting in datasets that vary slightly:
* In 2017 the backup was written as fixed-width text files
![image](https://user-images.githubusercontent.com/79434863/180590852-4da05768-61ce-4bb2-8917-8d61457823ae.png)
* In 2018 the backup was written a tab-separated text files
![image](https://user-images.githubusercontent.com/79434863/180591399-49950b46-26ca-43a5-8b2b-fe7664c5e7cb.png)
* In 2019 the backup was written as a "standard" comma-separted text files but the format of the column names was changed
![image](https://user-images.githubusercontent.com/79434863/180591570-3f6e2b66-0f2f-452f-a421-cf529ce2277d.png)


### Step 3:
* Once right after the required data ingested into the ADLS gen2 storage, I have created the dataFlows for all of the four files and creatd the required datasets for those. Now the DataFow will help us to create the transformations according to the project requirement. Once after the dataFlows build, I created the the pipelines for all of those 4 datasets which redirects to the another Container in the same ADLS storage.

*These the pictures of the dataFlows that are used for the transformations*

![](./Slides_and_Screenshots(Media)/dataflow_population_data.png)

![](./Slides_and_Screenshots(Media)/dataflow_cases_and_deaths_data.png)

![](./Slides_and_Screenshots(Media)/dataflow_hospial_admissions_data.png)

![](./Slides_and_Screenshots(Media)/dataflow_testing_data.png)


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




