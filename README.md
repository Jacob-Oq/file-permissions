<p align="center">
<img src="https://i.imgur.com/xlYwPUf.png" alt="Permissions Photo"/>
</p>

<h1>Understanding File Permissions</h1>
This lab focuses on file permissions and shares in the context of an Active Directory domain. File permissions and shares are key in a business setting to make sure users have the appropriate permissions and access to files they need. This is building up from a previous lab where we have a client joined to a domain. I am logged in as an admin account on the domain controller VM and as a normal user on the client VM. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>

<p>
In order to set permissions to folders and files, we need to create the folders to share. While logged in to the domain controller VM as an admin, create the folders. We can create 4 appropriately named folders (read-access, write-access, no-access and accounting) to set permissions to on the C:\ drive. 
</p>

![FP 1](https://github.com/Jacob-Oq/file-permissions/assets/150084528/45ed18d5-6984-4bc5-892e-5cb842b7c6cd)

<p>
To share a folder and assign permissions, open the folder's Properties and click on Share under the Sharing tab. You can specify people on the network to share with and assign appropriate permissions. I set the following permissions for the folders: Domain Users can Read the read-access folder and they have Read/Write permissions on the write-access folder. Domain Admins have Read/Write access to the no-access folder. (the accounting folder will be changed later).
</p>

![FP 2](https://github.com/Jacob-Oq/file-permissions/assets/150084528/625cafb8-b825-4ee6-a65e-3c73b703ec9c)

![FP 3](https://github.com/Jacob-Oq/file-permissions/assets/150084528/fcc512a2-5e78-4bfe-b1ff-5859290cbd18)

![FP 4](https://github.com/Jacob-Oq/file-permissions/assets/150084528/7e8c0527-4ec8-4562-867e-bcd14581c9ea)

![FP 7](https://github.com/Jacob-Oq/file-permissions/assets/150084528/edabb7eb-ba56-4129-af72-40b01f3d0d14)



<br />
<p>
On the client VM, navigate to the shared folders through the following path in File Explorer: \\dc-1. We will notice how some folders cannot allow you to add files, but only view them. One does not allow access at all. This is because as a Domain User, permissions for the folder are tied to the respective Security Group and the folder's own set permissions for users within that Security Group.
</p>

![FP 8](https://github.com/Jacob-Oq/file-permissions/assets/150084528/b275bb6f-0101-4e7f-9aff-9237589c86bf)

![FP 9](https://github.com/Jacob-Oq/file-permissions/assets/150084528/eeef7ceb-1e85-48e7-8b4f-24a5acba9645)

![FP 10](https://github.com/Jacob-Oq/file-permissions/assets/150084528/30cce471-9789-4857-8831-db4302fea53d)


<br />
<p>
Next, we will make a new Security Group and assign appropriate permissions to the accounting folder. On the domain controller, have the Active Directory Users and Computers panel open. Create a new Group called ACCOUNTANTS. After creating the new Group, go to the accounting folder and assign permissions to the folder so the ACCOUNTANTS Group has Read/Write permissions.
</p>

![FP 13](https://github.com/Jacob-Oq/file-permissions/assets/150084528/aacd9a04-623f-4a32-93a6-a27394bf56c9)

![FP 14](https://github.com/Jacob-Oq/file-permissions/assets/150084528/2c488f6c-e960-413f-a43d-52dc8da3e0c0)

<br />
<p>The user cannot access the accounting folder because they are not part of the ACCOUNTANTS Security Group.</p> 

![FP 15](https://github.com/Jacob-Oq/file-permissions/assets/150084528/8fa0d42e-6903-4b76-91d1-62b0f11e97c0)

<p>
Log off the client so that the permissions are in place by the time the client is logged into again. On the domain controller, open the ACCOUNTANTS Properties on Active Directory Users and Computers. In the Members tab, add the respective user. In my case, it is bap.toq. Upon logging into the client, bap.toq is now able to open the accounting folder because they are part of ACCOUNTANTS.
</p>

![FP 16](https://github.com/Jacob-Oq/file-permissions/assets/150084528/5e750dc6-ceb1-43d9-a5bb-c8ed3d28215c)

![FP 17](https://github.com/Jacob-Oq/file-permissions/assets/150084528/7eaf3869-c11d-4443-88b5-5774cb325d43)

![FP 18](https://github.com/Jacob-Oq/file-permissions/assets/150084528/785f6063-5c58-4f6a-b8c9-75accb7173f8)


<br />

<h2>Final Thoughts</h2>

This lab should help develop an understanding how file permissions work in the context of Windows/Active Directory. In a real setting, we may have to set permissions so that people can only access what they need to in order to complete their work. It is not necessary to give more permissions than what is needed.
