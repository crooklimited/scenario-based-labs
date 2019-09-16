<div class="MCWHeader1">
Cosmos DB scenario-based labs - IoT
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
September 2019
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2019 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Cosmos DB scenario-based labs - IoT hands-on lab step-by-step](#cosmos-db-scenario-based-labs---iot-hands-on-lab-step-by-step)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
  - [Exercise 1: Configure environment](#exercise-1-configure-environment)
    - [Task 1: Create Cosmos DB database and container](#task-1-create-cosmos-db-database-and-container)
      - [About Cosmos DB throughput](#about-cosmos-db-throughput)
      - [About Cosmos DB partitioning](#about-cosmos-db-partitioning)
    - [Task 2: Add Key Vault secrets](#task-2-add-key-vault-secrets)
    - [Task 3: Create Azure Databricks cluster](#task-3-create-azure-databricks-cluster)
    - [Task 4: Configure Key Vault-backed Databricks secret store](#task-4-configure-key-vault-backed-databricks-secret-store)
  - [Exercise 2: Deploy Azure functions and Web App](#exercise-2-deploy-azure-functions-and-web-app)
    - [Task 1: Open solution](#task-1-open-solution)
    - [Task 2: Code walk-through](#task-2-code-walk-through)
    - [Task 3: Deploy Event Hub consumer Function App](#task-3-deploy-event-hub-consumer-function-app)
    - [Task 4: Deploy Change Feed consumer Function App](#task-4-deploy-change-feed-consumer-function-app)
    - [Task 5: Deploy Web App](#task-5-deploy-web-app)
    - [Task 6: Configure application settings in Azure](#task-6-configure-application-settings-in-azure)
  - [Exercise 3: Configure Logic App for e-mail alerts](#exercise-3-configure-logic-app-for-e-mail-alerts)
    - [Task 1: Create new workflow](#task-1-create-new-workflow)
    - [Task 2: Configure email service](#task-2-configure-email-service)
  - [Exercise 4: Explore and execute data generator](#exercise-4-explore-and-execute-data-generator)
    - [Task 1: Open solution](#task-1-open-solution-1)
    - [Task 2: Update application configuration](#task-2-update-application-configuration)
    - [Task 3: Code walk-through](#task-3-code-walk-through)
    - [Task 4: Run generator](#task-4-run-generator)
  - [Exercise 5: Observe data using Cosmos DB Data Explorer and Web App](#exercise-5-observe-data-using-cosmos-db-data-explorer-and-web-app)
    - [Task 1: View data in Cosmos DB Data Explorer](#task-1-view-data-in-cosmos-db-data-explorer)
    - [Task 2: Search and view data in Web App](#task-2-search-and-view-data-in-web-app)
  - [Exercise 6: Performing CRUD operations using the Web App](#exercise-6-performing-crud-operations-using-the-web-app)
    - [Task 1: Update vehicle metadata](#task-1-update-vehicle-metadata)
    - [Task 2: View consignment, package, and trip data](#task-2-view-consignment-package-and-trip-data)
  - [Exercise 7: Observe Change Feed using Azure Functions and App Insights](#exercise-7-observe-change-feed-using-azure-functions-and-app-insights)
    - [Task 1: Open App Insights Live View](#task-1-open-app-insights-live-view)
  - [Exercise 8: Running the predictive maintenance batch scoring](#exercise-8-running-the-predictive-maintenance-batch-scoring)
    - [Task 1: Import lab notebooks into Azure Databricks](#task-1-import-lab-notebooks-into-azure-databricks)
    - [Task 2: Run batch scoring notebook](#task-2-run-batch-scoring-notebook)
    - [Task 3: Create scheduled notebook job](#task-3-create-scheduled-notebook-job)
  - [Exercise 9: Deploying the predictive maintenance web service](#exercise-9-deploying-the-predictive-maintenance-web-service)
    - [Task 1: Run deployment notebook](#task-1-run-deployment-notebook)
  - [Exercise 10: Configure windowed queries in Stream Analytics](#exercise-10-configure-windowed-queries-in-stream-analytics)
    - [Task 1: Add Stream Analytics Event Hubs input](#task-1-add-stream-analytics-event-hubs-input)
    - [Task 2: Add Stream Analytics outputs](#task-2-add-stream-analytics-outputs)
    - [Task 3: Create Stream Analytics query](#task-3-create-stream-analytics-query)
    - [Task 4: Run query](#task-4-run-query)
  - [Exercise 11: Creating the Fleet status real-time dashboard in Power BI](#exercise-11-creating-the-fleet-status-real-time-dashboard-in-power-bi)
    - [Task 1: Log in to Power BI online](#task-1-log-in-to-power-bi-online)
    - [Task 2: Create real-time dashboard](#task-2-create-real-time-dashboard)
  - [Exercise 12: Creating the Predictive Maintenance & Trip/Consignment Status reports in Power BI](#exercise-12-creating-the-predictive-maintenance--tripconsignment-status-reports-in-power-bi)
    - [Task 1: Add Cosmos DB data sources to Power BI Desktop](#task-1-add-cosmos-db-data-sources-to-power-bi-desktop)
    - [Task 2: Create new report in Power BI Desktop](#task-2-create-new-report-in-power-bi-desktop)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Delete the resource group](#task-1-delete-the-resource-group)

<!-- /TOC -->

# Cosmos DB scenario-based labs - IoT hands-on lab step-by-step

## Overview

![A big rig truck is displayed containing packages and telemetry sensors.](media/truck-with-sensors.png 'Truck with sensors')

Contoso Auto is a high value cargo logistics organization that is collecting vehicle and package telemetry data and wants to use Azure Cosmos DB to rapidly ingest and store this data in its raw form, do some processing in near real-time to generate insights to support several business objectives and surface these to the most appropriate user communities within the organization. It is a fast growing organization and wants to be able to scale and manage the associated cost of its chosen technology to enable it to cope with its explosive growth and the inherent seasonality of the logistics business. This scenario includes applicability to both the vehicle telemetry and logistics use cases by focusing on trucking and inclusion of cargo sensing data. This additionally allows for many representative customer analytics scenarios.

From a technology perspective Contoso would like to leverage Azure Cosmos DB as the core repository for its hot data path and leverage the Azure Cosmos DB Change Feed as a means to drive a solid and robust event sourcing architecture that would allowing Contoso developers to quickly enhance the solution. This achieved using a robust and agile serverless approach by leveraging events published by the Change Feed that reflect the state changes within the application (database).

Ultimately Contoso would surface the raw and derived insights data to its users in one of three roles:

- **Logistic Operations personnel** who are interested in the current state of the vehicles and cargo logistics and who would use a web app to quickly understand the status of any single vehicle or piece of cargo, be notified of alerts as well as load vehicle and cargo meta data into the system. What they would like to see on the dashboard are various visualizations of detected anomalies, like engines overheating, abnormal oil pressure, and aggressive driving.

- **Management and Customer Reporting personnel** who would like to be in a position to see the current state of the vehicle fleet and customer consignment level information presented in on a Power BI report that automatically updates with new data as it flows in after being processed. What they would like to see are reports on bad driving behavior by driver and using visual components such as a map to show anomalies related to cities or areas, as well as various charts and graphs depicting aggregate fleet and consignment information in a clear way.

In this experience, you will use Azure Cosmos DB to ingest streaming vehicle telemetry data as the entry point to a near real-time analytics pipeline built on Cosmos DB, Azure Functions, Event Hubs, Azure Databricks, Azure Storage, Azure Stream Analytics, Power BI, Azure Web Apps, and Logic Apps.

## Solution architecture

Below is a diagram of the solution architecture you will build in this lab. Please study this carefully, so you understand the whole of the solution as you are working on the various components.

![A diagram showing the components of the solution is displayed.](media/solution-architecture.png 'Solution Architecture')

The solution for the IoT scenario centers around **Cosmos DB**, which acts as the globally-available, highly scalable data storage for streaming event data, fleet, consignment, package, and trip metadata, and aggregate data for reporting. Vehicle telemetry data flows in from the data generator, through registered IoT devices in **IoT Hub**, where an **Azure function** processes the event data and inserts it into a telemetry container in Cosmos DB. The Cosmos DB change feed triggers three separate Azure functions, with each managing their own checkpoints so they can process the same incoming data without conflicting with one another. One function serializes the event data and stores it into time-sliced folders in **Azure Storage** for long-term cold storage of raw data. Another function processes the vehicle telemetry, aggregating the batch data and updating the trip and consignment status in the metadata container, based on odometer readings and whether the trip is running on schedule. This function also triggers a **Logic App** to send email alerts when trip milestones are reached. A third function sends the event data to **Event Hubs**, which in turn triggers **Stream Analytics** to execute time window aggregate queries. These queries output vehicle-specific aggregates to the Cosmos DB metadata container, and overall vehicle aggregates to **Power BI** to populate its real-time dashboard of vehicle status information. A Power BI Desktop report is used to display detailed vehicle, trip, and consignment information, pulled directly from the Cosmos DB metadata container. It also displays batch battery failure predictions, pulled from the maintenance container. **Azure Databricks** is used to train a machine learning model to predict vehicle battery failure, based on historic information. It saves a trained model locally for batch predictions, and deploys a model and scoring web service to **Azure Kubernetes Service** or **Azure Container Instances** for real-time predictions. Azure Databricks also uses the **Spark Cosmos DB connector** to pull down each day's trip information to make batch predictions on battery failure and store the predictions in the maintenance container. A **Web App** allows Contoso Auto to manage vehicles and view consignment, package, and trip information that is stored in Cosmos DB. The Web App is also used to make real-time battery failure predictions while viewing vehicle information. **Azure Key Vault** is used to securely store centralized application secrets, such as connection strings and access keys, and is used by the Function Apps, Web App, and Azure Databricks. Finally, **Application Insights** provides real-time monitoring, metrics, and logging information for the Function Apps and Web App.

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN.
   - Trial subscriptions will not work.
   - **IMPORTANT**: To complete the OAuth 2.0 access components of this hands-on lab you must have permissions within your Azure subscription to create an App Registration and service principal within Azure Active Directory.
2. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
3. Install [Visual Studio 2019 Community](https://visualstudio.microsoft.com/vs/) or greater

## Before the hands-on lab

Refer to the Before the hands-on lab setup guide manual before continuing to the lab exercises.

## Exercise 1: Configure environment

**Duration**: 30 minutes

You must provision a few resources in Azure before you start developing the solution. Ensure all resources use the same resource group for easier cleanup.

In this exercise, you will configure your lab environment so you can start sending and processing generated vehicle, consignment, package, and trip data. You will begin by creating a Cosmos DB database and containers, then you will retrieve secrets used in the solution's application settings (such as connection strings) and securely store them in Azure Key Vault, then configure your Azure Databricks environment.

### Task 1: Create Cosmos DB database and container

In this task, you will create a Cosmos DB database and three SQL-based containers:

- **telemetry**: Used for ingesting hot vehicle telemetry data with a 90-day lifespan (TTL).
- **metadata**: Stores vehicle, consignment, package, trip, and aggregate event data.
- **maintenance**: The batch battery failure predictions are stored here for reporting purposes.

1. Using a new tab or instance of your browser, navigate to the Azure portal, <http://portal.azure.com>.

2. Select **Resource groups** from the left-hand menu, then search for your resource group by typing in `cosmos-db-iot`. Select your resource group that you are using for this lab.

   ![Resource groups is selected and the cosmos-db-iot resource group is displayed in the search results.](media/resource-group.png 'cosmos-db-iot resource group')

3. Select your Azure Cosmos DB account. The name starts with `cosmos-db-iot`.

   ![The Cosmos DB account is highlighted in the resource group.](media/resource-group-cosmos-db.png 'Cosmos DB in the Resource Group')

4. Select **Data Explorer** in the left-hand menu, then select **New Container**.

   ![The Cosmos DB Data Explorer is shown with the New Container button highlighted.](media/cosmos-new-container.png 'Data Explorer - New Container')

5. On the **Add Container** blade, specify the following configuration options:

   a. Enter **ContosoAuto** for the **Database id**.

   b. Leave **Provision database throughput** unchecked.

   c. Enter **metadata** for the **Container id**.

   d. Partition key: **/partitionKey**

   e. Throughput: **15000**

   ![The New Container form is displayed with the previously described values.](media/cosmos-new-container-metadata.png 'New metadata container')

6. Select **OK** to create the container.

7. Select **New Container** once again in the Data Explorer.

8. On the **Add Container** blade, specify the following configuration options:

   a. **Database id**: Select **Use existing**, then select **ContosoAuto** from the list.

   c. Enter **telemetry** for the **Container id**.

   d. Partition key: **/partitionKey**

   e. Throughput: **15000**

   ![The New Container form is displayed with the previously described values.](media/cosmos-new-container-telemetry.png 'New telemetry container')

9. Select **OK** to create the container.

10. Select **New Container** once again in the Data Explorer.

11. On the **Add Container** blade, specify the following configuration options:

    a. **Database id**: Select **Use existing**, then select **ContosoAuto** from the list.

    c. Enter **maintenance** for the **Container id**.

    d. Partition key: **/vin**

    e. Throughput: **400**

    ![The New Container form is displayed with the previously described values.](media/cosmos-new-container-maintenance.png 'New maintenance container')

12. Select **OK** to create the container.

13. You should now have three containers listed in the Data Explorer.

    ![The three new containers are shown in Data Explorer.](media/cosmos-three-containers.png 'Data Explorer')

#### About Cosmos DB throughput

You will notice that we have intentionally set the **throughput** in RU/s for each container, based on our anticipated event processing and reporting workloads. In Azure Cosmos DB, provisioned throughput is represented as request units/second (RUs). RUs measure the cost of both read and write operations against your Cosmos DB container. Because Cosmos DB is designed with transparent horizontal scaling (e.g., scale out) and multi-master replication, you can very quickly and easily increase or decrease the number of RUs to handle thousands to hundreds of millions of requests per second around the globe with a single API call.

Cosmos DB allows you to increment/decrement the RUs in small increments of 1000 at the database level, and in even smaller increments of 100 RU/s at the container level. It is recommended that you configure throughput at the container granularity for guaranteed performance for the container all the time, backed by SLAs. Other guarantees that Cosmos DB delivers are 99.999% read and write availability all around the world, with those reads and writes being served in less than 10 milliseconds at the 99th percentile.

When you set a number of RUs for a container, Cosmos DB ensures that those RUs are available in all regions associated with your Cosmos DB account. When you scale out the number of regions by adding a new one, Cosmos will automatically provision the same quantity of RUs in the newly added region. You cannot selectively assign different RUs to a specific region. These RUs are provisioned for a container (or database) for all associated regions.

#### About Cosmos DB partitioning

When you created each container, you were required to define a **partition key**. As you will see later in the lab when you review the solution source code, each document stored within a collection contains a `partitionKey` property. One of the most important decisions one must make when creating a new container is to select an appropriate partition key for the data. A partition key should provide even distribution of storage and throughput (measured in requests per second) at any given time to avoid storage and performance bottlenecks. For instance, vehicle metadata stores the VIN, which is a unique value for each vehicle, in the `partitionKey` field. Trip metadata also uses the VIN for the `partitionKey` field, since trips are most often queried by VIN, and trip documents are stored in the same logical partition as vehicle metadata since they are likely to be queried together, preventing fan-out, or cross-partition queries. Package metadata, on the other hand, use the Consignment ID value for the `partitionKey` field for the same purposes. The partition key should be present in the bulk of queries for read-heavy scenarios to avoid excessive fan-out across numerous partitions. This is because each document with a specific partition key value belongs to the same logical partition, and is also stored in and served from the same physical partition. Each physical partition is replicated across geographical regions, resulting in global distribution.

Choosing an appropriate partition key for Cosmos DB is a critical step for ensuring balanced reads and writes, scaling, and, in the case of this solution, in-order change feed processing per partition. While there are no limits, per se, on the number of logical partitions, a single logical partition is allowed an upper limit of 10 GB of storage. Logical partitions cannot be split across physical partitions. For the same reason, if the partition key chosen is of bad cardinality, you could potentially have skewed storage distribution. For instance, if one logical partition becomes larger faster than the others and hits the maximum limit of 10 GB, while the others are nearly empty, the physical partition housing the maxed out logical partition cannot split and could cause an application downtime.

### Task 2: Add Key Vault secrets

### Task 3: Create Azure Databricks cluster

### Task 4: Configure Key Vault-backed Databricks secret store

## Exercise 2: Deploy Azure functions and Web App

### Task 1: Open solution

### Task 2: Code walk-through

### Task 3: Deploy Event Hub consumer Function App

### Task 4: Deploy Change Feed consumer Function App

### Task 5: Deploy Web App

### Task 6: Configure application settings in Azure

## Exercise 3: Configure Logic App for e-mail alerts

### Task 1: Create new workflow

### Task 2: Configure email service

## Exercise 4: Explore and execute data generator

### Task 1: Open solution

### Task 2: Update application configuration

### Task 3: Code walk-through

### Task 4: Run generator

## Exercise 5: Observe data using Cosmos DB Data Explorer and Web App

### Task 1: View data in Cosmos DB Data Explorer

### Task 2: Search and view data in Web App

## Exercise 6: Performing CRUD operations using the Web App

### Task 1: Update vehicle metadata

### Task 2: View consignment, package, and trip data

## Exercise 7: Observe Change Feed using Azure Functions and App Insights

### Task 1: Open App Insights Live View

## Exercise 8: Running the predictive maintenance batch scoring

### Task 1: Import lab notebooks into Azure Databricks

### Task 2: Run batch scoring notebook

### Task 3: Create scheduled notebook job

## Exercise 9: Deploying the predictive maintenance web service

### Task 1: Run deployment notebook

## Exercise 10: Configure windowed queries in Stream Analytics

### Task 1: Add Stream Analytics Event Hubs input

### Task 2: Add Stream Analytics outputs

### Task 3: Create Stream Analytics query

### Task 4: Run query

## Exercise 11: Creating the Fleet status real-time dashboard in Power BI

### Task 1: Log in to Power BI online

### Task 2: Create real-time dashboard

## Exercise 12: Creating the Predictive Maintenance & Trip/Consignment Status reports in Power BI

### Task 1: Add Cosmos DB data sources to Power BI Desktop

### Task 2: Create new report in Power BI Desktop

## After the hands-on lab

Duration: 10 mins

In this exercise, you will delete any Azure resources that were created in support of the lab. You should follow all steps provided after attending the Hands-on lab to ensure your account does not continue to be charged for lab resources.

### Task 1: Delete the resource group

1. Using the [Azure portal](https://portal.azure.com), navigate to the Resource group you used throughout this hands-on lab by selecting Resource groups in the left menu.

2. Search for the name of your resource group, and select it from the list.

3. Select Delete in the command bar, and confirm the deletion by re-typing the Resource group name, and selecting Delete.

You should follow all steps provided _after_ attending the Hands-on lab.