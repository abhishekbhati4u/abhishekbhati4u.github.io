# Using GenAI to Resolve Vulnerabilities

![writing](https://i.ytimg.com/vi/bLKqf1gh_Z0/maxresdefault.jpg)

Hi, Namaste, Hello, Hola, Kon’nichiwa 😄

As you might have guessed from some of the previous articles that I have been posting, I have started using Generative AI for a number of tasks recently. No one wants to miss the bandwagon, so why should I?

One of the key areas in which I have been using these tools extensively has been for sharing recommendations related to patching.

One of the oldest discoveries of mankind is that nobody starts perfect. One of the most recent discoveries of mankind is that Generative AI Based tools also don’t start perfect.

Henceforth, I further discovered that none of us are perfect in using the tools according to our own use cases. I am unable to sleep right now. So, I thought of sharing my notes and some of the pitfalls, blind spots and improvement areas that I have come across during my course of using these tools. I will try to concentrate only on one very particular use case here, which many cybersecurity engineers might be able to relate.

And as always, just so that you don’t get bored, we will start with the story of Tom and Jerry. Just FYI, they have evolved now. Tom wants to fix some vulnerabilities, and Jerry is helping him by sharing recommendations and steps to patch the vulnerabilities. Jerry is also taking down notes about how to improve his skills and get a promotion. 


![tomandjerry](https://myinspiringthoughts.com/wp-content/uploads/2020/12/tomjerry1.jpg)


#### Not Giving Proper Context for Patching Vulnerabilities
One fine Friday evening, Tom comes to Jerry asking how to fix an issue on an application using Java. Since, Jerry wants to go out for drinks, he just enters a basic prompt that says something like “How to patch this CVE-2025-12ABC?”. In almost all the scenarios, this will give an answer that neither Jerry and Tom will like. Suppose the JAVA package file that is causing the CVE to be reported is being deployed as part of a package. In that scenario, the correct way to fix the issue will be to upgrade the package to the latest stable version. If the JAVA version in that version is not the latest, it will be a good course of action to contact the vendor for the same. **A correct context about the issue, the details about the tech stack, the constraints regarding the patch, the security tool that has reported the issue, the possible file location, when were the last updates done, the environment in which the application has been deployed and the use case of the application.** Adding as many details about the vulnerability will help to get more accurate information about the issue. You can read more about creating a refined prompt for the same in one of [my earlier articles](https://abhishekbhati4u.github.io/2025/06/07/prompt-engineering.html).


#### Not Sharing Details about Your Constraints to Patch
I personally feel that this is one of the most overlooked factors while using the Generative AI tools for finding patch recommendations. Suppose Tom wants to fix a vulnerability being reported for an older version of Spring Boot. Jerry prompts his GPT tool and gets a recommendation that the best way is to update the Spring Boot to its latest stable version. Even though this is the correct way to move forward, there might be certain conditions that might not allow an immediate upgrade. In that scenario, Jerry should ask Tom beforehand about the constraints that he is having. A major upgrade will take time and require proper testing from performance to availability metrics to ensure that nothing breaks down after the upgrade. However, if there is a patch that needs to be applied immediately, Jerry should ask for **individual packages** that can be **upgraded safely**, explore the **possibility of workaround patches**, take into consideration **defensive measures** such as firewalls that can be deployed for the time being.

#### Not Sharing Organizational Policies about Patching
Often, there are certain organizational policies that are necessary to be strictly enforced or alternatively allow some added leeway for patching vulnerabilities. Again, let’s say Tom is running a Django based application that needs an update to fix a CVE. Now, the application can be a crown jewel for the organization, and is publicly available, the reported CVE is being actively exploited. In that scenario, Jerry should prompt the GenAI tool accordingly and ask for the strictest measures that need to be shared as part of the recommendations, including the timelines for fixing such issues.

Alternatively, let's assume that Tom is asking the same about an application that is used only internally, and it has very few users. In that scenario, Jerry can prompt the GenAI tool about these conditions and provide Tom with recommendations that allow more time and flexibility to implement the patches.

Hence, in addition to the factors mentioned in the first two points, Jerry should share the **organizational policies related to security** with the GenAI tool while prompting it.

#### Assuming the developers will “take care of it”
The most presumption that security engineers have about developers is that they should take care of it. Let’s assume Tom comes to ask Jerry about how to fix an issue reported for a Third Party Package that he is using in his application. Jerry prompts his GenAI tool, finds information about the package version that contains the patch for the vulnerability, and shares the same with Jerry. In this scenario, however, it should be taken into account that the developer may not consider the stability of the application when applying the patch. So, in addition to the prompt with details mentioned in the previous points, Jerry should ask the GenAI tool to **share details about what can go wrong while applying this patch** and what Tom should be **cautious about**.

#### Assuming the “AI will take care of it”
Often times, we blindly believe that the output of AI will be accurate. However, several studies indicate that this implicit trust in AI tools can often cause more problems than it solves. If you want, you can [read this article](https://abhishekbhati4u.github.io/2024/03/01/security-risks-of-using-AI-Code.html) as well to know more about such cases.

Suppose Tom wants to deploy a patch for a vulnerability, but he knows that some patches can cause performance issues as it messes up another component of the application. However, Jerry assumes that the AI application will take care of it while recommending the patch. In that scenario, if Jerry doesn’t share the conditions that Tom describes, the GenAI tool may skip it and suggest a solution that, if implemented, may cause the application to break.

Henceforth, Jerry should ask Tom beforehand if there are any certain conditions that need to be **specifically taken care of and not depend on AI to assume those conditions. They should be told explicitly to the GenAI tool.**

#### Assuming that the Third Party Tool that you are Using Understands Everything
Let’s assume that Tom’s application is onboarded to a cloud scanning tool that scans for security issues. The tool also has an integration with ChatGPT that can recommend patches. Jerry logs in to the tool and ask for a recommendation related to a vulnerable jar file that is causing a CVE due to an older version. The ChatGPT integration takes into context the infrastructure which is EC2 on which the application is running and shares a recommendation to update the specific file to the patched version. However, what the integration misses here is that the package is a part of the running ServiceNow deployment that has its own package with the patch. _**Here, the AI tool may miss the context about the vendor, and it can cause problems later on if the file is individually updated.**_

Hence, Jerry should **not assume that the third party tool integrations of GenAI have all the context just because they are part of a tool he trusts.** He should **ensure as much context to AI as possible, and should manually parse the output at least once for any inconsistency before sharing any recommendations.**

#### Sharing Sensitive Information while asking for Patch Recommendations
Suppose Tom is asking to fix a vulnerability in some lines of code and asks Jerry for recommendations by sharing a code snippet of the vulnerability. However, in that code snippet, there are also API keys that Tom is paying for. In that scenario, Jerry should take care to **mask any sensitive data like that, including PII and other data that may raise privacy concerns.** In the unfortunate event of an attack like Prompt Injection, the data can be exposed if it's shared just as it is in the code snippet. Additionally, Jerry should use subscription and only GenAI tools authorized and recommended by his organization for generating recommendations. This ensures that the data shared by Jerry is not being used for any retraining purposes.

#### Depending on Openly Available Tools Rather than Organizational Deployment of Tools
As mentioned in the previous points, using public and free tools for security purposes always comes with a drawback, particularly around data security. Hence, Jerry should always **ensure that he is using only the GenAI tools that have been authorised by his organization.**
These tools have been tested against security test cases, data security concerns, have proper subscriptions and have relevant guardrails to protect any possible incidents. Additionally, they are mostly monitored with logging and monitoring solutions to detect any anomaly. This can control the impact in case of any security incident happening.

#### Not Asking the AI Tool to share detailed steps
Again, let’s assume Tom is asking for recommendations to fix a vulnerability in a particular snippet of code. Jerry asks the GenAI tool about the same. However, Jerry overlooks several possibilities that are normally present as part of patching a security issue. Jerry prompts his GenAI tool with just a simple prompt that says “Give me recommendations to patch this CVE in this code.” In addition to all the points mentioned previously, Jerry should also **ask for detailed steps post the patch and prior to the patch.** For example, Jerry can prompt the GenAI tool to consider all possibilities where this code snippet might be used in the context of the application. Then, ask it to share steps about identifying other possible places where the code might be used, how to patch it, the quality tests and security reviews that should be followed post the patch.



For now, this wraps up this small article. 

Will keep updating this blog with more tips.

Suggestions are welcome.

Happy & Secure Development.
