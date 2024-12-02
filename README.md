
### **Use Case: Real-Time Financial Reporting and Analytics**

**Overview:**
A financial services company needs to generate real-time financial reports for its clients by integrating its existing Azure SQL database with dashboards and analytics platforms. The company wants to avoid the lengthy process of creating custom APIs and instead utilize XenHey's API connector to expose stored procedures and views securely and efficiently.

---

### **Use Case Description:**
**Problem Statement:**
- The finance team relies on stored procedures in Azure SQL to calculate real-time balances, portfolio performance, and risk analysis.
- Existing manual processes or ad-hoc integrations are inefficient and prone to errors, causing delays in reporting.

**Solution with XenHey:**
- XenHey's API connector is used to expose stored procedures and views from the Azure SQL database.
- These APIs are configured to provide real-time financial data to a client-facing dashboard, ensuring seamless data access.
- The secure, configuration-based approach simplifies integration while maintaining compliance with financial data governance policies.

---

### **Mermaid Diagram:**

```mermaid
graph TD
    A[Client Dashboard] -->|API Call| B[XenHey API Connector]
    B -->|Stored Procedure Call| C[Azure SQL Database]
    C -->|Execute Stored Procedure| D[Financial Data Views]
    D -->|Return Data| B
    B -->|API Response| A
```

Set Up Steps 

Creating a serverless API using Azure that leverages Service Bus to communicate with an SQL Database involves several steps. Here's a high-level overview of how you can set this up:

1. **Set Up Azure SQL Database**:
   - Create an Azure SQL Database instance.
   - Set up the necessary tables and schemas you'll need for your application.
     
2. **Deploy Serverless API using Azure Functions**:
   - Create a new Azure Function App.
   - Develop an HTTP-triggered function that will act as your API endpoint.
   - In this function, when data is received, send a message to the Service Bus queue or topic.

3. **Optimize & Monitor**:
   - Monitor the performance of your functions using Azure Monitor and Application Insights.
   - Optimize the performance, scalability, and cost by adjusting the function's plan (Consumption Plan, Premium Plan, etc.) and tweaking the configurations.

4. **Deployment**:
   - Deploy your functions to the Azure environment. You can use CI/CD pipelines using tools like Azure DevOps or GitHub Actions for automated deployments.

By following these steps, you'll have a serverless API in Azure that uses Service Bus as a mediator to process data and store it in an SQL Database. This architecture ensures decoupling between data ingestion and processing, adding a layer of resilience and scalability to your solution.


## Appplication Setting 

|Key|Value | Comment|
|:----|:----|:----|
|AzureWebJobsStorage|[CONNECTION STRING]|RECOMMENDATION :  store in AzureKey Vault.|
|ConfigurationPath| [CONFIGURATION FOLDER PATH] |Folder is optional
|ApiKeyName|[API KEY NAME]|Will be passed in the header  :  the file name of the config.
|AppName| [APPLICATION NAME]| This is the name of the Function App, used in log analytics|
|StorageAcctName|[STORAGE ACCOUNT NAME]|Example  "AzureWebJobsStorage"|
|ServiceBusConnectionString|[SERVICE BUS CONNECTION STRING]|Example  "ServiceBusConnectionString".  Recommmended to store in Key vault.|
|DatabaseConnection|[DATABASE CONNECTION STRING]|Example  "DatabaseConnection". Recommmended to store in Key vault.|
|TimerInterval|[TIMER_INTERVAL]|Example  "0 */1 * * * *" 1 MIN|


> **Note:**  Look at the configuration file in the **Config** Folder and created a Table to record information.

## Configuration Files 

> **Note:** The **Configuration** is located in the  FunctionApp  in a **Config** Folder.

|FileName|Description|
|:----|:----|
|99F77BEF300E4660A63A939ADD0BCF68.json| **Upload File** Parse CSV file --> Write Batched Files To Storage|
|43EFE991E8614CFB9EDECF1B0FDED37A.json| **File Parser** Parse CSV file --> File received from SFTP will use this process to parse files|
|43EFE991E8614CFB9EDECF1B0FDED37D.json| **Upload File** Parse JSON/CSV Directly to NO SQL DB|
|43EFE991E8614CFB9EDECF1B0FDED37C.json| **Service Bus Trigger for SQL DB** | Receive JSON payload and insert into SQL DB|
|43EFE991E8614CFB9EDECF1B0FDED37F.json| **Service Bus Trigger for No SQL DB** | Receive JSON payload and insert into NO SQL DB|
|43EFE991E8614CFB9EDECF1B0FDED37E.json| **Blob Trigger** Send parsed/sharded file  to Send to Service Bus|
|43EFE991E8614CFB9EDECF1B0FDED37B.json| **Search Resullt from NO SQLDB** |
|43EFE991E8614CFB9EDECF1B0FDED37G.json| **Search SQL DB. Return resultset** |
|3FB620B0E0FD4E8F93C9E4D839D00E1E.json| **Copy File from SFTP into the pickup folder** |
|3FB620B0E0FD4E8F93C9E4D839D00E1F.json| **Create a new Record in NoSQL Database** |
|CC244934898F46789734A9437B6F76CA.json| Encode Payload Request |
|6B427917E36A4DA281D57F9A64AD9D55.json| Get reports from DB  |


