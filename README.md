 <p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>AD-Group policy and Managing accounts</h1>
This repository demonstrates the configuration and management of Active Directory, Group Policy, and user accounts in a Windows domain environment.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 

<h2>Project Environment </h2>

To simulate a real corporate IT setup, I created two virtual machines:

DC-1 (Domain Controller): Hosts Active Directory Domain Services. This is where the user accounts and domain are managed.

Client-1: A Windows client machine joined to the domain. This VM is used to log in with domain accounts and test user access before and after enabling/disabling accounts.


## Table of Contents
- [Dealing with Account Lockouts](#dealing-with-account-lockouts)
- [Enabling and Disabling Accounts](#enabling-and-disabling-accounts)
- [Observing Logs](#observing-logs)



<h2>##Dealing with Account Lockouts</h2>

<p>
<img width="1458" height="777" alt="image" src="https://github.com/user-attachments/assets/0bc8db93-86c6-4df1-b690-304c885c8c1c" />
<img width="1455" height="777" alt="image" src="https://github.com/user-attachments/assets/92c671bf-a93d-4155-a7b3-3e17605a471a" />
<img width="1459" height="779" alt="image" src="https://github.com/user-attachments/assets/2a35baa6-3b2b-4ae0-817b-0d6fe585966c" />
<img width="1454" height="780" alt="image" src="https://github.com/user-attachments/assets/0b1be837-a9b2-4e55-9fd0-75c7ca4dc11f" />


</p>
<p>
Launch Group Policy Management Console (GPMC) on DC-1 by running gpmc.msc. 
  
Edit the Default Domain Policy and modify the Account Lockout Policy, setting accounts to lock after 5 unsuccessful logon attempts to enhance security.

Steps : 

1.Log into DC-1.

2.Open GPMC by typing gpmc.msc.

3.Navigate to Default Domain Policy and select Edit.

4.Go to Account Policies → Account Lockout Policy.

5.Set Account Lockout Threshold to 5 invalid logon attempts.
</p>
<br />


<p>
<img width="1455" height="778" alt="image" src="https://github.com/user-attachments/assets/766035af-9bb5-4a06-8167-e6868e982297" />

</p>
<p>
Execute gpupdate /force in PowerShell or Command Prompt on DC-1 to immediately apply the updated Group Policy settings.
</p>
<br />

<p>
<img width="450" height="468" alt="image" src="https://github.com/user-attachments/assets/98602330-07b8-4e60-a050-e7260b909e54" />
<br/>
<img width="417" height="107" alt="image" src="https://github.com/user-attachments/assets/e71b42c6-7265-430a-9990-13d80c1a0e0b" />


</p>
<p>
Test the account lockout policy on Client-1 by attempting to log in with one of the newly created user accounts using incorrect passwords. 
  
After 5 failed attempts, verify that the system displays a warning indicating the account is locked.
</p>
<br />

<p>
<img width="1456" height="779" alt="image" src="https://github.com/user-attachments/assets/58239fe5-40b1-4e60-aa59-b3bc1cf96913" />
<img width="1455" height="780" alt="image" src="https://github.com/user-attachments/assets/b6fc0ecc-c2fa-49d7-827f-ef5b91c8311e" />


</p>
<p>
Access Active Directory Users and Computers (ADUC) on DC-1, identify the locked user account, unlock it, and reset the password, ensuring the user can log in after the account lockout triggered by multiple failed login attempts.

Steps:
1.Open ADUC on DC-1.

2.Navigate to the OU containing the locked user account.

3.Right-click the user account → Properties → Account → Unlock account.

4.Reset the user password to a new secure password.

5.Confirm the account is unlocked and the password reset is successful.

</p>
<br />

<h2>##Enabling and Disabling Accounts</h2>
<h4>I wanted to better understand how user account management works in real-world environments. 
 
 Enabling and disabling accounts is one of the most common tasks for IT technicians I believe, especially when onboarding or offboarding employees.</h4>
<p>
<img width="1456" height="780" alt="image" src="https://github.com/user-attachments/assets/f872c458-716f-48fb-bac0-ed8a619f7c54" />
<img width="448" height="421" alt="image" src="https://github.com/user-attachments/assets/401ed2f4-0ddb-47d8-84dc-80633ec4e5e9" />
<br/>
<img width="416" height="95" alt="image" src="https://github.com/user-attachments/assets/5b1dbf46-cc2d-4f28-bb40-85430347f44a" />


</p>
<p>
Using ADUC on DC-1, disable a selected user account. 
  
Test the effect by attempting to log into Client-1 with the disabled account, verifying that the system displays a notification that the account is disabled.
</p>
<br />

<h2>##Observing Logs</h2>

<p>
<img width="1455" height="777" alt="image" src="https://github.com/user-attachments/assets/4a8a166b-b734-47ee-beb6-afa4b5b105b0" />
<img width="1456" height="777" alt="image" src="https://github.com/user-attachments/assets/2b465518-3b17-4954-aa74-5924f66e829c" />


</p>
<p>
On Client-1, authenticate with an administrator account, launch Event Viewer, and examine the Security logs to monitor and verify failed logon events triggered by invalid login attempts or disabled accounts.
</p>
<br />



