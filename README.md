<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Post Installation Configuration</h1>
In this tutorial, users will learn how to configure and manage osTicket by setting up roles, departments, teams, agents, users, SLA policies, and help topics. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)

<h2>Post-Install Configuration Objectives</h2>

- Item 1
- Item 2
- Item 3
- Item 4
- Item 5


<h2>Configuration Steps</h2>

![image](https://github.com/user-attachments/assets/167e9e99-374b-4556-b04b-e721d347af28)

<p>
When setting up the VM, create a new resource group and assign the vm to that group. Then, give your vm a name and make it a Windows 10 pro version 22H2 with a size of at least 2 vcpus and 8GB memory. Also create a username and password for your vm while making sure to take note of both in a notepad. After everything is ready, press review + create and then create.
</p>
<br />

![image](https://github.com/user-attachments/assets/f0bd3ebb-019a-472d-864d-0d69643f1db5)

<p>
Once the vm has finished deploying, use a remote desktop client to access the vm (In the image, I am using Windows built in Remote Desktop Client). You will need the public IP of the machine as well as the credentials you created for it.
</p>
<br />

![image](https://github.com/user-attachments/assets/2734156c-25f6-4331-9d8f-13257ce753c3)
<p>
When you are inside the vm, download the following files inside the vm - https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD 
You can just copy the link inside of the Edge browser. Once is is downloaded, extract it somewhere on your computer. We will use the files in this folder to install osTicket and some of the dependencies.
</p>
<br />


![image](https://github.com/user-attachments/assets/3d91a441-144f-4fe5-b1cd-c422499c1e9a)
<p>
For the next step, we will be enabling Internet Information Services (IIS) within Windows. osTicket is a web-based application, and IIS is required to serve its files and handle HTTP requests.
To do so, open the control pannel and click Programs > Turn Windows features on or off and check the Internet Information Services and CGI boxes
</p>
<br />

![image](https://github.com/user-attachments/assets/f9e90279-2e2a-4703-90cd-cd7c28244193)

<p>
Now, if you go into edge and enter the IP address 127.0.0.1 (Your lookback IP address), you should be presented with a default windows server page that looks similar to the image above.
</p>
<br />


![image](https://github.com/user-attachments/assets/511082c0-88ca-47df-97e9-e8d6dc582390)

<p>
Next, we will be running some of the installation files from the folder we set up earlier (osTicket-Installation-Files) to set up all the dependancies for osTicket
Start by running the PHPManagerForIIS file and walk through the installation leaving everything as default
Next, run the rewrite_amd64_en-US file and walk through the installation leaving everything as default
Now, we will need to create a folder called "PHP" inside the C drive and unzip the contents of the PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) file into that PHP folder 
Then, run the VC_redist.x86 file. Next, install mysql through the mysql-5.5.62-win32.msi file and leave everything as default aside from the user and password which can both be set to "root". Also make sure you select the Typical installation method and Standard Configuration.

</p>
<br />

![image](https://github.com/user-attachments/assets/a1a2f681-a3de-439c-a3e2-a7278c8d00e9)
<p>
Next, we will need to open the IIS manager as an admin (right click and select "Run as administrator")
</p>
<br />

![image](https://github.com/user-attachments/assets/b7d639bf-dd1d-4cc6-846e-a112562c25aa)
<p>
Next, we need to register PHP through the IIS manager (Show the computer where the PHP installation exists)
We can do this in the IIS manager my clicking PHP manager, Register new version of PHP, and then selecting the php-cgi Application file inside the PHP we created on the C drive earlier.
</p>
<br />

![image](https://github.com/user-attachments/assets/a86507d7-a4b9-410f-bc77-46ed80195560)
<p>
Then, we will need to stop and start the IIS server for the changes to take effect
</p>
<br />

![image](https://github.com/user-attachments/assets/6b956a6e-1f8e-443a-ac93-4d044e675f76)
<p>
Now, we can extract the contents of the osTicket-v1.15.8.zip into the same folder it is in.
Copy the “upload” folder into “c:\inetpub\wwwroot”
Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”
We will need to start and stop the IIS server after this again.

</p>
<br />

![image](https://github.com/user-attachments/assets/9fb8bea6-3fc7-4120-9d03-2472f5c0640f)
<p>
We can view the osTicket landing page through servername > Sites > osTicket and the press "Browse *.80(http)" on the right side which should result in the following web page appearing:
</p>
<br />

![image](https://github.com/user-attachments/assets/901f623b-38d4-40a5-a2ab-af87a784bd6d)

<p>
Notice that some extensions are not enabled
Go back to IIS, sites > Default > osTicket
Double-click PHP Manager
Click “Enable or disable an extension”
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opcache.dll
Refresh the osTicket site in your browser, observe the changes
</p>
<br />

![image](https://github.com/user-attachments/assets/7c35e725-7070-4624-a1ff-da3f391bf136)

<p>
Navigate to the file shown above called ost-sampleconfig.php. We will need to rename this to ost-config.php
Next, we will need to edit the file so that osTIcket has access to it
Right click the file > Properties > Security > Advanced > Disable inheritance > Remove all inherited permissions 
</p>
<br />

![image](https://github.com/user-attachments/assets/d61f036f-9538-4792-8928-42ba5d4c3e21)

<p>
Now, we need to add a new principal. Click Add > Select a principal > Type everyone into the last box > Check Names > ok > check the full control box > Apply > ok
</p>
<br />

![image](https://github.com/user-attachments/assets/3b7bfb69-bbf0-4814-ae82-8f1c87a4ba39)
<p>
We can now continue setting up our osTicket installation in the browser. Give your helpdesk a name, and a default email(receives email from customers)
. Set up your admin user (take note of the username and password in notepad)
</p>
<br />

![image](https://github.com/user-attachments/assets/75c535d4-9bab-473f-8933-320f77487cda)

<p>
Before clicking Install now, we need to install heidiSQL from the installation files folder. Leave all installation options as default. This is necessary so that our osTicket has a database to connect to and store its information
</p>
<br />

![image](https://github.com/user-attachments/assets/06e645de-407f-4ed1-a2a8-d20e8ee4ddfb)

<p>
After the installation has finished, click New at the bottom left and make sure the user and password fields are both "root" like we specified before. Then click Open. If successful, the following page will be displayed showing all database connections.
</p>
<br />

![image](https://github.com/user-attachments/assets/c374cdbd-8ffd-4688-8acd-3f676efb7530)


<p>
We will now create our database that osTicket will use by right clicking the Dolphin picture with "Unamed" next to it and click create new > database. Name the database osTicket. Once the database is created, we can finalize the osTicket installation process. Fill out the remaining database setting section as follows with a password of root:
</p>
<br />

![image](https://github.com/user-attachments/assets/b72736d4-30d5-4405-b9e2-d40e06d4e5b1)

<p>
Good job, hopefully it is installed with no errors!
Browse to your help desk login page: http://localhost/osTicket/scp/login.php

End Users osTicket URL:
http://localhost/osTicket/ 




