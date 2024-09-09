To create and configure VPN gateways in Google Cloud, follow these steps. I'll cover both the Google Cloud Console and Cloud Shell methods.

### **1. Using Google Cloud Console**

**Step 1: Create a Cloud VPN Gateway**

1. **Go to the Google Cloud Console**:
   - Navigate to [Google Cloud Console](https://console.cloud.google.com/).

2. **Open the VPN Section**:
   - In the left-hand menu, go to **Hybrid Connectivity** > **VPN**.

3. **Create a VPN Gateway**:
   - Click on **Create VPN**.
   - Enter a name for your VPN gateway.
   - Select the region where you want to deploy the VPN gateway.
   - Choose the network to which the VPN gateway will be attached.
   - Click **Create**.

**Step 2: Create a VPN Tunnel**

1. **Add a Tunnel**:
   - After creating the VPN gateway, click on **Add Tunnel**.
   - Enter a name for the tunnel.
   - Provide the **Peer IP Address** (the public IP address of your on-premises VPN device).
   - Configure **IKE Version** and **Shared Secret** for encryption and authentication.

2. **Configure Traffic Selectors**:
   - Specify the local IP ranges and remote IP ranges that should be used for the VPN tunnel.

3. **Click Create**:
   - Click **Create** to finalize the tunnel setup.

**Step 3: Configure Firewall Rules**

1. **Go to Firewall Rules**:
   - Navigate to **VPC Network** > **Firewall**.

2. **Create a New Firewall Rule**:
   - Click on **Create Firewall Rule**.
   - Define the **Name**, **Network**, and **Priority** for the firewall rule.
   - Set **Targets** and **Source IP Ranges** to allow traffic from the VPN tunnel.
   - Define **Protocols and Ports** to permit traffic as needed.
   - Click **Create**.

**Step 4: Configure On-Premises VPN Device**

- Follow your VPN device's documentation to configure it with the same settings (IP address, IKE version, shared secret) you used in Google Cloud.
- Make sure to set up routes to direct traffic to the VPN tunnel.

### **2. Using Cloud Shell**

**Step 1: Create a Cloud VPN Gateway**

1. **Open Cloud Shell**:
   - Go to [Google Cloud Console](https://console.cloud.google.com/).
   - Click the **Activate Cloud Shell** button.

2. **Create VPN Gateway**:
   ```bash
   gcloud compute vpn-gateways create [VPN_GATEWAY_NAME] \
       --network [NETWORK_NAME] \
       --region [REGION]
   ```

**Step 2: Create a VPN Tunnel**

1. **Create a VPN Tunnel**:
   ```bash
   gcloud compute vpn-tunnels create [TUNNEL_NAME] \
       --peer-address [PEER_IP_ADDRESS] \
       --shared-secret [SHARED_SECRET] \
       --ike-version 2 \
       --region [REGION] \
       --target-vpn-gateway [VPN_GATEWAY_NAME]
   ```

2. **Create a Forwarding Rule for the Tunnel**:
   ```bash
   gcloud compute forwarding-rules create [FORWARDING_RULE_NAME] \
       --region [REGION] \
       --ip-protocol ESP \
       --port-range 0-65535 \
       --target-vpn-gateway [VPN_GATEWAY_NAME]
   ```

**Step 3: Configure Firewall Rules**

1. **Create Firewall Rule**:
   ```bash
   gcloud compute firewall-rules create [RULE_NAME] \
       --network [NETWORK_NAME] \
       --allow tcp,udp,icmp \
       --source-ranges [SOURCE_IP_RANGES]
   ```

**Step 4: Configure On-Premises VPN Device**

- Configure the on-premises VPN device with the details you used in Google Cloud (IP address, IKE version, shared secret).

### **Additional Configuration**

- **Routing**: Ensure that the routing configuration is set up to direct traffic to and from the VPN tunnel. You may need to add routes in Google Cloud and on your on-premises network to properly handle traffic.
- **Monitoring**: Use Cloud Monitoring to track the status and performance of your VPN connections.

By following these steps, you’ll set up a VPN gateway in Google Cloud, configure it with a tunnel, and ensure that it communicates securely with your on-premises infrastructure.