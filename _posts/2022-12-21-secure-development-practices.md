# Some Practices to Make Software Development More Secure

With the growing amount of cyberthreats and a world that is moving online at an exponential rate, the times are necessitating developers to follow the best cybersecurity practices. It is not a secondary thing anymore, but a critical part of the Software Development Cycle that needs to be followed habitually. A cyberbreach can cause an organization millions of dollars on average. The additional costs of reputational damage increase this amount further. Most of the time, it has been observed that cyberattacks can be prevented or at least the damage from them can be minimized if some simple practices are adopted by all the stakeholders involved. So, here are some easy to follow guidelines to make your projects more secure on the internet.
### Choose and Manage Your Passwords Very, Very Carefully
You might think, _“Well, this is a very common thing. Everyone keeps their password secure.”_ and yet, this is one of the most common reasons for multiple large scale cyberattacks. The systems of a vast number of companies have been breached due to weak password policies. **Company-name@123** has been one of the most common passwords being used by developers for even sensitive access to assets like VPN connection, development environments and many more.
Here are some points for a good password policy:
- It is mandatory to use a good combination of Uppercase and Lowercase letters, special symbols, and numbers in your password.
- Your password should be at least 8 characters long at the bare minimum and preferably, it should be more than 16 characters long.
- You should not use any password from at least 5 of your last used passwords while changing your password.
- The password should not contain part of the username, real name of the user, their commonly known personal details like DOB or phone number, company name, or any word spelled completely.
- Do not use default credentials for any services, including third party services. Even if you are using software from a third party vendor, ensure that you get it changed from them, if the option for the same is not available on your end. Many times, passwords for third party software that is not available in documentation is available on the forums being used by developers for community help in debugging.

Besides implementing a strong password policy, an organization should also mandate changing the password compulsorily after a fixed period of time like 3 months or less and after any suspicious event or attempt of a cyberattack. Also, a proper alert system should be in place giving users an alert whenever their password is changed. This can help in minimizing the damage if a user’s credentials are compromised.

### Don’t use Hard-coded credentials in Application Source Code
It is recommended not to use credentials in plaintext for authentication to various services or API calls while writing the code of the application. There are multiple ways in which application source codes are often accessed by attackers. However, the possibility of exploiting the services is greatly minimized if the attacker doesn’t have the proper credentials. It increases the effort, time and resources required by the attacker for a successful exploitation and at the same time, gives the organizations a bigger window of opportunity to identify and take preventive measures as part of the responsive practices. Ensure that you don’t store passwords of the users in plaintext format in any database, and store them using a strong hashing algorithm.

###	Keep the Public Code Repositories of Your Project In check
If you are using services like GitHub and Postman to build your project, and you are habituated to upload code on these services, it is very much necessary to keep checking these repositories regularly. Even if you are publishing only test code on these services, if they are left out in the open, then they can reveal sensitive information to attackers. These can include application source code which can be used to find many vulnerabilities, hard-coded credentials, or it can also give an idea to the attacker about the level of security practices being followed by that particular department of the organization while writing code.
Postman API collections can also provide a lot of information about the working of the various components of an application. It has been further observed that many developers leave the API calls in publicly available API collections on Postman which can then simply be used by attackers to extract, delete or modify data.
If you have particular need to share the code publicly, then double-check your code before publishing it on any platform.

###	Developer Comments
Developer comments are one of the easiest ways to gain information about the application and its working if an attacker gets hold of the source code. Many times, developers even mention PII (Personally Identifiable Information) and plaintext credentials in the comments. This is specially true in case of legacy web applications. So, remove all the developer comments before deploying an application to production environment. If necessary, keep a backup of the code with comments some place safe.

###	Open S3 Buckets
Usage of cloud services has been on the rise ever since their arrival, and this has raised a new kind of threat landscape in the cyberspace. Various cloud services mostly provide a common way of storing the files in the form of storage blocks. Among all the vulnerabilities that arise in this regard, one of the most common ones is the public accessibility of storage blocks like S3 Buckets in AWS and Azure Blob storage. This can provide an attacker with various ways to gain access to system and sensitive information. It can also provide an attacker to host their own files, thereby leading to website defacement or using up storage space on the containers, which can increase the bills for the targeted company. Needless to say, this can cause financial and reputational damage for an organization.

###	Principle of The Least Privileges
It is very common, easy, and comfortable to give most privileges to users and developers. However, this can cause havoc in case of a breach. If a user requiring low privileges has access to even those resources that aren’t required, then this expands the horizon of exploitation for an attacker. Also, since junior developers in organizations are less sophisticated in terms of coding practices, they are more likely to fall prey to a cybersecurity attack. Hence, provide the least amount of privileges necessary for the task to the users of various systems and tools deployed by your organization.
Segregating users into roles can help in managing the privileges to a huge extent.

###	Proper Backups
Take proper backups of the source code and all the sensitive data that is critical to your business. Since Ransomware attacks are on the rise lately, the importance of this practice can’t be overstated. In case of a cyberattack wiping out the critical data, backups will be the best rescue for the restoration of the services of your organization. Also ensure that you keep the backups in reliable hardware storage locations that are easily accessible and highly secure. Backups, even though they look simple, need to be properly coordinated and routinely checked to ensure smooth functioning.

###	Suspicious Links and Emails
The good old social engineering is one of the most effective ways that attackers use to carry out successful cyberattacks. If you think that developers being tech-savvy individuals don’t fall for such attacks, you might be proven very wrong. Proper awareness regarding phishing emails is required to ensure that no user clicks on a link or interacts with an email that can lead to sensitive data falling into the hands of an attacker. Also, proper communication channels should be present within development teams and the IT Security department for reporting any suspicious communication received from external sources or even internal sources within an organization.

###	Suspend the Services that are not being Used
Do not leave that AWS EC2 instance open after its use cases have been completed. Open services and tools that are left out without being shut down even after their requirements have been exhausted can provide a very good entry point for any external attacker. Ensure that you keep track of all the online assets that you use in your software development process and close down everything that isn’t needed. This can help you save some money on the bills and can drastically reduce the attack surface your organization is exposed to.

###	Update Your Tools, Libraries and Services
This point simply can’t be repeated enough number of times. Always ensure that you are regularly updating the tools and services that you are using. Multiple new vulnerabilities are discovered everyday by researchers, and multiple patches are released by software vendors to fix them. While this process of regularly updating your software can seem to be exhausting and time-consuming, it increases the security of your systems by leaps and bounds. Most of the exploitation following a successful breach happens because of unpatched software programs being used by organizations. Using various threat detection and prevention programs is also advisable. They can alert you regarding any possible threat actor and also regarding the updates for various services and programs.

So, these are some of the best practices that you can follow and turn them into a habit while developing projects. If you are the owner or manager of a software or application within an organization, it is also advisable to regularly conduct Application, Network, Cloud security assessments, Source Code reviews, and Red Teaming exercises via a third party cybersecurity company or by internal security team to minimize the vulnerabilities and assess the breach exposure and threat level to your organization in the cyberspace.

I will keep updating this blog with more tips. Your suggestions are welcome.

Happy & Secure Development

Let's have a chat on Twitter:
[Abhishek](https://twitter.com/abhibhati4u)
