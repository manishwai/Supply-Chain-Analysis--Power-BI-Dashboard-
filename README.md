# Supply-Chain-Analysis--Power-BI-Dashboard-
# Supply-Chain-Analysis

## Background

- **Company:** AtliQ Mart
- **Industry:** FMCG Manufacturing
- **Headquarters:** Gujarat, India
- **Current Operations:** Surat, Ahmedabad, Vadodara
- **Expansion Plan:** To enter other metro/tier-1 cities within the next 2 years.

## Problem Statement

AtliQ Mart is facing a challenge where several key customers did not renew their annual contracts due to service issues. The suspected problems include:

- Essential products either not delivered on time or not delivered in full over a sustained period.
- Resulting in poor customer service and dissatisfaction.

**Objective:** The management seeks to address these issues before expanding to new cities. They have requested the supply chain analytics team to:

- Track ‘On-Time’ and ‘In-Full’ delivery service levels for all customers on a daily basis.
- Use these metrics to swiftly respond to service issues.

## Key Performance Indicators (KPIs)

The supply chain team will measure the following KPIs to evaluate service levels:

1. **On-Time Delivery (OT) %**
   - Percentage of orders delivered on or before the promised date.
   
2. **In-Full Delivery (IF) %**
   - Percentage of orders delivered with all items as per the order specifications.
   
3. **On-Time In-Full (OTIF) %**
   - Percentage of orders delivered on time and in full, combining both OT and IF metrics.

**Target:** Each customer has a set target service level for these KPIs, which will be monitored daily to ensure compliance.

## Goals

- **Identify:** Track and identify any deviations from the target service levels.
- **Address:** Implement corrective actions to resolve service issues and improve customer satisfaction.
- **Prepare:** Ensure the supply chain is robust and reliable before expanding to new markets.

## Next Steps

1. **Data Collection:** Gather and maintain daily records of delivery performance.
2. **Analysis:** Continuously analyze OT, IF, and OTIF metrics.
3. **Reporting:** Develop regular reports and dashboards to monitor service levels.
4. **Action:** Address any identified issues promptly to enhance service quality.

## Data Overview

The following datasets are utilized in the supply chain analysis:

1. **dim_customers.csv**
2. **dim_products.csv**
3. **dim_date**
4. **dim_targets_orders**
5. **fact_order_lines.csv**
6. **fact_orders_aggregate.csv**

---

### Column Descriptions

#### **dim_customers.csv**
This table contains information about customers.

- **customer_id:** Unique ID assigned to each customer.
- **customer_name:** Name of the customer.
- **city:** City where the customer is located.

---

#### **dim_products.csv**
This table contains information about the products.

- **product_id:** Unique ID assigned to each product.
- **product_name:** Name of the product.
- **category:** Category to which the product belongs.

---

#### **dim_date**
This table contains date information at various levels.

- **date:** Specific date (daily level).
- **mmm_yy:** Date formatted at the monthly level.
- **week_no:** Week number of the year corresponding to the date.

---

#### **dim_targets_orders**
This table contains target data for customer orders.

- **customer_id:** Unique ID assigned to each customer.
- **ontime_target %:** Target percentage for on-time delivery for a given customer.
- **infull_target %:** Target percentage for full delivery for a given customer.
- **otif_target %:** Target percentage for on-time in-full delivery for a given customer.

---

#### **fact_order_lines.csv**
This table provides detailed information about individual order lines.

- **order_id:** Unique ID for each customer order.
- **order_placement_date:** Date when the order was placed.
- **customer_id:** Unique ID assigned to each customer.
- **product_id:** Unique ID assigned to each product.
- **order_qty:** Quantity of products requested for delivery.
- **agreed_delivery_date:** Date agreed upon for delivery between the customer and AtliQ Mart.
- **actual_delivery_date:** Actual date when the product was delivered to the customer.
- **delivered_qty:** Quantity of products actually delivered.

---

#### **fact_orders_aggregate.csv**
This table contains aggregated information on delivery performance at the order level per customer.

- **order_id:** Unique ID for each customer order.
- **customer_id:** Unique ID assigned to each customer.
- **order_placement_date:** Date when the order was placed.
- **on_time:** '1' if the order was delivered on time; '0' if not.
- **in_full:** '1' if the order was delivered in full quantity; '0' if not.
- **otif:** '1' if the order was delivered both on time and in full quantity; '0' if not.



