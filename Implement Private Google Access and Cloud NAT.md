Implementing **Private Google Access** and **Cloud NAT** in Google Cloud allows your VMs without external IP addresses to access Google APIs and services securely and provides managed network address translation for private VMs. Below are the steps for setting these up using both Google Cloud Console and Cloud Shell.

### **1. Implement Private Google Access**

**Private Google Access** allows instances without external IP addresses to access Google services, such as Google Cloud Storage and BigQuery, using internal IP addresses. 

#### **Using Google Cloud Console**

1. **Enable Private Google Access:**
   - Go to the [Google Cloud Console](https://console.cloud.google.com/).
   - Navigate to **VPC Network** > **VPC networks**.
   - Select the VPC network you want to configure.
   - Click on the **Subnets** tab.
   - Click on the **Edit** button next to the subnet where you want to enable Private Google Access.
   - Check the box for **Private Google Access** under **Private Google Access**.
   - Click **Save** to apply the changes.

2. **Verify Private Google Access:**
   - Ensure that the VM instances in the subnet can access Google APIs and services without external IP addresses by testing API calls or service access.

#### **Using Cloud Shell**

1. **Enable Private Google Access:**
   - Use the `gcloud` command to modify the subnet to enable Private Google Access:
     ```bash
     gcloud compute networks subnets update my-subnet --region=us-central1 --enable-private-ip-google-access
     ```
   - Replace `my-subnet` with your subnet name and `us-central1` with the region where the subnet is located.

2. **Verify Private Google Access:**
   - Deploy a VM instance without an external IP address in the subnet and test access to Google APIs or services.

### **2. Implement Cloud NAT**

**Cloud NAT** (Network Address Translation) allows VMs in a private network to access the internet for updates or software installations without having external IP addresses. 

#### **Using Google Cloud Console**

1. **Create a Cloud NAT Gateway:**
   - Go to the [Google Cloud Console](https://console.cloud.google.com/).
   - Navigate to **Hybrid Connectivity** > **Cloud NAT**.
   - Click on **Create NAT gateway**.
   - Provide a **Name** for the NAT gateway.
   - Select the **VPC network** for which you want to create the NAT gateway.
   - Choose or create a **NAT Gateway** configuration:
     - **NAT Configuration:** Define NAT configuration options such as NAT IP address and NAT gateway settings.
   - Click **Create** to provision the NAT gateway.

2. **Create a NAT Router:**
   - Go to **Hybrid Connectivity** > **NAT routers**.
   - Click on **Create NAT router**.
   - Provide a **Name** for the NAT router and select the **VPC network**.
   - Select the **Region** and configure NAT settings:
     - **Cloud NAT:** Configure the NAT gateway to use the newly created NAT router.
   - Click **Create** to apply the settings.

#### **Using Cloud Shell**

1. **Create a Cloud NAT Router:**
   - Use the `gcloud` command to create a Cloud NAT router:
     ```bash
     gcloud compute routers create my-nat-router --network=my-custom-vpc --region=us-central1
     ```
   - Replace `my-nat-router` with your desired router name, `my-custom-vpc` with your VPC network, and `us-central1` with your region.

2. **Create a Cloud NAT Configuration:**
   - Create the Cloud NAT configuration using the `gcloud` command:
     ```bash
     gcloud compute routers nats create my-nat-config --router=my-nat-router --region=us-central1 --nat-all-subnet-ip-ranges
     ```
   - Replace `my-nat-config` with your NAT configuration name and `my-nat-router` with your router name.

### **Verification and Testing**

- **Verify Private Google Access:**
  - Deploy a VM instance without an external IP address in the subnet and attempt to access Google services (e.g., using `curl` to access Google Cloud Storage or BigQuery APIs).

- **Verify Cloud NAT:**
  - Deploy a VM instance without an external IP address in the VPC and attempt to access the internet (e.g., by running an `apt-get update` or `yum update` command).

By following these steps, you will have configured Private Google Access and Cloud NAT, enabling secure access to Google services and internet connectivity for private VMs in Google Cloud.