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
BusinessName: 	This includes the name of the business. 
LicenseNumber: 	A unique key for every license provided so that a permit can easily be tracked. 
LicenseType: 		The category of the business license is barristers and solicitors. 
IssueDate: 		  The date the permit was granted was entered into the database. 
ExpiryDate: 		The specific date at the end of the licensed period. 
Business Location: 	The place of the business, whether it is an address, street, city, town, or region where it has set up its operations. 
Status: 			  The current license status could be either Active, Expired, or so on). 
Renewal: 		    Specifies whether the license was renewed, was issued initially, or is valid permanently. 

### Methodology:
#### Data Collection and Preparation
![Data Collection and Preparation drawio](https://github.com/user-attachments/assets/c9fa5e42-6308-4756-8265-014333a22341)

After downloading the two datasets in Excel format (one for 2023 and one for 2024), they are loaded into Google Colab. Google Colab is the best suited for Exploratory Data Analysis because it allows for combining data analysis tools such as Pandas, NumPy, Matplotlib, and Seaborn. On the other hand, exploratory data analysis involves going through datasets to identify patterns and outliers and verifying assumptions through summarized statistics and graphical displays. After uploading the files, they were loaded into Pandas DataFramess.

#### Data Cleaning
The Data Cleaning process Was then done to check for missing values, correct data types, and rename columns if necessary. In this case, the dataset was first assessed to identify missing values in the datasets, as this will help in the cleaning process. Specifically, both datasets' IssuedDate and ExpiredDate columns were changed to datetime format thanks to pd. to_datetime() with errors = ‘coerce’. It helps to change all invalid entries to NaT (Not a Time). Then, rows with missing values in the important columns, IssuedDate or BusinessName, are excluded to remove missing data in important fields. Last, of all, the missing values in the fields, which are not essentially important, and thus the BusinessType or LicenseType field, are filled with the ‘Unknown’ value so that the datasets would not be distorted as much as possible while excluding the records with missing values in crucial columns.

#### Descriptive Statistics
First, the summary statistics for both datasets were generated to get an overview of the numerical data. The summary statistics for the 2023 and 2024 business license datasets provide critical insights into the nature of business licenses issued for those years. Some of these outcomes include a rise in licenses from 2023 to 2024. The fees remained almost fixed, with a standard value of nearly $250 and with a variation. The business activity is higher in Downtown Vancouver than in other regions with limited business activities. Small loopholes dominate most businesses, with 1 to 5 employees, but the data set shows extreme outliers that affect the average employee count. Most licenses are working, and it is rare to find an inactive business license or the business that the license was issued to folded, implying that the business environment is relatively stable. 


The findings of the frequency analysis for the frequency of gaps in the 2023 and 2024 datasets show the following picture: From the license status perspective, it can be noted that the majority of the licenses concerned were ‘Issued’ in both the years 2023 and 2024 with a total of 478 and 394 respectively and only a few licenses were ‘Inactive’ in both the years that is 13 in 2023 and 10 in 2024 along with very little evidence of cancellations/ business closure. As for **business type**, all licenses were classified under ‘‘Office’’ in both years, implying that the dataset only contains licenses of office-type businesses. Related to ‘local areas,’ most of the licenses obtained in 2023 and 2024 are in Downtown, which consists of 356 licenses in 2023 and 333 licenses in 2024, and the rest of the licenses are scattered in the West End and Fairview. In this case, several areas of operation had only a few licenses, while some businesses belonged to the “Unknown” segment. This evaluation affirms that the central regions of Vancouver witnessed the most business license activity in the two years under consideration, and this is evident from the fact that there is petty variation between geographical and business diversification.

#### Data Visualization
Then, some visualizations were created to better understand trends and distributions in the data. First, a histogram was created to visualize the `FeePaid` column from the `df_2023` and ‘df_20234’ datasets. The histogram displays the distribution of the `FeePaid` values, while the boxplot visualizes the spread and potential outliers in the `FeePaid` data.

![Time Series Graphs - Trends in Issuance of New Licenses (2023-2024)](https://github.com/user-attachments/assets/d5133472-fb83-4e54-b50e-455b0fcf9351)

![Local Area Frequency 2024](https://github.com/user-attachments/assets/6f52697e-c740-4862-866d-30174731f791)

![Local Area Frequency 2023](https://github.com/user-attachments/assets/42adecfd-02ba-4acd-9c50-259f22fe9bc4)

![License Status Freuency 2024](https://github.com/user-attachments/assets/a7965224-47a6-4af3-ba99-7c1c5317806d)

![License Status Freuency 2023](https://github.com/user-attachments/assets/ab201693-9676-44b8-a1e0-b9784dc8b6c7)

![Fees Paid Trands](https://github.com/user-attachments/assets/b9a19bdb-7db9-41db-81c6-002a9e0ff9ae)

![Fees Paid 2024](https://github.com/user-attachments/assets/4b25759e-d0e7-4922-a904-9252e06b4739)

![Correlation Heatmap 2024](https://github.com/user-attachments/assets/684b0dbb-ccf8-4cac-a183-9e668762c67e)

![Correlation Heatmap 2023](https://github.com/user-attachments/assets/7a0c7ee0-8291-4587-a82d-ab9498bb82c6)


#### Survival Analysis For Business Segmentation
Then, the survival analysis for the business license dataset was conducted, comparing survival rates by year, business type, and local area. The analysis demonstrates that the business's overall survival is high, at 96.96% in 2023 and 97.04% in 2024. All analyzed businesses belong to the “Office” sector, and their survival has been very similar in both years. An inspection of survival rates by local area shows little variability. From the 2023 perspectives, most zones like Fairview, Kitsilano, and Mount Pleasant have 100% survival rates; the West End is slightly less, with 95%, and the lowest survival rate of 50% is West Point Grey. In 2024, almost all areas depicted a 100% survival rate. Nonetheless, areas like Arbutus-Ridge depicted a significant percentage drop to 66.67%, and West End dropped to 92.31%. These findings suggest that most businesses continued to operate, with the overall survival rates only slightly dropping in some local areas.

#### Insights and Findings

![Concept Map On the Insights Obtained drawio (3)](https://github.com/user-attachments/assets/da2b44ce-902c-48e5-a9e0-5ea2516df23d)

The following trends and patterns are identified after examining the business license data for 2023 and 2024 in Vancouver business licenses. From the analysis of the business license database of Vancouver for the years 2023 and 2024, several trends and patterns can be established in the business activity. One such observation is the significant upsurge in the number of licenses granted for the year 2024 from the year 2023, where only 12 licenses were granted. Such a change implies that data for 2023 is still missing or there was a sharp increase in business registrations in 2024 due to the economic revival or changes in policies or conditions affecting the businesses. Moreover, license fees suggest that many businesses pay approximately $250 for their licenses, and if you take the raw average ($253.92) and the median ($250) license fees, they are nearly the same. This means that the structure of costs for business licenses is relatively consistent in Vancouver, with only minor fluctuations. 
 
Regionally, there is a strong focus on the Downtown area since 689 licenses were allocated to it. Some places like the West End and Fairview had fewer permits, while some other regions like Oakridge and Strathcona had only a single licensed outlet each. This implies that Downtown Vancouver remains the core business district and that little business activities occur in areas out in the suburbs. Also, the majority of the businesses in the dataset are small, as is revealed by the fact that the median number of employees is one where most companies employ 1-5 employees. Likewise, the average number of employees in the dataset is over 960,000, but there are distortions, probably due to data entry mistakes, that significantly pull this figure up. Most enterprises are small-scale, and most licenses are “Office” type, corresponding to the enterprise scale. 
 
As for the license status, most of them have remained ‘Issued,’ as indicated by 872 licenses; only 23 licenses are labeled ‘Inactive,’ and 2 licenses are ‘Cancelled. ’ This implies a reasonably constant business climate in Vancouver as many companies hold on to their licenses. However, more research is needed on why some regions have low business activity or higher rates of inactive licenses among the establishments. In summary, it reads the data underpinning a relatively stable and centralized economic structure with business activity concentrated in Vancouver. It also suggests developing relatively less active zones for business growth and strengthening the focus on SMBs targeting the definite policy or stimulus. 

#### Recommendations
Hence, after a statistical analysis of the business license data of Vancouver for 2023 and 2024, The following recommendations could be of great importance when formulating policies and developing the economy in the city. First, specific targeted incentives to support business development in these areas should be adopted, considering the higher intensity of business activity in the Downtown area and the relatively low activity level in some peripheral zones, such as Oakridge, Strathcona, and West Point Grey (Warner & Zheng, 2013). This may entail free incentives such as tax holidays, subsidies to companies that open operations in less developed areas, or concessions to license charges. Another area is that the city could redesign specific neighborhoods as business districts or provide incentives to improve infrastructure in such districts to decentralize the economy and take the pressure off the downtown area. 
Second, while the average and median fees for a license are approximately $250, there is evidence that the rates are standardized across licensees and may not consider differences in business size or type. The city could implement a scaled system where businesses within the city, especially those with few employees, pay less than an equivalent business with a sizeable number of employees. This would reduce the licensing process's asymmetry, potentially benefitting most of the dataset, comprising small companies with 1–5 employees. This fee structure could reduce the barriers that prevent new players from participating, thus creating employment and boosting the economy. 

Moreover, the overall relatively high survival rates indicate that most regions have a stable business environment; however, the considerable decline of the given indicator in neighborhoods like West Point Grey and Arbutus-Ridge leads to the conclusion that the concentrated local economy should be supported. Government stakeholders should find out why businesses operating in such areas have lower survival rates, which could be because of high operating costs, lack of traffic, or stiff competition, and develop specific measures to support struggling businesses. Such problems could be solved by support mechanisms such as financial aid, tutoring of firms in trouble, or community support projects (Pergelova & Angulo-Ruiz, 2014). To that effect, the city should ensure that it works towards raising probabilities of business survival in areas that are perceived to record low probabilities; this is because when these probabilities are standardized, it creates an even ground for businesses and their provision of resources that might not otherwise be available.

Finally, due to the changes in the flow of licenses from 2023 to 2024, the authorities need to inquire into the reasons for such a drastic increase. If the growth is attributed to economic improvement or adopting the right policies, then such policies should be supported and enlarged to help sustain business development. If some factors outside this state trigger this rising trend, for instance, the relaxation of measures put in place to curb the spread of COVID-19 or even the increasing demand for business ventures, then the city in question should ensure that it supports these new business establishments to maintain this kind of growth. Cutting down licensing procedures and formalities, minimizing organizational hassles, and offering better directions to entrepreneurs related to state laws can increase the rate of business registrations and renewal that, as a result, will foster a more robust economy in the country.


