# Merge Multiple Datasets with Azure Data Factory

Create data-driven workflows to organize data movement and convert data at scale with Azure Data Factory (ADF) a cloud-based ETL data integration solution.

In conclusion, Azure Data Factory facilitates the transfer of data across different computational resources and data repositories. You can construct and schedule data-driven workflows and access data from various data storage. Additionally, you can use compute services like Azure HDInsight, Azure Databricks, Azure Synapse Analytics, and Azure SQL Datasets to build intricate ETL processes that graphically change data.

In this article, after giving general information about Azure Data Factory, I will explain how the join process progresses on the platform.

# Azure Data Factory Components

Azure Data Factory consists of many components that allow you to create workflows such as copying, importing, and transforming data. You can create pipelines to execute one or more activities, access data sources or services through linked services, and then create a specific pipeline after creating a pipeline. We can add triggers to run our processes automatically at times or according to changing scenarios.

To better understand the Azure Data Factory environment, we can see the equivalent of SSIS components, which we are familiar with from ETL processes, compared to ADF components in the image below.

![image](https://user-images.githubusercontent.com/127193220/232229558-79676092-8f90-463c-84ff-ee07728ea791.png)

# Using Inner Join

After making a general introduction to Azure Data Factory, let’s move on to the example of the “Join” operation on the platform.

1) Creating Data Flow

Right-click on the data flows section and create a new flow from the “new data flow” tab to create a Mapping Data Flow.

![image](https://user-images.githubusercontent.com/127193220/232229587-6f327cf2-30b3-4a65-9c5a-9dd04011079a.png)

2) Data Flow Naming Stage

After creating a new flow, the “Properties” section will open on the right side of the screen. Complete the naming of the data flow (ProductDF) here.

![image](https://user-images.githubusercontent.com/127193220/232229623-8128e4a0-6899-4463-a040-3e7a5b983e88.png)

3) Add Source

Get your source by clicking the add source field on the data flow level.

![image](https://user-images.githubusercontent.com/127193220/232229683-1d3b6f82-3740-4d03-b42a-7557d8713ccf.png)

4) Resource Naming and Defining Dataset

After naming the source (Product) in the Output stream name field, proceed to the data set definition stage.

