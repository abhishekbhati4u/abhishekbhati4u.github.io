# Reconnaissance - The Art of Looking for Secrets in Plain Sight 🔍🕵️

![Sherlock](/sherlock.jpg)

Reconnaissance is a very important activity in the realm of cybersecurity. It is the first stage in the five phases of ethical hacking and provides extremely valuable input for the several other activities that are undertaken in any cybersecurity assessment. The scope of the activity can be defined in a limited number of objectives or it can be taken extensively. One of the key things to note is that the activity of reconnaissance is never absolute in its scope and can also turn into a rabbit hole and can go on forever as well. There will always be something more to find, some more technique to try, some more tools that can give a few more results. It is upon the analysts to call a stop on the process when they feel that they have enough data in accordance with their objectives. And that requires a set of processes and a defined methodology to complete the activity in due time. In this blog, I present one such methodology with a list of tools that I learnt over the course of multiple reconnaissance activities and red teaming exercises. Also, for the sake of glamor, let’s call the organization for which we are doing the reconnaissance as the target organization.

Have categorized them into stages of the activity which can help to navigate and analyze the results gathered. So, let’s get started:

## Corporate Profiling

Corporate Profiling is done to gather general information about the firm or organization on whose assets the reconnaissance activity is being performed. It helps to get a general idea of the sector in which the company operates. This can later be utilized in other stages of reconnaissance and even further down the line, it can be used for penetration testing and red teaming. The information retrieved from the activity can also be utilized to gather the leaks available in the public internet for the organization. I try to categorize this activity in two phases:

### Organization Summary
In this phase, we try to list key information about the target organization or company. This can include details like the geography of its operation, its key industry, its revenue and its employee count. Let’s take a look at how each of this information can be utilized:
+ **The Geography for Operation:** The location where the company operates can often tell you about where its assets might be hosted. The awareness level, regulations and protections related to cybersecurity that might or might not be present in that part of the world.
+ **The Key Industry:** The industry in which the target company operates can tell you about the cybersecurity protocols that the competition and the industry as a standard follows there. Also, the sensitivity of the assets that are being utilized there. For example, the information systems in the healthcare industry are highly sensitive as they can literally present matters of life and death if the information systems are compromised. It can also tell you about the kind of attacks that have happened against that industry in the past. For example, continuing on the example of the healthcare industry, the recent past has shown us that ransomware attacks against the healthcare industry have been gaining popularity. So, you can look for the history of the attacks and then look if there were any past attacks against your target and how those weaknesses have been exploited. Those can serve as a good starting point for similar weaknesses.
+ **Revenue:** The revenue of the company can also tell you about the level of defenses that you can expect to find in the infrastructure of the company. This can also give you a hang of the type of cybersecurity teams that the company might have in place. A general notion that normally holds to be true is, “A company with a smaller budget almost always doesn’t have good cybersecurity in place, but it's not necessary that a company with a large budget has a good cybersecurity team in place.” Hence, this can help you to refine your approach further. For example, you may find weaknesses and you are pressed for time, you know there is a very less chance of any advanced defensive mechanism present, so you can be a bit more reckless with your obfuscation techniques. (Although, I would advise against it, as obfuscation and evasion are almost always fun. I mean who doesn’t like saying I evaded a detection mechanism that took them 💲💲💲💲	 to set up.)
+ **Employee Count and Department Composition:** The employee count will give you the scale of the IT systems that might be deployed within the organization. Collate that with the industry and you can guess the type of infrastructure that you might encounter. For example, a company in manufacturing with a small scale and headcount will have a significantly less number of IT assets compared to a software company of the same size. If you can somehow also enumerate the departments of the company and how many employees work there, you can be even more precise and granular in your attack path, but more on this perhaps later.

