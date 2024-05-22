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
     - Leave the default gateway and DNS server fields empty.

4. **Verify Connectivity**:
   - Ensure that the "INTERNET" NIC has internet access.
   - The "INTENAL" NIC should be isolated from the internet but able to communicate with internal clients.

Now that the NICs are configured, the server is set up to connect to the internet and to serve client machines on a private network.


