author:            Ravi Ranjan
summary:           From data ingestion to insight prediction
id:                01-Data-Meetup-Demo
categories:        sdk
environments:      python
status:            draft
feedback link:     github.com/raviranjan0309
analytics account: 0

# Demo: From data ingestion to insight prediction

## Overview of the demo
Duration: 0:05

This demo shows you how to ingest, transform, explore and train ML model on without writing a single line of code. In this tutorial you will do the following: 

* Simplifying data migration and integration
* Accelerating time to insights
* Turning data into predictions


**Prerequesites**

* Basic understaing of extraction, transformation and ingestion of data.
* Basics of exploratory data analysis
* Basics of supervised machine learning algorithms

Negative
: Limitations: This is just a quick demo of end to end ML pipeline on structured dataset leveraging managed services of Google Cloud Platform.

## Introduction
Duration: 1:00

In this tutorial we will build end to end ML pipeline from data ingestion to prediction using newly launched Google Cloud Analytics managed services. We are in the era where technology grow exponentially and it become very difficutlt to analyze and do prediction in very short span of time. Google comes up with very innnovative products that will help Data analyst, engineer and scientist to perfrom basic operations on just few click, abstracting the complexity of code. 

From data ingestion to insight prediction: Google Cloud smart analytics accelerates your business transformation. Google introduced radically simple ways to move data into Google Cloud—and to clean, categorize, and understand it.

**Case study**
This demo uses a publicly available dataset, Games of Thrones almost 2000 characters from the books to train a machine learing model to predict whether a character lives or dies. The model traning and performance is assessed using Google Cloud Auto ML, it shows a descent Accuracy of 75% indicating it can predict well whether a character lives or not based on the data.

**What You'll Learn**

1. How to extract, transform and ingest data from GCS to BigQuery using Cloud Data Fusion (beta)
2. How to perforom exploratory data analysis on processed data using BigQuery BI Engine (beta) and Data Studio
3. How analyze, train and evaluate ML model using Google Cloud AutoML (beta)

**What You'll Need**

