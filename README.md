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

![image](https://github.com/user-attachments/assets/7e7aba1f-5a26-4089-8458-0fc6bb8f2376)


<p>
Start by using remote desktop to access the vm we set up and created in the last walkthrough (osticket-prereqs)
</p>
<br />

![image](https://github.com/user-attachments/assets/040dea27-9fe8-4c92-9a9a-30264e0f927d)

<p>
To access the Admin/Analyst page for osTicket, use the following link - http://localhost/osTicket/scp/login.php <br />
To access the Client/End User side of osTicket, use the following link - http://localhost/osTicket
Go ahead and log into the Admin page using the credentials you set up when installing osTicket. This should be in your notepad file. Once you are logged in, you will be able to switch between the agent and admin role through the Admin Panel and Agent Panel links at the top of the page:
</p>
<br />

![image](https://github.com/user-attachments/assets/2d381773-9a3c-400d-adb8-a3037e9205da)

![image](https://github.com/user-attachments/assets/f8e147d9-9a7c-4ee4-894c-03590f9cf037)

<p>
From within the Admin Panel, we will now configure a role that will have the ability to make any changes they want. To do so, navigate to Agents > Roles > Add New Role. Name the role "Supreme Admin", then under the permissions tab, make sure all boxes are checked. This includes all boxes under the tickets and tasks tabs. Lastly, click Add Role.
</p>
<br />

![image](https://github.com/user-attachments/assets/c36ee981-69e1-4f27-9c61-1febac8b0e20)

<p>
Next, we will add a new department. To do this, go to Agents > Departments > Add New Department > Name your department "SysAdmins". Leave everything else as default and click Create Dept
</p>
<br />

![image](https://github.com/user-attachments/assets/95566d9a-2c43-4374-88f9-03f5e0e5767c)

<p>
Now, we will create a team which can be assigned tickets. This can be done through Agents > Teams > Add New Team. Name the team anything. I will call mine "Online Banking". Then click Create Team.
</p>
<br />

![image](https://github.com/user-attachments/assets/1ba689b3-04cc-41f4-9096-ca48e21d4f71)


<p>
Next, we will create two agents from different depratments that will be able to assist end users with tickets. We can do this through Agents > Add New Agent . Name the agents anything. Make sure to record the credentials for both Agents inside a notepad. When creating the passwords, you will click Set Password, and then uncheck the "Send the agent a password reset email" box. Also, make sure that the "Require password change at next login" box is unchecked. When making the first Agent, go to the Access tab and change the primary department and role to be the ones we created earlier. Also add this Agent to the team we made through the Teams tab.
</p>
<br />

![image](https://github.com/user-attachments/assets/72abd2f3-3824-465b-95d1-bd3b05663b0e)


<p>
When creating the second Agent, put them in the Support department and give them a role of View Only.
</p>
<br />

<p>
Now we will create an account for an end user that can open tickets. To do this, navigate to the Agent Panel > Users > Add User. Give them a name and email, then click Add User.
</p>
<br />

![image](https://github.com/user-attachments/assets/7b7b850d-b5d1-4d10-8935-ab659f3e5483)

<p>
Next, we will set and configure a few Service Level Agreements (SLA's). The purpose of this is to set time frames for when tickets of a specific severity should be responded to or resolved. To add them go to Admin Panel > Manage > SLA > Add new SLA Plan. 
Add the following SLA Plans:

Name: Sev-A (Grace Period: 1 hour, Schedule: 24/7)
Name: Sev-B (Grace Period: 4 hours, Schedule: 24/7)
Name: Sev-C (Grace Period: 8 hours, Business Hours)

</p>
<br />

![image](https://github.com/user-attachments/assets/c612cee6-2806-4dde-aa7f-8a244bb9dc98)

![image](https://github.com/user-attachments/assets/09c87c90-dd92-4c53-963c-74acb0824dfc)

<p>
Lastly, we will create a few Help Topics which will be helpful for categorizing the type of tickets submitted. To add them, got to Manage > Help Topics > Add New Help Topic. Create a help topic for each of the following:
Business Critical Outage,
Personal Computer Issues,
Equipment Request,
Password Reset,
Other
The final result of all help topics should look like the following.
</p>
<br />

![image](https://github.com/user-attachments/assets/f2038a3b-11a1-46d9-842c-f4045ac8d0b9)

<p>
Congratulations! This section of the walkthrough is complete and you can now move onto the tickets-lifecycle section
</p>
<br />

