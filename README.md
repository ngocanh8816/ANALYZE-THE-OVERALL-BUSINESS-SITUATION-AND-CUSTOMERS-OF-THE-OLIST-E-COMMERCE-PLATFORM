# ANALYZE THE OVERALL BUSINESS SITUATION AND CUSTOMERS OF THE OLIST E-COMMERCE PLATFORM
Clarify the questions, issues encountered in business operations and conduct exploratory data analysis to help Olist better understand its e-commerce platform and optimize available growth opportunities.

# Overviews
The analysis project covers the following areas:

+ **Data collection**: Utilize the available data provided by the educational organization.
+ **Descriptive analytics**: Calculate the necessary metrics for the analysis.
+ **Diagnostic analytics**: Identify and analyze the root causes of issues found in past data.
+ **RFM analysis**: Divide customers into four main segments to understand their characteristics and behaviors.
+ **Churn analysis**: For retail services, segment customers into different groups based on churn duration.
+ **Clarify business issues**: Summarize the metrics that help understand customer profiles and the overall business situation.

# Applied Skills
Basic EDA Data, Data Analysis, Data Visualization (using Python)

# Key Features
+ **Transform data**: Calculate the necessary indices for customer classification, indices on customer behavior and characteristics, churn rate, business situation indices, etc.
+ **Data analysis**: Explore customer shopping behavior, business performance results, and investigate the causes of past occurrences.
+ **Data visualization**: Use two visualization libraries, Matplotlib and Seaborn, in Python to represent and extract useful information from the data.

# Key Findings
**Customer-related aspects**

+ Customers are segmented into four main groups (High Customer, Potential Customer, Customer Requiring Attention, Low Customer) based on their purchase frequency, the most recent purchase time, and transaction value
+ Generally, the majority of the company’s customers have relatively high transaction values and repeat purchase frequencies. However, they need more attention and engagement to shorten the time since their last purchase.
+ Regarding the average rating that each customer segment gives to Olist when they experience using the shopping service, they are all at a fairly similar level.
+ For the High Customer segment, they have an average spending of about $14,681 from 09/2016 to 10/2018. Customers in this segment of Olist are distributed across 5 main cities. However, the majority, accounting for over 50% of this customer base, comes from the city of Sao Paulo.

**The churn rate of each customer segment for the shopping service**

+ If customers do not make a purchase for more than 2 months, there is a possibility that these customers will churn.
+ Overall, the number of churned customers is quite high. In addition to the High and Requiring Attention customer segments that have churned consecutively over the past 2 months, there are also many customers in the Potential and Low customer segments who have churned in the long term.
+ The number of customers likely to churn in the long term fluctuates around 8,098 people.
+ Generally, the characteristics of customers with a high likelihood of churning show that they tend to gradually decrease their purchase frequency. The final transaction values for churned customers in the High and Requiring Attention segments are 33,943,537 and 99,526,365 respectively. This indicates that before churning in the long term, customers have a relatively high level of spending.

**Aspects of business operations**

*Data exploration*
+ Overall, the business situation in the first 3 quarters of 2018 was stable and at a higher level compared to the same period in 2017. On the other hand, most of the revenue recorded in the first 3 quarters of 2018 tends to be concentrated on the right side of the average value (usually smaller than the average value).
+ The revenue data in 2017 has a higher spread, indicating that business activities experienced fluctuations (in this case, rapid growth).

*Assessment of business performance results*
+ Both revenue and number of orders have shown significant increases since the period when business activities began to be recorded.
+ However, in the last two months of the period (September 2018 and October 2018), the report shows a very large decline in these two indicators. To investigate the cause, we examine the correlation between revenue and the number of customers purchasing within the month.
+ We observe a positive correlation between the number of customers who made purchases and the recorded revenue. In reality, it is possible that customers did not continue using the purchasing service, which could also be the reason for the significant decline in Olist’s revenue during the last two months of the business period (September 2018 and October 2018).

*Product aspects*
+ We focus on the Top 10 categories that include products sold in large quantities and record outstanding revenue. Categories such as household items and personal care products have significant sales volumes and correspondingly high revenue.

*Average order value by product*
+ The following are the Top 10 product categories that customers spent the most on throughout the company’s business period: technology devices, utilities, household items, musical instruments, furniture, etc.
+ The company should leverage and invest more resources in developing sellers, applying upselling strategies, or quantity discount programs for these key product categories.

*Average order value by payment type*
+ From this, we know which payment methods customers prefer when making purchases at Olist. Boleto and Credit Card are the two most commonly used payment methods. However, the average order value for Credit Card transactions is higher, indicating that customers using credit cards tend to make higher-value purchases (spend more money).

# Example Code
```
# Merge 2 bảng df_order và df_order_payment để tính các chỉ số RFM
df_join = pd.merge(df_order, df_order_payment, how='inner',on='order_id')[['order_id','customer_id','order_purchase_timestamp','payment_value','order_approved_at','order_delivered_customer_date']]

# Tính RFM
current_date = df_join['order_purchase_timestamp'].max()
## Tính Recency, Frequency, Monetary với mỗi customer_id
rfm_df = df_join.groupby('customer_id').agg({
    'order_purchase_timestamp': lambda x: (current_date - pd.to_datetime(x).max()).days, # Recency
    'order_id': 'nunique',  # Frequency
    'payment_value': 'sum'  # Monetary
}).reset_index()
rfm_df.columns = ['customer_id', 'Recency', 'Frequency', 'Monetary']

## Sắp xếp thứ tự cho 3 cột Recency, Frequency, Monetary
rfm_df['R_rank'] = rfm_df['Recency'].rank(pct=True)
rfm_df['F_rank'] = rfm_df['Frequency'].rank(pct=True)
rfm_df['M_rank'] = rfm_df['Monetary'].rank(pct=True)
```
# Project Structure
+ `README.md`: This file provides information and an overview of the analysis.
+ `Analyze The Overall Business Situation and Customers of The OLIST E-Commerce Platform`: The Google Colab file contains code for processing, transforming, and retrieving data.
