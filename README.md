# Case Study #04: Global Electronics Store Chain

---

## **1. Executive Summary**: 
This case study analyzes a global electronics store chain (primarily across Europe), covering **144** stores across **37** countries, using sales, inventory, and product data from January **2-5, 2017**.  
The Analysis reveals that *Solar Blender Lux* was the best-selling product, contributing approx. **€85M** in revenue, while *Expert MegaDom* **(€13M)** was the top-performing store and *Moscow* **(€20M)** the leading city.  
This suggests that Week 1 (02-05 Jan) was a strong period for both *Expert MegaDom* and *Moscow*, and also indicates that the marketing and promotional offer for *Solar Blender Lux* was very attractive and effective.  

Hence, my recommendations are:
1. *Building on these marketing campaigns and offers in future periods*
2. *Applying best practices from top-performing stores to improve performance across underperforming stores.*  

## **2. Business Task**:
#### *Analyze the revenue distribution across products, stores and cities, and identify key drivers.*

This descriptive dashboard displays *total revenue, number of stores and cities along with top 10 performing stores & cities, and daily revenue* in the first week of 2017. 

![image1](Screenshots/01_Descriptive_Dashboard.png)  

## **3. Dataset Overview**

**Data Source**: *IBM BI Analyst Course - Capstone Project*  
**Dataset**: *6 Tables(City_Names, Product_Hierarchy, Product_Names, Sales, Store_Cities, Store_Names)*  
**Time Period**: *Jan 02 - Jan 05 (2017)*

Dataset Tables:  
![image2](Screenshots/02_03_Dataset_Overview.png)  

## **4. Data Cleaning & Preparation**

1. Created main folder *CS04_GlobalElectronicsStoreChain*
2. Created subfolders: 00_Dataset; 01_Data_Cleaning; 02_Data_Analysis; 03_Data_Visualization; 04_Reporting
3. Downloaded and saved original files under *CS04_GlobalElectronicsStoreChain > 00_Dataset*
4. Copied and pasted files under *CS04_GlobalElectronicsStoreChain > 01_Data_Cleaning*
5. Cleaned all 6 tables and made sure they are ready for analysis (examined the tables, checked for data types, spelling mistakes, missing values, duplicates, formated columns, standardized texts, removed columns that contained all blank rows)  
    5.1 used pivot tables, helper columns, flash fill, xlookup and other functions to ensure data is clean and ready for analysis
6. BONUS: Used synthetic data to fill the rows (only minority of data) with/or average/most used value

## **5. Methodology**

1. Downloaded and organized the dataset  

![image3](Screenshots/02_03_Dataset_Overview.png)  
*Dataset Folder*

---

2. Cleaned, prepared and joined the dataset for analysis  
|  
v  
Example (before and after):  
![image4](Screenshots/04_Cleaning.png) into ![image5](Screenshots/05_Cleaning.png)  

---

3. Analyzed the dataset and derived key insights in both Excel and SQL

Excel:  

![image6](Screenshots/06_Excel_Analysis.png)  


SQL:  

![image7](Screenshots/07_SQL_Analysis.png)  

---

4. Created Interactive Power BI Dashboards (Descriptive Dashboard, Products, Stores and Cities)  

![image8](Screenshots/08_Interactive_BI_Dashboard_Cities.png)  

---

## **6. Skills**

    SQL: Trend analysis, CTEs, Joins, Window Functions
    Excel: Data Transformation, Data Cleaning, Pivot Tables, Data Analysis
    Power BI: Data Transformation, Interactive Dashboard Creation, Data Visualization, DAX  
    Jupyter Notebook: Markdown documentation  

**Quick SQL Code**:
```
#Task 8: Find daily running total and running average per store
CREATE OR REPLACE VIEW GESC_DataAnalysis.08_Daily_Revenue_RunningTotal_and_RunningAVG_per_Store AS
  SELECT
    store_id,
    date,
    daily_revenue,
    SUM(daily_revenue) OVER(partition by store_id ORDER BY date) AS running_total,
    AVG(daily_revenue) OVER(partition by store_id ORDER BY date) AS running_average
  FROM(
    SELECT
      store_id,
      date,
      SUM(revenue) AS daily_revenue
    FROM
      `globalelectronicstorechain.GESC_DataAnalysis.Sales`
    GROUP BY
      store_id,
      date
  )
  ORDER BY
    store_id,
    date;
```
## **7. Results**

This analysis is based on a dataset snapshot covering **699 products, 144 stores, and 37 cities** across the global chain.  
Moscow was the leading revenue city **(€20M)** in this dataset snapshot, with Expert MegaDom as the top-performing store in Moscow, and also the overall #1 store by revenue **(€13M)**.

The best-selling product was Solar Blender Lux, sold over **420K** times, generating **€85M** in revenue and contributing to **83%** of total revenue.  
There are two logical explanations for this outlier:  
    1. More realistic: this dataset is only a small snapshot of the full dataset, and due to its limited scope, it happens that a large portion of transactions involve Solar Blender Lux (the full dataset likely contains millions of rows, so distribution would normalize).  
    2. Alternatively, for the sake of this case study, we could assume a marketing campaign was abnormally successful (though this would be unlikely to create such an extreme outlier on its own) and build a narrative around that campaign.  

Store Type 4 accounted for the majority of revenue share **(83%)**, heavily influenced by the Solar Blender Lux outlier effect.  
The stock-to-sales correlation is **0.33**, however, since many stores are deviating from the trend line, this does not necessarily mean that higher stock directly leads to higher sales.  
Even though London had the highest number of stores, Moscow was the best-performing city overall in terms of revenue.  

#### **Visuals**

Top 10 Cities by Revenue:

![image9](Screenshots/09_Top_10_Cities.png)  

---

Revenue Drivers and Best Selling Products:  

![image10](Screenshots/10_Revenue_Drivers.png)

---

Best performing Stores:

![image11](Screenshots/11_Best_Performing_Stores.png)

---

Revenue Share by Store Type:

![image12](Screenshots/12_Revenue_Share_by_Storetype.png)

---

Stock to Sales Correlation:

![image13](Screenshots/13_Stock_to_Sales_Correlation.png)

---

Total Stores per City:

![image14](Screenshots/14_Total_Stores_per_City.png)

## **8. Key Insights**

* Moscow is the leading revenue city
* Expert MegaDom is the top-performing store
* Solar Blender Lux is the best selling product
* Overstocking doesn't show a strong positive relationship with sales  

## **9. Recommendations**

* Building on **Solar Blender Lux** marketing campaign
* Replicate top-store practices across underperforming stores
* Minimize overstock levels across stores for low-priority products

## **10. Limitations**

* This dataset is only a small snapshot of the complete dataset
* The timeframe is only from 02 Jan – 05 Jan (1 week is too short to draw stable conclusions and is prone to outliers)
* This dataset is from 2017
* Solar Blender Lux outlier effect, which heavily skews revenue distribution (although it could be excluded from analysis, it was useful for the marketing narrative)
* The dataset contains fictional stores mixed with real existing stores, which may affect data consistency and interpretation

## **11. Next Steps**

* Obtain access to the full dataset for more reliable and representative analysis
* Use a longer historical timeframe (e.g. last 2–3 years) for proper descriptive and diagnostic insights
* Enable real-time or near real-time data to support predictive analysis and trend monitoring
* Include seasonality, marketing campaigns and events data to better understand spikes and anomalies across the year
* Investigate and validate outlier products (e.g. Solar Blender Lux) to confirm whether they are data issues or true business drivers
## **12. Tools**

* SQL
* Excel
* Power BI
* Jupyter
