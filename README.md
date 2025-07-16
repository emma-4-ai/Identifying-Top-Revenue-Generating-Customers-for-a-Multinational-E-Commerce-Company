# Identifying-Top-Revenue-Generating-Customers-for-a-Multinational-E-Commerce-Company
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe. 



# Project overview 
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe. 


The objective of the study is to analyze and identify the **Top 10 highest revenue-generating customers**, offering critical business insights into customer value, regional sales dynamics, and strategic growth opportunities.


Leveraging advanced data analytics techniques, including data preprocessing, aggregation, and visualization, this project uncovers key patterns in customer spending behavior across diverse markets. 


By ranking customers based on total revenue contribution, the analysis empowers business stakeholders with actionable intelligence to optimize customer relationship management, tailor marketing strategies, and enhance profitability in a globally competitive landscape.

This project serves as a practical application of data science principles in the domain of e-commerce, showcasing the impact of data-driven decision-making on strategic business outcomes.

### Problem Statement  
**Who are Top 10 Customers of the Company interms of Total Revenue generated since the company started ?**

### Project Objectives 
1. **To Identify Top Revenue-Generating Customers**

   * By Analyzing sales data to determine the top 10 customers contributing the highest total revenue across all regions.


2. **To Understand Revenue Concentration**

   * By Analyzing how much of the company's total revenue is concentrated among top customers.


3. **To Uncover Geographic Patterns**

   * By Assessing the global distribution of high-value customers across the Countries to identify key markets and regional revenue   clusters.


4. **To Support Strategic Decision-Making**

   * By Providing actionable insights to the company’s sales and marketing teams for developing targeted retention, loyalty, and upselling strategies.



5. **To Demonstrate Real-World Data Science Application**

   * By Showcasing the use of data science tools and techniques (data preprocessing, aggregation, visualization) in solving a real-world business problem.


6. **To Enable Stakeholder Communication**

   * By Creating intuitive visualizations and summaries that allow non-technical stakeholders to understand key findings and insights.


7. **To Lay the Groundwork for Predictive Modeling**

   * By Establishing a foundational dataset and insights that could be extended into customer lifetime value prediction or churn modeling in future phases.

### Data Source
**The Company's central transaction database**

### Project Methodology
- **Data Collection**: Data was collected from the Company's Central Transaction Database

- **Data Pre-processing**: Loaded the data from a CSV file into a Pandas Dataframe

- **Data Inspection and Cleaning**: Checked for Missing values, Checked for Duplicates.

- - Handled missing values
  - Handled duplicate values

- **Data Modification**: generated some  core metrics which were NOT provided from the dataset, and would be required for the purpose of the data   analysis

- **Data Aggregation**: To Compute the major metric : Total Revenue by Customer**

- **Data Sorting/ Data Ranking**: To Determine the Most Importat Metric:  **Top 10 highest revenue-generating customers**

- **Data Visualization**: To uncover the **Top 10 highest revenue-generating customers** in a pictorial form.

- **Data Interpretation**:

- **Key Findings**

- **Conclusions**

- **Recommendation**

### Data Collection
Sales data was obtained from a central transaction database of the company representing orders placed by customers across multiple countries. Each record included attributes such as:

* `Customer ID`
* `OrderNo`
* `OrderQuantity`
* `CostPrice_usd`
* `SellingPrice_usd`
* `OrderDate`
* `CustomerName`
* `CustomerCity`
* `CustomerState`
* `CustomerCountry`
* `ProductCategory`
* `ProductColor`
* `Model`

### Data Pre-processing
**Data Loading**: 
Reading the Raw Dataset which originally existed as a CSV file into a Pandas Dataframe

__Task:__ Follow the appropriate steps in reading a CSV file into a pandas Dataframe, 


and  Read the data stored  in the csv file named:  `bikes` From your computer.


The resulting Dataframe should be named : `bikes_df`

```python
# solution

import pandas as pd 

bikes_df = pd.read_csv("C:/Users/User/Downloads/bikes.csv")

bikes_df.head()

```

### Data Inspection and Cleaning
- **1. Check for Missing values**:

```python
# solution 

bikes_df.isna().any()
```


```python
# counting the number of missing values 

total_number_of_missing_values_by_collumn = bikes_df.isna().sum()

total_number_of_missing_values_by_collumn
```


```python
# visualizing the total number of misssing values

import matplotlib.pyplot as plt

# using a bar plot to visualize the missing values 

total_number_of_missing_values_by_collumn.plot(kind = "bar")

# to show the plot 

plt.show()

```

- **2.Handling Missing values**:

```python
# solution 

# bikes_df["ProductColor"].mode()

bikes_df = bikes_df.fillna("Black")

bikes_df
```


```python
# to verify that there are no more missing values on our dataset 

bikes_df.isna().any()
```

