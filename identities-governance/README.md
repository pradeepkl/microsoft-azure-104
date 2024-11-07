# Identities and Governance - AZ-104 Study Guide

This module covers **Azure Identity and Governance** services, focusing on Azure Active Directory (Azure AD), Role-Based Access Control (RBAC), Azure Policy, and subscription/resource management. These skills are essential for managing identity, access, and compliance across Azure environments.

---

## Weekly Study Plan (4 Hours per Day)

### Day 1: Azure Active Directory Overview and User Management
- **Topics Covered**:
  - Introduction to Azure AD and its role as an identity provider.
  - Core differences between Azure AD and on-premises Active Directory.
  - Managing Azure AD users and groups.
- **Objectives**:
  - Understand Azure AD basics and how it supports identity and access management in Azure.
  - Create, manage, and configure users and groups in Azure AD.
- **Study Tasks**:
  - **Reading**:
    - [Introduction to Azure AD](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis)
    - [Create, delete, and manage Azure AD users](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/add-users-azure-active-directory)
  - **Lab**:
    - Create several users and groups in Azure AD.
    - Practice adding users to groups, modifying user attributes, and resetting passwords.

---

### Day 2: Role-Based Access Control (RBAC) in Azure
- **Topics Covered**:
  - Azure RBAC for managing access to Azure resources.
  - Assigning built-in roles and understanding role scopes.
  - Least privilege principle.
- **Objectives**:
  - Apply RBAC to restrict access to resources.
  - Understand the hierarchy and scope of roles in Azure.
- **Study Tasks**:
  - **Reading**:
    - [Role-Based Access Control in Azure](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)
    - [Built-in roles for RBAC](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)
  - **Lab**:
    - Assign roles (e.g., Reader, Contributor) to users and groups at different scopes (resource group, resource).
    - Test access permissions by assigning the roles and verifying user access.

---

### Day 3: Conditional Access Policies
- **Topics Covered**:
  - Conditional Access basics and policy creation.
  - Implementing Multi-Factor Authentication (MFA) and location-based access.
- **Objectives**:
  - Configure Conditional Access policies to enforce MFA and other access controls.
  - Test Conditional Access scenarios for common use cases.
- **Study Tasks**:
  - **Reading**:
    - [Introduction to Conditional Access](https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/overview)
    - [Set up Conditional Access policies](https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/howto-conditional-access-policy-all-users-mfa)
  - **Lab**:
    - Create a Conditional Access policy to require MFA for a test user or group.
    - Test the policy by signing in with and without MFA requirements.

---

### Day 4: Azure AD Connect and Hybrid Identity
- **Topics Covered**:
  - Azure AD Connect for synchronizing on-premises AD with Azure AD.
  - Hybrid identity fundamentals.
- **Objectives**:
  - Configure Azure AD Connect for a hybrid identity setup.
  - Understand the different authentication methods (Pass-through Authentication, Seamless SSO).
- **Study Tasks**:
  - **Reading**:
    - [Azure AD Connect Overview](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect)
    - [Hybrid Identity with Azure AD](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/choose-ad-authn)
  - **Lab**:
    - Review the installation steps for Azure AD Connect.
    - If feasible, set up a test environment for synchronizing users from an on-premises AD.

---

### Day 5: Administrative Units and Delegated Administration
- **Topics Covered**:
  - Administrative Units (AUs) and their role in organizing users and groups.
  - Delegated administration for role-based access at different scopes.
- **Objectives**:
  - Set up Administrative Units to manage subsets of users and resources.
  - Delegate administration roles for decentralized management.
- **Study Tasks**:
  - **Reading**:
    - [Azure AD Administrative Units](https://learn.microsoft.com/en-us/azure/active-directory/roles/admin-units)
    - [Delegate access and manage access permissions](https://learn.microsoft.com/en-us/azure/active-directory/roles/delegate-access-portal)
  - **Lab**:
    - Create an Administrative Unit and assign it to a specific department or group.
    - Assign role-based permissions within the AU for scoped management.

---

### Day 6: Azure Policy and Compliance
- **Topics Covered**:
  - Azure Policy basics for enforcing governance at scale.
  - Using initiatives and assigning policies for compliance.
- **Objectives**:
  - Create and assign policies to enforce compliance across resources.
  - Use policy definitions and initiatives to apply organizational standards.
- **Study Tasks**:
  - **Reading**:
    - [Overview of Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview)
    - [Azure Policy definition structure](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure)
  - **Lab**:
    - Create a policy to restrict VM sizes or enforce tag compliance.
    - Apply the policy to a resource group and verify enforcement.

---

### Day 7: Subscription and Resource Management
- **Topics Covered**:
  - Managing Azure subscriptions and resource groups.
  - Resource tagging and organization for cost management.
- **Objectives**:
  - Organize resources with tagging and manage subscriptions efficiently.
  - Implement best practices for resource management in large environments.
- **Study Tasks**:
  - **Reading**:
    - [Organize resources with resource groups and tags](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)
    - [Manage Azure subscriptions](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/manage-subscriptions)
  - **Lab**:
    - Create and manage resource groups with consistent tags.
    - Set up a basic cost management report for subscription tracking.

---

## Additional Resources

- **Microsoft Learn Paths**:
  - [Manage identities and governance in Azure](https://docs.microsoft.com/en-us/learn/paths/az-104-manage-identities-governance/)
  - [Azure Active Directory Documentation](https://docs.microsoft.com/en-us/azure/active-directory/)
- **Azure Documentation**: [Azure Identity and Access Management](https://docs.microsoft.com/en-us/azure/security/fundamentals/identity-management-overview)

---

This module covers foundational and intermediate concepts of Azure identity and governance, preparing you to confidently manage identity, access, and compliance on Azure. Follow each day’s study plan and complete the labs to solidify your understanding.

Happy studying!
