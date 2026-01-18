# Manage Microsoft Entra ID Identities


# Create Users and Groups in Azure AD
## Lab Overview
Practice creating and managing users and groups in Microsoft Entra ID (Azure AD)

## What I Learned
- How to navigate the Azure Portal
- How to create new users in Azure AD
- How to create security groups
- How to assign users to groups
- How to manage user properties

## Steps Completed

### 1. Access Azure Active Directory
- Logged into Azure Portal (portal.azure.com)
- Searched for "Azure Active Directory" or "Microsoft Entra ID"
- Clicked on Azure Active Directory from the menu

### 2. Create New Users
- Clicked on "Users" in the left menu
- Clicked "+ New user" at the top
- Selected "Create new user"
- Filled in the details:
  - User name: john.doe@yourdomain.onmicrosoft.com
  - Name: John Doe
  - First name: John
  - Last name: Doe
- Created a temporary password
- Clicked "Create"
- **Repeated this process to create 3 test users**

### Invite a New User via Email 
- Clicked in the New user drop-down & selected Invite an external user.
- Filled in the details:
  - Email: octavia.hall@azureexpert.com
  - Display name: Octavia Hall
  - Send invite messgae: Yes
  - Message: Welcome to Azure and our group project
  - Clicked Properties tab
  - User type: Guest
  - Job title: Cloud Administrator
  - Company name: Octavia's Lemonade Stand
  - Clicked Review + invite, and then Invite

  ## Screenshots
(I took screenshots of each step and saved them in the screenshots folder)


### 3. Create Security Groups
- Went back to Azure Home in the Portal
- Clicked on "Groups" in the left menu
- Clicked "+ New group"
- Filled in the details:
  - Group type: Security
  - Group name: IT Department
  - Group description: IT team members
  - Membership type: Assigned
- Clicked "Create"
- **Created 2 groups: IT Department and HR Department**

### 4. Add Users to Groups
- Clicked on the "IT Department" group
- Clicked "Members" in the left menu
- Clicked "+ Add members"
- Selected the users I wanted to add
- Clicked "Select"
- Verified the users appeared in the members list

### 5. Verify Everything Works
- Checked that all users were created successfully
- Verified group memberships
- Tested user properties and made sure everything looked correct

## Results
- Successfully created 3 test users
- Created 2 security groups (IT Department and HR Department)
- Assigned users to appropriate groups
- All users can now be managed through their groups

## Challenges I Faced
- Initially forgot to enable the user account (it was disabled by default)
- Learned that user names must include the domain (@yourdomain.onmicrosoft.com)

## Key Takeaways
- The Portal is more visual and beginner-friendly than PowerShell
- Security groups help organize users by department or role
- Always document your temporary passwords securely
- Group management makes it easier to assign permissions to multiple users at once

















----------------------
#Create Users and Groups in the CLI using Powershell

## Prerequisites
- Azure subscription
- Azure AD/Entra ID access
- Azure PowerShell module installed

## PowerShell Scripts Used

### 1. Connect to Azure AD
```powershell
# Connect to Azure AD
Connect-AzureAD
```

### 2. Create a New User
```powershell
# Create a new user
$PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
$PasswordProfile.Password = "TempPassword123!"

New-AzureADUser -DisplayName "John Doe" `
    -PasswordProfile $PasswordProfile `
    -UserPrincipalName "john.doe@yourdomain.onmicrosoft.com" `
    -AccountEnabled $true `
    -MailNickName "johndoe"
```

### 3. Create a Security Group
```powershell
# Create a new security group
New-AzureADGroup -DisplayName "IT Department" `
    -MailEnabled $false `
    -SecurityEnabled $true `
    -MailNickName "ITDept"
```

### 4. Add User to Group
```powershell
# Get the user and group
$user = Get-AzureADUser -ObjectId "john.doe@yourdomain.onmicrosoft.com"
$group = Get-AzureADGroup -Filter "DisplayName eq 'IT Department'"

# Add user to group
Add-AzureADGroupMember -ObjectId $group.ObjectId -RefObjectId $user.ObjectId
```

### 5. Verify Group Membership
```powershell
# Check members of the group
Get-AzureADGroupMember -ObjectId $group.ObjectId
```

## Results
- Successfully created 3 test users
- Created 2 security groups (IT Department and HR Department)
- Assigned users to appropriate groups

## Notes
- Remember to use strong passwords in production
- Always verify group membership after adding users
- Consider using bulk import for creating multiple users

## Next Steps
- Manage user and group properties
- Manage licenses in Microsoft Entra ID
- Manage external users
- Configure self-service password reset (SSPR)
