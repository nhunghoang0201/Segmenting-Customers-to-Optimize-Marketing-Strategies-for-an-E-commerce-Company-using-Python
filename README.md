# Segmenting Customers to Optimize Marketing Strategies for an E-commerce Company using Python & RFM model
![Image](https://github.com/user-attachments/assets/3abaca16-da25-4a78-864d-194928d9c1f6)

- Author: Hoang Thi Hong Nhung 

- Date: 2025-09-03

- Tools Used: Python

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

## 📌 1. Background & Overview 
#### 1.1. Situation
SuperStore is a global retail company with a massive customer base. As the Christmas and New Year holidays approach, the Marketing department wants to launch appreciation campaigns to recognize and retain loyal customers while also converting high-potential customers into loyal ones. Given the large dataset, manual segmentation is no longer feasible. Therefore, a data-driven approach using the RFM model is employed to identify valuable customer segments.

#### 1.2. Complication
- The exponential growth in the volume of customer data has made manual segmentation using Excel no longer feasible. The company requires a systematic, data-driven approach to effectively segment customers
- How to design loyalty and appreciation campaigns that boost revenue and retain high-value customers.
- How to turn promising customers into loyal and profitable customers 

#### 1.3. Question
This analysis was conducted to answer two core business questions:
- How can we build the most effective customer appreciation campaign to maximize revenue during the Christmas and New Year season?
- What is the optimal strategy to convert "Promising" customers into "Loyal" customers?

#### 1.4. Target Audience
Strategy & marketing teams

## 📂 2. Dataset Description & Data Structure  
#### Table Name: Ecommerce retail

#### Table description
| Field       | Type    | Definition                                                                                      | Example                            |
| ----------- | ------- | ----------------------------------------------------------------------------------------------- | ---------------------------------- |
| InvoiceNo   | object  | Invoice number. A 6-digit unique ID for each transaction. If it starts with 'C' → cancellation. | 536365                             |
| StockCode   | object  | Product (item) code. Unique 5-digit code for each product.                                      | 85123A                             |
| Description | object  | Product (item) name.                                                                            | WHITE HANGING HEART T-LIGHT HOLDER |
| Quantity    | int64   | Quantity of each product (item) per transaction.                                                | 6                                  |
| InvoiceDate | object  | Timestamp of when each transaction was generated.                                               | 2010-12-01 08:26:00                |
| UnitPrice   | float64 | Product price per unit (GBP).                                                                   | 2.55                               |
| CustomerID  | float64 | Unique 5-digit identifier for each customer.                                                    | 17850.0                            |
| Country     | object  | Country name where the customer resides.                                                        | United Kingdom                     |

#### Data Snapshot
| Column Name | Data Type | Description                                                       | Example                            |
| ----------- | --------- | ----------------------------------------------------------------- | ---------------------------------- |
| InvoiceNo   | object    | Invoice number (6-digit unique). Starts with 'C' if cancellation. | 536365                             |
| StockCode   | object    | Unique product/item code.                                         | 85123A                             |
| Description | object    | Product/item description.                                         | WHITE HANGING HEART T-LIGHT HOLDER |
| Quantity    | int64     | Quantity purchased per transaction.                               | 6                                  |
| InvoiceDate | datetime  | Date & time of transaction.                                       | 2010-12-01 08:26:00                |
| UnitPrice   | float64   | Price per unit (£).                                               | 2.55                               |
| CustomerID  | float64   | Unique customer ID (5-digit).                                     | 17850.0                            |
| Country     | object    | Country of customer.                                              | United Kingdom                     |


## 3. RFM Model:
#### 3.1. RFM introduction 
RFM stands for Recency, frequency, and Monetary. RFM segmentation is a scoring technique used to better quantify customer behavior. The RFM model evaluates customer value based on:
- Recency (R): How recently a customer has purchased.
- Frequency (F): How often a customer purchases.
- Monetary (M): How much money a customer spends

#### 3.2. RFM scoring
- To standardize and segment customers, I applied **quantile-based binning (quintiles)**.

*Quantile-based binning (quintiles) splits data into 5 equal groups (20% each), ranking values from lowest (group 1) to highest (group 5).*
  
- The logic:

  - Recency: recent buyers get higher scores (5 = very recent, 1 = very old).

  - Frequency & Monetary: higher frequency/spending get higher scores (5 = highest, 1 = lowest).

- Scoring RFM:
  
| Score | Recency (days since last purchase) | Frequency (number of purchases) | Monetary (total spending, £) |
|-------|----------------|------------------------|----------------|
| **5** | 0–13           | ≥ 210                  | ≥ 2057         |
| **4** | 14–32          | 7–209                  | 942–2056       |
| **3** | 33–71          | 3–6                    | 490–941        |
| **2** | 72–179         | 2                      | 250–489        |
| **1** | 180–373        | 1                      | < 250          |

- RFM value is obtained by concatenating the scores of R, F, and M (e.g., Recency=5, Frequency=4, Monetary=5 → RFM value = 545).
  
#### 3.3. Customer Segmentation with RFM
| Segment             | RFM Values                                                                                             | Behavior                                                 | Marketing Strategy                                       |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| **Champions**       | 555, 455                                                                                                          | Bought recently, buy often, spend the most.              | Best customers – reward them, upsell, ask for referrals. |
| **Loyal Customers** | 554, 553, 454, 453, 355, 354, 353                                                                                 | Frequent buyers, strong relationship, spend medium-high. | Build loyalty programs, exclusive offers.                |
| **Big Spenders**    | 545, 535, 525, 515, 435, 425, 415, 345, 335, 325, 315, 524, 523, 514, 513, 424, 423, 414, 413, 324, 323, 314, 313 | High spenders but not frequent/recent.                   | Focus on retention, offer bundles or premium products.   |
| **Promising**       | 544, 543, 534, 533, 444, 443, 434, 433, 344, 343, 334, 333                                                        | Recent buyers, medium spend & frequency.                 | Nurture them with targeted campaigns.                    |
| **New Customers**   | 522, 521, 512, 511, 422, 421, 412, 411                                                                            | Just purchased, low frequency & spend.                   | Welcome campaigns, education, build trust.               |
| **Need Attention**  | 552, 551, 542, 541, 532, 531, 452, 451, 442, 441, 432, 431, 352, 351, 342, 341, 332, 331, 322, 321, 312, 311      | Recent or frequent, but low spending.                    | Encourage more spending via cross-sell & upsell.         |
| **Sleepers**        | 255, 254, 253, …, 115, 114, 113                                                                                   | Not recent, used to buy more, spending varies.           | Re-engagement campaigns, discounts.                      |
| **Lost**            | 222, 221, 212, 211, 122, 121, 112, 111                                                                            | Haven’t bought in long time, very low activity & spend.  | Win-back campaigns or stop investing.                    |

## ⚒️ 4. Main Process
#### 1️⃣ 4.1. EDA & Data Cleaning

| Findings                                         | Solution                                                                 | Result / Data Readiness                                                                 |
|--------------------------------------------------|--------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Wrong data type: Column `CustomerID` is float64   | Convert to String                                                        | ✅ Converted successfully → IDs are consistent                                          |
| Null values: Column `CustomerID` has 135,080 null values (~25% of dataset) | - Drop rows with `CustomerID` is null <br> - Fill missing `CustomerID` using same `InvoiceNo` | ✅ Dataset reduced from **541,909 → 406,829 rows** (≈75% retained)                       |
| Abnormal values: `InvoiceNo` starting with `C` = Cancellation transactions | Drop rows with `InvoiceNo` starting with `C`                             | ✅ **9,288 rows removed** (≈2.3% of dataset)                                             |

📌 **Final dataset after cleaning**: **397,129 transactions, 4,372 unique customers** → ✔️ ready for RFM modeling.    

#### 2️⃣ 4.2 RFM Metrics & Scores Calculation
#### Creating Recency, Frequency and Monetary
- From the `ecom_transactions` dataset, transactions are **aggregated per CustomerID**.  
- The new table `RFM_dataset` is created with 3 main metrics:  
  - **Recency (R):** Days since the last purchase.  
  - **Frequency (F):** Total number of transactions.  
  - **Monetary (M):** Total spending amount.

<img width="918" height="677" alt="image" src="https://github.com/user-attachments/assets/0659c4a3-ca0a-4fbd-b4ea-cec2b6af0af3" />

<img width="918" height="677" alt="image" src="https://github.com/user-attachments/assets/ac879d4b-2b7e-482a-9f1d-f3c610a84cb5" />

<img width="1030" height="622" alt="image" src="https://github.com/user-attachments/assets/3b84b682-345d-4b9e-8d28-ed82506c94f2" />

#### Scoring RFM
- After calculating **R, F, and M**, scores are assigned based on **quantile-based binning (quintiles)**.  
- Data is split into **5 equal groups (20% each)**, and assigned scores from **1 → 5**:  
  - **1 = lowest values**, **5 = highest values** for Monetary and Frequency
  - **1 = oldest purchase**, **5 = most recent purchase** for Recency
- The three scores are concatenated into the **RFM_Score** column (e.g., R=5, F=4, M=2 → RFM_Score = 542).
  
<img width="724" height="580" alt="image" src="https://github.com/user-attachments/assets/6d5782f7-7ab7-479c-87d5-7a3fe52cf3b5" />

<img width="1274" height="699" alt="image" src="https://github.com/user-attachments/assets/8a93b44f-7124-4423-bd42-ae1c01fdceca" />

<img width="1113" height="562" alt="image" src="https://github.com/user-attachments/assets/82f1315b-645a-4de4-915f-33d990aa4503" />


#### Customer Segmentation based on RFM model
- Using the **RFM_Score**, customers are segmented into groups for business insights.  

<img width="1104" height="748" alt="image" src="https://github.com/user-attachments/assets/c690a5e6-676a-472e-a335-e8f334f61077" />

<img width="1265" height="501" alt="image" src="https://github.com/user-attachments/assets/d9080f7b-b8e5-4f28-bfa6-306708dacbb8" />

<img width="805" height="397" alt="image" src="https://github.com/user-attachments/assets/21a5bce3-0a0f-4644-afd5-be4e411a3e45" />

#### 3️⃣ 4.3. Visualization
#### Compare different numbers of customers and revenue in different segments from 2010 to 2011

**Insight**: From 2010 to 2011, Top 3 most crowded customer groups include Sleepers, Lost, Promissing while  Top 3 customer groups with highest revenue include Champions, Big spenders, Sleepers => Champion & Big spender customers take up a small number of customers but contribute the most to the revenue.

<img width="1000" height="289" alt="image" src="https://github.com/user-attachments/assets/cc80b56a-a4ef-408a-8b03-853db801caea" />

<img width="834" height="504" alt="image" src="https://github.com/user-attachments/assets/2b1dcb9e-a5ad-4632-9eb9-5347c7080dcf" />

#### Compare revenue in different segments at end of the year in 2010 and 2011
**Insight**: At the end of 2010 and 2011, Champions and Big Spenders—though few in number—contributed the most revenue, while Promising customers showed strong potential for future growth.

<img width="1000" height="289" alt="image" src="https://github.com/user-attachments/assets/cc80b56a-a4ef-408a-8b03-853db801caea" />

<img width="1008" height="599" alt="image" src="https://github.com/user-attachments/assets/d0f4f6c1-b318-493e-abd4-02c52fa0f19f" />


#### Compare the quantity of customers in different segmentations and countries
**Insight**: Over 90% of SuperStore’s customers come from the UK, with Sleepers and Promising segments forming the majority—highlighting both a strategic market and untapped growth potential.
<img width="1478" height="490" alt="image" src="https://github.com/user-attachments/assets/36e264de-6edb-4339-83f4-27bde80b671f" />

#### Compare revenue in date of the end of 2010 and 2011
**Insight**: Revenue surges from the beginning of October to mid-December, confirming this as the golden period for launching sales-driving campaigns
<img width="979" height="1990" alt="image" src="https://github.com/user-attachments/assets/6d3a0d20-ce2b-4495-994d-8d72676fdacf" />

###### Top 3 products with highest revenue in each segmentation in the end of 2010 and 2011
**Insight**: Top 3 products with having highest revenue in important customer segmentation
  
  - Champion customer: REGENCY CAKESTAND 3 TIER, RABBIT NIGHT LIGHT, and PAPER CHAIN KIT 50'S CHRISTMAS.
  
  - Big spender customer: PAPER CRAFT LITTLE BIRDIE, Manual and POSTAGE.
  
  - Promissing customer: JUMBO BAG RED RETROSPOT, RABBIT NIGHT LIGHT, and PAPER CHAIN KIT 50'S CHRISTMAS.

  - Sleepers: WHITE HANGING HEART T-LIGHT HOLDER, RED HARMONICA IN BOX, and ROUND SNACK BOXES SET OF 4 FRUITS
    
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/4ea71a4d-3cb7-47a2-aa90-c858770fa351" />

###### Average value per order
**Insight**: Big Spenders, Sleepers, and Champions deliver the highest average order values at £1,062, £587, and £528, respectively

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/34ea2b6c-c444-4070-9775-3161313dc83b" />

## 🔎 5. Final Conclusion & Recommendations  
#### Objective 1: Customer Appreciation and ROI Maximization
##### General Recommendations:

- Focus on 4 Strategic Segments: Campaigns should prioritize resources for four groups: Champions, Big Spenders, Promising, and Sleepers, as they contribute the most revenue.

- Prioritize the UK Market: Implement robust and in-depth campaigns in the United Kingdom.

- The campaign should be launched in early October and mid December.

- Detailed Recommendations per Segment:
##### Tailored Campaigns for key Customer Segment  

| Segment    | Objective                          | Campaign                                                                 | Expected Impact                                      |
|------------|------------------------------------|--------------------------------------------------------------------------|------------------------------------------------------|
| 🏆 Champions | Retain & reward loyalty            | VIP appreciation program during Christmas & New Year: exclusive gifts, early access to holiday collections, personalized thank-you notes | Strengthen retention, maximize lifetime value         |
| 💎 Big Spenders | Boost purchase frequency          | Time-limited vouchers, free shipping, or luxury bundles on next high-value purchase | Encourage repeat purchases, lift avg. revenue/customer |
| 🌱 Promising  | Convert into Champions / Big Spenders | Cross-sell & upsell on favorite products (e.g., JUMBO BAG RED RETROSPOT, RABBIT NIGHT LIGHT) + loyalty points & tiered benefits | Increase order value & frequency; move into high-value segments |
| 😴 Sleepers   | Reactivate & improve recency       | “We Miss You!” reactivation campaign with special discounts, vouchers, or gifts | Bring inactive customers back, reduce churn           |



#### Objective 2: Turning Promising Customers into Potential High-Value Segments

### 🎯 Campaign Playbook: Converting Promising Customers into High-Value Segments

### 🎯 Campaign Playbook: Upgrading Promising Customers

| Goal | Action | Example |
|------|---------|---------|
| **Increase Frequency** | Offer repeat-purchase incentives (discounts, loyalty fast-track, gamified challenges) | "Get £10 off your next order this week" / "Earn double points on next 2 orders" |
| **Increase Monetary Value** | Encourage larger baskets through bundling, upselling, and free-shipping thresholds | "Free shipping on orders over £60" / "Bundle Rabbit Night Light + Paper Chain Kit and save 15%" |
| **Enhance Recency** | personalized recommendations, VIP perks, and referral rewards based on recent purchase | "Enjoy free next-day delivery this weekend – VIP for a day!" / "Give £5, Get £5 when you share with friends" |

📌 **Key Transition Path**:  
- **Promising → Big Spender**: focus on **Monetary growth** via bundles, upselling, higher basket size.  
- **Promising → Champion**: focus on **Frequency & Loyalty** via fast-track programs, streak rewards, and seasonal exclusives.  








