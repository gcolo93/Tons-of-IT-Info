### **User Authentication and Access Control**
Authentication, authorization, and accounting (AAA) describes the process of granting or denying access to data and network resources as well as verifying that the security controls are working properly. The first step is authentication, in which you confirm the user is who they claim to be. Next is authorization, where you define what that user is able to access. Finally, you must account for and report on the access that a user has been granted, including how often the user accesses the resource or data.

User authentication and access control refer to the way we access and get access to computer resources. It’s part of the category that includes authentication, authorization, and accounting or AAA.

Authentication, the first area, is about proving our identity. Typically, this involves using a name and a password to log into a phone, mobile device, laptop, website, or Google account. A username and a password, also referred to as login credentials, prove you are who you say you are.

Once a system validates user identity, the next step is authorization, which refers to what the user is allowed to do. Permission to do various tasks includes whether or not the user can open, delete, change, or print a document. Another type of authorization might be the ability to do something with a virtual machine— or to create a new one. Regardless of the situation, authorization is about our ability to do whatever we want to do with a particular system.

The third part of AAA is accounting, which means verifying that the rules we created are being enforced as expected, without unauthorized access. It also permits auditing of authorized access to figure out if there really was a breach, and, if so, when it happened or how it happened. Accounting helps us learn from these successful attacks, harden our defenses, and prevent similar future attacks. Another advantage of accounting is verifying that the things we think are happening, are happening. They say an administrator goes rogue and directs us to start copying data out of a system. We would receive that notification, note that it’s abnormal behavior, and have a second person validate, that yes, it's OK or no, something weird may be occurring and requires further investigation.

Now that we’ve discussed authentication, authorization, and accounting, let’s look more closely at the idea of access control and proving authentication. In reality, it's not difficult to figure out another person’s username and password. For example, a hacker may attempt to log into various websites using a known email address. Once the hacker confirms that the email address corresponds to an account for a particular website, the hacker would then attempt to determine the user's password for that account. Many people use the same password repeatedly, essentially saying, “Please hack me,” because eventually, someone will try the password that worked in one place to access another. A more secure option with better control is to use a password manager instead. However, passwords can be compromised or guessed.

Multi-Factor Authentication or MFA takes access control a step further. Sometimes called Two-Factor Authentication or 2FA, it combines something we know with something we have, such as an authentication device. What we know is the password; what we have can be a physical key fob with a code that changes every thirty seconds or a virtual version that runs on a smartphone. Other ways of providing multi-factor authentication include fingerprint, retina, or face scans. Each method proves you are who you say you are. Even if somebody steals your password, unless they also take your phone, fob, or whatever, they won’t have the ability to log in and act like you. The bigger a person’s potential attack surface, the more crucial is multi-factor authentication. Adding multi-factor authentication for sensitive sites like banking and credit card accounts enhances security, and everyone should use it.

To summarize, user authentication and access control refer to the way we access and get access to computer resources. Authentication is about proving our identity, which we typically do with a username and password or, more securely, with multi-factor authentication. Authorization is about our ability to access a particular system and use it correctly as per the set organizational rules. Finally, accounting verifies that users are following the rules we created as expected and that unauthorized users don’t have access to the system.
### **Authentication**
When you think of authentication, you may think of a person gaining access to resources, but authentication is actually just the process of confirming a person’s identity. A system can confirm your identity via usernames and passwords or with certificates, as is the case with public key infrastructure (PKI).

Microsoft Active Directory is an example of an authentication system that confirms the identity of users via passwords. Another example is your web browser, which can use PKI certificates to validate the identity of websites, such as those belonging to your bank or healthcare provider.
### **Authorization**
Once the identity of the user has been confirmed through authentication, the authorization system steps in to determine what the user may access. For example, can the user access resources in a particular subnet? Does the user have access to a particular server or file? If data access is in question, can the user write to or delete the data, or is the access read-only? The list of questions (and potential restrictions) goes on almost endlessly.

It is critical to apply restrictive permissions to your data and to carefully secure access to your servers and network devices. If left unrestricted, users could intentionally or accidentally gain access to confidential data and perhaps even post the information publicly. Keep in mind that permitting extra or unneeded access to data or servers is not just a risk for data leaks or breaches of confidentiality. You must also consider the potential for accidents. For instance, if a user’s computer becomes infected with malware, that user may accidentally infect all the data files that they can access on the network.

*Diagram. A typical AAA interaction.*Diagram DescriptionFirst, the client sends an access request. The server responds with access-accept (with exec authorization in attributes). The client then sends an accounting request (start). The server sends the accounting response to client. The client sends another accounting request (stop). The server sends the accounting response to client.
### **Accounting**
In a perfect world, accounting (auditing) would not be needed, but then again, in a perfect world you would not need authentication or authorization because everyone would be properly trained and live by the rules; unfortunately, this is not a perfect world. Thus, you have a need for the critical nature of accounting to verify that the restrictions you thought were in place are working as expected and that there is not attempted or actual unauthorized access. Accounting also includes verifying the correct access control settings on data files, providing a forensic trail after a security breach to determine how the attacker got in (to harden defenses for the future) and what they accessed (for damage control and potential changes to permissions in the future). The data gathered during the accounting process should be stored in a different location than the data that is being audited. In this way, an attacker cannot easily access your security logs or records and then change them to hide their attack. Additionally, these logs should be stored in an immutable, or unchangeable, form to prevent anything from happening, including the auditing system from changing or deleting the audit logs. Read access to this data should also be limited to those with a need to know; this typically includes security auditors and administrators.