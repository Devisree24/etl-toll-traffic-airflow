# ETL Toll Traffic Pipeline - Commands Reference

This document contains all the commands used for environment setup, DAG tasks, and deployment.

## Step 2: Environment & Project Setup

### 1. Start Apache Airflow
```bash
# Start Airflow webserver (Terminal 1)
airflow webserver --port 8080

# Start Airflow scheduler (Terminal 2)
airflow scheduler
```

### 2. Create Directory Structure for Staging Area
```bash
sudo mkdir -p /home/project/airflow/dags/finalassignment/staging
```

### 3. Set Appropriate Permissions
```bash
sudo chmod -R 777 /home/project/airflow/dags/finalassignment
```

### 4. Download the Dataset
```bash
sudo curl https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0250EN-SkillsNetwork/labs/Final%20Assignment/tolldata.tgz -o /home/project/airflow/dags/finalassignment/tolldata.tgz
```

## Step 4: ETL Tasks Inside the DAG (BashOperator)

### Task 1: Unzip Data
```bash
tar -xvf tolldata.tgz -C /home/project/airflow/dags/
```

### Task 2: Extract Data from CSV
```bash
cut -d"," -f1,2,3,4 vehicle-data.csv > /home/project/airflow/dags/csv_data.csv
```

### Task 3: Extract Data from TSV
```bash
cut -d"\t" -f5,6,7 tollplaza-data.tsv > /home/project/airflow/dags/tsv_data.csv
```

### Task 4: Extract Data from Fixed Width File
```bash
cut -c59-62,63-67 payment-data.txt > /home/project/airflow/dags/fixed_width_data.csv
```

### Task 5: Consolidate Data
```bash
paste /home/project/airflow/dags/csv_data.csv /home/project/airflow/dags/tsv_data.csv /home/project/airflow/dags/fixed_width_data.csv > /home/project/airflow/dags/extracted_data.csv
```

### Task 6: Transform Data
```bash
tr "[a-z]" "[A-Z]" < /home/project/airflow/dags/extracted_data.csv > /home/project/airflow/dags/transformed_data.csv
```

## Step 5: Deploying the DAG to Airflow

### 1. Set the AIRFLOW_HOME Variable
```bash
export AIRFLOW_HOME=/home/project/airflow
echo $AIRFLOW_HOME
```

### 2. Copy the DAG File to Airflow DAGs Directory
```bash
cp ETL_toll_data.py $AIRFLOW_HOME/dags
```

### 3. Verify the DAG Submission
```bash
airflow dags list
```

### 4. Verify ETL_toll_data DAG is Listed
```bash
airflow dags list | grep "ETL_toll_data"
```

### 5. List All Tasks in the DAG
```bash
airflow tasks list ETL_toll_data
```

### 6. Trigger the DAG Manually (Optional)
```bash
airflow dags trigger ETL_toll_data
```
