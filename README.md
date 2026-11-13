# Zenmap-Scanning-Report-1

PENETRATION TESTING REPORT

Footprinting & Network Scanning Phases
W2-PM1 + W2-PM5 | CYBERSECURITY & ETHICAL HACKING | NETWORKWALKS

Field	Detail
Name	NANTHINI G B
Program / Batch	[B084-Networkwalks]
Date	13 November 2026
Modules completed	W2-PM1 (Footprinting with Multiple Kali Tools)
                  W2-PM5 (Network Scanning with Zenmap)
Target	1. networkwalks.com (the lab target assigned in the course)
        2. My own local LAN network
Permission secured?	Yes. The website is the assigned course lab target, and the LAN is my own                           network.
Phases covered	Phase 1: Reconnaissance & Footprinting
                Phase 2: Scanning & Network Discovery

1. Liability Disclaimer
I performed these activities only on the lab target assigned in my course and on a network that I own. This material is for education and research only. Do not use anything here to break the law. Unauthorised access is a crime in most countries, even when nothing is damaged. Every action you take is your own responsibility.

2. Introduction
This report covers two Week 2 practicals. In W2-PM1, I footprinted the domain networkwalks.com using six Kali Linux tools. In W2-PM5, I used Zenmap on Windows to discover live hosts on my own local network.

Together they show how a tester first gathers public information about a target, then maps which hosts are alive on a network. For every step I record the command used, the result, a screenshot as evidence, and a short note on why it matters from an attacker's point of view.

3. Tools Used
Tool	Purpose
Kali Linux & Windows	Operating systems used for the activities
whois	Find domain registration details (registrar, dates, name servers)
whatweb	Fingerprint web technologies (server, CMS, plugins, IP)
nslookup	Resolve the domain name to its IP address
curl -I	Read the HTTP response headers
wafw00f	Detect whether a Web Application Firewall protects the site
dnsrecon	Enumerate DNS records (NS, MX, SPF, TXT, SRV)
Zenmap (Nmap GUI)	Scan the local subnet for live hosts, IPs and MAC addresses
Windows CMD (ipconfig)	Find my local IP address, subnet mask and MAC address

4. Activities Performed
4.1 Footprinting & Reconnaissance (W2-PM1)
All six tools only read public information. None of them attacks the target.

Task 1: whois
whois networkwalks.com
The record shows the domain registered through GoDaddy. It was created on 2019-11-06 and is set to expire on 2027-11-06. The name servers are NS6135.HOSTGATOR.COM and NS6136.HOSTGATOR.COM, so the hosting provider is HostGator.

Why it matters: registrar details, dates and name servers reveal the hosting provider and help with social engineering and planning.

Task 2: whatweb
whatweb networkwalks.com
The site redirects from HTTP to HTTPS and runs on Apache. It uses WordPress 7.0.4 with WP Download Manager 3.3.58, plus Bootstrap 7.0.4 and jQuery 3.7.1. The output also exposed the server IP 192.232.216.135 and the email address info@networkwalks.com.

Why it matters: exact software versions can be compared with vulnerability databases to look for known issues.

Task 3: nslookup
nslookup networkwalks.com
The domain resolves to 192.232.216.135.

Why it matters: knowing the real IP lets an attacker scan the server directly and map related infrastructure.

Task 4: curl -I
curl -I https://networkwalks.com
The response was HTTP/2 200. The headers show server: Apache, a set-cookie value, an x-nginx-cache: WordPress header and a link header that exposes the WordPress REST API at /wp-json/.

Why it matters: headers reveal the web server, caching setup and hidden endpoints without loading the full page.

Task 5: wafw00f
wafw00f networkwalks.com
The site is behind a ModSecurity (SpiderLabs) Web Application Firewall.

Why it matters: knowing a WAF is present tells an attacker that simple attempts will be blocked or logged.

Task 6: dnsrecon
dnsrecon -d networkwalks.com
DNSRecon found 8 records. They include the SOA and name servers on HostGator, DNS software version Bind 9.16.23, an MX record for mail.networkwalks.com (192.232.216.135), an SPF TXT record, a Google site-verification TXT record, and several cPanel SRV records (_autodiscover._tcp).

Why it matters: DNS records map the mail and hosting setup and expose software versions.

Note: values above come from the W2-PM1 lab output. Replace them with the exact results from my own Kali terminal if they differ.

4.2 Network Scanning with Zenmap (W2-PM5)
For the second activity, I used Zenmap to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.

I first used the Windows ipconfig command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected Ping Scan to identify active hosts.

After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.

Note: The actual subnet, number of hosts and addresses should be replaced with the results from my own network when submitting the report.

5. Risk Analysis / Impact

![image alt](https://github.com/gbnanthini-57/Zenmap-Scanning-Report/blob/c5d374ff736f1ffaba4299e44e2664337a9e6258/Screenshot%202026-11-13%20183418.png)

6. Recommendations
Review publicly exposed technology information. Check what the website reveals about its CMS, plugins and versions.
Keep software updated. Update WordPress, plugins and server software and check them against security advisories.
Review HTTP headers. Remove unnecessary technical details from server responses.
Review DNS records regularly. Keep only the records and services that are needed, and keep DNS software updated.
Keep the WAF enabled and tuned. ModSecurity already blocks simple attacks, so keep its rules current.
Limit exposed contact details. Avoid publishing plain email addresses where possible.
Scan your own network regularly. Check which devices are connected and investigate any unknown device.
Maintain network documentation. Keep topology and device lists up to date.
Test only with authorisation. Reconnaissance and scanning must stay within an approved scope.

7. Conclusion
In Week 2 of my Cybersecurity & Ethical Hacking program, I completed practical work in footprinting and network scanning. With six Kali tools I learned how whois, whatweb, nslookup, curl, wafw00f and dnsrecon each reveal a different part of a target, from ownership and hosting to software versions, firewall use and DNS setup. With Zenmap I learned how to find my IP address and subnet, run a ping scan, read live hosts and save a network topology.

My own scan found 1 live host, which differs from the 4 hosts in the guide's example, because results depend on how the network is configured. The exercises showed that a lot can be learned before any attack is attempted, and that a good report explains what was done, what was found, what it means, what risk it creates and how to reduce it. I also learned that all of this must stay within an authorised scope.

8. Evidences Collected
Screenshots are stored in the folder.
