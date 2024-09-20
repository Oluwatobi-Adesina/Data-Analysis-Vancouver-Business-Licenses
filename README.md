# Portfolio Project
## Descriptive Data Analysis

### Project Description: 		
Descriptive Analysis of Business Licensing Trends in Vancouver

### Project Title: 			
Understanding Business License Trends in Vancouver (2023–2024).

### Objective: 		
The main goal of this project is to perform a descriptive study on the business license data of Vancouver for 2023 & 2024. Thus, this analysis aims to provide an overall overview of the general characteristics of the issued Business Licenses, reveal dynamics of Business Activity by regions and types of economic activities, and develop recommendations for further support of businesses and the development of economic policies in the spheres. 

### Dataset:
The dataset consists of business license records, including:

![Open Data Portal 2](https://github.com/user-attachments/assets/4379a92a-f139-44b6-a732-cf73694805c2)

![Open Data Portal](https://github.com/user-attachments/assets/df80dc15-936e-4030-9b57-6100eefa68dd)

BusinessName: 	This includes the name of the business. 
LicenseNumber: 	A unique key for every license provided so that a permit can easily be tracked. 
LicenseType: 		The category of the business license is barristers and solicitors. 
IssueDate: 		  The date the permit was granted was entered into the database. 
ExpiryDate: 		The specific date at the end of the licensed period. 
Business Location: 	The place of the business, whether it is an address, street, city, town, or region where it has set up its operations. 
Status: 			  The current license status could be either Active, Expired or so on). 
Renewal: 		    Specifies whether the license was renewed, was issued initially, or is valid permanently. 

### Methodology For Designing The DAP, Impemntinga and Conducting The Descriptive Analysis.

#### Data Collection and Preparation

![Data Collection and Preparation drawio](https://github.com/user-attachments/assets/c9fa5e42-6308-4756-8265-014333a22341)

The above-selected datasets were obtained from Vancouver’s Open Data Portal and contained accurate information regarding the business license data spanning from 2023 to 2024. A structured approach ensures that the data is well-managed and categorized. Data related to the business was stored in an Amazon S3 bucket called `businesslicensing-registration-team5`. In this bucket, the folders divide data by metric and year. Specifically, the bucket contains top-level folders for each year, `2023` and `2024`, under which `Landing` folders are designated for raw data storage.

#### Data Ingestion

![Data Ingestion Into The Operational Environment png](https://github.com/user-attachments/assets/2eb2ce33-eb9d-49b2-b65e-a6ba6e29fde9)

![S3 bucket business licensing](https://github.com/user-attachments/assets/f3b4ff06-e016-41ef-92a9-5197d18d6f76)

Another crucial part of integrating the AWS Data Analytic Platform for the City of Vancouver is pipeline design. This entails making the following Data Lineage Diagram, which indicates how a specific data set is transformed through several processing stages before it is analyzed. The following is a systematic data flow diagram of the AWS Data Analytic Platform for the City of Vancouver. Using data from the Landing folder, the diagram depicts the subsequent data processing the data undergoes. 

#### The Data Lineage Diagram

![Data Lineage1](https://github.com/user-attachments/assets/468f7ad6-c8e4-4478-8205-72e0242a98d5)

![Data Lineage 2](https://github.com/user-attachments/assets/20315988-48d7-41e9-9d07-a06be1d9a75a)

![Data Lineage3](https://github.com/user-attachments/assets/924b3494-d1c3-4977-a168-e3e07ab2d7fb)

![Data Lineage 4](https://github.com/user-attachments/assets/14058ef2-ab8e-4659-998c-4d0a606c0018)

#### Data Cleaning
The Data Cleaning process Was then done to check for missing values, correct data types, and rename columns if necessary. In this case, the dataset was first assessed to identify missing values in the datasets, as this will help in the cleaning process. Specifically, both datasets' IssuedDate and ExpiredDate columns were changed to datetime format thanks to pd. to_datetime() with errors = ‘coerce’. It helps to change all invalid entries to NaT (Not a Time). Then, rows with missing values in the important columns, IssuedDate or BusinessName, are excluded to remove missing data in important fields. Last of all, the missing values in the fields, which are not essentially important, and thus the BusinessType or LicenseType field, are filled with the ‘Unknown’ value so that the datasets would not be distorted as much as possible while excluding the records with missing values in crucial columns.

###### The Data Cleaning Process Using AWS Glue Databrew:

This process included creating AWS Glue Databrew projects to transform and prepare the two datasets used in the analysis. Both datasets were linked to their specific landing folder within S3, and data preprocessing metrics were run to check for none, null or otherwise missing/invalid values. Some of the presented columns underwent data type changes. Once the cleaning steps were set, jobs were defined, and cleaned jobs were written in CSV format to raw folders in S3. Lastly, the jobs were executed to clean the datasets and prepare them for further processing in the data pipeline to the next stage. Below are screenshots depicting the process taken. 

![Data Cleaning 1](https://github.com/user-attachments/assets/e89e2221-82ab-4cfa-b103-1fb87e7ad85a)

![Data Cleaning 2](https://github.com/user-attachments/assets/0444dbc4-da48-4cf2-82f6-eb12b3537fab)

![Data Cleaning 3](https://github.com/user-attachments/assets/73c71e9d-9f14-4dc4-8cff-035bb186f769)

![Data cleaning 4](https://github.com/user-attachments/assets/9a6c2912-e3b5-4f35-bfed-fbdad718061f)

![Jobs created 1](https://github.com/user-attachments/assets/5f896e14-1d03-4ea5-965e-1854dcb6c85a)

![Job Created 2](https://github.com/user-attachments/assets/00996925-ec14-4896-b8b2-df8962390ea8)

![Recipe Jobs 1](https://github.com/user-attachments/assets/85b3f8d7-1948-4ce6-b76a-8d3f49580a50)

![Job Output Locations](https://github.com/user-attachments/assets/7a19d527-20c3-49fe-99de-9b91e324050a)

![Job Ouput Location   Dataset Preview png](https://github.com/user-attachments/assets/18745aca-c33e-4f73-9e38-3a06e9223b80)

#### Data Pipeline Implementation (ETL):
Data Pipeline Implementation focuses on setting up the ETL (Extract, Transform, Load) process using AWS Glue's Visual ETL tool. This step involves creating a data pipeline that automates the extraction of raw data from your S3 Landing folders, transforming it according to the cleaning and structuring steps already defined, and then loading the processed data into a suitable data store that is another S3 bucket. 

![The Visual ETL](https://github.com/user-attachments/assets/948a3612-4c9b-42d5-94aa-c025f01914c5)

#### Data Analysis
In this step, the cleaned and structured data is interpreted using AWS Athena, the serverless interactive query service for analytical use cases that runs directly against the data; the analyzed data is stored in S3. It is the process of using the Structured Query Language, abbreviated as SQL, which interacts with databases to investigate the license data set and learn more about the data, for instance, the pattern, trends, or gaps in it. 

![Data analysis Through Queries](https://github.com/user-attachments/assets/660bcea3-c6e3-416c-b75b-59778e1969f4)

![Queries Saved](https://github.com/user-attachments/assets/3d58b46f-1062-4bc5-b6dc-712483b47f95)

#### Data Publishing:

This step involved deploying the analyzed data and visualizations onto a web server hosted on an AWS EC2 instance named "BusinessLicensing-Registration-Server-Team5" (Instance ID: `i-0e4c90c0fb6c67b6c`). This instance was securely accessed using a .pem file (licensing. pem) via SSH, ensuring the data could be published securely. 

![Data Publishing 2](https://github.com/user-attachments/assets/76e4f0ba-86a1-4136-aebe-9003e90829ac)

![EC2 Instance for Publsihing](https://github.com/user-attachments/assets/155b9af6-d0cd-4445-90a5-0acbec1daa9b)

#### Data Protection
This step involves putting measures in place to ensure that data stored at rest and in transit are secure in the platform. Such policies include encryption, access management, and data backups. For data at rest, encryption is implemented on the Amazon S3 bucket using SSE-KMS (Server-Side Encryption with AWS Key Management Service). This encryption method offers more flexibility in managing encryption keys, viewing key usage through AWS CloudTrail, and implementing key rotation policies in the city. To enhance the cost efficiency, the S3 Bucket Key option is enabled, thus decreasing the number of times KMS API is called while simultaneously providing coded security.
Moreover, AWS IAM (Identity and Access Management) policies are used to ration and manage access to the S3 bucket to prevent unauthorized users and services from gaining access to the data. These IAM policies are designed to allow only specific permission, therefore minimizing the intrusion by unauthorized individuals. Lastly, Amazon CloudWatch and CloudTrail are used to analyze usage patterns and record unauthorized attempts to gain access. This multi-layered approach preserves the privacy of municipal data and does not burden operations with excessive expenses.

![S3 buckets for governnece](https://github.com/user-attachments/assets/f9ebc239-dee8-4835-bfd5-e74aa21ed223)

![Data Governnace with Encryption](https://github.com/user-attachments/assets/afc3f8b6-6220-40ff-94b8-3d50d6773636)

![Assigned Administrative Permissions](https://github.com/user-attachments/assets/22fe59f2-40db-49cb-bdeb-a37605fa19a6)

![Replication For Backup](https://github.com/user-attachments/assets/d23f1f25-b1db-468e-acc3-49314e15f3c9)

#### Data Governance
This step aims to implement a comprehensive data governance framework to ensure data security, integrity, and compliance with internal policies. It relies heavily on AWS services, including AWS Glue Data Catalog and AWS Glue ETL, to ensure proper management and handling of the city’s datasets. The AWS Glue Data Catalog is critical in organizing and maintaining metadata for the datasets to facilitate efficient data discovery, governance, and accountability by ensuring that data can be tracked and verified throughout its lifecycle. To further enhance data quality and security, trusted zones must be established to differentiate raw data from cleaned data. This will allow for better control and governance over the data, ensuring only verified data is moved into production environments. Regular checks must also be conducted to ensure that data stored in these trusted zones adhere to the predetermined policies.

![Data Governance ETL](https://github.com/user-attachments/assets/d38776c2-15c3-497d-b6cb-9e7bdbb08dc8)

![Governance Job Execution](https://github.com/user-attachments/assets/b064147e-0460-480e-baf4-d6b7fe4754b8)

![Populated Trusted ZOne](https://github.com/user-attachments/assets/899c7526-774b-4fee-8177-20f33777edfa)

#### Data Monitoring
The City of Vancouver Data Analytic Platform is integrated with a detailed monitoring plan that incorporates system health, performance, and security, revealing their status at any time. Amazon CloudWatch monitors metrics such as CPU usage, memory usage, storage space, and creating event alarms. CloudWatch Logs contain detailed system logs, which means that application-level errors are closely watched, and the same can be said for anomalies. AWS CloudTrail also enhances the monitoring and logging of API calls and user activity, adding another layer before every request and action taken is accounted for, especially where sensitive data is involved. In synergy, these tools create a robust monitoring system that simultaneously allows for the occurrence of real-time system monitoring as well as optimization for security, costs, and process efficacy to maintain and manage a platform, which requires constant alerts to various possible problems to function at optimal efficiency.

![Cloudwatch Aarms](https://github.com/user-attachments/assets/6bf72d14-6507-4b62-9125-f3074905bcfb)

![Cloudwatch dashboard](https://github.com/user-attachments/assets/953c5888-927f-47c4-b5ca-ae5a938f91ff)

![Scheduling](https://github.com/user-attachments/assets/e03ef8e5-1c86-486b-937b-2667be5c01de)

![Workflow Dashboard](https://github.com/user-attachments/assets/3f32a0fd-928e-4544-84a1-ccdc5fb98072)

![Cloudwatch Log Events](https://github.com/user-attachments/assets/155e1591-a5de-4202-a954-1fadbba7a51b)

#### Descriptive Statistics
First, the summary statistics for both datasets were generated to get an overview of the numerical data. The summary statistics for the 2023 and 2024 business license datasets provide critical insights into the nature of business licenses issued for those years. Some of these outcomes include a rise in licenses from 2023 to 2024. The fees remained almost fixed, with a standard value of nearly $250 and with a variation. The business activity is higher in Downtown Vancouver than in other regions with limited business activities. Small loopholes dominate most businesses, with 1 to 5 employees, but the data set shows extreme outliers that affect the average employee count. Most licenses are working, and it is rare to find an inactive business license or the business that the license was issued to folded, implying that the business environment is relatively stable. 

The findings of the frequency analysis for the frequency of gaps in the 2023 and 2024 datasets show the following picture: From the license status perspective, it can be noted that the majority of the licenses concerned were ‘Issued’ in both the years 2023 and 2024 with a total of 478 and 394 respectively and only a few licenses were ‘Inactive’ in both the years that is 13 in 2023 and 10 in 2024 along with very little evidence of cancellations/ business closure. As for **business type**, all licenses were classified under ‘‘Office’’ in both years, implying that the dataset only contains licenses of office-type businesses. Related to ‘local areas,’ most of the licenses obtained in 2023 and 2024 are in Downtown, which consists of 356 licenses in 2023 and 333 licenses in 2024, and the rest of the licenses are scattered in the West End and Fairview. In this case, several areas of operation had only a few licenses, while some businesses belonged to the “Unknown” segment. This evaluation affirms that the central regions of Vancouver witnessed the most business license activity in the two years under consideration, and this is evident from the fact that there is petty variation between geographical and business diversification.

#### Data Visualization

Several visualizations were created to better understand trends and distributions in the data. First, a histogram was created to visualize the `FeePaid` column from the `df_2023` and ‘df_20234’ datasets. The histogram displays the distribution of the `FeePaid` values, while the boxplot visualizes the spread and potential outliers in the `FeePaid` data.

##### The Time Series Graphs - Trends in Issuance of New Licenses (2023-2024)

![Time Series Graphs - Trends in Issuance of New Licenses (2023-2024)](https://github.com/user-attachments/assets/d5133472-fb83-4e54-b50e-455b0fcf9351)

##### The Bar Charts Depicting the Frequency of the Local Area In the 2023 and 2024 Datasets.

![Local Area Frequency 2024](https://github.com/user-attachments/assets/6f52697e-c740-4862-866d-30174731f791)

![Local Area Frequency 2023](https://github.com/user-attachments/assets/42adecfd-02ba-4acd-9c50-259f22fe9bc4)

##### The Bar Charts Depicting the Frequency of the License Status In the 2023 and 2024 Datasets.

![License Status Freuency 2024](https://github.com/user-attachments/assets/a7965224-47a6-4af3-ba99-7c1c5317806d)

![License Status Freuency 2023](https://github.com/user-attachments/assets/ab201693-9676-44b8-a1e0-b9784dc8b6c7)

##### The Histogram and Box Plots for the 2023 and 2024 Datasets.

![Fees Paid Trands](https://github.com/user-attachments/assets/b9a19bdb-7db9-41db-81c6-002a9e0ff9ae)

![Fees Paid 2024](https://github.com/user-attachments/assets/4b25759e-d0e7-4922-a904-9252e06b4739)

##### The Correlation Heatmaps For The 2023 and 2024 Datasets.

![Correlation Heatmap 2024](https://github.com/user-attachments/assets/684b0dbb-ccf8-4cac-a183-9e668762c67e)

![Correlation Heatmap 2023](https://github.com/user-attachments/assets/7a0c7ee0-8291-4587-a82d-ab9498bb82c6)

#### Survival Analysis For Business Segmentation

Then, the survival analysis for the business license dataset was conducted, comparing survival rates by year, business type, and local area. The analysis demonstrates that the business's overall survival is high, at 96.96% in 2023 and 97.04% in 2024. All analyzed businesses belong to the “Office” sector, and their survival has been very similar in both years. An inspection of survival rates by local area shows little variability. From the 2023 perspectives, most zones like Fairview, Kitsilano, and Mount Pleasant have 100% survival rates; the West End is slightly less, with 95%, and the lowest survival rate of 50% is West Point Grey. In 2024, almost all areas depicted a 100% survival rate. Nonetheless, areas like Arbutus-Ridge depicted a significant percentage drop to 66.67%, and West End dropped to 92.31%. These findings suggest that most businesses continued to operate, with the overall survival rates only slightly dropping in some local areas.

#### Insights and Findings

![Concept Map On the Insights Obtained drawio (3)](https://github.com/user-attachments/assets/da2b44ce-902c-48e5-a9e0-5ea2516df23d)

The following trends and patterns are identified after examining the business license data for 2023 and 2024 in Vancouver business licenses. From the analysis of the business license database of Vancouver for the years 2023 and 2024, several trends and patterns can be established in the business activity. One such observation is the significant upsurge in the number of licenses granted for the year 2024 from the year 2023, where only 12 licenses were granted. Such a change implies that data for 2023 is still missing or there was a sharp increase in business registrations in 2024 due to the economic revival or changes in policies or conditions affecting the businesses. Moreover, license fees suggest that many businesses pay approximately $250 for their licenses, and if you take the raw average ($253.92) and the median ($250) license fees, they are nearly the same. This means that the structure of costs for business licenses is relatively consistent in Vancouver, with only minor fluctuations. 
 
Regionally, there is a strong focus on the Downtown area since 689 licenses were allocated to it. Some places like the West End and Fairview had fewer permits, while some other regions like Oakridge and Strathcona had only a single licensed outlet each. This implies that Downtown Vancouver remains the core business district and that little business activities occur in areas out in the suburbs. Also, the majority of the businesses in the dataset are small, as is revealed by the fact that the median number of employees is one where most companies employ 1-5 employees. Likewise, the average number of employees in the dataset is over 960,000, but there are distortions, probably due to data entry mistakes, that significantly pull this figure up. Most enterprises are small-scale, and most licenses are “Office” type, corresponding to the enterprise scale. 
 
As for the license status, most of them have remained ‘Issued,’ as indicated by 872 licenses; only 23 licenses are labelled ‘Inactive,’ and 2 licenses are ‘Cancelled. ’ This implies a reasonably constant business climate in Vancouver as many companies hold on to their licenses. However, more research is needed on why some regions have low business activity or higher rates of inactive licenses among the establishments. In summary, it reads the data underpinning a relatively stable and centralized economic structure with business activity concentrated in Vancouver. It also suggests developing relatively less active zones for business growth and strengthening the focus on SMBs targeting the definite policy or stimulus. 

#### Recommendations

Hence, after a statistical analysis of the business license data of Vancouver for 2023 and 2024, The following recommendations could be of great importance when formulating policies and developing the economy in the city. First, specific targeted incentives to support business development in these areas should be adopted, considering the higher intensity of business activity in the Downtown area and the relatively low activity level in some peripheral zones, such as Oakridge, Strathcona, and West Point Grey. This may entail free incentives such as tax holidays, subsidies to companies that open operations in less developed areas, or concessions to license charges. Another area is that the city could redesign specific neighbourhoods as business districts or provide incentives to improve infrastructure in such districts to decentralize the economy and take the pressure off the downtown area. 

Second, while the average and median fees for a license are approximately $250, there is evidence that the rates are standardized across licensees and may not consider differences in business size or type. The city could implement a scaled system where businesses within the city, especially those with few employees, pay less than an equivalent business with a sizeable number of employees. This would reduce the licensing process's asymmetry, potentially benefitting most of the dataset, comprising small companies with 1–5 employees. This fee structure could reduce the barriers that prevent new players from participating, thus creating employment and boosting the economy. 

Moreover, the overall relatively high survival rates indicate that most regions have a stable business environment; however, the considerable decline of the given indicator in neighbourhoods like West Point Grey and Arbutus-Ridge leads to the conclusion that the concentrated local economy should be supported. Government stakeholders should find out why businesses operating in such areas have lower survival rates, which could be because of high operating costs, lack of traffic, or stiff competition, and develop specific measures to support struggling businesses. Such problems could be solved by support mechanisms such as financial aid, tutoring of firms in trouble, or community support projects. To that effect, the city should ensure that it works towards raising probabilities of business survival in areas that are perceived to record low probabilities; this is because when these probabilities are standardized, it creates an even ground for businesses and their provision of resources that might not otherwise be available.

Finally, due to the changes in the flow of licenses from 2023 to 2024, the authorities need to inquire into the reasons for such a drastic increase. If the growth is attributed to economic improvement or adopting the right policies, then such policies should be supported and enlarged to help sustain business development. If some factors outside this state trigger this rising trend, for instance, the relaxation of measures put in place to curb the spread of COVID-19 or even the increasing demand for business ventures, then the city in question should ensure that it supports these new business establishments to maintain this kind of growth. Cutting down licensing procedures and formalities, minimizing organizational hassles, and offering better directions to entrepreneurs related to state laws can increase the rate of business registrations and renewal that, as a result, will foster a more robust economy in the country.


