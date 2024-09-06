Implementing VPC networks and firewall rules in Google Cloud can be done through the Google Cloud Console and Cloud Shell. Below are step-by-step instructions for both methods.

### **1. Implementing VPC Networks**

#### **Using Google Cloud Console**

1. **Create a VPC Network:**
   - Go to the [Google Cloud Console](https://console.cloud.google.com/).
   - In the navigation menu, select **VPC Network** > **VPC networks**.
   - Click on **Create VPC Network**.
   - Provide a **Name** for your VPC.
   - Choose **Automatic** or **Custom** mode:
     - **Automatic**: Subnets are created automatically in each region.
     - **Custom**: You define your subnets manually.
   - If you chose **Custom** mode:
     - Click on **Add subnet**.
     - Enter the **Subnet Name**, **Region**, and **IP address range** (e.g., 10.0.0.0/24).
     - Add as many subnets as needed.
   - Click **Create** to provision the VPC.

2. **Create Additional Subnets (for Custom Mode):**
   - After creating the VPC, you can add more subnets by clicking on the VPC network you created.
   - Click on **Add subnet** and fill in the details.

#### **Using Cloud Shell**

1. **Open Cloud Shell:**
   - Access Cloud Shell from the Google Cloud Console by clicking on the **Activate Cloud Shell** icon in the top-right corner.

2. **Create a Custom VPC Network:**
   - Use the following command to create a VPC network in **Custom** mode:
     ```bash
     gcloud compute networks create my-custom-vpc --subnet-mode=custom
     ```

3. **Create Subnets:**
   - Create a subnet within the VPC network:
     ```bash
     gcloud compute networks subnets create my-subnet-1 --network=my-custom-vpc --region=us-central1 --range=10.0.0.0/24
     ```
   - You can add more subnets by repeating the command with different regions and IP ranges.

### **2. Implementing Firewall Rules**

#### **Using Google Cloud Console**

1. **Create Firewall Rules:**
   - In the Google Cloud Console, navigate to **VPC Network** > **Firewall rules**.
   - Click on **Create Firewall Rule**.
   - Provide a **Name** for the rule.
   - Select the **VPC Network** where the rule will apply.
   - Set the **Direction of Traffic** (Ingress or Egress):
     - **Ingress**: Controls incoming traffic to instances.
     - **Egress**: Controls outgoing traffic from instances.
   - Set the **Source IP ranges** (e.g., 0.0.0.0/0 for all traffic or a specific IP range).
   - Set the **Protocol and Ports** (e.g., tcp:80 for HTTP traffic).
   - Set **Action on Match** to **Allow** or **Deny**.
   - Click **Create** to apply the firewall rule.

#### **Using Cloud Shell**

1. **Create a Firewall Rule to Allow HTTP Traffic:**
   - Use the following command to create a firewall rule that allows HTTP traffic (port 80):
     ```bash
     gcloud compute firewall-rules create allow-http --network=my-custom-vpc --allow=tcp:80 --source-ranges=0.0.0.0/0 --direction=INGRESS
     ```

2. **Create a Firewall Rule to Allow SSH Traffic:**
   - Allow SSH traffic (port 22) from a specific IP range:
     ```bash
     gcloud compute firewall-rules create allow-ssh --network=my-custom-vpc --allow=tcp:22 --source-ranges=192.168.1.0/24 --direction=INGRESS
     ```

3. **Create a Firewall Rule to Allow Egress Traffic:**
   - Allow all egress traffic to the internet:
     ```bash
     gcloud compute firewall-rules create allow-all-egress --network=my-custom-vpc --allow=all --direction=EGRESS
     ```

### **Verification and Testing**

- **Check VPC and Subnets:**
  - Verify the creation of VPC and subnets by navigating to **VPC Network** > **VPC networks** in the Google Cloud Console.

- **Check Firewall Rules:**
  - Verify firewall rules by navigating to **VPC Network** > **Firewall rules** in the Google Cloud Console.

- **Test Connectivity:**
  - Deploy a VM instance in your VPC network and test the connectivity to ensure the firewall rules are functioning as expected (e.g., access via HTTP or SSH).

By following these steps, you can successfully create and manage VPC networks and firewall rules in Google Cloud, both via the Console and Cloud Shell. This setup allows for secure and controlled access to your Google Cloud resources.