1. An active [GCP project](https://cloud.google.com/resource-manager/docs/creating-managing-projects)
2. Download dataset and push it to GCS bucket. [Download Dataset](https://github.com/raviranjan0309/Demo-From-data-ingestion-to-insight-prediction/blob/master/Data/character-predictions.csv)


## Simplifying data migration and integration
Duration: 10:00

Cloud Data Fusion is a fully managed, cloud-native data integration service that helps users efficiently build and manage ETL/ELT data pipelines. With a graphical interface and a broad open-source library of preconfigured connectors and transformations, Data Fusion shifts an organization’s focus away from code and integration to insights and action.

This section shows you how to do basic operations in Cloud Data Fusion using the Google Cloud Platform Console. You will create a Cloud Data Fusion pipeline that completes the following tasks:

1. Reads a csv file containing GOT character death prediction data from Google Cloud Storage
2. Runs basic transformations on the file to parse and clean the data
3. Loads the parsed data into BigQuery table

**Before you begin**

1. Select or create a Google Cloud Platform project. [GCP project](https://cloud.google.com/resource-manager/docs/creating-managing-projects)
[GO TO THE MANAGE RESOURCE PAGE](https://console.cloud.google.com/cloud-resource-manager?_ga=2.163079807.-230042825.1535092331&_gac=1.229438958.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
2. Enable the Cloud Data Fusion API. [ENABLE THE API](https://console.cloud.google.com/flows/enableapi?apiid=datafusion.googleapis.com&_ga=2.62737135.-230042825.1535092331&_gac=1.159178184.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
3. Create a Cloud Data Fusion instance. [OPEN THE CREATE INSTANCE PAGE](https://console.cloud.google.com/data-fusion/instance-create?_ga=2.62737135.-230042825.1535092331&_gac=1.159178184.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
It takes up to 20 minutes to deploy Cloud Data Fusion. The instance creation process is completed when a green checkmark displays to the left of the instance name on the Instances page in the GCP Console.
4. When instance creation completes, grant permissions to the service account associated with the instance.
    * In the **Instances** page, under **Instance name**, click the name of your instance.
    ![cloud_data_fusion_1](https://cloud.google.com/data-fusion/docs/images/quickstart/click-instance.png)
    * In the **Instance details** page that opens up, copy the **Service account** value.
    ![cloud_data_fusion_2](https://cloud.google.com/data-fusion/docs/images/quickstart/copy-service-account.png)
    * In the left navigation menu, under **IAM & Admin**, navigate to the **IAM** page.
    * At the top of the **IAM** page, click **Add**.
    * In the **Add members** panel that opens, in the **New members** box, paste the service account that you copied.
    * Under **Select a role**, start typing **Cloud Data Fusion API Service Agent**. Click the **Cloud Data Fusion API Service Agent** role.
    ![![cloud_data_fusion_2](https://cloud.google.com/data-fusion/docs/images/quickstart/add-iam-role.png)
    * Click **Save**.

**View instance details**

1. In the GCP Console, open the **Instances** page. [OPEN THE INSTANCE PAGE](https://console.cloud.google.com/data-fusion/locations/-/instances?_ga=2.96273119.-230042825.1535092331&_gac=1.127293951.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
2. Click the name of the instance to see its details. The **Instance Details** page provides information, such as the Cloud Data Fusion graphical interface, the zone, networking configuration, labels and advanced configuration.

**Access the Cloud Data Fusion graphical interface**

1. In the GCP Console, open the **Instances page**. [OPEN THE INSTANCE PAGE](https://console.cloud.google.com/data-fusion/locations/-/instances?_ga=2.95842143.-230042825.1535092331&_gac=1.50327636.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
2. In the **Actions** column for the instance, click the **View Instance** link. The Cloud Data Fusion graphical interface opens.


**Deploy sample pipeline for GOT dataset**

1. Click and open **Wrangler** from dashboard.
2. Go to **Create a pipeline** then **Batch Pipeline**.
3. Click on **Properties** under **GCSFile**.
4. Fill the required details.
5. Goto **Properties** under **Wrangler**. Set columns name, datatypes and perfrom transformations on the dataset.
6. Goto **Sink** and select **BigQuery**.
7. Link **Wrangler** with **BigQuery**.
8. Goto **Properties** under **BigQuery**. Set Reference Name, Dataset, Table.
9. Set pipeline name and click **Deploy**.

**View the pipeline**

1. After the pipeline is deployed, Cloud Data Fusion displays the pipeline on the Pipeline Detail page: 
    * View the pipeline's structure and configuration
    * Run the pipeline manually or set up a schedule or a trigger
    * View a summary of the pipeline's historical runs, including execution times, logs, and metrics

**Execute your pipeline**

1. To execute your pipeline, click **Run** in the Pipeline Detail view.

**View the results**

1. The pipeline takes a 10 minutes to complete. After pipeline completes, you can see the status of the pipeline transition to Succeeded and the number of records that each node in the pipeline has processed.
2. To view the results of the GOT pipeline, go to the BigQuery UI. The results of the pipeline are in the table, which is inside the GOT dataset in your project.

## Accelerating time to insights
Duration: 10:00

Google Data Studio visualize the data through highly configurable charts and tables. Easily connect to a variety of data sources. Share the insights with team or with the world. Collaborate on reports with team. Speed up the report creation process with built-in sample report

**Steps to perform EDA on character prediction dataset and generate report**

1. Open [Google Data Studio](https://datastudio.google.com/). 
2. Goto **Data Source**
3. Click on **+** symbol and select BigQuery
4. Under **MY PROJECT**, select GCP project where dataset is stored.
5. Select GOT dataset and character prediction table and **Connect**
6. Verfiy all the feature columns on the dashboard and click on **CREATE REPORT**
7. Start performing all the ECA and save reports for future use.



## Turning data into predictions
Duration: 10:00

AutoML Tables enables team of data scientists, analysts, and developers to automatically build and deploy state-of-the-art machine learning models on structured data at massively increased speed and scale. Transform the business by leveraging enterprise data to tackle mission-critical tasks.


SEND FEEDBACK
AutoML Tables   Documentation
Quickstart
Beta

This product or feature is in a pre-release state and might change or have limited support. For more information, see Product launch stages.

This section walks you through the process of using AutoML Tables web application to do the following steps:

1. Create a dataset.
2. Import table data from BigQuery into the dataset.
3. Identify schema columns in the imported data.
4. Train a model from the imported data.
5. Use the model to make predictions.

The entire process takes a couple of hours to complete. Most of that time is not active time; you can close your browser window and return to the task later.

**Before you begin**

1. Create a project and enable AutoML Tables
    * In the GCP Console, go to the **Manage resources** page and select or create a project. [GO TO MANAGE RESOURCE PAGE](https://console.cloud.google.com/cloud-resource-manager?_ga=2.103163715.-230042825.1535092331&_gac=1.53409114.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
    * Make sure that billing is enabled for your Google Cloud Platform project. [LEARN HOW TO ENABLE BILLING](https://cloud.google.com/billing/docs/how-to/modify-project)
    * Enable the Cloud AutoML and Storage APIs. [ENABLE THE APIS](https://console.cloud.google.com/flows/enableapi?apiid=storage-component.googleapis.com,automl.googleapis.com,storage-api.googleapis.com&redirect=https://console.cloud.google.com&_ga=2.92096089.-230042825.1535092331&_gac=1.190124505.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)

**1. Create a dataset and train a model**

1. Visit **AutoML Tables** in the Google Cloud Platform Console to begin the process of creating your dataset and training your model. [GO TO THE AUTOML TABLES PAGE](https://console.cloud.google.com/automl-tables?_ga=2.166546429.-230042825.1535092331&_gac=1.195944030.1560426979.Cj0KCQjw6IfoBRCiARIsAF6q06v1ZNxpMvFahZVNlF3836-3eID3U5rw0SxEf2_kZCBJGEaaXNKTE_UaAhVrEALw_wcB)
2. Select **Datasets**, and then select **New dataset**.
3. Select **Table from BigQuery** and fill Project ID, dataset ID and table ID. The dataset import takes a few minutes to complete.
4. After the dataset import completes, select **isAlive** for the Target column. The target column identifies the value the model will be trained to predict. Click **Continue**.
5. After the statistics for dataset have refreshed, you can review and verify the statistics for the imported data. Click individual rows to see more about distribution and correlation for a specific feature.
6. Select the **Train** tab. Enter GOT_Character_Prediction_Model for Model name, and 1 for Training budget. Select input feature columns.
7. In the **Summary** section, click the **Train** button to train your model. Model training takes about two hours to complete. After the model is successfully trained, the Train tab shows high-level metrics for the model.
8. Select the **Evaluate** tab for a detailed view of the model evaluation metrics.
9. Select the **Predict** tab, and click **Online prediction**.
10. Click **Deploy** model to deploy the model. You must deploy your model before you can request online predictions. Deploying a model takes a few minutes to complete.
11. AutoML Tables fills in sample data to help you test your model. Click **PREDICT** to request the online prediction.


**Clean up all the resources**

1. Delete the BigQuery dataset and Cloud Data Fusion instance.
2. Delete the reports from Google Cloud Data Studio.
3. Undeploy ML model. Select Models and click on the model you want to undeploy. Select the Predict tab and click Online prediction. Click Remove deployment.
4. Delete ML model. To delete a model, select Models. Click the More actions menu for the model that you want to delete, and then select Delete model.
5. Delete the dataset, select Datasets. Click the More actions menu for the model that you want to delete, and then select Delete dataset.
6. If there is no need to GCP prjoect, then delete the project.



