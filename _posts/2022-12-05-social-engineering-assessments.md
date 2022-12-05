# TWO CENTS ON SOCIAL ENGINEERING ASSESSMENTS

Hi, me and my colleague [Vatsal](https://github.com/vatsal-mob) started with Social Engineering assessments almost a year ago and after conducting such assessments for multiple clients now, we thought to share our two cents from what we have learned about social engineering. In particular, we will be covering email based phishing assessments since they are the most common ones.

Social engineering assessments are conducted to assess the organization’s level of resistance and awareness against attacks targeting human weaknesses. We attempt to target users by sending them customized messages that can trick them into sharing credentials or other sensitive information that can then be utilized in order to conduct further attacks against the victim person or organization.

Phishing is one of the most common methods to gain an entry point to the internal network of an organization.

In this document, we discuss a series of steps and methods that we have learned over a number of assessments that can help you to become a pro fisherman. So, keep your patience and let's tell you about some great fishing rods to catch some tuna.

## THE BEGINNING

We start the phishing assessments by asking the client requirements as a first and foremost process. 

*Pre-requisites and Client Requirements:* 

* Start with the reason that the client is asking for phishing or social engineering. There can be multiple reasons for the phishing assessment:
  * The client has suffered a phishing attack before.
  * They want to judge the normal awareness level in the organization.
  * They work in an industry that is sensitive to phishing attacks. Banks in particular are extremely sensitive when it comes to phishing assessments.
  * They want to check the email or other related security parameters implemented in their organization.
  * This will help you to customize the email or other messages later down the assessment.
* Ask whether the client wants a black box or white box phishing assessments. But what are these two new fish in the pond?
Well, both are related to our normal VAPT terminology. In **black box** phishing, the client will not whitelist our email domains, or help us to evade their spam filters. We will have to increase the reputation of our domain, evade the spam filters and do everything else on our own. The maximum information that we will get is the list of the users that the client wants to be targeted. ***Sometimes, the client won’t give us even that list, we have to find the users of the organization and their email addresses ourselves.*** In **white box** phishing assessments, the client will give us the list of the users, help us evade spam filters by changing their email policies during the assessments, and whitelist our email domain and Web URL for the duration of the assessments. Any other support from the client that lies in between these two extremes of white box and black box assessments is a gray area and can be considered GREY BOX ASSESSMENT.
* The question of the white box or black box assessment is extremely important as it will help you and the project manager in deciding the timeline of the project. We will discuss the timeline at the end also.
* An important point to note here is that if the client uses O365, then there are high chances that Emails from domains other than the company’s domain will land in the spam box as O365 has very strict policies. In that case, you need to request the client to whitelist your domain to conduct a successful phishing assessment.
* Once the discussion about the type of the assessment is over, you should ask about the status of the targeted users from the client, their criticality. If a number of high ranking executives are part of the assessment, **HANDLE THE GATHERED DATA EXTREMELY CAREFULLY.**
* Most of the time, phishing assessments are conducted as part of the red teaming activities. Some of the data that you found in the Red Team Assessment can be useful in the phishing assessments. So, keep this in mind and if you have found some sensitive data that can be useful in phishing assessment, discuss with the project manager, the team and if required, the client before using it.


## RECON AND INFORMATION GATHERING

After the project scope and prerequisites are gathered, the information gathering phase needs to be initiated. In this phase, we try to determine the domain that we might be using for phishing and the landing page.

The first step in the process involves finding a similar sounding domain and purchasing it. For example, if you are performing phishing on *allaboutmobilephones.com* , then a good phishing domain can be *alllaboutmobilephones.com* or *allboutmobilephones.com*. It is a good idea to have the extra or missing or changed characters somewhere in the middle of the phishing domain name and not in the beginning or end. For example, the extra ‘l’ in the first domain name and the missing ‘a’ in the second domain name. This makes it harder for the victim to distinguish between a phishing domain and a normal domain. The domain’s reputation can be checked from multiple sources. The following links can be used to check the reputation of the domain:

* https://postmaster.google.com/
* https://mxtoolbox.com/blacklists.aspx
* https://multirbl.valli.org/lookup/
* https://transparencyreport.google.com/safe-browsing/search?hl=en 

The domain can be registered from GoDaddy or any other service, and then it should be left idle for at least two weeks to increase its reputation. We will cover the process of selecting and setting up the landing page in the infra setup section. Keep this in mind when you discuss the timelines of the project with the client. Also, it is advisable to purchase the domain as soon as possible, preferably after the subdomain enumeration is done, so that you have ample time for the rest of the process. In addition to that, it is advisable to purchase at least two domains for phishing in case one of them gets blacklisted. Domains also get blacklisted frequently during the setup process. Hence, you also need to consider the scenario of things going south.

Once the domain is decided, start searching for information about the list of the victim users. LinkedIn is the best place to find out about it. However, due to a fiasco that happened some time back, LinkedIn prevents web scraping tools aggressively from collecting information.
You can still search for the information by using LinkedIn by manually going to each page. We try to automate a bit of it by google queries and [BulkURLOpener](https://chrome.google.com/webstore/detail/bulk-url-opener/kgnfciolbjojfdbbelbdbhhocjmhenep?hl=en) browser extension. In addition, [phonebook](https://phonebook.cz/), [hunter](https://hunter.io/) and [rocketreach](https://rocketreach.co/person) can be a very useful tool to extract emails related to an organization. Rocketreach in particular is a really good tool to find verified emails, but it is a paid tool with limited number of results in the free tier, so you might need to try a few tricks ;-).

Since most of the phishing engagements are part of the Red Team Assessment, the landing page is chosen from the list of the login websites that we found during the recon process. The login page should be the one that most of the victim users to be targeted might be using. Post identification of the page for phishing, the next step is to replicate but one step at a time, we will cover it in the infra setup.

Post deciding all the domains, it is advisable to search for any known phishing attacks that might have happened against the organization in the past. This can help a lot in deciding the email template and theme. Even when the client tells about the phishing assessments that have been conducted or the phishing attacks that have happened in the past, this information can be highly useful as it can often reveal information and psychological mapping of the victims regarding the awareness among the target organization’s users. 


## INFRASTRUCTURE AND RESOURCES SET UP

Post gathering all the information, we start with the infrastructure setup to get started with the entire process. From this point, the activity can fork into two paths, depending on the phishing manner in which you want to complete the assessment. You can take the path of the MiTM server, or you can set up your own landing page from the list of the applications you want to consider that you found in the recon process for the client. It is even possible that the client wants an engagement based on social media. So, in that particular case, it is advisable to use content and infrastructure related to that particular social media to use as the landing page for the social engineering engagement. 

###### Using an MiTM server for Phishing

MiTM phishing is conducted by making a server sit between the targeted users and the actual website services. The phishing server captures the credentials and the authentication tokens that the users submit. Evilginx is one such server configuration that comes with preconfigured templates for multiple popular websites used in the enterprise and consumer sector alike. This includes websites like Google, O365, Paypal, Citrix, GitHub, Instagram, Facebook, etc.

It works on the principle of reverse proxying to capture the credentials. It is also to be noted that it is one of the most successful solutions for doing phishing assessments on services that are likely to have 2FA enabled for their users. It can capture the cookies and authentication tokens as well that can be loaded in the browser to replay those credentials and gain actual legit access to the victim accounts. This can also help in gaining the initial foothold and provide the starting point for the Red Team Assessment assessments.

The complete setup for the Evilginx has been documented in great detail in this blog link by [Cilynx](https://cilynx.com/how-to/evilginx2-vs-2fa-phishing/424/). As mentioned in the blog link, the phishlets provide attributes that can be altered according to the need of the assessment. Evilginx can be installed on your server using this [GitHub link](https://github.com/kgretzky/evilginx2.git). 
It is also worth noting that first you will have to install the SSL certificate for the server before adding the phishing template configuration (known as phishlets) for any service. You can install the SSL certificate by using certbot.

You can use the following command to install the SSL certificate using Certbot:
```
sudo apt install openssl keytool certbot
certbot certonly -d "<DOMAIN>" -d "*.<DOMAIN>" -a manual --preferred-challenges dns --register-unsafely-without-email
```

Post setting up the Evilginx, you can embed the link to it in your email and send it to the victims for starting the assessment. It is imperative that you continuously monitor the credentials that are being captured by Evilginx during which your assessment is taking place.

###### Using Customized Phishing page

Although Evilginx is quite a good tool to conduct phishing assessments, many times it is good to conduct phishing assessments for the clients based on customized phishing pages based on the client’s login page.
So, the process here starts by some recon and finding out applications from the client’s organization with these characteristics:
* They should be easy to clone and load. Hence, they should be simple login portals.
* If the phishing assessment is part of an Red Team Assessment, the application should be such that it is used by most people in the organization. If you want to narrow down and are targeting a particular kind of portal, like VPN access page, then you need to do also consider the users that you will be targeting.
* The application should also be of enough critical nature that everyone feels the urgency to open the phishing link once the email is received.
* The application should also be one whose credentials are likely to be used in other portals as well so that you can compromise multiple login portals for a single person in one go.

Once the application is decided, you can make a copy of the application using software like [httrack](https://www.httrack.com/). After that, it is suggested that once the application has been successfully hosted, it should be viewed in different resolutions to ensure that it is appearing correctly and as intended on screens with all resolutions. In addition, if the page decided upon for the phishing uses https, then it is recommended to generate a SSL certificate and ensure that it is reflected correctly across the internet as we did in the Evilginx setup earlier.

Once the page is hosted, you can use the following python script to generate traffic for the website. It can also be useful to use this script in conjunction with the [proxychains](https://github.com/haad/proxychains) tool. Just remember this script, once your phishing page is set up, this script will be your PR in the mess called the internet.

 ```
 import webbrowser
 import schedule
 import time
 def task():
  webbrowser.open('https://phishingassessmentsite.com')
  print("socket probe done")
  schedule.every(20).seconds.do(task)
 #20 means every 20 seconds, should change this to a relevant time frequency
 while 1:
	 schedule.run_pending()
	 time.sleep(5)
```

You should regularly keep checking the reputation of the domain to avoid getting blacklisted using the tools described earlier.
After the page is hosted, you might want to use GoPhish for sending the campaign and tracking the credentials. The GoPhish website describes it as “a powerful, open-source phishing framework that makes it easy to test your organization's exposure to phishing.” Setting up GoPhish is a time taking process, and it will be out of scope for this article. So, we will suggest going through the [Installation Docs](https://docs.getgophish.com/user-guide/installation) or perhaps also a [freecodecamp tutorial](https://www.youtube.com/watch?v=S6S5JF6Gou0). This [blog](https://www.sprocketsecurity.com/resources/never-had-a-bad-day-phishing-how-to-set-up-gophish-to-evade-security-controls) link by Sprocket Security details the various customizations that can be done in order to get the required setup of GoPhish. Additionally, you can use your own code to get the task done, as mentioned in this blog post by [NullByte](https://null-byte.wonderhowto.com/forum/make-phishing-page-for-harvesting-credentials-yourself-0185161/).

## EMAIL

One thing that we have kept a distance from till now and which should be done parallelly along with this process is phishing email itself. First of all, you need to decide on the email template.
To decide on that, it will be advisable to look at the services provided by the company and check for benefits they provide to their employees. This can help in deciding the theme of the email. For example, if you are doing a phishing attack on an ecommerce platform, it will be nice to plan an attack based on special discounts for the employees one week ahead of the Christmas season. A useful way to gather this information can be the section of the [Ambition Box](https://www.ambitionbox.com/) profile of the company containing the Employee benefits.
After the email template is decided, then you should go ahead and write the email. You should ensure that the email theme is as close as it can get to the actual emails sent by the company. To get a gist of the email format, signatures, titles being used by the company, you can send an email to the customer care, sales department, etc. about some inquiry for business, and you can guess the format from the email you receive in response. For example, if you are assessing a company selling paints, it will be good to email them asking about the estimated paint prices for a 12-floor building that you want to get constructed and get a brochure on the email ;-). 

Post that, you need a service for sending the emails. There are many out there, including the best ones called [MailChimp](https://mailchimp.com/), [MailGun](https://www.mailgun.com/) and [SendGrid](https://sendgrid.com/). The setting up process of the mail service including the DNS Records and other things will be a different process and one that needs proper referencing with the relevant details of the setup. Hence, we suggest referring to the installation docs of these services. Also, if money is not an issue, it is advisable to use dedicated IP addresses for sending the emails as they have a lower chance of being blacklisted in the past. Even when the client has whitelisted your domains, there is a high chance that the spam filters of the email client will block the emails from a blacklisted domain, which brings us to our next problem, evading spam filters. Also add the relevant DNS records to your domain to increase the reputation of your domain. If a domain is not spoofable, then it has greater reputation. The spoofability of the domain can be checked using the [SmartFense Spoofcheck](https://www.smartfense.com/en-us/tools/spoofcheck/). Similarly, you can check the DMARC records and other relevant records using the tool [DMARCAnalyzer](https://www.dmarcanalyzer.com/). You can find information about DMARC, DKIM, SPF and BIMI records along with various tools on the website.

If it is a black box phishing assessment, then evading spam filters will be a time taking and tiresome process of the assessment. After you have written the email, check for the spam words using tools like [Emailtooler spam Word Analysis](https://www.emailtooler.com/spam-words-analysis/#), [Blogiestools Email Spam Trigger Words Checker](https://blogiestools.com/email-spam-trigger-words-checker-tool/), or the [MailMeteor Spam Check](https://blogiestools.com/email-spam-trigger-words-checker-tool/). After that, you need to test if the email lands in the Spam by using the same email client as the target. But prior to testing on the email client, it is advisable to check using tools like Free Mail Tester & Email Deliverability Test by [MailGenius](https://app.mailgenius.com/). This is because if an email from a domain lands in spam for an email client like Outlook, then it becomes highly likely that the next email from the domain will be checked stringently will land in spam, and this probability increases with every following email. 

Post this, you need to send a few Email IDs on the target email client and check for the spam. It is advisable to use multiple email IDs for them and for automating the email sending process, you can use a python script like the one mentioned in this blog by [RealPython](https://realpython.com/python-send-email/). 

When the testing is done, you need to decide the timing at which the campaign needs to be launched. The time should be such that most employees check the email and click on the phishing link. This will depend a lot on the theme and content of the email, the position of the individuals targeted, the nature of the department, etc. With GoPhish, you can time the campaign and launch it to automate a lot of the stuff.

## CLOSURE & REPORTING

After the setup and testing is done, you launch the campaign. Post that, you need to gather the results and prepare a report. If you used GoPhish, then the process will be very easy for you. Here, we would like to keep this short and will discuss some of the key factors while reporting:
* You need to report the users for which you gathered the credentials.
* If it was part of the scope, then you need to check the login with these credentials for their validity.
* If the portal had 2FA, and you got the cookies of the user, you need to check them using browser extensions like Edit My Cookie.
* The other metrics like the number of times the email was opened, the number of times a user clicked the link should also be presented.
* The pattern of users during the assessment, for example, if the users of a particular department fell for the phishing email more than others, then that should be highlighted.
* Recommendations for training and awareness program for the individuals that fell for the phishing attack.

The reporting will highly depend upon your organization practices and the client’s organization structure. So, you need to develop it accordingly.

At last, a few words of caution, this article **does not promote attacks against an organization for malicious purposes, and we intend it to be used only for security assessment with due permissions from the clients.** Phishing continues to be one of the foremost reasons for major cybersecurity incidents, and a good phishing assessment and appropriate training program can help a lot in improving the cybersecurity posture of an organization. We will continue to update the article with more tools and information we come across. Suggestions and recommendations are always welcome.

Happy Fishing

For any suggestions or a general chat, reach out to us on Twitter:

[Vatsal](https://twitter.com/vatsal_mob) and [Abhishek](https://twitter.com/abhibhati4u)
