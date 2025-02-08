<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

• Microsoft Azure (Virtual Machines/Compute)

• Remote Desktop

• Active Directory Domain Services

• PowerShell

<h2>Operating Systems Used </h2>

• Windows Server 2022

• Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

• Login into Domain controller and Install Active Directory

• Create a Domain Admin User within the Domain

• Join client-1 to the domain name (mydomain.com as example)

• Setup Remote Desktop for non-administrative users on client-1

• Create a bunch of additional users in Powershell 

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1438" alt="Beginning step 1" src="https://github.com/user-attachments/assets/acf14826-056b-460b-af05-d489dd645b4c"/>
</p>
<p>
Establish the virtual machine in Microsoft Azure in order to do a remote desktop connection. By creating a Domain Controller and Client user this is how you are able to create the Active Directory database that allows the domain controller to be able to store information and give access to users to connect to certain resources within the network
</p>
<br />

<p>
<img width="1065" alt="AD INSTALL STEP 1" src="https://github.com/user-attachments/assets/26f69fdb-466a-47fc-9bf7-c6d6e6ac127c"/>
</p>
<p>
Open Service Manager from start window -> Add roles and features -> Click Next, Click Next again, ensure operating system of the domain controller is selected -> Check Active Directory Domain Services box -> Add features -> Next -> Next -> Next -> Next -> Restart is reuqired box pops up -> Select Yes -> Install complete.
</p>
<br />

<p>
<img width="1435" alt="INSTALL AD STEP 2" src="https://github.com/user-attachments/assets/199bc8a7-d4c3-402f-9c40-a2d2de7c8933"/>
</p>
<p>
Close out roles and features -> Look at the top right at yellow flag(Yellow flag isnt appeared becasue I have done this step already) -> (Acting as if Yellow flag did appear, you'd Click on it and select Promote the Server to a Domain Controller.
</p>
<br />

<p>
<img width="606" alt="AD INSTALL STEP 3" src="https://github.com/user-attachments/assets/1d884f87-8d5d-4184-90b3-529ca62b6d38"/>
<img width="1440" alt="Active Directory User and Computers AD STEP 4" src="https://github.com/user-attachments/assets/aacdcdc9-75b6-4133-8d4c-7768f369843c" />
</p>
<p>
Now that Active Directory is installed we are going to configure it to become a Domain Controller within a new forest in our Domain.
Go back to Domain Controller -> After above steps of clicking on "Promote this server to a domain controller" -> Click on it -> Add a new forest -> Type in the domain name -> Next -> Next -> Ensure Create DNS delegation is unchecked -> Next -> Next -> Install and wait for the new forest to be installed for the computer to turn into a Domain controller completely -> Automatically restarts -> Login again into Domain Controller using the domain "\" domain controller name and or user name
</p>
<br />

<p>
<img width="1440" alt="USER CREATED IN DOMAIN STEP 2 AD" src="https://github.com/user-attachments/assets/f1c5cfcb-4821-47c1-9293-a4473b907272"/>
</p>
<p>
Once restarted you will be logged back in, now as again as a domain controller -> Start -> Click Windows Adminastrative tools -> Click Active Directory Users and Computers
</p>
<br />

<p>
<img width="1440" alt="Adding an Admin User in AD STEP 6" src="https://github.com/user-attachments/assets/bf8c5415-b92b-4a9e-b3d1-1cd74a91d97b"/>
<img width="1440" alt="AD INSTALL ORGANIZATIONS CREATED STEP 5" src="https://github.com/user-attachments/assets/d9b9da06-e28e-484f-acd2-49d0193f1616"/>
</p>
<p>
Create Organizational Unit (Here is how you create a user/s and or admins within an Organization) -> Create a new Organizational Unit for ADMINS by Right-Clicking domain name site -> New -> Organizational Unit(Add Organization Unit in the domain site) -> Click Ok -> now repeat these steps and create organazational unit for users named Employees 
</p>
<br />

<p>
<img width="1436" alt="Create a Domain Admin within Domain STEP 2 AD" src="https://github.com/user-attachments/assets/c305ea07-a930-463c-8e93-b2e86f944d83"/>
<img width="1440" alt="PART of STEP 6 AD ADDING TO A SECURITY GROUP" src="https://github.com/user-attachments/assets/cc7286ad-34ef-42e4-a1ad-a2186e28cb3e"/>
</p>
<p>
Now create a domain admin user within the domain by Right-Clicking ADMINS folder within domain name still in Active Directory Users and Computers folder -> New -> User -> Fill out using the users credentials -> Next -> Finish(the account isnt an admin yet, to make it fully active as an admin) -> We must now add the admin to the built-in "Security group" -> Back to Active Directory Users and Computers -> click on Admins -> Right-Click the admin user -> properties  -> Member of -> domain admins -> Check Names -> OK -> Apply -> OK(Now the account is an actual domain admin)   
</p>
<br />

<p>
<img width="1440" alt="CLIENT 1 IS JOINED TO DOMAIN CONTROLLER STEP 3" src="https://github.com/user-attachments/assets/081e7407-d4e0-4c7b-835c-f0e7eea534e1"/>
<img width="1440" alt="client 1 clearly is apart of the domain step 3 AS" src="https://github.com/user-attachments/assets/2a09ea7a-655e-43d7-a1ec-b913b1c5df91"/>
</p>
<p>
Now to join Clients/Users to a domain name -> Login as the original local admin user in Client 1 and join into the domain(computer will restart -> Right-Click start menu -> System -> Rename this PC -> Change -> Ensure "Member of" Domain category is ticked -> add the domain name site -> OK -> add the Domain Controller using the domain admin credentials for Computer Name/Domain changes tab -> OK -> Restart -> Login to Domain Controller using an admin login to verify Client-1 shows up in ADUC(Active Directory Users and Computers)
</p>
<br />

<p>
<img width="1013" alt="ALLOW DOMAIN USERS TO ACCESS REMOTE DESKTOP" src="https://github.com/user-attachments/assets/a3088295-05ba-4b05-9348-2fc995cf29e0"/>
</p>
<p>
Now to Setup a Remote Desktop for non administrative users on client-1 -> login to client-1 as admin/domain user -> Open system properties -> Click “Remote Desktop” -> Allow “domain users” access to remote desktop -> OK -> OK -> Now all domain users should be allowed to login to that computer
</p>
<br />

<p>
<img width="780" alt="STEP 5 RUN ADMINISTRATOR RIGHT CLICK HERE" src="https://github.com/user-attachments/assets/11c8e812-acf6-4075-8e2e-06c8b6e54755"/>
<img width="1274" alt="RUNNING SCRIPT IN PSH STEP 5" src="https://github.com/user-attachments/assets/8cb78ed3-9989-4fa7-bab8-52e15249a3da"/>
<img width="1269" alt="step 5 push play in PSh" src="https://github.com/user-attachments/assets/4481d49e-6fca-4558-9685-327336dce0f5"/>
<img width="1261" alt="users created in PSH STEP 5" src="https://github.com/user-attachments/assets/4b92145a-ce50-4f9d-8f47-0c4bbad07b90"/>
</p>
<p>
Now to create additional users as a domain admin -> login as a domain admin -> Right-Click on Powershell ISE and run as administrator -> PSh opens -> Run coded scrpit in Power Shell ISE -> Click RUN icon -> Users will be created in the PSh ISE -> Now you can ensure setup is correct by attempting to login using one of the user usernames from PSh to ensure users can seamlessly login
</p>
<br />


