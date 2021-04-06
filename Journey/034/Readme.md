# Azure subscription & AD directory/tenant

## Azure subscription: relationship with AD tenent/directory
- An Azure subscription has a trust relationship with Azure Active Directory (Azure AD). 
- A subscription trusts Azure AD to authenticate users, services, and devices.
- Multiple subscriptions can trust the same Azure AD directory. 
- Each subscription can only trust a single directory.


## AD Tenant
- To build apps that use the Microsoft identity platform for identity and access management, you need access to an Azure Active Directory (Azure AD) tenant. It's in the Azure AD tenant that you register and manage your apps, configure their access to data in Microsoft 365 and other web APIs, and enable features like Conditional Access.

- A tenant represents an organization. It's a dedicated instance of Azure AD that an organization or app developer receives at the beginning of a relationship with Microsoft. That relationship could start with signing up for Azure, Microsoft Intune, or Microsoft 365, for example.

- Azure AD tenant = directory, and there is a strict 1:1 relationship between them (you cannot create several directories under a tenant). Each tenant has it's globally unique 'tenant ID' (in some places in the Portal referred as 'directory ID', but the ID is the same.
