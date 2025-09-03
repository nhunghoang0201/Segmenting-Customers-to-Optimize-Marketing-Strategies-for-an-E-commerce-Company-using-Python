# RFM Analysis in Ecommerce
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
- This analysis was conducted to answer two core business questions:
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


