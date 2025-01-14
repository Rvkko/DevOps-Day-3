# NBA Data Lake

This project automates the creation of a data lake for NBA analytics using AWS services. The `setup_nba_data_lake.py` script integrates **Amazon S3**, **AWS Glue**, and **Amazon Athena** to store and query NBA-related data efficiently.


## Overview

The `setup_nba_data_lake.py` script performs the following actions:

- Creates an **Amazon S3 bucket** to store both raw and processed data.
- Uploads **sample NBA data** (in JSON format) to the S3 bucket.
- Creates an **AWS Glue** database and an external table to enable querying.
- Configures **Amazon Athena** for querying the data stored in the S3 bucket.


## Prerequisites

Before running the script, make sure you have:

1. **SportsData.io API Key**:
   - Go to [SportsData.io](https://sportsdata.io).
   - Create a free account and select NBA under the API resources.
   - After registration, find your API key under the "NBA" section, specifically in the "Query String Parameters."

2. **IAM Role/Permissions**:
   Ensure that the IAM user or role running the script has the following permissions:
   - **S3**: `s3:CreateBucket`, `s3:PutObject`, `s3:DeleteBucket`, `s3:ListBucket`
   - **Glue**: `glue:CreateDatabase`, `glue:CreateTable`, `glue:DeleteDatabase`, `glue:DeleteTable`
   - **Athena**: `athena:StartQueryExecution`, `athena:GetQueryResults`


## Setup Instructions

### Step 1: Open CloudShell Console
- Go to [AWS Console](https://aws.amazon.com) and sign in to your account.
- In the top navigation, next to the search bar, click on the **CloudShell** icon (a square with `>_` inside) to open the CloudShell.

### Step 2: Create the `setup_nba_data_lake.py` file
1. In CloudShell, type the following command to create the Python script:
   ```bash
   nano setup_nba_data_lake.py
   ```
2. Copy the contents of the `setup_nba_data_lake.py` file from the repository.
3. Paste the copied contents into the CloudShell file.
4. Locate the line under `#SportsData.io configurations` where the API key is defined:
   ```python
   api_key = "your_api_key"
   ```
   Paste your API key between the quotation marks.
5. Press **Ctrl+X** to exit, press **Y** to save the file, and press **Enter** to confirm the file name.

### Step 3: Create the `.env` file
1. In CloudShell, type the following command to create the environment file:
   ```bash
   nano .env
   ```
2. Paste the following code into the file, replacing `"your_sportsdata_api_key"` with your actual API key:
   ```bash
   SPORTS_DATA_API_KEY=your_sportsdata_api_key
   NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
   ```
3. Press **Ctrl+X** to exit, press **Y** to save, and press **Enter** to confirm the file name.

### Step 4: Run the script
1. In CloudShell, run the script:
   ```bash
   python3 setup_nba_data_lake.py
   ```
2. You should see a message confirming that the resources were successfully created, the sample data was uploaded, and the data lake setup is complete.

### Step 5: Manually Check For Resources
1. In the AWS Console, type **S3** in the search bar and click on the **S3** link.
2. You should see a general-purpose bucket named `Sports-analytics-data-lake`.
3. Inside the bucket, click on the `raw-data` folder to see the uploaded file `nba_player_data.json`.
4. Open the file to view the NBA data.
5. Go to **Amazon Athena** and paste the following sample query:
   ```sql
   SELECT FirstName, LastName, Position, Team
   FROM nba_players
   WHERE Position = 'PG';
   ```
6. Click **Run**. You should see the results under the "Query Results" section.

---

## Conclusion

By following these steps, you'll have a fully functional NBA data lake that can store and query NBA data using AWS services like S3, Glue, and Athena.

Let me know if you need further adjustments!
```

This format should work well for your project. Let me know if you'd like any changes or additions!