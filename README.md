# PENETRATION TESTING REPORT

## FOOTPRINTING & NETWORK SCANNING PHASES

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Field | Details |
|---|---|
| **Pentester Name** | Marouane Doaa |
| **Program/Batch** | B084-Networkwalks |
| **Date** | 12 November 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools); W2-PM3 (Footprinting with Maltego); W2-PM4 (theHarvester-based Footprinting Attacks); W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. NetworkWalks (written permission secured); 2. My own local LAN network |
| **Permission secured from client?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting; **Phase 2:** Scanning & Network Discovery; **Phases 3–5:** In Progress |

---

# 1. Liability Disclaimer

I confirm that all cybersecurity activities documented in this report were performed only on systems and devices that I own or for which I had obtained the necessary authorization. These activities were conducted strictly for educational and research purposes as part of the NetworkWalks internship program (Batch B084).

I understand that unauthorized access to computer systems and networks is illegal and may result in legal consequences, even if no damage is caused.

I acknowledge that I am solely responsible for my actions and for ensuring that all activities are conducted ethically, legally, and within the scope of the authorization granted.

# 2. Introduction

This report presents the practical activities completed during Week 2 of my NetworkWalks internship (Batch B084). It covers four modules: W2-PM1, focused on domain footprinting using Kali Linux tools; W2-PM3, focused on footprinting with Maltego; W2-PM4, focused on information gathering using theHarvester; and W2-PM5, focused on scanning my own local network using Zenmap.

The report includes the commands and procedures used, the results obtained, supporting screenshots, and brief explanations of the security relevance of each activity.

# 3. Tools Used

The following table presents the tools used in this report and their main functions.

| Tool | Purpose |
|---|---|
| **Kali Linux & Windows** | Operating systems used for reconnaissance activities. |
| **WHOIS** | Find domain registration details (owner, dates, name servers). |
| **WhatWeb** | Fingerprint web technologies (server, CMS, plugins, IP). |
| **Nslookup** | Resolve the domain name to its IP address using DNS. |
| **Curl (`-I`)** | Read the HTTP response headers of the website. |
| **Wafw00f** | Detect whether a Web Application Firewall protects the site. |
| **DNSRecon** | Enumerate DNS records (NS, MX, SPF, TXT, SRV). |
| **Maltego** | Visualize relationships between entities and gather publicly available information, such as email addresses related to a target domain. |
| **theHarvester** | Gather publicly available email addresses, subdomains, hosts, and other information related to a target domain. |
| **Zenmap (Nmap GUI)** | Scan the local subnet to find live hosts, IPs and MAC addresses. |
| **Windows CMD** | Identify local IP and MAC addresses. |

# 4. Activities Performed

## 4.1 Footprinting & Reconnaissance

I performed reconnaissance on the networkwalks.com domain using six Kali Linux tools: **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, and DNSRecon**. Each tool helped gather a specific type of information about the target.

First, I used **WHOIS** to retrieve publicly available domain registration details, including information about its name servers and registration.

Next, **WhatWeb** was used to identify the technologies running on the website. The results revealed **WordPress 7.1.4** and **WP Download Manager 3.3.76**, along with other technical details.

I then used **Nslookup** to resolve the domain name and identify its IP address, which was **192.232.216.135**.

I used **Curl** with the `-I` option to inspect the website's HTTP response headers. The response confirmed that the website was accessible (HTTP 200) and revealed information about its server configuration, including the use of Apache and the WordPress REST API endpoint (`/wp-json/`).

After that, I used **Wafw00f** to check for the presence of a Web Application Firewall. The tool identified **ModSecurity (SpiderLabs)**.

Finally, I used **DNSRecon** to enumerate the domain's DNS records. The results identified two name servers, the mail server, the domain's IP address, SPF and other TXT records, as well as SRV records related to the Autodiscover service. The tool also revealed the DNS software version running on the identified name servers.

## 4.2 Footprinting with Maltego

