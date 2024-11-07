# Azure AD Beginner to Intermediate Learning Plan

## Overview
This is a one-week learning plan for Azure Active Directory (Azure AD), designed for 4 hours of study per day. The plan covers core Azure AD concepts, user and group management, security, integration, and best practices, providing a solid foundation in Azure AD administration.

---

### **Day 1: Core Azure AD Concepts and Initial Setup**
- **Azure AD Overview** (30 mins): Understanding Azure AD fundamentals, differences from traditional AD, and key benefits.
- **Licensing** (30 mins): Overview of Azure AD Free, P1, and P2 licenses.
- **User and Group Creation** (60 mins): 
  - Hands-on: Add cloud-only users, manage user attributes, and set up basic groups.
  - Create dynamic groups and set up sample dynamic memberships.
- **Azure AD Connect Overview** (30 mins): Introduction to hybrid identity, AD Connect, and identity synchronization basics.
- **Lab** (90 mins): Set up a test tenant, create users, configure dynamic groups, and explore Azure AD Connect options.

---

### **Day 2: External Collaboration and Access Controls**
- **Guest Users and Azure AD B2B** (45 mins): Explore B2B capabilities, inviting guest users, and configuring collaboration settings.
- **Self-Service Password Reset (SSPR)** (30 mins): Enable SSPR and review configuration options.
- **Multi-Factor Authentication (MFA)** (60 mins):
  - Enable and configure MFA for specific users and groups.
  - Configure authentication methods (phone, email, authenticator app).
- **Lab** (105 mins): 
  - Invite guest users, configure guest access restrictions, and test SSPR and MFA.
  - Explore SSPR options and troubleshoot MFA scenarios.

---

### **Day 3: Conditional Access and Identity Protection**
- **Conditional Access Overview** (45 mins): Introduction to Conditional Access policies, use cases, and planning.
- **Creating Policies** (75 mins): 
  - Set up policies based on user, device, location, and app conditions.
  - Require MFA, block risky sign-ins, and limit access by location.
- **Identity Protection Essentials** (45 mins): Configure risk policies for risky sign-ins and risky users.
- **Lab** (75 mins): 
  - Create and test Conditional Access policies.
  - Enable Identity Protection and test configurations for user and sign-in risk policies.

---

### **Day 4: Role-Based Access Control (RBAC) and Privileged Identity Management (PIM)**
- **RBAC Overview** (30 mins): Learn about built-in roles, custom roles, and how to assign roles at tenant and resource levels.
- **Role Assignment and Custom Roles** (60 mins): 
  - Apply least privilege.
  - Create a custom role and assign it.
- **Privileged Identity Management (PIM) Introduction** (45 mins): Configure PIM for just-in-time access for sensitive roles.
- **Administrative Units (AUs)** (30 mins): Learn to create AUs to organize users and delegate permissions.
- **Lab** (75 mins): 
  - Assign roles, create custom roles, configure PIM, and manage role activations.
  - Create AUs, assign administrative roles within AUs, and test scoped access limitations.

---

### **Day 5: Application Integration and Single Sign-On (SSO)**
- **Enterprise Application Basics** (30 mins): Overview of SaaS integration and SSO with Azure AD.
- **Adding and Configuring Applications** (60 mins): Set up applications, explore API permissions, and assign users.
- **Single Sign-On (SSO) Configurations** (45 mins): 
  - Set up SSO with password-based, SAML, and OpenID Connect.
  - Explore SSO settings and permissions.
- **Azure AD Application Proxy** (45 mins): Introduction to Application Proxy for secure access to on-premises applications.
- **Lab** (60 mins): 
  - Integrate a SaaS app with SSO, configure permissions, and test user access.
  - Set up an Application Proxy and secure with Azure AD pre-authentication.

---

### **Day 6: Monitoring, Alerts, and Compliance Auditing**
- **Audit Logs and Sign-In Logs** (45 mins): Explore Azure AD’s logging options.
- **Alerting and Monitoring with Azure Monitor** (45 mins): Set up alerts for critical events like failed sign-ins.
- **Access Reviews and Identity Governance** (60 mins): 
  - Set up access reviews for groups and applications.
  - Use Identity Governance for lifecycle and compliance management.
- **Lab** (90 mins): 
  - Configure alerts, view audit logs, set up access reviews, and test lifecycle management settings.

---

### **Day 7: Managed Identities, Best Practices, and Wrap-Up**
- **Managed Identities Overview** (30 mins): Introduction to system-assigned and user-assigned managed identities.
- **Configuring Managed Identities** (45 mins): Configure and use managed identities with services like Azure Key Vault.
- **Security Best Practices** (60 mins): Review key security recommendations:
  - Least privilege, MFA, Conditional Access policies, and guest access management.
- **Final Lab and Review** (105 mins): 
  - Practice setting up managed identities, securing apps with Key Vault, and reviewing key concepts.
  - Summary and additional resources for continued learning.

---

## Additional Resources
- **Microsoft Learn**: Explore learning paths on Azure AD.
- **Azure Documentation**: Detailed guides on each feature.
- **Microsoft Docs Labs**: Practice hands-on with Azure-provided labs.