![image](https://user-images.githubusercontent.com/127193220/232229706-3152490c-0f0d-4719-a5fa-aa8747fab3a0.png)

You can reach your source by clicking the “New” button next to the dataset section of the file (product.csv) that you previously published to the container field.

![image](https://user-images.githubusercontent.com/127193220/232229727-07593837-498c-4f53-896e-8e3341c3f5ac.png)

After clicking the “New” button, you need to specify your path on the right side of the screen, where you will get the resource. In this scenario, our dataset product.csv file is located in Azure Blob Storage.

Note: Azure Cosmos, Azure SQL Database, etc. You can also access the datasets that you have defined in different areas such as.

Click on the Azure Blob Storage area and select the format of the dataset. In our example, since our dataset is CSV, we select the “DelimitedText” field and continue.

![image](https://user-images.githubusercontent.com/127193220/232229755-dca04ac3-82df-46cd-950f-ce26f068cc6e.png)

After naming the Set Properties field, select the previously defined linked service field.

![image](https://user-images.githubusercontent.com/127193220/232229768-31f950c8-7b89-4546-a960-43cd5f02e974.png)

To define where the file is located, click on the file sign on the right side of the “file path” section as the last step.

![image](https://user-images.githubusercontent.com/127193220/232229792-e38934cc-a58d-465e-b152-92e2b4cba189.png)

Since the file (Product.csv) is in the alvedonustur container, we continue by clicking on the alvedonustur container.
![image](https://user-images.githubusercontent.com/127193220/232229817-32847235-faf4-4419-b557-94547ef28aaf.png)

The root of the file (Product.csv) has been accessed. At this stage, select the file and confirm. You can preview your file in the “Data Preview” tab.

![image](https://user-images.githubusercontent.com/127193220/232229841-440b080a-7f4c-4889-9ccd-7eec17c2e46e.png)

We can create the ProductCategory file, which is the 2nd resource to be joined, as we defined our Product resource, and proceed to our join process.

5) Join Operation

First of all, you need to define what operation you will do by clicking the + sign on the bottom right of the Product resource created. To combine the Product and ProductCategory resources, we must choose to join.

![image](https://user-images.githubusercontent.com/127193220/232229855-e61a6923-b0a1-4fa4-a51c-2a05d29dcd65.png)

The left stream field comes as default because we choose from the product source. In the Right Stream field, we need to select the ProductCategory field, which is another source we will join.

![image](https://user-images.githubusercontent.com/127193220/232229883-ea265dd0-99f8-4cad-92fe-234dac6c38d0.png)

In the join conditions, we must specify that we want to inner join both sources and define the ProductCategoryID column common to both sources as the join condition.

![image](https://user-images.githubusercontent.com/127193220/232229902-2803a0aa-2cc5-4fe8-aeda-8dbf0a48205d.png)

In the data preview tab, we can see that the data is coming without any problems by inner joining according to the ProductCategoryID field in both sources.

![image](https://user-images.githubusercontent.com/127193220/232229921-82e061ef-e373-4c36-bd79-5455eeeac45e.png)

6) Stage of Creating the Destination Task (Sink)

To determine in which area the output will be stored, the “sink” task should be added to the data flow area by clicking the + icon at the bottom right of the Join task.
![image](https://user-images.githubusercontent.com/127193220/232229934-1c53e0e4-0cb3-449f-9b88-e68423af4442.png)

To select the stored area, we must specify the path of the container after clicking the “new” button next to the dataset section.

![image](https://user-images.githubusercontent.com/127193220/232229955-a811867b-7409-427e-bda9-f1671b50ca69.png)

The stage sources here are the same as the defined datasets, except for the last stage. Since we want to save it as a new CSV file when it comes to the container stage, we only need to specify and confirm the alvedonustur container without selecting any dataset.

![image](https://user-images.githubusercontent.com/127193220/232229969-1cb99f5b-8203-4591-acf6-846a3a98ba21.png)

By default, Azure DF defined the name of the resource as DelimitedText5. If you want to change its name, you can change the name of your source in the “open” tab on the right side of the dataset field.

In the Mapping section, first of all, the columns should be matched between the two sources by opening the Auto Mapping field.
![image](https://user-images.githubusercontent.com/127193220/232229985-07f194f9-3c82-498f-a2c7-cd87197ab95c.png)

In the Data Preview tab, we can see that our data is coming in without any problems.
![image](https://user-images.githubusercontent.com/127193220/232229997-c643beaa-f0f3-4cb0-a6b9-55e666f5ca37.png)

7) Pipeline Creation Stage

Right-click on the Pipeline section and select new pipeline and give a new name(ProductJoinPipeline) to the pipeline area from the properties section on the right side of the screen.
![image](https://user-images.githubusercontent.com/127193220/232230077-d31f8381-4045-4f0e-a5f3-c97e991d8b60.png)

To run the ProductDF flow after creating the pipeline, drag and drop it to the Data flow task pipeline area under the Move&Transform field in the Activities section. (Optionally, you can also drag and drop the data flow task we created in the previous stage to the pipeline area.)
![image](https://user-images.githubusercontent.com/127193220/232230095-4bb2fe99-58e5-4a6d-ac49-651398d31400.png)

To select the data flow you will run, define the data flow (ProductDF) you have created in the Data flow field under the Settings tab.

8) Pipeline Publish and Run Phase

Publish it by clicking the publish button in the upper left corner of the pipeline you created.
![image](https://user-images.githubusercontent.com/127193220/232230118-f198934c-32d0-406a-a2b6-947a9394b981.png)

After your publish process is complete, you can run the pipeline. For this, we need to click on the debug button in the upper corner of the screen. After the debug process is completed, you can see that the data flow is running smoothly from the Output tab.
![image](https://user-images.githubusercontent.com/127193220/232230131-89dee258-7762-4c1f-8516-a828c010aada.png)

9) Dataset Preview and Debug

You can see the file, which is subjected to the join process, stored as CSV in the container area in the image below.

![image](https://user-images.githubusercontent.com/127193220/232230146-ff10e7d8-73f4-4285-9902-e1cb75a6c33b.png)

To download the file to your desktop, you can also save it in CSV format by clicking the Download button at the top.
![image](https://user-images.githubusercontent.com/127193220/232230161-942e790a-7166-492c-a04c-c2fdfb02ec98.png)