For this activity, I installed and used **Maltego** on a Windows computer to gather publicly available information related to the target domain **networkwalks.com**. The objective was to identify email addresses associated with the domain.

First, I created a new Maltego graph and added **networkwalks.com** as the starting entity. I then used the **To Emails @domain [Search Engine]** transform to search for email addresses associated with the target domain.

The transform completed successfully in approximately 18 seconds and returned **one entity**. However, the execution log alone did not provide enough information to confirm whether this entity was an email address.

This activity helped me understand how Maltego uses transforms to collect information and visualize relationships between different entities during the footprinting process.

## 4.3 Footprinting with theHarvester

For the third activity, I used **theHarvester** in Kali Linux to gather publicly available information related to the target domain **microsoft.com**. The objective was to identify email addresses, subdomains, and other information using different public sources.

First, I used **Baidu** as the data source and set the search limit to **1,000 results**. However, the tool did not find any IP addresses, email addresses, people, or hosts associated with the target domain.

Next, I performed another search using **all available sources** with a limit of **50 results**. During this search, theHarvester attempted to collect information from several sources, including Baidu, DuckDuckGo, CRT.sh, and HackerTarget. However, many other sources could not be accessed because their required API keys were missing or invalid.

This activity helped me understand how theHarvester collects publicly available information from different sources and how API key requirements can affect the results of a footprinting process.

## 4.4 Network Scanning with Zenmap

For the last activity, I used **Zenmap** to perform network discovery on my local Wi-Fi network. The objective was to identify my local network configuration, discover active hosts, and examine their IP and MAC addresses.

First, I used the Windows `ipconfig` command to identify my local IPv4 address and subnet. I then entered the corresponding network range into Zenmap and selected **Ping Scan** to discover active devices on the network.

The scan successfully identified **3 active hosts**. The results displayed their IP addresses and, where available, their MAC addresses. For privacy and security reasons, the device names were anonymized, the last two parts of the IP addresses were partially hidden, and the MAC addresses were fully masked in the screenshots.

Finally, I used Zenmap's **Topology** tab to visualize the discovered hosts, enabled the legend, and exported the network topology as a PDF file.

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| # | **Risk / Finding** | **Evidence / Observation** | **Potential Impact** | **Risk Level** |
|---:|---|---|---|---|
| **1** | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager. | Attackers may use exposed technology/version information to identify software requiring further security review. | **Medium** |
| **2** | Server IP address identifiable | Nslookup resolved the domain to 192.232.216.135. | Provides information about the network location of the web service. | **Low** |
| **3** | HTTP technical information exposed | Curl returned HTTP response headers and exposed `/wp-json/`. | May assist technology fingerprinting and further enumeration. | **Low** |
| **4** | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs). | Reveals information about the web application’s security architecture. | **Low** |
| **5** | DNS infrastructure information exposed | DNSRecon identified DNS, mail and service-related records. | DNS information can help build a broader infrastructure profile. | **Medium** |
| **6** | Potential exposure of email-related information | Maltego's email search transform returned one entity, but its type was not confirmed. | If the entity is an email address, it could potentially be used for phishing or targeted attacks. | **Low** |
| **7** | Limited information retrieved through theHarvester | No emails, IP addresses, people, or hosts were found using Baidu. Several sources in the second search required API keys. | Limited results may leave some publicly available information undiscovered during reconnaissance. | **Low** |
| **8** | Multiple live hosts visible on local network | Zenmap identified three live hosts in the example network. | Unknown or unauthorized devices may potentially be present on a network. | **Medium** |

**Risk level key:** Critical · Medium · Low

The findings above are based on the footprinting and scanning activities and do not represent confirmed vulnerabilities.

These activities focused on information gathering and host discovery. No exploitation or vulnerability testing was performed.

Therefore, identifying information such as IP addresses, software versions, or DNS records does not necessarily mean that a system is vulnerable. Further authorized testing would be needed to confirm any vulnerabilities.

# 6. Recommendations

