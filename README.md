# Importing necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Placeholder DataFrames for the four platforms (simulate dataset structure)
# Actual datasets will need to be collected and loaded from real sources
data_amazon = pd.DataFrame({
    'Category': ['Electronics', 'Books', 'Clothing', 'Home'],
    'User_Rating': [4.5, 4.7, 4.0, 4.3],
    'Price_Consistency': [0.9, 0.95, 0.85, 0.92],
    'Customer_Service': [4.4, 4.6, 4.2, 4.3]
})

data_ebay = pd.DataFrame({
    'Category': ['Electronics', 'Books', 'Clothing', 'Home'],
    'User_Rating': [4.3, 4.5, 4.1, 4.0],
    'Price_Consistency': [0.88, 0.9, 0.87, 0.89],
    'Customer_Service': [4.1, 4.3, 4.0, 4.2]
})

data_walmart = pd.DataFrame({
    'Category': ['Electronics', 'Books', 'Clothing', 'Home'],
    'User_Rating': [4.4, 4.6, 4.2, 4.1],
    'Price_Consistency': [0.91, 0.93, 0.89, 0.88],
    'Customer_Service': [4.2, 4.5, 4.1, 4.0]
})

data_shopify = pd.DataFrame({
    'Category': ['Electronics', 'Books', 'Clothing', 'Home'],
    'User_Rating': [4.2, 4.4, 4.0, 3.9],
    'Price_Consistency': [0.85, 0.88, 0.84, 0.86],
    'Customer_Service': [4.0, 4.2, 3.9, 4.0]
})

# Combining the data into a single DataFrame for analysis
platforms = ['Amazon', 'eBay', 'Walmart', 'Shopify']
data_combined = pd.concat([
    data_amazon.assign(Platform='Amazon'),
    data_ebay.assign(Platform='eBay'),
    data_walmart.assign(Platform='Walmart'),
    data_shopify.assign(Platform='Shopify')
], ignore_index=True)

# Data Cleaning (No missing values or outliers in simulated data)
# Transformation and Analysis
# Calculate mean metrics for each platform
platform_means = data_combined.groupby('Platform').mean().reset_index()

# Visualization: Bar charts for comparison
plt.figure(figsize=(12, 6))
for metric in ['User_Rating', 'Price_Consistency', 'Customer_Service']:
    sns.barplot(data=platform_means, x='Platform', y=metric)
    plt.title(f"Average {metric} by Platform")
    plt.ylabel(metric)
    plt.xlabel("Platform")
    plt.show()

# Heatmap of category-wise comparison
pivot_data = data_combined.pivot(index='Category', columns='Platform', values='User_Rating')
plt.figure(figsize=(10, 6))
sns.heatmap(pivot_data, annot=True, cmap='coolwarm', fmt=".2f")
plt.title("Category-wise User Ratings Heatmap")
plt.show()

# Save results
output_path = "/mnt/data/EDA_Optimal_ECommerce_Analysis.py"
with open(output_path, "w") as file:
    file.write("""# EDA Python Script for Optimal E-Commerce Platform Analysis
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Dataframes for platforms (sample data simulated)
data_amazon = {data_amazon}
data_ebay = {data_ebay}
data_walmart = {data_walmart}
data_shopify = {data_shopify}

# Combining data
platforms = ['Amazon', 'eBay', 'Walmart', 'Shopify']
data_combined = pd.concat([
    data_amazon.assign(Platform='Amazon'),
    data_ebay.assign(Platform='eBay'),
    data_walmart.assign(Platform='Walmart'),
    data_shopify.assign(Platform='Shopify')
], ignore_index=True)

# Analysis and Visualization omitted for brevity
# Replace this with analysis code if needed
print("Script saved successfully.")
""")