Data Model 
![image](https://github.com/user-attachments/assets/94ef2a77-860e-429e-9ee9-96b97ce034ef)

## Metrics

### Order Lines and Fill Rates

- **Total Order Lines:** 
  - **Definition:** Count of all order lines recorded in the `fact_order_lines` table.
  - **Calculation:** Total number of individual items requested by customers.

- **Line Fill Rate:** 
  - **Definition:** Measures the proportion of order lines that were shipped in full quantity compared to the total number of order lines.
  - **Calculation:** 
    \[
    \text{Line Fill Rate} = \frac{\text{Number of Order Lines Shipped In Full Quantity}}{\text{Total Order Lines}}
    \]

- **Volume Fill Rate:** 
  - **Definition:** Measures the proportion of the total quantity shipped compared to the total quantity ordered.
  - **Calculation:** 
    \[
    \text{Volume Fill Rate} = \frac{\text{Total Quantity Shipped}}{\text{Total Quantity Ordered}}
    \]

### Orders and Delivery Performance

- **Total Orders:** 
  - **Definition:** Total number of unique orders recorded in the `fact_orders_aggregate` table.
  
- **On Time Delivery %:** 
  - **Definition:** Percentage of orders delivered on time relative to the total number of orders.
  - **Calculation:** 
    \[
    \text{On Time Delivery \%} = \frac{\text{Number of Orders Delivered On Time}}{\text{Total Number of Orders}} \times 100
    \]

- **In Full Delivery %:** 
  - **Definition:** Percentage of orders delivered in full quantity relative to the total number of orders.
  - **Calculation:** 
    \[
    \text{In Full Delivery \%} = \frac{\text{Number of Orders Delivered In Full Quantity}}{\text{Total Number of Orders}} \times 100
    \]

- **On Time In Full %:** 
  - **Definition:** Percentage of orders delivered both on time and in full quantity relative to the total number of orders.
  - **Calculation:** 
    \[
    \text{On Time In Full \%} = \frac{\text{Number of Orders Delivered Both On Time and In Full}}{\text{Total Number of Orders}} \times 100
    \]

### Target Metrics

- **On Time Target:** 
  - **Definition:** The average target set for on-time delivery performance across all customers.
  - **Calculation:** Average of the on-time delivery targets from `dim_targets_orders`.

- **In Full Target:** 
  - **Definition:** The average target set for delivery in full quantity across all customers.
  - **Calculation:** Average of the in-full delivery targets from `dim_targets_orders`.

- **On Time In Full Target:** 
  - **Definition:** The average target set for on-time in full delivery performance across all customers.
  - **Calculation:** Average of the OTIF targets from `dim_targets_orders`.

---

This section clearly defines each metric, how it's calculated, and its purpose in the supply chain analysis.
![image](https://github.com/user-attachments/assets/82a76430-672a-4853-bd2b-aa219cc478b9)

## Business Understanding

### Orders and Lines

- **Orders:** An order represents a unique request placed by a customer on a specific date. Each order can include one or more items.
- **Order Lines:** Within an order, each item requested is considered an order line. For example, if a customer orders 4 notebooks and 2 pens, a single order ID is generated for this request. Each item (notebook and pen) represents a separate order line.

    **Example:** 
    If you order 4 notebooks and 2 pens from Amazon, the order ID encompasses all these items. The notebook and pen are considered separate order lines.

### Measuring Line Fill Rate & Volume Fill Rate

- **Line Fill Rate:** This metric helps the supply planning team understand the proportion of order lines that were shipped out of the total lines ordered. It does not take into account the delivery time of the order.

    **Calculation:**
    \[
    \text{Line Fill Rate} = \frac{\text{Order Lines Fulfilled}}{\text{Total Order Lines Ordered}}
    \]
    **Example:** 
    If Amazon shipped 1 pen out of the 2 pens you ordered, the line fill rate would be:
    \[
    \text{Line Fill Rate} = \frac{1}{2} = 50\%
    \]

- **Volume Fill Rate (Case Fill Rate):** This metric indicates the proportion of the total quantity shipped relative to the total quantity ordered. It is useful for understanding how much of the requested quantity was actually delivered.

    **Calculation:**
    \[
    \text{Volume Fill Rate} = \frac{\text{Total Quantity Shipped}}{\text{Total Quantity Ordered}}
    \]
    **Example:** 
    If Amazon shipped 4 notebooks and 1 pen out of the 4 notebooks and 2 pens you ordered, the volume fill rate would be:
    \[
    \text{Volume Fill Rate} = \frac{5}{6} \approx 83\%
    \]

---

This section provides a clear explanation of the concepts related to orders and order lines, as well as how to measure and interpret the Line Fill Rate and Volume Fill Rate.

# Dashboard Overview 

The dashboard provides comprehensive insights into supply chain performance, with a focus on key metrics and analysis across different dimensions:

- **City Analysis**: Overview of product and consumer insights based on KPI performance.
- **Monthly KPI Analysis**: Visualization of KPI trends over time with an interactive KPI Switch Chart button.
- **Quantity Analysis**: Examination of ordered vs. delivered quantities, categorized by product, city, and category.
- **Delivery Delay Analysis**: Assessment of average delivery delays and their impact on overall performance.

## City, Product, & Customer Analysis (KPI)

![City, Product & Customer Analysis](https://i.imgur.com/5JAcV61.gif)

### KPI Metrics
- **In Full Delivery**: 52.78% (Target: 76.5%)
- **On Time Delivery**: 59.03% (Target: 86.1%)
- **On Time In Full Delivery**: 29.02% (Target: 65/91%)
- **Line Fill Rate**: 65.96%
- **Volume Order Fill Rate**: 96.5%

**Key Insights:**
- All key metrics (OT%, IF%, OTIF%) are significantly below target levels across cities. The Vadodara location is notably underperforming compared to the overall average.
- **Vadodara On Time Delivery %**: 36% below target and 29% below the overall average.
- **Vadodara In Full Delivery %**: 24% below target and below the overall average of 52%.
- **Average Delivery Delay**: Orders are delayed by an average of 1.69 days.

## Monthly KPI Analysis 

![Monthly KPI Analysis](https://i.imgur.com/FeEAllE.gif)

**Observations:**
- **MAY'22 and AUG'22** show slight improvements in IF% and OTIF%, but these remain well below target levels.
- **Daily OT% Trends**: Daily OT% figures are consistently lower than targeted levels.
- **Overall Performance**: Only 59.03% of orders are delivered on time. Daily trends for IF% and OTIF% consistently fail to meet target levels, with OTIF% showing particularly poor performance.

## Quantity Ordered & Delivered Analysis

![Quantity Ordered & Delivered Analysis](https://i.imgur.com/4O4Ujo1.gif)

**Insights:**
- A total of 458K units were not delivered, indicating issues with stock management and demand forecasting.
- **Dairy Products**: Leading category with significant delivery shortfalls, including Milk, Curd, and Butter.
- **City-Level Analysis**: All cities experience similar issues, with Vadodara being the most impacted.

## Average Delivery Delay Rate Analysis

![Average Delivery Delay Rate Analysis](https://i.imgur.com/LwyWgU3.gif)

**Findings:**
- **13000 Orders** were delivered late, averaging a delay of 1.69 days from the agreed delivery date.
- **Dairy Products** contribute significantly to average delays, particularly Ghee, Curd, and Butter.
 Stores with highest ADDR: Lotus Mart, Coolblue, and Acclaimed stores have the highest number of delayed orders.




KPI CITY ANALYSIS 
![image](https://github.com/user-attachments/assets/6a856ae2-d111-4a88-a21f-d9b55a126c55) 

![image](https://github.com/user-attachments/assets/04f4e15e-e5a9-44ce-9e00-9d533ffb9617) 

![image](https://github.com/user-attachments/assets/9e9ebedf-c96f-4918-9c7b-164de5248986)

![image](https://github.com/user-attachments/assets/5ccc39a4-1341-4926-b890-006609ddb8a8) 

![image](https://github.com/user-attachments/assets/f8c98e89-b602-481d-b571-4bff1d4752eb) 

![image](https://github.com/user-attachments/assets/8a60b182-b283-452d-a673-0a7683d94c70)

KPI MONTHLY ANALYSIS 

![image](https://github.com/user-attachments/assets/7f05a964-8572-4125-a08a-519ebffbe4f7) 
![image](https://github.com/user-attachments/assets/e986dc31-5af0-4f65-823c-9d85edf0de15)

![image](https://github.com/user-attachments/assets/3eadaf75-ac41-460f-923b-17e751e15d00) 
![image](https://github.com/user-attachments/assets/cb2a2e3c-86d4-4cea-b257-a53a1e95919d)

![image](https://github.com/user-attachments/assets/b9b599cb-8977-4a8b-adcb-ac0ddfb6061a) 
![image](https://github.com/user-attachments/assets/1779010a-1163-4891-934d-522ad8d8079b)


DELAYED PRODUCT ANALYSIS 

![image](https://github.com/user-attachments/assets/340bd47e-1541-42e8-97eb-26116f976f48)

![image](https://github.com/user-attachments/assets/c3cfb7ee-7757-4b85-a4ab-a6c26bdbecc8)

![image](https://github.com/user-attachments/assets/01acb140-5fdb-4377-925a-6c740ee8a066)



QUANTITY ORDER NOT DELIVERED ANALYSIS 

![image](https://github.com/user-attachments/assets/4200b866-9b5d-4ff9-92b1-71baedffa0c8)
![image](https://github.com/user-attachments/assets/be5e2770-ef04-40d1-a671-bf5d21441f8b)
![image](https://github.com/user-attachments/assets/dd8e85b2-0a4b-4920-b0a5-cff6f062c6ac)






