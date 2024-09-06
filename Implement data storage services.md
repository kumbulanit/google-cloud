To implement Google Cloud data storage services, you can follow these step-by-step instructions for different types of storage solutions: Google Cloud Storage, Cloud SQL, Cloud Spanner, Cloud Firestore, and Cloud Bigtable. 

### **1. Implementing Google Cloud Storage (GCS)**

**Using Google Cloud Console:**
1. **Navigate to Cloud Storage**:
   - Go to the Google Cloud Console: [Console](https://console.cloud.google.com/)
   - In the left-hand menu, click on “Storage” and then “Browser”.

2. **Create a Bucket**:
   - Click “Create bucket”.
   - Enter a unique name for your bucket.
   - Choose the appropriate **Location type** and **Location**.
   - Select a **Storage class** (e.g., Standard, Nearline, Coldline, Archive).
   - Set **Access control** settings as needed.
   - Click “Create”.

**Using Cloud Shell:**
1. **Open Cloud Shell**:
   - Click on the terminal icon in the Google Cloud Console.

2. **Create a Bucket**:
   ```sh
   gsutil mb -l LOCATION gs://BUCKET_NAME/
   ```
   - Replace `LOCATION` with your desired location (e.g., `US`, `europe-west1`) and `BUCKET_NAME` with a unique name for your bucket.

### **2. Implementing Cloud SQL**

**Using Google Cloud Console:**
1. **Navigate to Cloud SQL**:
   - Go to the Google Cloud Console: [Console](https://console.cloud.google.com/)
   - In the left-hand menu, click on “SQL” under “Databases”.

2. **Create an Instance**:
   - Click “Create instance”.
   - Choose your database type (MySQL, PostgreSQL, SQL Server).
   - Fill in the **Instance ID**, **Root password**, and **Database version**.
   - Configure **Instance settings** (e.g., region, machine type).
   - Click “Create”.

**Using Cloud Shell:**
1. **Open Cloud Shell**:
   - Click on the terminal icon in the Google Cloud Console.

2. **Create an Instance**:
   ```sh
   gcloud sql instances create INSTANCE_NAME --database-version=DB_VERSION --tier=TIER --region=REGION
   ```
   - Replace `INSTANCE_NAME` with your desired instance name, `DB_VERSION` with the version of the database (e.g., `MYSQL_8_0`), `TIER` with the instance tier (e.g., `db-f1-micro`), and `REGION` with the desired region (e.g., `us-central1`).

### **3. Implementing Cloud Spanner**

**Using Google Cloud Console:**
1. **Navigate to Cloud Spanner**:
   - Go to the Google Cloud Console: [Console](https://console.cloud.google.com/)
   - In the left-hand menu, click on “Spanner”.

2. **Create an Instance**:
   - Click “Create instance”.
   - Enter the **Instance ID**, **Instance name**, and **Configuration**.
   - Choose the **Number of nodes** based on your performance needs.
   - Click “Create”.

3. **Create a Database**:
   - After the instance is created, click on the instance name.
   - Click “Create database”.
   - Enter a **Database ID** and click “Create”.

**Using Cloud Shell:**
1. **Open Cloud Shell**:
   - Click on the terminal icon in the Google Cloud Console.

2. **Create an Instance**:
   ```sh
   gcloud spanner instances create INSTANCE_NAME --config=CONFIGURATION --nodes=NODES --description="DESCRIPTION"
   ```
   - Replace `INSTANCE_NAME`, `CONFIGURATION`, `NODES`, and `DESCRIPTION` with your desired values.

3. **Create a Database**:
   ```sh
   gcloud spanner databases create DATABASE_NAME --instance=INSTANCE_NAME
   ```
   - Replace `DATABASE_NAME` and `INSTANCE_NAME` with your database and instance names.

### **4. Implementing Cloud Firestore**

**Using Google Cloud Console:**
1. **Navigate to Firestore**:
   - Go to the Google Cloud Console: [Console](https://console.cloud.google.com/)
   - In the left-hand menu, click on “Firestore”.

2. **Create a Firestore Database**:
   - Click “Create database”.
   - Choose a **Firestore mode** (Native or Datastore mode).
   - Select a **Location** for your Firestore database.
   - Click “Create”.

**Using Cloud Shell:**
1. **Open Cloud Shell**:
   - Click on the terminal icon in the Google Cloud Console.

2. **Create Firestore Database**:
   Firestore setup is primarily done through the Cloud Console, as it involves database creation and management through a UI. Use Firebase CLI for programmatic setup:
   ```sh
   firebase init firestore
   ```
   - Follow the prompts to configure Firestore.

### **5. Implementing Cloud Bigtable**

**Using Google Cloud Console:**
1. **Navigate to Cloud Bigtable**:
   - Go to the Google Cloud Console: [Console](https://console.cloud.google.com/)
   - In the left-hand menu, click on “Bigtable”.

2. **Create a Cluster**:
   - Click “Create instance”.
   - Enter the **Instance ID**, **Instance name**, and **Cluster configuration**.
   - Choose the **Number of nodes** and **Region**.
   - Click “Create”.

3. **Create a Table**:
   - After creating the instance, click on it.
   - Click “Create table”.
   - Enter a **Table ID** and configure column families as needed.
   - Click “Create”.

**Using Cloud Shell:**
1. **Open Cloud Shell**:
   - Click on the terminal icon in the Google Cloud Console.

2. **Create an Instance**:
   ```sh
   gcloud bigtable instances create INSTANCE_NAME --cluster=CLUSTER_NAME --cluster-zone=ZONE --display-name="DISPLAY_NAME" --num-nodes=NODES
   ```
   - Replace `INSTANCE_NAME`, `CLUSTER_NAME`, `ZONE`, `DISPLAY_NAME`, and `NODES` with appropriate values.

3. **Create a Table**:
   ```sh
   gcloud bigtable tables create TABLE_NAME --instance=INSTANCE_NAME
   ```
   - Replace `TABLE_NAME` and `INSTANCE_NAME` with your table and instance names.

### **Summary**

- **Google Cloud Storage (GCS)**: Use for object storage needs.
- **Cloud SQL**: Use for relational database requirements.
- **Cloud Spanner**: Use for globally distributed and horizontally scalable relational databases.
- **Cloud Firestore**: Use for real-time, NoSQL document-based storage.
- **Cloud Bigtable**: Use for large-scale, NoSQL wide-column data storage.

By following these steps, you can implement and configure each data storage service according to your specific needs and application requirements.