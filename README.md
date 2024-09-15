# Random-Dummy-Data-Generation-For-Data-Engineering-Project
Generation of random dummy data for a data engineering project using the Python faker module.

## Step 1 : Installation the faker module

pip install faker

## Step 2: Import Required Libraries

import pandas as pd

import numpy as np

from faker import Faker

import random

from datetime import datetime, timedelta

fake = Faker()

num_rows = 5000

## Step 3: Python Script for Random Dummy Data Generation

## Define product categories related to medicines
product_categories = [
    'Cardiovascular Diseases (Prescription)',
    'Diabetes (Prescription & OTC)',
    'Pain Relief (OTC & Prescription)',
    'Respiratory Diseases (OTC & Prescription)',
    'Gastrointestinal (OTC & Prescription)',
    'Antibiotics (Prescription)',
    'Mental Health (Prescription)',
    'Dermatological (OTC & Prescription)',
    'Neurological Disorders (Prescription)',
    'Bone Health (OTC & Prescription)',
    'Eye Health (OTC & Prescription)',
    'AIDS Treatment (Prescription)',
    'Cancer Treatment (Prescription)'
]

## Define medicines for each category
medicines = {
    'Cardiovascular Diseases (Prescription)': ['Atenolol', 'Lisinopril', 'Metoprolol'],
    'Diabetes (Prescription & OTC)': ['Metformin', 'Insulin', 'Glyburide', 'Glipizide'],
    'Pain Relief (OTC & Prescription)': ['Ibuprofen', 'Aspirin', 'Acetaminophen', 'Oxycodone'],
    'Respiratory Diseases (OTC & Prescription)': ['Albuterol', 'Fluticasone', 'Montelukast'],
    'Gastrointestinal (OTC & Prescription)': ['Omeprazole', 'Loperamide', 'Ranitidine'],
    'Antibiotics (Prescription)': ['Amoxicillin', 'Ciprofloxacin', 'Azithromycin'],
    'Mental Health (Prescription)': ['Sertraline', 'Citalopram', 'Diazepam'],
    'Dermatological (OTC & Prescription)': ['Hydrocortisone', 'Clotrimazole', 'Benzoyl Peroxide'],
    'Neurological Disorders (Prescription)': ['Levetiracetam', 'Carbamazepine', 'Gabapentin'],
    'Bone Health (OTC & Prescription)': ['Calcium Carbonate', 'Vitamin D', 'Alendronate'],
    'Eye Health (OTC & Prescription)': ['Loratadine', 'Olopatadine', 'Artificial Tears'],
    'AIDS Treatment (Prescription)': ['Tenofovir', 'Emtricitabine', 'Efavirenz'],
    'Cancer Treatment (Prescription)': ['Cisplatin', 'Doxorubicin', 'Paclitaxel']
}

## Define store locations
store_locations = [
    'New York City',
    'Los Angeles',
    'Chicago',
    'Houston',
    'Phoenix',
    'Philadelphia',
    'San Antonio',
    'San Diego',
    'Dallas',
    'San Jose'
]

## Generate random dates within June, July, and August 2024 - POS_Sales_Data_2024 - Generation
def generate_random_date(start_date, end_date):
    delta = end_date - start_date
    random_days = random.randint(0, delta.days)
    return start_date + timedelta(days=random_days)

start_date = datetime(2024, 6, 1)
end_date = datetime(2024, 8, 31)

## Generate data
data = {
    'Transaction ID': [f'T{str(i).zfill(4)}' for i in range(1, num_rows + 1)],
    'Transaction Date': [generate_random_date(start_date, end_date).strftime('%Y-%m-%d') for _ in range(num_rows)],
    'Transaction Time': [fake.time(pattern='%H:%M:%S') for _ in range(num_rows)],
    'Store ID': [f'S{str(np.random.randint(1, 11)).zfill(3)}' for _ in range(num_rows)],
    'Store Location': [np.random.choice(store_locations) for _ in range(num_rows)],
    'Cashier ID': [f'C{str(np.random.randint(1, 10)).zfill(3)}' for _ in range(num_rows)],
    'Customer ID': [f'U{str(np.random.randint(1, 100)).zfill(3)}' for _ in range(num_rows)],
    'Customer Age': [np.random.randint(18, 70) for _ in range(num_rows)],
    'Customer Gender': [np.random.choice(['Male', 'Female']) for _ in range(num_rows)],
    'Product ID': [f'P{str(np.random.randint(1, 50)).zfill(3)}' for _ in range(num_rows)],
    'Product Category': [np.random.choice(product_categories) for _ in range(num_rows)],
    'Product Name': [np.random.choice(medicines[cat]) for cat in np.random.choice(product_categories, num_rows)],
    'Quantity': [np.random.randint(1, 5) for _ in range(num_rows)],
    'Unit Price': [round(np.random.uniform(5.0, 500.0), 2) for _ in range(num_rows)],
}

## Create DataFrame
df = pd.DataFrame(data)

## Combine Date and Time into Timestamp
df['Timestamp'] = pd.to_datetime(df['Transaction Date'].astype(str) + ' ' + df['Transaction Time'])

## Drop the original Date and Time columns
df = df.drop(columns=['Transaction Date', 'Transaction Time'])

## Calculate Total Amount
df['Total Amount'] = df['Quantity'] * df['Unit Price']