Based on the information gathered during the footprinting and network scanning activities, I suggest the following security recommendations:

**Review publicly exposed technology information**

Organizations should regularly review the information available about their websites, including CMS platforms, plugins, and software versions, to reduce unnecessary exposure.

**Keep software and plugins updated**

CMS platforms, plugins, and web server components should be kept up to date to address known security issues and reduce potential attack risks.

**Review HTTP response headers**

Organizations should examine their HTTP response headers and avoid disclosing unnecessary technical details that could help attackers identify the technologies in use.

**Regularly review DNS records**

DNS records should be reviewed periodically to ensure that they are accurate, necessary, and properly configured. Unused or unnecessary records should be removed.

**Maintain proper WAF configuration**

The Web Application Firewall (WAF), identified as ModSecurity during the reconnaissance activity, should be properly configured, maintained, and monitored to help protect the website against malicious requests.

**Monitor publicly available information**

Organizations should periodically review publicly available information, such as email addresses and subdomains, to identify unnecessary exposure and reduce potential risks.

**Review publicly exposed email addresses**

Organizations should monitor publicly available email addresses and limit unnecessary exposure to reduce the risk of phishing and targeted attacks.

**Perform regular internal network scans**

Organizations should periodically scan their internal networks to identify active devices and maintain an up-to-date view of their network environment.

**Investigate unknown or unexpected devices**

Devices that are not recognized should be checked to verify whether they are authorized to connect to the network.

**Keep network documentation up to date**

Network topology, device information, and IP address assignments should be documented and updated regularly to facilitate network monitoring and administration.

**Conduct security assessments within an authorized scope**

Footprinting, scanning, and further security testing should always be performed with appropriate authorization and within the defined scope of the assessment.

# 7. Conclusion

During the second week of my Cybersecurity and Ethical Hacking internship at NetworkWalks, I completed three practical activities focused on domain footprinting and local network scanning.

In the first activity, I used six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, and DNSRecon. These tools allowed me to collect and analyze different types of information about the target domain, including domain registration details, web technologies, IP address information, HTTP response headers, WAF identification, and DNS records.

In the second activity, I used **Maltego** to perform footprinting on networkwalks.com. I created a graph using the target domain as the starting entity and applied an email search transform. The transform returned one entity, giving me practical experience with Maltego's transforms and graphical representation of collected information.

In the third activity, I used **theHarvester** to gather publicly available information related to microsoft.com. I performed searches using Baidu and all available sources to look for email addresses, subdomains, and other information. Although the searches returned limited results, I learned how the tool uses different public sources and how API key requirements can affect information gathering.

In the last activity, I used **Zenmap** to scan my own local Wi-Fi network. I identified my network configuration and successfully discovered three active hosts. I also examined the available IP and MAC address information and used Zenmap's Topology feature to visualize the discovered network devices.

These activities helped me better understand the importance of reconnaissance and network discovery in cybersecurity. I learned how different tools can be used together to collect information, examine network environments, and identify details that may be relevant to a security assessment.

Overall, this week's practical work strengthened my understanding of information gathering, passive reconnaissance, basic network scanning, and security documentation. It also highlighted the importance of handling collected information responsibly and performing all cybersecurity activities within an authorized scope.

# 8. Evidences Collected
![WHOIS Results](screeshots%20week2/whois.png)
![Whatweb Results](screeshots%20week2/whatweb.png)
![nslookup Results](screeshots%20week2/nslookup.png)
![curl Results](screeshots%20week2/curl%20-I.png)
![wafwoof Results](screeshots%20week2/wafw00f.png)
![dnsrecon Results](screeshots%20week2/dnsrecon%20-d.png)
![maltego Results](screeshots%20week2/maltego.png)
![harv1000 Results](screeshots%20week2theharvester1000.png)
![harv50 Results](screeshots%20week2theharvester50.png)
![zenmap Results](screeshots%20week2/zenmap.png)
![zenmaptopo Results](screeshots%20week2/zenmaptopo.png)
-end-
