# Segmenting Customers to Optimize Marketing Strategies for an E-commerce Company using Python & RFM model
![Image](https://github.com/user-attachments/assets/3abaca16-da25-4a78-864d-194928d9c1f6)

## 📊 Project Title: [Your Project Name]  
Author: Hoang Thi Hong Nhung 
Date: 2025-09-03 
Tools Used: Python

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

#### 3.2. Customer Segmentation & Scoring Criteria
| Segment             | RFM Values (examples)                                                                                             | Behavior                                                 | Marketing Strategy                                       |
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
| Issue              | Findings                                     | Solution                                                                 |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------|
| Data type          | Column `CustomerID` is float64               | Change to String                                                         |
| Check Null value   | Column `CustomerID` has 135080 null values   | - Delete rows with `CustomerID` is null <br> - Fill `CustomerID` by using same `InvoiceNo` |
| Check Abnormal value | `InvoiceNo` starting with `C` = Cancellation transactions | Drop rows with `InvoiceNo` starting with `C` |

#### 2️⃣ 4.2 RFM Metrics & Scores Calculation
#### 3️⃣ 4.3. RFM Metrics & Scores Calculation
###### Creating Recency, Frequency and Monetary
<img width="1236" height="609" alt="image" src="https://github.com/user-attachments/assets/fae12e10-a4da-45f6-9c0a-ec1ffaa1f502" />
<img width="957" height="542" alt="image" src="https://github.com/user-attachments/assets/27fd7e5f-f35e-4526-8e90-3a0f18701598" />
<img width="1145" height="550" alt="image" src="https://github.com/user-attachments/assets/e7a1bd79-b040-47be-9f64-1c4fd633cc81" />
<img width="1143" height="530" alt="image" src="https://github.com/user-attachments/assets/170c6228-5340-413d-920c-e007de3076c9" />
<img width="1284" height="585" alt="image" src="https://github.com/user-attachments/assets/d38ffc1f-e18b-427f-82a7-82d9a0d7b3fc" />
<img width="1448" height="508" alt="image" src="https://github.com/user-attachments/assets/9d914a29-38b2-4781-9b4c-dc798e4b3495" />

###### Customer Segmentation based on RFM model
<img width="1363" height="791" alt="image" src="https://github.com/user-attachments/assets/092d2d67-8b4a-4dc1-b8de-e1388494682c" />


#### 3️⃣ 4.4. Visualization
###### Compare different number of customers in different segmentation
<img width="1191" height="617" alt="image" src="https://github.com/user-attachments/assets/40942f4f-d8a5-41b8-b3bc-9327e92a802c" />

###### Compare revenue in different segmentation
<img width="1226" height="797" alt="image" src="https://github.com/user-attachments/assets/34e8c95d-f318-4fe6-b8f5-dc7ace22ad55" />
<img width="1186" height="797" alt="image" src="https://github.com/user-attachments/assets/971f36fc-1e79-418c-9a4a-75f65c4a03c6" />

###### Compare quantity of customer in different segmentation and countries
<img width="1413" height="270" alt="image" src="https://github.com/user-attachments/assets/db697f8b-9675-4a32-b03b-ba90d24d8644" />
<img width="1802" height="989" alt="image" src="https://github.com/user-attachments/assets/826254e9-6cc0-445c-a979-90e38a8a3293" />

###### Compare revenue in date of the end of 2010 and 2011
<img width="1450" height="332" alt="image" src="https://github.com/user-attachments/assets/8a98fdee-ad42-4492-aaa3-5fb005ad1f7e" />
<img width="979" height="1990" alt="image" src="https://github.com/user-attachments/assets/6d3a0d20-ce2b-4495-994d-8d72676fdacf" />

###### Top 3 products with highest revenue in each segmentation
<img width="1402" height="211" alt="image" src="https://github.com/user-attachments/assets/2b1d446f-5b09-4338-bd96-ec676ac40146" />
<img width="1256" height="739" alt="image" src="https://github.com/user-attachments/assets/777c0d8a-e41e-4dd5-bbab-28f8a8762c4c" />
<img width="1295" height="867" alt="image" src="https://github.com/user-attachments/assets/38fcb2fb-e6e9-4bbc-b111-ac438838bd4c" />

###### Average value per order
<img width="1244" height="360" alt="image" src="https://github.com/user-attachments/assets/4bdacfba-6329-4618-8d91-71c655224d07" />
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/55492083-33c3-43a3-8458-0c3d1b1e6130" />

## 🔎 5. Final Conclusion & Recommendations  
#### 5.1. Insight
-  Insight 1: In the end of 2010 and 2011, Top 3 most crowded customer groups include Sleepers, Lost, Promissing while  Top 3 customer groups with highest revenue include Champions, Big spenders, Promising => Champion & Big spender customers take up small number of customer but contribute the most to the revenue

- Insight 2: From 2010 to 2011, Top 3 most crowded customer groups include Sleepers, Lost, Promissing while  Top 3 customer groups with highest revenue include Champions, Big spenders, Sleepers => Champion & Big spender customers take up small number of customer but contribute the most to the revenue

- Insight 3: Over 90% of SuperStore's customers are from the UK, making it an undeniable strategic market

- Insight 4: Revenue surges from the beginning of October to mid-December, confirming this as the golden period for launching sales-driving campaigns.

- Insight 5 : Top 3 products with having highest revenue in important customer segmentation

+ Champion customer: REGENCY CAKESTAND 3 TIER, RABBIT NIGHT LIGHT, and PAPER CHAIN KIT 50'S CHRISTMAS.

+ Big spender customer: PAPER CRAFT LITTLE BIRDIE, Manual and POSTAGE.

+ Promissing customer: JUMBO BAG RED RETROSPOT, RABBIT NIGHT LIGHT, and PAPER CHAIN KIT 50'S CHRISTMAS.

+ Sleepers: WHITE HANGING HEART T-LIGHT HOLDER, RED HARMONICA IN BOX, and ROUND SNACK BOXES SET OF 4 FRUITS

#### 5.2. Recommendations
###### Objective 1: Customer Appreciation and Revenue Maximization
General Recommendations:

Focus on 4 Strategic Segments: Campaigns should prioritize resources for four groups: Champions, Big Spenders, Promising, and Sleepers, as they contribute the most revenue.

Prioritize the UK Market: Implement robust and in-depth campaigns in the United Kingdom.

The campaign should be launched in early October and mid December.

Detailed Recommendations per Segment:

Champions:

Goal: Enhance retention, recognition, and maximize lifetime value.

Actions: Create a top-tier loyalty program exclusively for them, Send personalized, exclusive Christmas & New Year gifts, Provide early access to limited-edition holiday collections, Include a handwritten thank-you card with their orders.

Big Spenders:

Goal: Increase purchase frequency.

Actions: Offer an exclusive gift set or luxury bundle when they make another high-value purchase; Provide a time-limited voucher or free shipping on their next order to encourage a quicker return.

Promising:

Goal: Increase order value (Monetary) and encourage repeat purchases.

Actions: Offer vouchers, discounts, or gifts for their next purchase, especially on high-value orders; Implement cross-selling promotions related to their favorite products like JUMBO BAG RED RETROSPOT and RABBIT NIGHT LIGHT.

Sleepers:

Goal: Reactivate them and improve their Recency score.

Actions: Launch a "We Miss You!" campaign via email with special offers (discounts, gifts, vouchers) to encourage them to return.


###### Objective 2: Launch campaigns to turn prospects into loyal customers
Voucher/Discount/Cashback when buy combo especially when customer buy top product including JUMBO BAG RED RETROSPOT, RABBIT NIGHT LIGHT, and PAPER CHAIN KIT 50'S CHRISTMAS

Offer points, voucher, discount & coupon when buy the next time

Launch loyalty program and offer special benefits if promissing customer become loyal customer











