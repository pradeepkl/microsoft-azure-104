# Azure Block Storage Guide

This guide provides a comprehensive overview of Azure Block Storage, covering available storage types, their performance characteristics, real-world use cases, and a hands-on lab for various operations including creating, attaching, mounting, unmounting, snapshots, encryption, performance testing, and replication.

---

## Key Points

- **Azure Block Storage Types**:
  Azure offers several block storage types suited for a range of performance and cost requirements. From cost-effective **Standard HDD** to high-performance **Ultra Disk**, Azure's block storage options address various needs for IOPS, throughput, and latency.

- **Use Cases**:
  Each storage type has specific scenarios where it performs best. For example, **Standard HDD** is suitable for archival storage, while **Premium SSD** and **Ultra Disk** support high-performance applications like databases and analytics.

---

## Azure Block Storage Summary Table

| **Azure Storage Type** | **Max IOPS**             | **Max Throughput**        | **Latency**                     | **Use Cases**                                                                                     |
|------------------------|--------------------------|---------------------------|---------------------------------|--------------------------------------------------------------------------------------------------|
| **Standard HDD**       | Up to 500 IOPS           | Up to 60 MBps             | High (tens to hundreds of ms)   | Archival storage, infrequent access data, backups, non-critical storage needs, simple file storage |
| **Standard SSD**       | Up to 6,000 IOPS         | Up to 750 MBps            | Moderate (tens of ms)           | Web servers, application servers, development and test environments, boot disks                    |
| **Premium SSD**        | Up to 20,000 IOPS        | Up to 900 MBps            | Low (single-digit ms)           | Production databases, high-traffic web applications, transactional systems needing consistent performance |
| **Ultra Disk**         | Up to 160,000 IOPS       | Up to 4,000 MBps          | Very Low (sub-ms)               | High-performance databases (e.g., SAP HANA, SQL Server), high-frequency trading, real-time analytics, mission-critical applications |

---

## Lab Guide: Working with Azure Block Storage

This lab covers creating, attaching, mounting, unmounting, creating snapshots, enabling encryption, performance testing, resizing disks, and disk replication.

### Prerequisites
- **Azure Subscription**: Access to an active Azure subscription.
- **Azure CLI or Azure Portal**: You can perform these tasks using Azure CLI commands or through the Azure Portal.
- **Virtual Machine**: An existing Azure Virtual Machine to which the disk will be attached.

---

### Basic Operations

#### Step 1: Create a Managed Disk

1. **In Azure Portal**:
   - Go to **Azure Portal** > **Disks** > **Create Disk**.
   - Select the subscription, resource group, and provide a name for the disk.
   - Choose the **Disk Size** and **Performance** (Standard HDD, Standard SSD, or Premium SSD).
   - Select **Data Disk** for disk type (unless creating an OS disk).
   - Click **Review + create** and then **Create**.

2. **Using Azure CLI**:
   ```bash
   az disk create \
     --resource-group <YourResourceGroup> \
     --name <YourDiskName> \
     --size-gb <DiskSize> \
     --sku <Standard_LRS or Premium_LRS> \
     --zone <optional: zone number>
   ```
---
#### Step 2: Attach the Disk to a Virtual Machine

1. **In Azure Portal**:
   - Navigate to the **Virtual Machines** section.
   - Select the target **VM**.
   - Under **Settings**, select **Disks** and click **Add Data Disk**.
   - Choose the managed disk created in Step 1 from the dropdown.
   - Click **Save** to attach the disk.

2. **Using Azure CLI**:
   ```bash
   az vm disk attach \
     --resource-group <YourResourceGroup> \
     --vm-name <YourVMName> \
     --disk <YourDiskName>

  

#### Step 3: Mount the Disk on the VM (Linux Example)

After attaching the disk, log in to the VM and perform the following steps:

1. **Find the Disk**:
   ```bash
   lsblk
Locate the new disk (usually something like /dev/sdc).
```bash
sudo fdisk /dev/sdc

Press n for a new partition, choose defaults, and then w to write.

Format the Disk:

bash
Copy code
sudo mkfs -t ext4 /dev/sdc1
Mount the Disk:

bash
Copy code
sudo mkdir /mnt/mydisk
sudo mount /dev/sdc1 /mnt/mydisk
Add to /etc/fstab for Auto-Mounting:

bash

This command lists the available block devices. Locate the new disk (usually something like /dev/sdc).

Create a Partition:

bash
Copy code
sudo fdisk /dev/sdc
Press n to create a new partition.
Follow the prompts to accept the defaults, and then press w to write the changes.
Format the Disk:

bash
Copy code
sudo mkfs -t ext4 /dev/sdc1
This command formats the newly created partition with the ext4 filesystem.

Mount the Disk:

bash
Copy code
sudo mkdir /mnt/mydisk
sudo mount /dev/sdc1 /mnt/mydisk
This command mounts the disk to /mnt/mydisk.

Add to /etc/fstab for Auto-Mounting:

bash
Copy code
echo "/dev/sdc1 /mnt/mydisk ext4 defaults 0 0" | sudo tee -a /etc/fstab
This command ensures that the disk is automatically mounted after a reboot by adding an entry to /etc/fstab.

Additional Scenarios
Scenario 1: Disk Performance Testing
Install Performance Tool (Linux):

bash
Copy code
sudo apt-get install fio -y
Run Performance Test:

bash
Copy code
fio --name=test --filename=/mnt/mydisk/testfile --size=1G --time_based --runtime=60 --rw=randwrite --bs=4k --ioengine=libaio --direct=1 --numjobs=1 --iodepth=32
Scenario 2: Resizing a Managed Disk
Resize Disk:
bash
Copy code
az disk update --resource-group <YourResourceGroup> --name <YourDiskName> --size-gb <NewSize>
Scenario 3: Disk Replication Between Regions
Enable Replication:
bash
Copy code
az disk replication create --resource-group <YourResourceGroup> --source <YourDiskName> --replication-region <TargetRegion>
Scenario 4: Automated Snapshots
Create Snapshot Using CLI:

bash
Copy code
az snapshot create --resource-group <YourResourceGroup> --source <YourDiskName> --name <YourSnapshotName>
Automation: Use Azure Automation or Azure Logic Apps to schedule snapshots automatically.

Cleaning Up Resources
Detach and Delete Disks:

bash
Copy code
az vm disk detach --resource-group <YourResourceGroup> --vm-name <YourVMName> --name <YourDiskName>
az disk delete --resource-group <YourResourceGroup> --name <YourDiskName> --yes
Delete Snapshots:

bash
Copy code
az snapshot delete --resource-group <YourResourceGroup> --name <YourSnapshotName>


   
