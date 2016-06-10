---
title: Add the RDSH Server, create a collection, and publish the RemoteApp programs
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae9767e3-864a-4eb2-96c0-626759ce6d60
author: lizap
---
# Add the RDSH Server, create a collection, and publish the RemoteApp programs
Use the following steps to deploy RemoteApp programs in your desktop hosting environment. Make sure you have reviewed and completed the prerequisites before starting.  
  
## Add the RD Session Host to your deployment  
1.	Create a public IP address for the virtual machine running Remote Desktop Management Services (RDMS). The RDMS virtual machine is usually the virtual machine running the first instance of the RD Connection Broker role. Note that this step is not necessary if the RDMS virtual machine already has a public IP address to allow RDP connections.  
    1. In the Azure portal, click **Browse > Virtual Machines**, and then click the RDMS virtual machine (for example, Contoso-CB1).  
    2. Click **Settings > Network interfaces**, and then click the corresponding network interface.   
    3. Click **Settings > IP address**.   
    4. For **Public IP address**, select **Enabled**, and then click **IP address**.   
    5. If you have an existing public IP address you want to use, select it from the list. Otherwise, click **Create new**, enter a name, and then click **OK** and then **Save**.   
2.	Connect to the RDMS virtual machine:  
    1.	In the Azure portal click **Browse > Virtual Machines**.  
    2.	Select the new RDMS virtual machine (for example, Contoso-CB1).  
    3.	Click **Connect > Open** to open the Remote Desktop client.  
    4.	In the client, click **Connect**, and then click **Use another user account**. Enter the user name and password for a user in the Azure AD DC Administrators group.  
    5.	Click **Yes** when warned about the certificate.  
3.	Add the new RDSH server to Server Manager:  
    1. Launch Server Manager, click **Manage > Add Servers**.   
    2. In the Add Servers dialog, click **DNS**.   
    3. Browse to and select the newly created RD Session Host server, e.g. Contoso-SH2.   
    4. Click **OK**.  
 4.	Add RDSH server to the deployment  
    1. Launch Server Manager .  
    2. Click **Remote Desktop Services > Overview > Deployment Servers > Tasks > Add RD Session Host Servers**.   
    3. Select the newly created server (for example, Contoso-SH2), and then click **Next**.  
    4. On the Confirmation page, select **Restart remote computers as needed**, and then click **Add**.  
5.	Create a file share for the RemoteApp collection user provide disks  
    1.	Open File Explorer, click **This PC**, and open the disk that you created for file shares.  
    2.	Click **Home > New Folder**.  
    3.	Enter a name for the user disks folder, for example, **UserDisksr**.  
    4.	Right-click the new folder, and then click **Properties > Sharing > Advanced Sharing**.  
    5.	Select **Share this folder**, and then click **Permissions**.  
   6.	Select **Everyone**, and then click **Remove**. Now click **Add**, enter **AAD DC Administrators**, and click **OK**. If you are using AD DS on a VM and not Azure AD Domain Services, enter **Administrators** instead of **AAD DC Administrators**.  
    7.	Select **Allow Full Control**, and then click **OK > OK > Close**.  
  
## Create a session collection and publish RemoteApp programs  
1.	In Server Manager, click **Remote Desktop Services > Collections > Tasks > Create Session Collections**.  
2.	Enter a name for the collection, for example **ContosoApps**.  
3.	Select the new RD Session Host server you created (for example, Contoso-SHr1).  
4.	Accept the default **User Groups**.  
5.	Enter the location of the file share you created for the user profile disks for this collection (for example, **\\Contoso-CB1\UserDisksr**).   
6.	Click **Create**. When the collection is created, click **Close**.  
8.	In Server Manager, select the new collection (**ContosoApps**).  
9.	Under RemoteApp Programs, click **Publish RemoteApp programs**.  
10.	Select the programs you want to publish, and then click **Publish**.  
  
  
