# Building a Virtual Mini Corporate Environment

This tutorial will guide you through the process of setting up a virtual corporate environment using Windows Server 2019. You'll learn how to install Windows Server 2019, configure Active Directory, DHCP, and DNS Server roles, create an administrative account, and add 50 users to Active Directory simultaneously. Let's get started!

## Prerequisites
Before we start, ensure you have the following:

1. **Hardware Requirements**:
   - A computer with at least 8 GB of RAM (16 GB recommended).
   - A multi-core processor (Quad-core or higher recommended).
   - Sufficient storage space (at least 50 GB free for the virtual machine).

2. **Software Requirements**:
   - **Virtualization Software**: Microsoft Hyper-V, VMware Workstation, or Oracle VirtualBox.
   - **Windows Server 2019 ISO**: Download from the Microsoft website.
   - **Windows 10 ISO**: Download from the Microsoft website.

3. **Network Requirements**:
   - A stable internet connection for downloading necessary software and updates.
   - Basic understanding of network concepts and IP addressing.

Next, we'll start with the installation of the virtualization software and setting up the virtual machine.

## Step 1: Installing Windows Server 2019

1. **Create a New Virtual Machine**:
   - Open your virtualization software (e.g., VMware Workstation or VirtualBox).
   - Click on "Create a New Virtual Machine" or a similar option.
   - Choose the option to install the operating system later if prompted.

2. **Configure the Virtual Machine**:
   - **Name**: Give your virtual machine a name (e.g., "Windows Server 2019").
   - **Location**: Choose a location to store the virtual machine files.
   - **Type**: Select "Microsoft Windows".
   - **Version**: Choose "Windows Server 2019".

3. **Allocate Resources**:
   - **Memory (RAM)**: Allocate at least 2 GB of RAM.
   - **Processor**: Assign at least 2 virtual processors.
   - **Hard Disk**: Create a new virtual hard disk with at least 32 GB of storage.

4. **Attach the Windows Server 2019 ISO**:
   - In the virtual machine settings, find the "CD/DVD" drive option.
   - Attach the Windows Server 2019 ISO file you downloaded earlier.

5. **Start the Virtual Machine**:
   - Power on the virtual machine.
   - The virtual machine will boot from the attached ISO file.

6. **Windows Server 2019 Installation**:
   - **Language, Time, and Keyboard**: Choose your preferences and click "Next".
   - **Install Now**: Click the "Install Now" button.
   - **Edition**: Select the Windows Server 2019 Standard Datacenter.
   - **License Agreement**: Accept the license terms and click "Next".
   - **Installation Type**: Choose "Custom: Install Windows only (advanced)".
   - **Partition**: Select the unallocated space and click "Next". The installer will create the necessary partitions and start the installation.

7. **Complete Installation**:
   - The installation process will take several minutes. Once complete, the system will restart.
   - **Initial Configuration**: After the restart, set a strong password for the Administrator account.

8. Login with the Administrator account using the password you set.

Once you're logged in, the basic installation of Windows Server 2019 is complete.

## Step 2: Configure NICs in Windows Server 2019

1. **Open Network Connections**:
   - Open the **Control Panel**.
   - Navigate to **Network and Sharing Center**.
   - Click on **Change adapter settings** on the left side.

2. **Rename NICs for easier identification**:
   - **NIC 1**: Rename "Ethernet" to "INTERNET".
   - **NIC 2**: Rename "Ethernet 2" to "INTERNAL".

3. **Configure Internal Network NIC**:
   - Right-click on "INTERNAL" and select **Properties**.
   - Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
   - Assign a static IP address. For example:
     - IP address: 192.168.0.1
     - Subnet mask: 255.255.255.0
     - DNS server: 127.0.0.1
     - Leave the default gateway field empty.

4. **Verify Connectivity**:
   - Ensure that the "INTERNET" NIC has internet access.
   - The "INTENAL" NIC should be isolated from the internet but able to communicate with internal clients.

Now that the NICs are configured, the server is set up to connect to the internet and to serve client machines on a private network.

## Step 3: Rename the Windows Server Machine
Renaming your server will help in identifying it easily on the network.

1. **Open Server Manager**:
   - Click on the **Start** menu.
   - Select **Server Manager**.

2. **Navigate to the System Properties**:
   - In Server Manager, click on **Local Server** on the left panel.
   - In the **Properties** section, click on the current **Computer Name**.

3. **Change Computer Name**:
   - In the **System Properties** window, click the **Change** button.
   - In the **Computer Name/Domain Changes** window, enter a new name for your server in the **Computer name** field (e.g. "DC").
   - Click **OK**.

4. **Restart the Server**:
   - You will be prompted to restart your server to apply the changes.
   - Click **OK** on the prompt and then click **Close** on the System Properties window.
   - Click **Restart Now** to reboot the server.

After the server restarts, it will have the new name you assigned. This will make it easier to manage and identify on your network.

## Step 4: Installing Active Directory and Creating a Domain

1. **Open Server Manager**:
   - Click on the **Start** menu.
   - Select **Server Manager**.

2. **Add Roles and Features**:
   - In Server Manager, click on **Manage** in the upper-right corner.
   - Select **Add Roles and Features**.

3. **Before You Begin**:
   - Click **Next** on the "Before You Begin" page.

4. **Select Installation Type**:
   - Choose **Role-based or feature-based installation** and click **Next**.

