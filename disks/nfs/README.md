# Azure NFS File Share Lab Guide

## Objective

This lab provides step-by-step instructions to:
1. Create an **NFS file share in Azure Files**.
2. Set up **two Linux VMs** in different availability zones.
3. Configure **Network Security Group (NSG) rules** for controlled access.
4. Test access using **Service Endpoint** and **Private Endpoint**.
5. Clean up all resources.

## Prerequisites
- An Azure subscription with appropriate permissions.
- Basic familiarity with Azure Portal and Linux command line.

---

## Lab Steps

### Step 1: Create a Premium Storage Account

1. Go to the **Azure Portal**.
2. Select **Create a resource** > **Storage account**.
3. **Basics Tab**:
   - **Subscription**: Select your subscription.
   - **Resource Group**: Create a new resource group (e.g., `NFSLabResourceGroup`).
   - **Storage account name**: Enter a unique name (e.g., `nfsstorageaccount`).
   - **Region**: Choose a region that supports Availability Zones.
   - **Performance**: Select **Premium**.
   - **Redundancy**: Select **Locally-redundant storage (LRS)**.
   - **Primary service**: Select **Azure Files**.
4. Click **Review + Create** and then **Create**.

### Step 2: Create an NFS File Share in the Storage Account

1. Once the storage account is created, navigate to the **Storage Account**.
2. Under **Data storage**, select **File shares** > **+ File share**.
3. **Name**: Enter a name for the file share (e.g., `nfs-share`).
4. **Protocol**: Select **NFS**.
5. **Root squash**: Choose **Root Squash** for enhanced security.
6. **Quota**: Set the desired storage limit (e.g., 100 GB).
7. Click **Create**.

### Step 3: Configure the Storage Account Settings

1. Go to **Configuration** under **Settings** for the storage account.
2. **Disable** the **Secure transfer required** setting (NFS doesn’t support HTTPS).
3. Click **Save**.

### Step 4: Create a Virtual Network and Subnet

1. In the **Azure Portal**, go to **Virtual networks** > **+ Create**.
2. **Basics Tab**:
   - **Subscription**: Select your subscription.
   - **Resource Group**: Select `NFSLabResourceGroup`.
   - **Name**: Enter a name (e.g., `NFSLabVNet`).
   - **Region**: Match the storage account’s region.
3. **IP Addresses Tab**:
   - **Address space**: Set to `10.0.0.0/16`.
   - **Subnet**: Create a subnet named `default` with `10.0.0.0/24`.
4. Click **Review + Create** and then **Create**.

### Step 5: Create Two Linux VMs in Different Availability Zones

1. **Create the First VM**:
   - Go to **Virtual machines** > **+ Create**.
   - **Resource Group**: `NFSLabResourceGroup`.
   - **Name**: `VM1`.
   - **Region**: Match the storage account’s region.
   - **Availability zone**: Zone 1.
   - **Image**: Choose **Ubuntu 20.04 LTS**.
   - **Size**: Select a Standard size (e.g., Standard D2s_v3).
   - **Authentication type**: Password or SSH.
   - **Virtual Network**: Select `NFSLabVNet`.
   - **Subnet**: Select `default`.
   - **Public inbound ports**: Allow **SSH (port 22)**.
   - Click **Review + Create** and **Create**.

2. **Create the Second VM** in Zone 2:
   - Follow the same steps, naming the VM `VM2` and selecting **Availability zone** 2.

### Step 6: Configure Network Security Group (NSG) Rules

1. Go to **Network Security Groups** in the portal and select the NSG associated with the `default` subnet in `NFSLabVNet`.
2. **Outbound Security Rule**:
   - **Destination**: `Service Tag: Storage`.
   - **Destination Port**: `2049` (for NFS).
   - **Protocol**: TCP.
   - **Action**: Allow.
3. **Inbound Security Rule**:
   - If necessary, configure inbound rules to allow SSH (port 22).

### Step 7: Configure and Test Access Using Service Endpoint

1. **Enable Service Endpoint** for Microsoft.Storage on the `default` subnet:
   - Go to **Virtual Networks** > `NFSLabVNet` > **Subnets** > `default`.
   - Under **Service Endpoints**, add **Microsoft.Storage**.
2. **Add VNet Access to Storage Account**:
   - Go to the storage account > **Networking** > **Firewalls and virtual networks**.
   - Set **Allow access from** to **Selected networks**.
   - Add `NFSLabVNet` to the list of allowed networks.
3. **Test NFS Mount**:
   - SSH into each VM.
   - Install NFS client: `sudo apt update && sudo apt install nfs-common`.
   - Mount the NFS share:
     ```bash
     sudo mount -t nfs -o vers=4.1 <storage_account_name>.file.core.windows.net:/nfs-share /mnt/nfs-share
     ```
   - Verify by creating files on `/mnt/nfs-share`.

### Step 8: Configure and Test Access Using Private Endpoint

1. **Create a Private Endpoint** for the storage account:
   - Go to **Storage Account** > **Networking** > **Private endpoint connections** > **+ Private endpoint**.
   - Select the storage account and `file` resource type.
   - Choose `NFSLabVNet` and `default` subnet.
2. **Configure DNS** (if necessary):
   - Ensure the VMs can resolve the storage account name to the private IP.
3. **Test NFS Mount via Private Endpoint**:
   - SSH into each VM and mount the NFS share again as done in Step 7.

### Step 9: Clean Up Resources

1. **Unmount the NFS share** from each VM:
   ```bash
   sudo umount /mnt/nfs-share
   ```
2. **Delete the Resources**:
   - Go to Resource groups in the Azure Portal.
   - Select NFSLabResourceGroup.
   - Click Delete resource group to remove all resources.

## Summary

- **Storage Account and NFS File Share Creation**:
  - Created a premium storage account with NFS support and configured the NFS file share.

- **Network Setup**:
  - Set up a virtual network with two VMs in different availability zones to simulate multi-zone access.

- **Network Security**:
  - Configured NSG rules to allow NFS access and tested connectivity using both Service Endpoints and Private Endpoints.

- **Cleanup**:
  - Unmounted the NFS share from each VM and deleted all resources to avoid incurring ongoing costs.
