# Merge Multiple Datasets with Azure Data Factory

Create data-driven workflows to organize data movement and convert data at scale with Azure Data Factory (ADF), a cloud-based ETL data integration solution.

In conclusion, Azure Data Factory facilitates the transfer of data across different computational resources and data repositories. You can construct and schedule data-driven workflows and access data from various data storage. Additionally, you can use compute services like Azure HDInsight, Azure Databricks, Azure Synapse Analytics, and Azure SQL Datasets to build intricate ETL processes that graphically change data.

In this article, after giving general information about Azure Data Factory, I will explain how the join process progresses on the platform.

# Azure Data Factory Components

Azure Data Factory consists of many components that allow you to create workflows such as copying, importing, and transforming data. You can create pipelines to execute one or more activities, access data sources or services through linked services, and then create a specific pipeline after creating a pipeline. We can add triggers to run our processes automatically at times or according to changing scenarios.

To better understand the Azure Data Factory environment, we can see the equivalent of SSIS components, which we are familiar with from ETL processes, compared to ADF components in the image below.