5. **Select Destination Server**:
   - Ensure your server is selected in the server pool and click **Next**.

6. **Select Server Roles**:
   - Scroll down and select **Active Directory Domain Services**.
   - A dialog box will pop up to add required features. Click **Add Features**.
   - Click **Next**.

7. **Select Features**:
   - Click **Next** on the "Select Features" page.

8. **Active Directory Domain Services**:
   - Click **Next** on the AD DS page.

9. **Confirm Installation Selections**:
   - Click **Install**.
   - The installation will begin. Once complete, click **Close**.

#### Step 2: Promote the Server to a Domain Controller

1. **Post-Deployment Configuration**:
   - In Server Manager, you will see a yellow notification flag indicating that there is a post-deployment configuration pending.
   - Click on the **notification flag** and then click on **Promote this server to a domain controller**.

2. **Deployment Configuration**:
   - Select **Add a new forest**.
   - In the **Root domain name** field, enter the name for your new domain (e.g., "mydomain.com").
   - Click **Next**.

3. **Domain Controller Options**:
   - Choose a **forest functional level** and **domain functional level** (Windows Server 2016 is recommended).
   - Ensure **Domain Name System (DNS) server** and **Global Catalog (GC)** are selected.
   - Enter a **DSRM password** (Directory Services Restore Mode password) and click **Next**.

4. **DNS Options**:
   - Click **Next** on the DNS options page. You may see a warning about a delegation for this DNS server; you can safely ignore this for now.

5. **Additional Options**:
   - The NetBIOS domain name will be automatically filled based on your domain name. Verify it and click **Next**.

6. **Paths**:
   - Accept the default paths for the database, log files, and SYSVOL, and click **Next**.

7. **Review Options**:
   - Review your selections and click **Next**.

8. **Prerequisites Check**:
   - The wizard will run a prerequisites check. If everything passes, click **Install** to begin the promotion.

9. **Complete Installation and Restart**:
   - The server will install the necessary components and then automatically restart.

Once the server restarts, it will be a domain controller for your new domain.

## Step 5: Installing and Configuring Remote Access Service (RAS)

Remote Access Service (RAS) will allow clients on the internal network to access the internet through the domain controller.

#### Step 1: Install Remote Access Role

1. **Open Server Manager**:
   - Click on the **Start** menu.
   - Select **Server Manager**.

2. **Add Roles and Features**:
   - In Server Manager, click on **Manage** in the upper-right corner.
   - Select **Add Roles and Features**.

3. **Before You Begin**:
   - Click **Next** on the "Before You Begin" page.

4. **Select Installation Type**:
   - Choose **Role-based or feature-based installation** and click **Next**.

5. **Select Destination Server**:
   - Ensure your server is selected in the server pool and click **Next**.

6. **Select Server Roles**:
   - Scroll down and select **Remote Access**.
   - A dialog box will pop up to add required features. Click **Add Features**.
   - Click **Next**.

7. **Select Features**:
   - Click **Next** on the "Select Features" page.

8. **Remote Access**:
   - Click **Next** on the Remote Access page.

9. **Role Services**:
   - Select **DirectAccess and VPN (RAS)**.
   - Click **Next**.

10. **Web Server (IIS)**:
    - Click **Next** on the Web Server (IIS) page.

11. **Role Services**:
    - Accept the default selections and click **Next**.

12. **Confirm Installation Selections**:
    - Click **Install**.
    - The installation will begin. Once complete, click **Close**.

#### Step 2: Configure Remote Access

1. **Open Remote Access Management**:
   - In Server Manager, click **Tools**.
   - Select **Remote Access Management**.

2. **Run the Getting Started Wizard**:
   - In the Remote Access Management Console, click on **Deploy VPN Only** under Step 2.

3. **Configure Remote Access**:
   - In the Routing and Remote Access console, right-click on your server name and select **Configure and Enable Routing and Remote Access**.

4. **Routing and Remote Access Setup Wizard**:
   - Click **Next** to begin the wizard.

5. **Configuration**:
   - Select **Custom configuration** and click **Next**.

6. **Custom Configuration**:
   - Check the **VPN access** and **NAT** options, then click **Next**.

7. **Finish and Start Service**:
   - Click **Finish**.
   - When prompted to start the service, click **Start service**.

#### Step 3: Configure NAT

1. **Open NAT Configuration**:
   - In the Routing and Remote Access console, expand your server name, then expand **IPv4**, and click on **NAT**.

2. **Configure Public Interface**:
   - Right-click on **NAT** and select **New Interface**.
   - Select the **INTERNET** interface and click **OK**.
   - In the dialog box that appears, select **Public interface connected to the Internet** and check **Enable NAT on this interface**.
   - Click **OK**.

3. **Configure Private Interface**:
   - Right-click on **NAT** and select **New Interface**.
   - Select the **Internal Network** interface and click **OK**.
   - In the dialog box that appears, select **Private interface connected to private network**.
   - Click **OK**.

#### Step 4: Configure VPN

1. **Enable VPN Access**:
   - In the Routing and Remote Access console, right-click your server name and select **Properties**.
   - Go to the **Security** tab.
   - Ensure **Allow custom IPSec policy for L2TP/IKEv2 connection** is unchecked unless you have a specific policy to apply.
   - Click **OK**.


With these steps, your server is now configured to allow clients on the internal network to access the internet through the domain controller.


