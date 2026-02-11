# Bank Customers Churn Analysis

## Introduction

## The Problem

Banks lose customers. That's not news. But understanding *why* they leave, and more importantly *who* is likely to leave next, is the difference between reactive damage control and proactive retention. Customer churn is expensive. Acquiring a new customer costs significantly more than keeping an existing one, and every departure represents lost revenue, lost cross-selling opportunities, and a signal that something in the experience isn't working.

This project takes a dataset of 10,000 bank customers and digs into the patterns behind churn. The goal isn't just to describe what happened. It's to surface actionable insight that a retention team could actually use.


## The Dataset

Source: [Kaggle - Bank Customer Churn Dataset](https://www.kaggle.com/datasets/gauravtopre/bank-customer-churn-dataset)

10,000 rows. 12 columns. Each row is one customer.

| Column | Description | Type |
|--------|-------------|------|
| customer_id | Unique identifier | Numeric |
| credit_score | Customer's credit score | Numeric |
| country | Customer's country | Categorical |
| gender | Customer's gender | Categorical |
| age | Customer's age | Numeric |
| tenure | Years with the bank | Numeric |
| balance | Account balance | Numeric |
| products_number | Number of bank products held | Numeric |
| credit_card | Has a credit card (1 = yes, 0 = no) | Binary |
| active_member | Is an active member (1 = yes, 0 = no) | Binary |
| estimated_salary | Estimated annual salary | Numeric |
| churn | Left the bank (1 = yes, 0 = no) | Binary |