## Calculate Discount Applied
df['Discount Applied'] = [round(np.random.uniform(0.0, 50.0), 2) for _ in range(num_rows)]

## Calculate Tax Amount
df['Tax Amount'] = df['Total Amount'] * 0.07

## Calculate Total Amount After Tax
df['Total Amount After Tax'] = df['Total Amount'] + df['Tax Amount'] - df['Discount Applied']

## Save to CSV (Put your local storage path)
df.to_csv('pos_transactional_data_medicines_with_timestamp_june_august_2024.csv', index=False)

print("Data generation complete and saved to 'pos_transactional_data_medicines_with_timestamp_june_august_2024.csv'.")


## Product_Categorywise_Vendor_Data_2024 & Inventory_Data - Generation

## Define constants
num_vendors = 10
num_stores = 10
num_products = 15
num_inventory_entries = num_stores * num_products

## Define store locations and product categories
store_locations = [
    'New York City',
    'Los Angeles',
    'Chicago',
    'Houston',
    'Phoenix',
    'Philadelphia',
    'San Antonio',
    'San Diego',
    'Dallas',
    'San Jose'
]

product_categories = [
    'Cardiovascular Diseases (Prescription)',
    'Diabetes (Prescription & OTC)',
    'Pain Relief (OTC & Prescription)',
    'Respiratory Diseases (OTC & Prescription)',
    'Gastrointestinal (OTC & Prescription)',
    'Antibiotics (Prescription)',
    'Mental Health (Prescription)',
    'Dermatological (OTC & Prescription)',
    'Neurological Disorders (Prescription)',
    'Bone Health (OTC & Prescription)',
    'Eye Health (OTC & Prescription)',
    'AIDS Treatment (Prescription)',
    'Cancer Treatment (Prescription)'
]

## Define medicines for each category
medicines = {
    'Cardiovascular Diseases (Prescription)': ['Atenolol', 'Lisinopril', 'Metoprolol'],
    'Diabetes (Prescription & OTC)': ['Metformin', 'Insulin', 'Glyburide', 'Glipizide'],
    'Pain Relief (OTC & Prescription)': ['Ibuprofen', 'Aspirin', 'Acetaminophen', 'Oxycodone'],
    'Respiratory Diseases (OTC & Prescription)': ['Albuterol', 'Fluticasone', 'Montelukast'],
    'Gastrointestinal (OTC & Prescription)': ['Omeprazole', 'Loperamide', 'Ranitidine'],
    'Antibiotics (Prescription)': ['Amoxicillin', 'Ciprofloxacin', 'Azithromycin'],
    'Mental Health (Prescription)': ['Sertraline', 'Citalopram', 'Diazepam'],
    'Dermatological (OTC & Prescription)': ['Hydrocortisone', 'Clotrimazole', 'Benzoyl Peroxide'],
    'Neurological Disorders (Prescription)': ['Levetiracetam', 'Carbamazepine', 'Gabapentin'],
    'Bone Health (OTC & Prescription)': ['Calcium Carbonate', 'Vitamin D', 'Alendronate'],
    'Eye Health (OTC & Prescription)': ['Loratadine', 'Olopatadine', 'Artificial Tears'],
    'AIDS Treatment (Prescription)': ['Tenofovir', 'Emtricitabine', 'Efavirenz'],
    'Cancer Treatment (Prescription)': ['Cisplatin', 'Doxorubicin', 'Paclitaxel']
}

## Generate Vendor Data
vendors = {
    'Vendor ID': [f'V{str(i).zfill(3)}' for i in range(1, num_vendors + 1)],
    'Vendor Name': [fake.company() for _ in range(num_vendors)],
    'Product Category': [np.random.choice(product_categories) for _ in range(num_vendors)],
    'Supply Rate': [np.random.uniform(0.8, 1.2) for _ in range(num_vendors)]  # Supply rate as a multiplier
}

df_vendors = pd.DataFrame(vendors)

## Generate Inventory Data
inventory = {
    'Store ID': [f'S{str(i).zfill(3)}' for i in range(1, num_stores + 1) for _ in range(num_products)],
    'Store Location': [np.random.choice(store_locations) for _ in range(num_inventory_entries)],
    'Product ID': [f'P{str(i).zfill(3)}' for i in range(1, num_products + 1) for _ in range(num_stores)],
    'Product Name': [],
    'Product Category': [],
    'Current Stock': [np.random.randint(10, 100) for _ in range(num_inventory_entries)],
    'Reorder Level': [np.random.randint(5, 20) for _ in range(num_inventory_entries)],
    'Reorder Quantity': [np.random.randint(20, 50) for _ in range(num_inventory_entries)],
    'Last Restock Date': [fake.date_this_year() for _ in range(num_inventory_entries)],
    'Projected Demand': [np.random.randint(10, 50) for _ in range(num_inventory_entries)]
}

## Assign product names and categories to match the product ID
product_names = []
product_categories_list = []

for _ in range(num_inventory_entries):
    category = np.random.choice(product_categories)
    product_names.append(np.random.choice(medicines[category]))
    product_categories_list.append(category)

inventory['Product Name'] = product_names
inventory['Product Category'] = product_categories_list

df_inventory = pd.DataFrame(inventory)

print("Supply chain data generation complete and saved to 'vendor_data.csv' and 'inventory_data.csv'.")




