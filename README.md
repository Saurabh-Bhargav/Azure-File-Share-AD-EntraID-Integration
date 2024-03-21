# Azure-File-Share-AD-EntraID-Integration
This project demonstrates the integration of Azure File Shares with on-premises Active Directory (AD) and Microsoft Entra ID (formerly Azure AD) for secure and centralized file access control.

This guide walks you through creating a secure and readily accessible file share on Azure, seamlessly integrated with your existing on-premises Active Directory (AD) environment and managed through Microsoft Entra ID (formerly Azure Active Directory).

## Network Diagram

![Screenshot 2023-11-08 152254](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/Screenshot%202024-03-21%20164709.png)

## Prerequisites:
- An Azure subscription with appropriate permissions to create storage accounts and file shares.
- An existing Active Directory domain.
- A Microsoft Entra ID tenant.
- A Windows machine for the client side testing.

## Step 1: Synchronize On-Premises AD with Entra ID

1. **Install Microsoft Entra Connect Agent:** Download and install the Microsoft Entra Connect agent on your Windows server machine within your on-premises network.
   
   ![Screenshot 2023-11-08 15224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/EntraConnect4.png)

2. **Configure Entra Connect:** Launch the Entra Connect agent and configure it to connect to your Microsoft Entra ID tenant. Provide valid credentials with permissions to manage directory synchronization.
3. **Synchronize AD Objects:** Define which user and group objects to synchronize from your on-premises AD to Microsoft Entra ID. Initiate the synchronization process.
   
   ![Screenshot 2023-11-08 15224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/Synchrnosie%20service.png)

## Step 2: Create an Azure Storage Account and File Share

1. **Sign in to Azure Portal:** Access the Azure portal using your Azure subscription credentials.
2. **Create Storage Account:** Navigate to the "Storage accounts" service and create a new storage account. Choose an appropriate resource group, location, and performance tier for your file share needs.
   
   ![Screenshot 2023-11-08 15224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/StorageAccountCreated.png)

3. **Create File Share:** Within the newly created storage account, create a dedicated file share. Choose a name that reflects the purpose of the share.

## Step 3: Enable Identity-Based Access for the File Share

1. **Access Storage Account Settings:** Navigate back to your storage account in the Azure portal and access its settings.
2. **Enable Azure AD authentication:** Under the "Settings" section, locate the option for "Identity" and enable Azure Active Directory (Azure AD) authentication for your storage account. Follow the guidance as mentioned on the Azure official portal. Below are the Powershell Commands that i used to enable identity access for the shared drive.

   ![Screenshot 2023-11-085224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/Screenshot%202024-03-21%20194932.png)
   
4. **Assign Permissions:** ensure you've installed the necessary prerequisites on your on-premises servers. Then use PowerShell commands to enable Identity-based access for the file share. Make sure you use the commands and steps mentioned in Azure Official Website.

   ![Screenshot 2023-11-085224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/IdentityAccessConfigured_Confirmation.png)
   
## Step 4: Manage User Access through Entra ID

1. **Access Entra ID Portal:** Sign in to the Microsoft Entra ID portal using your Entra ID tenant credentials.
2. **Manage User Permissions:** Navigate to the "Azure Active Directory" section (or equivalent) and locate the synchronized users and groups from your on-premises AD.
3. **Assign File Share Permissions:** Assign appropriate permissions, such as "Storage File Data SMB Share Contributor," to grant access to the file share.

![Screenshot 2023-11-08224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/IAMforStorageAccount.png)

## Step 5 (Optional): Mount the File Share on User Profiles

- **Group Policy or Management Tools:** Utilize Group Policy or other management tools within your on-premises environment to map the Azure file share to user profiles. This allows automatic mounting of the file share upon user login, improving user experience.

  ![Screenshot 2023-11-08524](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/AutoMountForUsers.png)

## Step 6 : Creating Backup for the Azure File Share
1. **Create the Recovery Service Vault:** CReate a Recovery Service Vault where you can store the data for backup.
  
  ![Screenshot 2023-11-5224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/Screenshot%202024-03-21%20195947.png)
   
3. **Create a Backup policy:** Create the backup policy for the azure file share. You can schedule timing and once its created click create backup now.

  ![Screenshot 203-11-5224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/Backup%20policy.png)

## Step 6: Test Access Levels

1. **Verify User Access:** Log in to a user account that should have access to the file share.

  ![Screenshot 203-11-5224](https://github.com/Saurabh-Bhargav/Azure-File-Share-AD-EntraID-Integration/blob/main/Images/AzureFileShareMapped.png)
   
3. **Test File Access:** Use tools like Windows File Explorer to access the Azure file share. Verify that users have the appropriate access based on permissions assigned in Entra ID.

## Benefits:

- **Simplified User Management:** Leverage existing on-premises AD user base.
- **Centralized Access Control:** Manage file share access from a single location (Entra ID).
- **Enhanced Security:** Benefit from Entra ID's robust identity and access management features.
- **Granular Access Control:** Fine-tune access permissions for individual users and groups.
- **Improved User Experience (Optional):** Automatic mounting of file share on user profiles streamlines access.

## Conclusion

By following these steps, you can create a user-friendly Azure file share solution that seamlessly integrates with your on-premises AD environment and leverages Entra ID for centralized access control. This approach simplifies user management, enhances security, and offers a convenient file sharing experience for your users.



