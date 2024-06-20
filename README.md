Customer Call List Data Cleaning Project
Overview
This project aims to clean and prepare a customer call list dataset (Customer Call List.csv) for machine learning algorithms or further analysis. The dataset contains various columns related to customer information such as phone numbers, addresses, and customer preferences.

Project Goals
Format phone numbers into the standard 000-000-0000 format.
Remove unwanted columns (Not_Useful_Column, Unnamed: 8, Unnamed: 9).
Handle missing values (NaN, N/a, NAs).
Standardize formats (Yes to Y and No to N).
Split address into street address and zip code.
Create a clean calling list of customers who have not opted out (Do_Not_Contact != 'Y') and have valid phone numbers.
Libraries Used
pandas: For data manipulation and analysis.
Instructions
Loading the Dataset:

python
Copy code
import pandas as pd

df = pd.read_csv("Customer Call List.csv")
Dropping Unwanted Columns:

python
Copy code
unwanted_columns = ["Not_Useful_Column", "Unnamed: 8", "Unnamed: 9"]
df = df.drop(columns=unwanted_columns)
Cleaning and Formatting Phone Numbers:

python
Copy code
df['Phone_Number'] = df['Phone_Number'].str.replace('[^a-zA-Z0-9]', '', regex=True)
df['Phone_Number'] = df['Phone_Number'].apply(lambda x: str(x))
df['Phone_Number'] = df['Phone_Number'].apply(lambda x: x[0:3] + '-' + x[3:6] + '-' + x[6:10])
Handling Missing Values:

python
Copy code
df = df.fillna("")
df = df.replace('N/a', '')
Standardizing Yes/No Responses:

python
Copy code
df['Paying Customer'] = df['Paying Customer'].str.replace('Yes', 'Y')
df['Paying Customer'] = df['Paying Customer'].str.replace('No', 'N')
df['Do_Not_Contact'] = df['Do_Not_Contact'].str.replace('Yes', 'Y')
df['Do_Not_Contact'] = df['Do_Not_Contact'].str.replace('No', 'N')
Arranging Address Columns:

python
Copy code
df[['Street_address', 'State', 'Zip_code']] = df['Address'].str.split(',', n=2, expand=True)
Creating a Clean Calling List:

python
Copy code
for i in df.index:
    if df.loc[i, 'Do_Not_Contact'] == 'Y' or df.loc[i, 'Phone_Number'] == '--':
        df.drop(i, inplace=True)
Next Steps
After cleaning the dataset using the above steps, you can proceed with exploratory data analysis, feature engineering, or directly apply machine learning algorithms depending on your project's objectives.

License
[Include your license information here, if applicable.]

Acknowledgements
[Optionally, acknowledge any contributors or resources used in your project.]

