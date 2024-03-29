# Export-AzureUsersToAmazonConnectCSV
script to export users from AzureAD for import into Amazon Connect dashboard. the script outputs a csv in the format provided by Amazon Connect for importing users into the Amazon Connect User Management menu. 

# Prerequisites:
- Azure Powershell module: Install-Module -Name Az -Repository PSGallery -Force, and ability to connect to Azure Account: Connect-AzAccount
- Assumes that Single-Sign On has already been configured for EntraID users to connect to Amazon Connect. All users will need to be assigned to the "AWS Single-Account Access" Enterprise Application.  This script is for ensuring that the AzureAD users have identites also created in Amazon Connect's "User Management".
- This script assumes the full upn is passed in the Azure App Claims
  where Claim Name https://aws.amazon.com/SAML/Attributes/RoleSessionName = user.userprincipalname
  if another claims value is being passed, edit line: $r."user login" = $m.<desiredValue>

# Description: 
 script prompts for an AzureAD Group displayname
 the members of this group are collected and exported to a csv

# Use:
- Add the desired Amazon Connect users to an Azure AD Group
- Ensure powershell has the Azure Powershell Module, and is able to connect to your tenant via Connect-AzAccount
- Edit script or open to verify the $exportFile filename
- Connect to the Azure Account. Change to the directory with .ps1, and Run Script, provide the displayname of the AzureAD Group containing the Connect Agents 
- upload the csv into Amazon Connect by a Connect Administrator
  (Connect -> User Management -> Add new users -> Import Users using a .csv template)
