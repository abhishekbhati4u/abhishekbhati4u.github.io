# Getting Together for Security: Shared Responsibility Models

Hi, Namaste, Hello, Hola, Kon'nichiwa.

With the advent of everything coming as a service today, the lines between what you own and what you don’t are becoming blurred. Blurrier still are the lines between what you are responsible for and what the service provider is responsible for. In this blog, let us attempt to unblur a few of them.

Responsibility has a very broad and moral meaning, but being the mechanical beings of IT that we are, here we will stick to the security of information systems.

>“Anyone who says that a system is completely secure is either a liar or heavily drunk.”
>                                                        -Every sane cybsersecurity engineer ever

If you try to trace back the origins of the shared responsibility model or even more so the Shared Security Responsibility Model (SSRM), chances are that the first few pages of your search will somehow lead you to shared responsibility in the cloud services. And why not? The Cloud Service providers are some of the strongest advocates for this, and a lot of the underlying thinking developed from there. A great post by CrowdStrike details this out [here](https://www.crowdstrike.com/cybersecurity-101/cloud-security/shared-responsibility-model/).

Also, it will feel incomplete to mention this model with the mention of the big old cloud giant, AWS. AWS provides extensive [documentation](https://aws.amazon.com/compliance/shared-responsibility-model/) and details about what it considers shared responsibility with respect to the AWS services. One example for bifurcation between the security parameters managed by the customers and those to be managed by AWS, that they provide is as follows:
- Customer: The customer shares the responsibility for security **“IN”** the cloud. While it depends on the services that they select for operation, broadly speaking there are certain factors that are quite common here. They are responsible for managing their customer data, platform, applications, identity, & access management, operating systems, network and firewall configurations, etc.
- AWS: The AWS shares the responsibility **“OF”** the cloud. This includes the software managed by them such as compute, storage, database, networking and hardware that includes the factors such as the regions, availability zones, and edge locations.

An abstract feeling that occurs in the mind here is that the shared responsibility of security means that whatever is manageable only by the vendor is the responsibility of the vendor and whatever is manageable by the customers (let us consider ourselves a Richie Rich customer) here is the responsibility of the customers (i.e., us). And that makes sense. We are responsible for what we own and manage. But somehow, the shared responsibility model also places the responsibility between us and the service provider in a mutually exclusive manner. Hold on to this thought for a while.

A worthy point to add here can also be that this is not limited to the cloud, but most of the software products that are offered in the market currently. Take, for example, a SaaS product to manage employee payroll data. Well, the service can manage the data of your employees that is stored on their servers, but if one of our employees falls for a phishing attack and adds the portal credentials, then the responsibility falls on us rather than the service provider.

Also, if we are the Richie Rich that we assumed to be for the narrative, then our company uses tons of such third party services and portals. So, there will be a lot of dependency in terms of security on the third party vendors. In addition to the monitoring and security intelligence service of the internal security team, we need to be sure that the third party vendors are also investing enough in their cybersecurity services.

Now, with these distinctions, the question arises as to how to manage security in such a state. Well, the first thing to do is to remove the distinction that this is a mutually exclusive game. (Now you can leave the though that I told you to hold on to earlier). It's not a gladiator combat arena for security teams, but rather a space for collaboration. The vendors are responsible for making sure that they are following the security measures during the development of their product, along with the communication of the security hardening guidelines to the customers (i.e., us). Our internal security team is responsible for the implementation of the guidelines and ensuring that the relevant detection mechanisms as an additional layer of defence are also in place.

One of the greatest managers of all time, Michael Scott (Regional Manager, Scranton Branch) of the Dunder Mifflin Paper Company, Inc. once said in his depressed moments,


![MichaelScottResponsibility](https://cdn.quotesgram.com/img/19/48/589920233-lol-michael-scott-quotes-the-office-Favim_com-812827.jpg)



But understanding that this was during one of his worst moments and gaining wisdom from that, it is imperative that during any incident, rather than starting a war with iron fists, the first step that any service provider and consumer should take is to analyse the incident. A collaboration between our internal security team and the vendor can help to minimise the damage in case of any breaches. For that, a certain degree of transparency is required. Better get that in the purchase agreement of the services itself. Additionally, if the internal security team also finds some issue in the products that they are using they can report it to the vendor as there might be many, many use cases which are uncovered only during actual use.

So, that wraps up this short article as to how the security should be managed.

Will keep updating this blog with more tips. Suggestions are welcome.

Happy & Secure Development.
