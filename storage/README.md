# Azure Storage - AZ-104 Study Guide

This module covers **Azure Storage** services, including storage accounts, blob storage, file shares, data protection, replication, and advanced security configurations. This guide will help you develop a solid foundation and progress to advanced topics in Azure Storage, preparing you for real-world Azure administration and the AZ-104 certification exam.

---

## 2-Week Study Plan (4 Hours per Day)

### Week 1: Fundamentals and Core Azure Storage Services

#### **Day 1: Introduction to Azure Storage Accounts**
- **Topics Covered**:
  - Overview of Azure Storage services and types of storage accounts.
  - Configuring storage accounts and understanding storage tiers.
  - Storage account replication options (LRS, GRS, ZRS, RA-GRS).
- **Objectives**:
  - Understand the purpose and types of Azure storage accounts.
  - Create and configure storage accounts with different replication and performance tiers.
- **Study Tasks**:
  - **Reading**:
    - [Azure Storage Overview](https://learn.microsoft.com/en-us/azure/storage/common/storage-introduction)
    - [Types of Storage Accounts](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview)
  - **Lab**:
    - Create a Standard and Premium storage account.
    - Configure replication options and observe how they affect availability and durability.

---

#### **Day 2: Azure Blob Storage - Basics**
- **Topics Covered**:
  - Understanding blob storage and storage tiers (hot, cool, archive).
  - Creating and managing containers and blobs.
  - Access levels for containers and blobs.
- **Objectives**:
  - Learn to create and configure blob containers.
  - Understand the use cases for each storage tier.
- **Study Tasks**:
  - **Reading**:
    - [Introduction to Blob Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)
    - [Azure Blob Storage Tiers](https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview)
  - **Lab**:
    - Create a blob container and upload blobs with different access levels.
    - Experiment with setting blob access to public, private, and blob-level permissions.

---

#### **Day 3: Azure Files and File Shares**
- **Topics Covered**:
  - Creating and managing Azure File shares.
  - Understanding SMB and NFS protocols in Azure Files.
  - Accessing Azure Files from Windows and Linux.
- **Objectives**:
  - Set up and access Azure File shares for different use cases.
- **Study Tasks**:
  - **Reading**:
    - [Introduction to Azure Files](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-introduction)
    - [SMB and NFS support in Azure Files](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-faq)
  - **Lab**:
    - Create an Azure File share and mount it on a Windows and Linux machine.
    - Configure different access permissions for shared files.

---

#### **Day 4: Securing Storage Accounts and Data**
- **Topics Covered**:
  - Storage account security features: shared access signatures (SAS), storage account keys.
  - Implementing RBAC on storage resources.
- **Objectives**:
  - Secure Azure storage accounts using best practices for access control.
- **Study Tasks**:
  - **Reading**:
    - [Secure Access to Storage Accounts](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-security)
    - [RBAC for Storage Accounts](https://learn.microsoft.com/en-us/azure/storage/common/storage-auth)
  - **Lab**:
    - Generate SAS tokens for limited access to blob storage.
    - Set up RBAC for different roles on storage resources.

---

#### **Day 5: Data Redundancy and Replication in Azure Storage**
- **Topics Covered**:
  - Data redundancy models in Azure (LRS, GRS, ZRS).
  - How replication works for high availability and durability.
- **Objectives**:
  - Understand and configure data redundancy options.
- **Study Tasks**:
  - **Reading**:
    - [Redundancy Options in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy)
  - **Lab**:
    - Experiment with different replication options in a storage account.
    - Configure a storage account for geo-redundant storage (GRS) and observe behavior.

---

#### **Day 6: Lifecycle Management and Automation**
- **Topics Covered**:
  - Azure Blob lifecycle management policies.
  - Automating blob tier transitions and deletion.
- **Objectives**:
  - Configure lifecycle management policies for blob data.
- **Study Tasks**:
  - **Reading**:
    - [Blob Lifecycle Management Policies](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-lifecycle-management-concepts)
  - **Lab**:
    - Set up a lifecycle policy to automatically transition blobs between tiers based on access patterns.

---

#### **Day 7: Backup and Recovery for Azure Storage**
- **Topics Covered**:
  - Backup options for Azure storage accounts.
  - Restoring deleted blobs and managing data recovery.
- **Objectives**:
  - Implement backup and recovery strategies for storage.
- **Study Tasks**:
  - **Reading**:
    - [Azure Storage Backup Options](https://learn.microsoft.com/en-us/azure/backup/backup-introduction-to-azure-backup)
  - **Lab**:
    - Enable soft delete for blobs and test blob deletion and recovery.

---

### Week 2: Advanced and Expert-Level Azure Storage Topics

#### **Day 8: Azure Storage Performance and Cost Optimization**
- **Topics Covered**:
  - Optimizing storage performance for different workloads.
  - Cost management with storage tiers and lifecycle policies.
- **Objectives**:
  - Configure storage accounts for optimized cost and performance.
- **Study Tasks**:
  - **Reading**:
    - [Performance Tiers for Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-performance-tiers)
    - [Cost Management in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-pricing)
  - **Lab**:
    - Adjust storage tiering for cost optimization and observe performance impacts.

---

#### **Day 9: Monitoring and Diagnostics for Azure Storage**
- **Topics Covered**:
  - Monitoring storage performance and diagnostics using Azure Monitor.
  - Configuring alerts and diagnostics for storage resources.
- **Objectives**:
  - Set up monitoring and alerts for storage account performance and health.
- **Study Tasks**:
  - **Reading**:
    - [Monitoring Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-monitor-storage-account)
  - **Lab**:
    - Enable monitoring and diagnostics for a storage account and configure custom alerts.

---

#### **Day 10: Encryption and Data Security in Azure Storage**
- **Topics Covered**:
  - Encryption at rest, encryption in transit, and customer-managed keys.
  - Advanced encryption configurations for sensitive data.
- **Objectives**:
  - Implement encryption options to secure Azure Storage.
- **Study Tasks**:
  - **Reading**:
    - [Encryption in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption)
  - **Lab**:
    - Configure customer-managed keys (CMK) for data encryption in a storage account.

---

#### **Day 11: Azure File Sync and Hybrid Storage Solutions**
- **Topics Covered**:
  - Setting up Azure File Sync to extend on-premises file servers to Azure.
  - Configuring hybrid storage solutions.
- **Objectives**:
  - Implement Azure File Sync for hybrid cloud storage scenarios.
- **Study Tasks**:
  - **Reading**:
    - [Azure File Sync Overview](https://learn.microsoft.com/en-us/azure/storage/files/storage-sync-files-deployment-guide)
  - **Lab**:
    - Set up Azure File Sync and synchronize an on-premises server with an Azure file share.

---

#### **Day 12: Access Control and Private Endpoints for Storage Security**
- **Topics Covered**:
  - Using private endpoints to secure storage accounts in virtual networks.
  - Configuring advanced access control with network security features.
- **Objectives**:
  - Implement network-level security for storage accounts.
- **Study Tasks**:
  - **Reading**:
    - [Private Endpoint for Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-private-endpoints)
  - **Lab**:
    - Create a private endpoint for a storage account and secure access within a virtual network.

---

#### **Day 13: Advanced Blob Storage Features - Append Blobs, Immutable Blobs**
- **Topics Covered**:
  - Append blobs for logging and auditing scenarios.
  - Immutable storage for regulatory compliance.
- **Objectives**:
  - Configure and use advanced blob types for specialized use cases.
- **Study Tasks**:
  - **Reading**:
    - [Append Blobs and Immutable Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-append)
  - **Lab**:
    - Create append blobs and test use cases for log storage.
    - Enable immutable storage on a container for compliance purposes.

---

#### **Day 14: Review and Practice Assessment**
- **Topics Covered**:
  - Review all key Azure Storage concepts.
  - Complete
