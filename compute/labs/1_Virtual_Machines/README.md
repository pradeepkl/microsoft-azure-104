# Virtual Machines (VMs) Basics - AZ-104 Study Guide

## Overview
This module introduces **Azure Virtual Machines (VMs)**, covering foundational topics such as VM deployment, configuration, connection, and basic management. Additionally, you’ll learn about key pairs, instance types, and organizing VMs within resource groups. Azure VMs provide on-demand, scalable computing resources and are commonly used for running applications, databases, development environments, and more.

## Learning Objectives
By the end of this module, you should be able to:
- Understand Azure VM concepts, VM sizes (instance types), and pricing options.
- Deploy Azure VMs using the Azure Portal and configure resource groups for organization.
- Generate and use SSH key pairs for secure authentication to Linux VMs.
- Configure basic VM settings such as disk size and networking.
- Connect to VMs using RDP (for Windows) or SSH (for Linux).
- Start, stop, and resize VMs as needed.

## Study Plan (4 hours)

### 1. Introduction to Azure VMs and Instance Types (30 minutes)
   - **Topics**:
     - Overview of Azure VMs and their use cases.
     - VM series, instance types (sizes), and pricing options.
   - **Resources**:
     - [Introduction to Azure Virtual Machines](https://learn.microsoft.com/en-us/azure/virtual-machines/)
     - [Azure VM Sizes](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes)

### 2. Setting Up SSH Key Pairs (30 minutes)
   - **Topics**:
     - Generating and using SSH key pairs for secure Linux VM access.
     - Key-based authentication for enhanced security.
   - **Resources**:
     - [Create and Use SSH Key Pairs](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed)

### 3. Deploying a Virtual Machine in a Resource Group (45 minutes)
   - **Topics**:
     - Creating and organizing VMs within resource groups.
     - VM configuration options: region, size, OS type, and authentication.
   - **Resources**:
     - [Create a Linux Virtual Machine in Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)
     - [Create a Windows Virtual Machine in Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal)
     - [Resource Groups Overview](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)

### 4. Configuring VM Networking (45 minutes)
   - **Topics**:
     - Configuring network interfaces and assigning public/private IPs.
     - Setting up Network Security Groups (NSGs) to control VM traffic.
   - **Resources**:
     - [Network Security Groups](https://learn.microsoft.com/en-us/azure/virtual-network/security-overview)

### 5. Connecting to VMs (30 minutes)
   - **Topics**:
     - Accessing a Windows VM using RDP.
     - Connecting to a Linux VM using SSH.
   - **Resources**:
     - [Connect to a Windows VM](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/connect-rdp)
     - [Connect to a Linux VM](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows)

### 6. Managing VM States and Resizing (30 minutes)
   - **Topics**:
     - Starting, stopping, restarting, and resizing VMs.
     - VM state management and cost considerations.
   - **Resources**:
     - [Resize a Virtual Machine](https://learn.microsoft.com/en-us/azure/virtual-machines/resize-vm)

### 7. Hands-On Labs (1 hour)
   - See the **Labs** section below for step-by-step instructions.

---

## Labs

### Lab 1: Generate an SSH Key Pair

**Objective**: Create an SSH key pair to use for secure authentication with Linux VMs.

#### Steps
1. **Open Terminal**:
   - On a **Linux** or **macOS** system, open a terminal.
   - On **Windows**, open PowerShell or use an SSH client.

2. **Generate SSH Key Pair**:
   - Run the following command to generate an SSH key pair (adjust the file path as needed):
     ```bash
     ssh-keygen -t rsa -b 2048 -f ~/.ssh/azure_key
     ```
   - Press **Enter** to accept the default file location.
   - Set an optional passphrase for additional security.

3. **Verify Key Pair**:
   - You should now have two files: `azure_key` (private key) and `azure_key.pub` (public key).
   - Use the public key (`azure_key.pub`) when creating a VM for SSH access.

---

### Lab 2: Create and Configure a Virtual Machine in a Resource Group

**Objective**: Deploy a new virtual machine in Azure within a specific resource group and configure its settings.

#### Steps
1. **Sign in to Azure Portal**:
   - Go to [https://portal.azure.com](https://portal.azure.com) and log in.

2. **Create a New Resource Group**:
   - In the Azure Portal, search for **Resource Groups**.
   - Click **+ Create** and provide the following information:
     - **Subscription**: Select your subscription.
     - **Resource Group Name**: Enter a name (e.g., `MyVMResourceGroup`).
     - **Region**: Choose a region (e.g., East US).
   - Click **Review + create** and then **Create**.

3. **Create a New VM**:
   - Go to **Virtual Machines** and click **+ Create**.
   - Configure the following settings:
     - **Subscription**: Select your subscription.
     - **Resource Group**: Choose the resource group you just created.
     - **Virtual Machine Name**: Enter a name (e.g., `MyLinuxVM`).
     - **Region**: Select the same region as the resource group.
     - **Image**: Choose an OS (e.g., Ubuntu Server 20.04 LTS for Linux).
     - **Size**: Select an instance type based on your needs (e.g., Standard B1s for testing).
     - **Authentication Type**: Choose **SSH public key** and paste in your public key from `azure_key.pub`.
     - **Username**: Enter a username.

4. **Configure Networking**:
   - Under the **Networking** tab, configure:
     - **Public IP**: Set to **Enabled** for remote access.
     - **Network Security Group**: Choose **Basic** and allow SSH (Linux) or RDP (Windows) access.

5. **Review and Create**:
   - Review the settings and click **Create** to deploy the VM in your resource group.

---

### Lab 3: Connect to the Virtual Machine

**Objective**: Connect to the VM you created using RDP (for Windows) or SSH (for Linux).

#### Steps
1. **Locate the VM's IP Address**:
   - Go to **Virtual Machines** in the Azure Portal.
   - Select your VM and find the **Public IP Address**.

2. **Connect to Linux VM (SSH)**:
   - Open a terminal and enter the following command, replacing `<public-ip>` and `<username>` with your VM's details:
     ```bash
     ssh -i ~/.ssh/azure_key <username>@<public-ip>
     ```
   - Accept the connection and enter the passphrase if prompted.

3. **Connect to Windows VM (RDP)**:
   - If using a Windows VM, open **Remote Desktop Connection**.
   - Enter the **Public IP Address** and log in using the credentials you set during VM creation.

---

### Lab 4: Start, Stop, and Resize the VM

**Objective**: Manage the VM’s power state and resize it as needed.

#### Steps
1. **Start and Stop the VM**:
   - In the **Virtual Machines** page, select your VM.
   - Use the **Start** and **Stop** buttons to control the VM's state.

2. **Resize the VM**:
   - With the VM in a **Stopped** state, go to **Size** in the VM’s left-hand menu.
   - Select a different size (e.g., resize to a higher tier for performance).
   - Click **Resize** and confirm.
   - Start the VM to apply the new size.

3. **Verify the VM Size**:
   - Go to the **Overview** tab to confirm the updated VM size.

---

## Additional Resources

- **[Azure Virtual Machines Documentation](https://learn.microsoft.com/en-us/azure/virtual-machines/)**
- **[Azure Pricing Calculator for VMs](https://azure.microsoft.com/pricing/calculator/)**

## Estimated Completion Time
- **Total Time**: Approximately 4 hours