- **3. Check for  Duplicates**:

```python
# solution

# counting the total number of our datapoint 

len(bikes_df)
```

```python
bikes_cleaned_data_df = bikes_df.drop_duplicates()

bikes_cleaned_data_df
```

```python
# dropping any duplicates if any exists 

bikes_df.drop_duplicates(inplace = True)

```

- **4. Handling Duplicates**:

```python
# solution

# re-counting our data point again 
len(bikes_df)

# This shows that there was NO duplicates on our dataset
```

### Data Modification

```python
# generating some core metrics which were NOT provided from the dataset, which would be required for the purpose of the data analysis

# solution 

# (1) TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# (2) SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 


# (3) Profit : To be obtained by (SalesRevenue - TotalCostPrice)


bikes_df["Profit"] = bikes_df["SalesRevenue"]  - bikes_df["TotalCostPrice"]


# Displaying the result

bikes_df.head()

```

### Data Aggregation

```python
# Computing/ Aggregating the sales data to show Total Revenue by Customer , including their City, State and Country. 

# solution 
cols = ["CustomerName", "CustomerCity", 	"CustomerState", "CustomerCountry"]

# computing the total revenue by customers 

total_revenue_by_customer = bikes_df.groupby(["CustomerName", "CustomerCity", 	"CustomerState", "CustomerCountry"])["SalesRevenue"].sum().reset_index()

total_revenue_by_customer
```
### Data Sorting/ Data Ranking

```python
# To Determine the Most Importat Metric: Top 10 highest revenue-generating customers 

# solution 

the_top_10_customers = total_revenue_by_customer.sort_values("SalesRevenue", ascending = False).head(10)

the_top_10_customers
```

### Comparizon of the Total Revenue Generated by the Top -10 Customers to the Entire Total Revenue of the Company

```python
# The Total Revenue Generated by the Top -10 Customers

revenue_sum_of_top_10_customers  = the_top_10_customers["SalesRevenue"].sum().round(1)

revenue_sum_of_top_10_customers 
```


```python
# Entire Total Revenue of the Company

revenue_sum_of_the_entire_company = bikes_df["SalesRevenue"].sum().round(1)

revenue_sum_of_the_entire_company
```


```python
percentage_rev_top_10_customers = (revenue_sum_of_top_10_customers / revenue_sum_of_the_entire_company) * 100

ratio  = percentage_rev_top_10_customers.round(2)

ratio
```


```python
print(f"The Total Revenue generated by the top 10 Customers,  accounts for {ratio}% of the company's total revenue")
```

### Data Visualization

```python
#  To uncover the Top 10 highest revenue-generating customers in a pictorial form.

# solution 

import matplotlib.pyplot as plt

the_top_10_customers.plot(kind = "bar", x = "CustomerName",  y = "SalesRevenue", color = "blue")

# axis label 

plt.xlabel("Customer Names")
plt.ylabel("Total Revenue in US Dollars")


# title label 

plt.title("The Top 10 Customers by Total Revenue Since the Company started")

# to show the plot 

plt.show()

```

### Data Interpretation

The Result from the data visualization above shows that all the **Top 10 Customers** are all based in **France**

### Key Findings

---

1. **France Dominates among Top-Tier-High-Value-Customers**: 
   All **The Top 10 Customers** are based in **France**, indicating a strong customer base and market penetration in this region.


2. The Company's **Top 10 Customers** Contribute Less Than **1% of Total Revenue of the entire Company**.

   
   Despite **France** being the **top revenue generators**, these customers collectively account for a **very small fraction** of the company's overall sales — indicating **broad and diversified revenue streams**.

4. **Revenue is Distributed, Not Concentrated**
   Unlike typical e-commerce businesses that follow the Pareto Principle (80% of revenue from 20% of customers), this company’s revenue is **evenly spread across thousands of customers**, highlighting a mass-market model.


5. **High-Value Customers Are Geographically Clustered**
   The top revenue-generating customers are concentrated in specific cities and departments such as:

   * **Tremblay-en-France**, **Les Ulis**, and **Saint-Denis** in **Seine Saint Denis** and **Essonne**
   * Major urban centers like **Paris**, **Metz**, and **Dunkerque**

6. **Narrow Revenue Spread Among Top Customers**
   The revenue range of the top 10 customers is relatively narrow—from **\$13,144.88** to **\$13,708.12**, suggesting consistent purchasing behavior across the top customer tier.

7. **Top Customers Still Exhibit Stable Purchasing Behavior**
   While their individual contribution is small relative to total revenue, the top customers show **stable, high-value purchasing patterns** — useful for identifying ideal customer personas or retention targets.

8. **Customer Loyalty and Repeat Purchases Likely**
   Given the similar revenue volumes, it’s likely that these customers have regular or subscription-based purchasing behavior.

---

### Conclusions


