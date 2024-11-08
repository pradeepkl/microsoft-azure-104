# Azure Entra ID Lab Guide

## Table of Contents
1. [Creating a User in Azure Entra ID](#1-creating-a-user-in-azure-entra-id)
2. [Setting Up Multi-Factor Authentication (MFA)](#2-setting-up-multi-factor-authentication-mfa)
3. [Enabling Self-Service Password Reset (SSPR)](#3-enabling-self-service-password-reset-sspr)
4. [Creating a Group](#4-creating-a-group)
5. [Creating Dynamic Groups](#5-creating-dynamic-groups)
6. [Conditional Access Policies](#6-conditional-access-policies)
7. [Managing Privileged Identity Management (PIM)](#7-managing-privileged-identity-management-pim)
8. [Configuring Identity Protection](#8-configuring-identity-protection)
9. [Application Registration and Single Sign-On (SSO) Setup](#9-application-registration-and-single-sign-on-sso-setup)
10. [Federated User Setup](#10-federated-user-setup)
11. [Using Managed Identities for Azure Resources](#11-using-managed-identities-for-azure-resources)
12. [Configuring Password Policy in Azure Entra ID](#12-configuring-password-policy-in-azure-entra-id)

---

## 1. Creating a User in Azure Entra ID

**Objective**: Create a user in Azure Entra ID who will be used in subsequent labs for authentication and access control.

### Steps:
1. Log in to the [Azure Portal](https://portal.azure.com).
2. Navigate to **Azure Active Directory** > **Users**.
3. Click **+ New user**, then select **Create user**.
4. Enter the user’s **Username**, **Name**, and **Password**.
5. Configure additional details as needed and click **Create**.

---

## 2. Setting Up Multi-Factor Authentication (MFA)

**Objective**: Add an extra layer of security by enforcing Multi-Factor Authentication (MFA) for users.

### Steps:
1. Navigate to **Azure Active Directory** > **Security** > **Multi-Factor Authentication**.
2. Under **Per-user MFA**, find the user to enforce MFA for.
3. Click on the user, then select **Enable**.
4. Confirm the setting. The user will be prompted to set up MFA on their next sign-in.

---

## 3. Enabling Self-Service Password Reset (SSPR)

**Objective**: Allow users to reset their own passwords, reducing helpdesk support requests.

### Steps:
1. In the Azure Portal, go to **Azure Active Directory** > **Password reset**.
2. Under **Properties**, enable **Self-service password reset** for **Selected** or **All** users.
3. Set **Authentication methods** like email or SMS.
4. Save changes. Users can now reset their passwords at the password reset page.

---

## 4. Creating a Group

**Objective**: Set up a group for easier permission management.

### Steps:
1. Go to **Azure Active Directory** > **Groups** > **+ New group**.
2. Set **Group type** to **Security**.
3. Provide a **Group name** and optionally, a **Description**.
4. Click **Create**. You’ll use this group for permissions management in upcoming labs.

---

## 5. Creating Dynamic Groups

**Objective**: Create a dynamic group that automatically adds or removes members based on specific criteria.

### Steps:
1. Go to **Azure Active Directory** > **Groups** > **+ New group**.
2. Set **Group type** to **Security** and **Membership type** to **Dynamic User**.
3. Click **Add dynamic query** and build a rule (e.g., `(user.department -eq "Sales")`).
4. Save and create the group. Azure Entra ID will populate the group based on your rule.

---

## 6. Conditional Access Policies

**Objective**: Enforce security policies for users based on specific conditions.

### Steps:
1. In the Azure Portal, go to **Azure Active Directory** > **Security** > **Conditional Access**.
2. Click **+ New policy**, name it, and define **Assignments** like users and apps.
3. Under **Conditions**, set parameters (e.g., location) and **Access Controls** (e.g., **Require MFA**).
4. Set the policy to **On** and click **Create**.

---

## 7. Managing Privileged Identity Management (PIM)

**Objective**: Enforce time-limited access for users in high-privilege roles.

### Steps:
1. Go to **Azure AD Privileged Identity Management**.
2. Under **Manage**, select **Azure AD roles** or **Azure resource roles**.
3. Click **+ Add assignments**, select the desired role, and set it as **Eligible**.
4. Save the changes to enforce just-in-time role activation.

---

## 8. Configuring Identity Protection

**Objective**: Configure policies that react to identity-based risks, such as blocking access or requiring MFA.

### Steps:
1. Go to **Azure Active Directory** > **Security** > **Identity Protection**.
2. Open **User risk policy** and **Sign-in risk policy**.
3. Configure each policy to block or require MFA based on risk level.
4. Save the settings. Monitor risky sign-ins in **Identity Protection** > **Risky users**.

---

## 9. Application Registration and Single Sign-On (SSO) Setup

**Objective**: Register an application and configure SSO to streamline user access.

### Steps:
1. In **Azure Active Directory**, go to **App registrations** > **+ New registration**.
2. Enter **Name** and **Redirect URI** for your application.
3. Click **Register** and configure **Authentication** settings under **App registrations**.
4. Go to **Enterprise applications** > **Single sign-on** and choose the appropriate method (e.g., SAML, OAuth2).
5. Follow prompts to complete SSO configuration. Test SSO by logging into the application.

---

## 10. Federated User Setup

**Objective**: Set up federated authentication, allowing users to authenticate through an external identity provider.

### Steps:
1. Set up an on-premises identity provider (e.g., AD FS) with the necessary trust configurations.
2. In the Azure Portal, go to **Azure Active Directory** > **External Identities**.
3. Under **All identity providers**, select **+ New SAML/WS-Fed identity provider**.
4. Enter the **Metadata URL** of the external identity provider and complete the configuration.
5. Configure user roles and permissions as needed. Users can now authenticate through the external provider.

---

## 11. Using Managed Identities for Azure Resources

**Objective**: Use managed identities to allow secure authentication of services without credentials.

### Steps:
1. Go to a resource (e.g., **Virtual Machines** or **App Services**).
2. Under **Settings**, select **Identity** and enable **System-assigned managed identity**.
3. In the target resource (e.g., **Key Vault**), grant access to the managed identity.
4. The application can now securely access resources using the managed identity without explicit credentials.

---

## 12. Configuring Password Policy in Azure Entra ID

**Objective**: Configure password policies in Azure Entra ID to enforce security requirements such as password length, complexity, and expiration.

### Lab Steps

1. **Log in to Azure Portal**
   - Go to [https://portal.azure.com](https://portal.azure.com) and log in with your administrator credentials.

2. **Navigate to Azure Active Directory** 
   - In the left sidebar, select **Azure Active Directory**.

3. **Access Security Settings**
   - Under **Security**, click on **Authentication methods**.
   - Select **Password protection** to view and configure password policies.

4. **Configure Password Policy Settings**
   - Under **Password protection settings**, review and adjust the following options:
     - **Lockout threshold**: Define the number of failed sign-in attempts before an account is locked.
     - **Lockout duration (seconds)**: Set the duration for which the account remains locked after exceeding the threshold.
   - Click **Save** after making changes.

5. **Set Password Complexity and Minimum Length Requirements (for Azure AD Cloud Only)**
   - Unfortunately, Azure Entra ID only enforces a built-in password policy for cloud-only accounts:
     - **Minimum Password Length**: 8 characters.
     - **Complexity Requirements**: Passwords must include three out of four character types (uppercase letters, lowercase letters, numbers, and symbols).
   - These default requirements apply automatically and cannot be modified further.

6. **Set Password Expiration (if applicable)**
   - **Note**: For cloud-only users, passwords do not expire by default. To change this setting:
     - Go to **Azure Active Directory** > **Users**.
     - Select **Password reset** > **Properties**.
     - Enable **Self-service password reset** if not already enabled.
     - Click on **Password expiration policy**.
     - Set the desired **Number of days until password expires** and **Days before expiration to notify users**.
     - Click **Save**.

7. **Enforcing Password Policies in a Hybrid Environment (Optional)**
   - If your environment includes on-premises Active Directory and you’ve configured Azure AD Connect, you can synchronize on-premises password policies to Azure Entra ID.
   - In this case, your on-premises Active Directory password policies (set in Group Policy) will apply to synchronized users in Azure Entra ID.

8. **Testing the Policy**
   - Inform users about the updated password policy settings.
   - Have a test user try changing their password to verify that the policy is enforced as expected.

> **Note**: Password protection in Azure Entra ID also includes protection against commonly used or easily guessed passwords through banned password lists.

---

This guide provides an incremental approach to setting up and exploring Azure Entra ID’s advanced identity management capabilities, covering everything from user creation to federated authentication and conditional access.