> Create the following blob containers and share in azure storage

|ContainerName|Description|
|:----|:----|
|config|Location for the configuration files|
|pickup|Thes are files that are copied from the SFTP share and dropped in the pickup container |
|processed|These are files the have been parsed and dropped in th processed container|

|Table|Description|
|:----|:----|
|csvbatchfiles|Track the CSV parsed files|
|training[YYYYMMDD]|N0 SQL DataStore|




**Conclusion:**
By leveraging XenHey's API connector, financial institutions can streamline their reporting processes, ensuring compliance, efficiency, and real-time access to critical data. This approach not only improves client satisfaction but also reduces operational complexity.


**Empowering Seamless Database Integrations with XenHey: API Connector to Azure SQL with Configurations over Code**

In today’s fast-paced development environment, enterprises need solutions that can quickly integrate with existing databases without lengthy coding processes. Enter **XenHey**—a powerful API connector that bridges the gap between your applications and Azure SQL. By enabling the ability to call stored procedures and views using configurations over code, XenHey simplifies and accelerates database integration, making it easier to unlock the power of your data.

### Key Benefits of Using XenHey’s API Connector with Azure SQL

1. **Seamless Integration with Existing SQL Resources**
   - XenHey directly connects with your existing Azure SQL database, allowing you to leverage stored procedures and views you've already created. This eliminates the need to rewrite complex logic, saving time and reducing errors.

2. **Configuration-Driven Approach**
   - Instead of writing extensive code to interact with your database, XenHey uses a configuration-based approach. This minimizes the need for custom scripts and code updates, making it easier to maintain and modify database interactions as your needs evolve.

3. **Flexibility and Adaptability**
   - XenHey's connector is highly customizable and can be configured to meet various operational requirements. You can control which stored procedures and views are accessible, specify parameter inputs, and even define response structures—all through intuitive configurations.

4. **Enhanced Security**
   - With secure, managed access to your Azure SQL database, XenHey ensures that database interactions are only available to authorized users. Its configuration-based approach also allows you to manage permissions and security settings with ease.

5. **Reduced Development Time**
   - By removing the need for complex code, XenHey drastically reduces the time developers spend on integration tasks. The configuration-over-code model also means that non-developers can manage and adapt database connections, increasing productivity and agility across teams.




  


# Dynamic configuration store with Endpoint support


## Architecture Diagram

![image](https://github.com/user-attachments/assets/2c5a335d-f723-4571-9952-f6be90f26d2d)



## Session Recorded 

[Session Video - 10/16/2024](https://pbsdatastore.blob.core.windows.net/training/TrainingInfo/video1527880342.mp4?sp=r&st=2024-10-22T15:12:48Z&se=2025-10-22T23:12:48Z&spr=https&sv=2022-11-02&sr=b&sig=h0J%2B99Qdn4NP%2BgFo1ny%2Bc2Vb3HOCEbq7pvQBWGHqMC8%3D)




### How It Works

Using XenHey to connect with Azure SQL is straightforward. Here’s a quick breakdown of the process:

1. **Configuration Setup**
   - In the XenHey dashboard, configure your API connector with details about your Azure SQL database. Define accessible stored procedures and views, set parameter requirements, and specify response structures.

2. **Connecting Stored Procedures and Views**
   - Instead of writing API endpoints manually, XenHey enables you to select stored procedures and views through a simple interface. This allows you to manage parameters, test API calls, and see the expected output directly in the platform.

3. **Testing and Validation**
   - XenHey’s platform provides a testing environment, allowing you to validate each connection before going live. This step ensures that your configurations align with expected database responses and business requirements.

4. **Deployment**
   - Once configurations are complete, deploy the API connector to make it available to your applications. XenHey supports various authentication methods, ensuring that only approved applications and users can access your Azure SQL database.

### Use Cases for XenHey’s API Connector

XenHey’s solution is particularly valuable for businesses looking to:

- **Expose Data to External Applications**: Quickly expose key data points or reports from stored procedures without requiring extensive code or complex API setups.
- **Enable Analytics and Reporting**: Allow analytics applications or dashboards to call stored procedures for real-time insights from your Azure SQL database.
- **Simplify Legacy Integrations**: If you have legacy applications that rely on Azure SQL, XenHey offers a straightforward way to integrate them with modern API calls.

### Final Thoughts

XenHey’s API connector is a game-changer for enterprises using Azure SQL. By embracing a configuration-over-code approach, XenHey enables faster integrations, enhances security, and reduces the technical burden on development teams. Whether you’re working with legacy databases or building new applications that require real-time data access, XenHey provides a flexible and efficient solution that grows with your business.

**Ready to integrate with ease?** Explore the power of XenHey’s API connector to streamline your Azure SQL interactions and unlock new efficiencies.