For this, Google, the website of the company, Wikipedia and other third party websites can be very useful for getting information about the company. Some of the third party websites that can be used are:
+ [Crunchbase](https://www.crunchbase.com/)
+ [Capital Market](https://www.capitalmarket.com/)
+ [Business Standard](https://www.business-standard.com/companies) 
+ [Owler](https://corp.owler.com/)

### Organisation Divisional Analysis & Organisation Offerings
In this step, we try to find out more information about the acquisitions and subsidiaries of the company that we are targeting. If the company has recently done some acquisitions, then it can help to increase the attack surface of the company as the corporate standard of the cybersecurity in place in the acquiring company is normally not present in the company that is being acquired. This can make them more vulnerable during the initial transfer of the assets between the company. The extensive sets of information for this phase includes domain names, IP Addresses, and Autonomous System Numbers of the identified subsidiaries and acquisitions. In addition to this, we also try to identify the various kinds of products and services that are being offered by the target company and the acquired company. For example, if the company is in SaaS business, you can expect to find a large number of internet facing applications which can vastly increase the attack surface. For this step, we can use the information available on the company’s website or through other third party websites.


After this, we move on to our next step in the process which includes attack surface discovery.


## Attack Surface Discovery
Attack Surface Discovery relates to the process in which we try to enumerate the major assets from the internet that are related to or owned by the organization. This can include the following:

+ **ASN Enumeration**
  + ASN stands for Autonomous System Numbers (ASNs) and they are groups of one or more IP prefixes run by one or more network operators that maintain a single, clearly defined routing policy.
  + The enumeration of the ASNs can give you information related to the Internet Service Providers being used by the company. It can help you to enumerate other services being used by the company as well. You can check if that particular ISP provides complementary network or software services as well and if they do, are those services being used by the target organization.
  + A useful tool for ASN lookup is [HackerTarget](https://hackertarget.com/as-ip-lookup/).
  + It can also be used to identify the subnets and the CIDR ranges.
  + You can also use [ASN lookup tool](https://github.com/yassineaboukir/Asnlookup)

+ **DNS Records Enumeration**
  + A lot of information can also be gathered by enumerating the associated DNS records for the target organization. The DNS records can be utilized to identify the correlation between the cloud services and the various associated CDNs as well.
  + One of the most popular and useful tools for DNS enumeration is the [AMASS project](https://github.com/owasp-amass/amass) from OWASP. It uses multiple sources and techniques to gather information related to the DNS records of the target organization. These include APIs, certificates, bruteforcing, Routing, Scraping, web archives, and WHOIS records.
  + Additionally, you can use bruteforcing and directory listing tools like [Gobuster](https://github.com/OJ/gobuster), [dirb](https://salsa.debian.org/pkg-security-team/dirb) or [dirbuster](https://gitlab.com/kalilinux/packages/dirbuster) to enumerate DNS records with some wordlists like from the [seclists](https://github.com/danielmiessler/SecLists/tree/master/Discovery/DNS).
  + Another useful tool for enumerating the DNS records is [DNSEnum](https://salsa.debian.org/pkg-security-team/dnsenum).
  + A useful command for this activity is dig. A sample dig command to find the A records for is as follows:
    ```dig companyname.com A```
  + A blog link regarding the dig command: [https://www.hostinger.in/tutorials/how-to-use-the-dig-command-in-linux/](https://www.hostinger.in/tutorials/how-to-use-the-dig-command-in-linux/)

+ **Domains and Subdomains Enumeration**
  + In this step, we try to find out about the domains that are alive using the DNS information and the TLS Certificates.
  + For this, first we need to identify all the parent domains belonging to that organization. There is no complete sure shot way of finding all the domains other than internet searches and finding out more and more about the domains from the information gathered during the entire recon process. Hence, it should be done iteratively by listing, verifying, enumerating and then again listing new domains that we find. For example, you might try to search for new certificates during the dorking process mentioned in the later sections and at that time, you might come across some new domains. So, you will need to again list them down, verify their ownership whether they belong to your organization or not and then enumerate them.
  + A useful tool for this step is the [subfinder](https://github.com/projectdiscovery/subfinder).
  + Make sure that the API keys are stored in the **provider-config.yaml**
  + Here is a useful [blog link](https://dhiyaneshgeek.github.io/bug/bounty/2020/02/06/recon-with-me/) for the tool usage.
  + A sample command for the same is as follows:
    ```subfinder -d companyname.com -o companydomains.txt```
  + Another useful tool for finding the subdomains is [assetfinder](https://github.com/tomnomnom/assetfinder). It is a fast go based tool.
  + You can also try to find out the [Sublist3r](https://github.com/aboul3la/Sublist3r) for subdomain enumeration.
  + After all the output from all these tools, you can create an extensive and unique list of subdomains belonging to that organization. This can then help you in the further steps of the process that include finding the IP Addresses, the web applications and more information about the third party services and softwares being used by the organization.
  + [Nuclei](https://github.com/projectdiscovery/nuclei) is also a very highly useful tool to find out information related to the subdomains and the possibility of vulnerabilities on them.
  + A command to find the IP addresses of the listed subdomains from the above process is:
    ```host -t a subdomain.com```
  + The listed IP addresses can be further utilized in the Network Security Phase of the activity.

+ **Domains Ownership Validation**
  + In this step, we try to verify whether the domains and the subdomains reported by the tool actually belong to our target organization or not.
  + We use the whois lookup to conclude this information and check for relatable logos or copyright information on that domain.
  + A useful tool for this activity is [GoDaddy WhoIs Lookup](https://in.godaddy.com/whois).


## Network Security
**IP Address Enumeration**
+ In this step, the IP addresses of the publicly facing assets of the organization are identified using the DNS lookups.
+ After this, the open ports on these IPs are determined with the help of various tools.
+ Nmap scans are used for active ports detection and shodan scans are used for passive port detection.
+ After this, the IP addresses are further scanned for known CVEs using shodan and other tools of your choice.
+ A link detailing about the commands for using Shodan CLI [https://cli.shodan.io](https://cli.shodan.io).
+ For active scanning of all the collected IP addresses, you can use [Nmap](https://nmap.org/) scans to enumerate the running services on the given IP addresses.
+ Some Nmap scripts can also be utilized to identify possible known vulnerabilities on the identified IP addresses. Two of such scripts are the [Nmap-vulners](https://github.com/vulnersCom/nmap-vulners) and Nmap [Vulscan](https://github.com/scipag/vulscan).


## Application Security
+ **Web Applications Enumeration**
  + In this step, the web applications of the target company are identified by establishing the ownership of the apps loading on the previously identified domains.
  + The tools [httpx](https://github.com/projectdiscovery/httpx) and [httpprobe](https://github.com/tomnomnom/httprobe) are highly useful to identify some applications running on the subdomains identified previously.
  + The application title, technologies being used by the application, status, IP address and the scope is determined.
  + The `curl` command can be used to get a lot of this information.
  + For taking screenshots of the homepage of the web applications, you can use the tool [WebScreenshot.py](https://github.com/maaaaz/webscreenshot).
  + The screenshots can help you to get a good idea of the overview of the applications and can help you to be precise in your approach to the target. For example, if you find a large number of applications from a particular vendor, then you can do credential stuffing of the default username/passwords for that vendor. From my experience, I can tell you that this approach can be ridiculously successful. ;-)
  + Another great tool to gather information about a large number of hosts is [Aquatone](https://github.com/michenriksen/aquatone). It can help you to gain an idea of a large number of hosts in a single go.
  + One more go based tool for website screenshots is the [gowitness](https://github.com/sensepost/gowitness).
  + After you have identified the applications and subdomains, it is a good idea to enumerate older endpoints from the subdomains. One of the most useful tools for this is the [waybackurls](https://github.com/tomnomnom/waybackurls). It will help to list down the older endpoints of the subdomains and applications that existed before.
  + After all the endpoints have been identified, these URLs can be fed to a secret finding tool like [JSFScan](https://github.com/KathanP19/JSFScan.sh) to find secret keys or other sensitive values from all the application code that can be enumerated.

+ **Mobile Applications Enumeration**'
  + Further, mobile applications are enumerated for the target organization using the Apple AppStore and the Google Play Store. Depending on the type of organization, you might need to look for the applications in other application distribution platforms as well.
  + Additionally, you can find the links to many mobile applications from web portals or landing pages of the company as well. Web Applications can help as a great supplement to enumerating the associated Mobile Applications.
  + For this, just search for the official publisher account of the target organization on the platform and then list down all the applications from that account.
  + After the mobile applications are enumerated, you can create their files and feed them to a static code analyzer. For example, for Android Applications, you can use [apkcombo](https://apkcombo.com/) to generate the APKs and then use the [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF) framework to identify security issues and sensitive data like keys. Another useful tool to identify secrets from the APK file is the [APKLeaks](https://github.com/dwisiswant0/apkleaks).


## Cloud Security
+ **Publicly Accessible Cloud Storage Resources**
  + In this step, we try to identify the cloud storage buckets that are publicly accessible.
  + If any open buckets are discovered containing sensitive data, then they are reported.
  + A useful online tool to check for publicly available cloud storage buckets is [GreyHatWarfare](https://buckets.greyhatwarfare.com)
After this, if you really want to do a deep dive in the Amazon S3 buckets security for the target organization, you can use some of the tools listed [here](https://github.com/mxm0z/awesome-sec-s3) according to your preference.

## Email Security Analysis
+ The process of filtering based on DKIM+SPF or header analysis can help detect whether the received email is a spoofed one or not. This is done for all the parent domains that have been identified in the Domain Enumeration process.
+ SPF Records and their analysis, DMARC Records and analysis, Aggregate Reports and Forensic Reports are checked for the primary domains of the target organization.
+ The `dig` tool can be used to find these records. Some such useful dig commands are:
  + `dig TXT <domain_name> | grep “v=spf”`
  + `dig TXT _dmarc.<domain_name> | grep “v=DMARC”`
  + `dig TXT <selector>._domainkey.<domain-name> | grep “v=DKIM”`
+ Another useful online tool to check for SPF and DMARC records is [SpoofCheck](https://www.smartfense.com/en-us/tools/spoofcheck/).
+ For checking DKIM records, [DKIM inspector](https://dmarcian.com/dkim-inspector/) can be used.
+ For using the above mentioned DKIM inspector tool, the DKIM selector will also be required. A DKIM selector is a string used to point to a specific DKIM public-key record in your DNS. The selector is specified as an “s=” tag in the DKIM-Signature header field and can be found in the technical headers of an email. Some common selectors that are used by various companies are:
  + Google: google
  + Microsoft: selector1, selector2
  + Everlytic: everlytickey1, everlytickey2 and eversrv (OLD Selector)
  + Mailchimp/Mandrill: k1
  + Global Micro: mxvault
  + Hetzner: dkim
  + Additionally, the DKIM selectors can also be identified by analyzing an actual email from the target organization.
  + Here is another useful tool [blog link](https://community.mimecast.com/s/article/dmarc-analyzer-dkim-selector).
+ If you want to identify the valid emails belonging to the users of that particular organization, you can use tools like [phonebook](https://phonebook.cz/). These can be useful during social engineering assessments. I have a detailed [article](https://abhishekbhati4u.github.io/2022/12/05/social-engineering-assessments.html) on the social engineering assessments.


## Leaks through Public Sources
+ Many times, a lot of sensitive information can be leaked through public sources as well and they are just there for the taking for anyone willing to look closely enough.
+ Several tools are available for identifying leaked credentials, personally identifiable information, application configuration details and other relevant information.
+ One of the best resources for completing this phase of information gathering is GitHub.
+ **GitHub Dorking**
  + Some good tools for GitHub recon are as follows:
    + [GitLeaks](https://github.com/zricethezav/gitleaks)
    + [GitDorker](https://github.com/obheda12/GitDorker)
    + GitHub dorking can very often give interesting results. So, it is advisable to manually verify all the findings from this phase.
+ **Dorking**
  + Google dorking and searching for information on the pastebin sites can help us to get a wide variety of information related to the target company.
  + Some good tools for Google Dorking are:
    + [PenTest  Tools](https://pentest-tools.com/information-gathering/google-hacking)
    + [Faisal Ahmed](https://dorks.faisalahmed.me/#random-fun)
    + In addition to all this, the dorking with in the tool of [codebeautify.org](https://codebeautify.org/) such as [jsonformatter.org](https://jsonformatter.org/) can show you old requests which might contain sensitive data.
  + In addition to this, you can also search in [postman.com](https://www.postman.com/) for finding publicly accessible collections of API requests pertaining to the target organization. If you are lucky enough, you can find some highly sensitive data in the API requests.


## Credential Exposure
Another useful tool to find out about the credentials exposed on the dark web is **pwndb**: [https://github.com/davidtavarez/pwndb](https://github.com/davidtavarez/pwndb)


## Botnet Infection
+ A botnet appears as a network of computers that have been infected by malware under the control of a single attacker, known as the “bot-herder.”
+ To check if any of the IP addresses of the target organization have been affected as part of a botnet, you can use the [FedoTracker](https://feodotracker.abuse.ch/browse/)


Note: A lot of the processes mentioned above can be automated using bash. 
A useful CLI command to run the tools on all the domains at once:
`cat <domain/ip-list-file> | xargs -I % sh -c '<tool-to-be-run> %'`
A reference link for the same for the usage of the tool is: [https://explainshell.com/explain?cmd=xargs+-I+%25+sh+-c+%22ping+%25%22](https://explainshell.com/explain?cmd=xargs+-I+%25+sh+-c+%22ping+%25%22)

These are some of the tools that I have utilized for reconnaissance as part of cybersecurity assessments.

Finally, a few words of caution, this article does not promote attacks against an organization for malicious purposes, and we intend it to be used only for security assessment with due permissions from the clients. I will continue to update the article with more tools and information we come across. Suggestions and recommendations are always welcome.

A special thanks to [Vatsal](https://twitter.com/vatsal_mob) for his suggestions regarding the tools.

For any suggestions or a general chat, reach out on [LinkedIn](https://www.linkedin.com/in/abhishekbhati4u) or any of the social media handles mentioned in the Footer of this page. I am usually active on Instagram as well.
