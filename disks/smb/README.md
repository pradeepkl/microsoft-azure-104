# Azure SMB File Share Lab Guide

## Objective

This lab provides step-by-step instructions to:
1. Create an **SMB file share in Azure Files**.
2. Set up **two Windows VMs** in different availability zones.
3. Configure **Network Security Group (NSG) rules** for controlled access.
4. Test access using **Service Endpoint** and **Private Endpoint**.
5. Clean up all resources.

## Prerequisites
- An Azure subscription with appropriate permissions.
- Basic familiarity with Azure Portal.

---

## Lab Steps

### Step 1: Create a Premium Storage Account

1. Go to the **Azure Portal**.
2. Select **Create a resource** > **Storage account**.
3. **Basics Tab**:
   - **Subscription**: Select your subscription.
   - **Resource Group**: Create a new resource group (e.g., `SMBLabResourceGroup`).
   - **Storage account name**: Enter a unique name (e.g., `smbstorageaccount`).
   - **Region**: Choose a region that supports Availability Zones.
   - **Performance**: Select **Premium**.
   - **Redundancy**: Select **Locally-redundant storage (LRS)**.
   - **Primary service**: Select **Azure Files**.
4. Click **Review + Create** and then **Create**.

### Step 2: Create an SMB File Share in the Storage Account

1. Once the storage account is deployed, go to the **Storage Account**.
2. Under **Data storage**, select **File shares** > **+ File share**.
3. **Name**: Enter a name for the file share (e.g., `smb-share`).
4. **Protocol**: Choose **SMB**.
5. **Quota**: Set the desired storage limit (e.g., 100 GB).
6. Click **Create**.

### Step 3: Configure the Storage Account Settings

1. Go to **Configuration** under **Settings** for the storage account.
2. Ensure **Secure transfer required** is set to **Enabled** (recommended for SMB).
3. Click **Save**.

### Step 4: Create a Virtual Network and Subnet

1. In the **Azure Portal**, go to **Virtual networks** > **+ Create**.
2. **Basics Tab**:
   - **Subscription**: Select your subscription.
   - **Resource Group**: Select `SMBLabResourceGroup`.
   - **Name**: Enter a name (e.g., `SMBLabVNet`).
   - **Region**: Match the storage account’s region.
3. **IP Addresses Tab**:
   - **Address space**: Set to `10.1.0.0/16`.
   - **Subnet**: Create a subnet named `default` with `10.1.0.0/24`.
4. Click **Review + Create** and then **Create**.

### Step 5: Create Two Windows VMs in Different Availability Zones

1. **Create the First VM**:
   - Go to **Virtual machines** > **+ Create**.
   - **Resource Group**: `SMBLabResourceGroup`.
   - **Name**: `WinVM1`.
   - **Region**: Match the storage account’s region.
   - **Availability zone**: Zone 1.
   - **Image**: Choose **Windows Server 2019 Datacenter**.
   - **Size**: Select a Standard size (e.g., Standard D2s_v3).
   - **Authentication type**: Password (set a secure password).
   - **Virtual Network**: Select `SMBLabVNet`.
   - **Subnet**: Select `default`.
   - **Public inbound ports**: Allow **RDP (port 3389)**.
   - Click **Review + Create** and **Create**.

2. **Create the Second VM** in Zone 2:
   - Follow the same steps, naming the VM `WinVM2` and selecting **Availability zone** 2.

### Step 6: Configure Network Security Group (NSG) Rules

1. Go to **Network Security Groups** in the portal and select the NSG associated with the `default` subnet in `SMBLabVNet`.
2. **Outbound Security Rule**:
   - **Destination**: `Service Tag: Storage`.
   - **Destination Port**: `445` (for SMB).
   - **Protocol**: TCP.
   - **Action**: Allow.
3. **Inbound Security Rule**:
   - Configure inbound rules to allow RDP (port 3389) for VM access.

### Step 7: Configure and Test Access Using Service Endpoint

1. **Enable Service Endpoint** for Microsoft.Storage on the `default` subnet:
   - Go to **Virtual Networks** > `SMBLabVNet` > **Subnets** > `default`.
   - Under **Service Endpoints**, add **Microsoft.Storage**.
2. **Add VNet Access to Storage Account**:
   - Go to the storage account > **Networking** > **Firewalls and virtual networks**.
   - Set **Allow access from** to **Selected networks**.
   - Add `SMBLabVNet` to the list of allowed networks.
3. **Connect to SMB Share from Windows VMs**:
   - Connect to each VM via **RDP**.
   - Open **File Explorer** and click on **This PC** > **Map network drive**.
   - Enter the path to the SMB share:
     ```
     \\<storage_account_name>.file.core.windows.net\smb-share
     ```
   - Select **Connect using different credentials** and enter:
     - **Username**: `Azure\<storage_account_name>`
     - **Password**: Access key from **Storage Account** > **Access keys**.
   - Verify access by creating files on the SMB share.

### Step 8: Configure and Test Access Using Private Endpoint

1. **Create a Private Endpoint** for the storage account:
   - Go to **Storage Account** > **Networking** > **Private endpoint connections** > **+ Private endpoint**.
   - Select the storage account and `file` resource type.
   - Choose `SMBLabVNet` and `default` subnet.
2. **Configure DNS** (if necessary):
   - Ensure the Windows VMs can resolve the storage account name to the private IP.
   - Use Azure Private DNS or set a custom DNS entry to resolve `<storage_account_name>.file.core.windows.net` to the private IP.
3. **Connect to SMB Share via Private Endpoint**:
   - In each VM, open **File Explorer** and map the network drive again using the same path:
     ```
     \\<storage_account_name>.file.core.windows.net\smb-share
     ```
   - Use the same credentials (`Azure\<storage_account_name>` and the storage account key).
   - Verify the connection works through the private IP.

### Step 9: Clean Up Resources

1. **Disconnect the SMB Share** from each VM:
   - In **File Explorer**, right-click the network drive and select **Disconnect**.
2. **Delete the Resources**:
   - Go to **Resource groups** in Azure Portal.
   - Select `SMBLabResourceGroup`.
   - Click **Delete resource group** to delete all resources (storage account, VMs, VNet, etc.).

---

## Summary

- **Storage Account and SMB File Share Creation**:
  - Created a premium storage account and configured an SMB file share.

- **Network Setup**:
  - Set up a virtual network with two Windows VMs in different availability zones.

- **Network Security**:
  - Configured NSG rules to allow SMB access and tested connectivity using both Service Endpoints and Private Endpoints.

- **Cleanup**:
  - Disconnected SMB shares from each VM and deleted all resources to avoid incurring ongoing costs.
