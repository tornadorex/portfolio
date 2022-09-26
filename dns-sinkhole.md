# DNS Sinkhole #

* [What is DNS?](#overview)
* [DNS Sinkholing](#sinkholing)
* [Applications](#applications)
* [Summary](#summary)


<h2 id="overview">What is DNS?</h2>

DNS stands for **"Domain Name Service."**

There are two key points to understanding the Domain Name Service: 

1. Computers communicate with one another using numerical identifiers (a.k.a an IP address) like `1.1.1.1`.
2. Human readable addresses like `name.example` are more intuitive and easier to remember.

The Domain Name Service is the system that translates human readable addresses like `name.example` to an IP address like `1.1.1.1`. Think of it as a phone book that a computer can utilize to reach the websites the users want to browse.

When a user wants to connect to `name.example`, their web browser sends a query to the configured DNS server to find its IP address. If the DNS server finds a match it will return the IP address. From there, the web browser sends a request to establish a connection with the website. 

If the DNS server doesn't have `name.example` in its database, it will forward the request to other DNS servers in the chain, and then cache the returning result.


<h2 id="sinkholing">DNS Sinkholing</h2>

A DNS Sinkhole, also referred to as *Blackhole DNS*, is a configuration where the DNS server provides a false result for a domain name. This can be very useful in cases where the user is attempting to connect to a known malicious website or may be infected as part of a botnet. 

There are several ways to create a DNS sinkhole: 

* DNS sinkholing can be a security feature on some firewalls or proxies.
* It can be achieved by altering the host file on the client machine.
* Some ISPs and domain registrars configure their DNS servers to provide this service to protect their clients. 

The result of any of these methods is that the request for the original website is diverted to another (often a controlled) IP address for security analysis.

>Let's look at a case where the `name.example` domain is known to be malicious. An ISP administrator has configured one of their high-level DNS servers to provide DNS sinkholing, and have included `name.example` as one of the websites to be sinkholed. Now, when the client computer queries the DNS server for the IP address of `name.example`, the DNS server returns a false result. The client computer connects to the sinkhole at `2.2.2.2` rather than `name.example` at `1.1.1.1`.


<h2 id="applications">Applications for DNS Sinkholing</h2>

DNS Sinkholing has several applications for which it proves useful.

1. **Blocking drive-by downloads**. A drive-by happens when an attacker has infected a legitimate website with a malicious hidden link that forces the user's browser to download and execute malicious code without their knowledge or permission. All it takes to become infected is to access the website in question. DNS sinkholing can block the malicious hidden link and protect the client computer from becoming infected by a drive-by download.

2. **Blocking ads, adware, spyware, and other unwanted traffic** by redirecting that traffic elsewhere.

3. **Blocking command & control traffic for botnets**. If a computer is infected, it will try to connect to a C&C server for further malicious commands. By using a DNS Sinkhole to redirect traffic, the connection is never established. An organization can not only prevent the botnet from infecting more systems, but they can also consult system logs and identify the infected machines trying to make C&C connections.


<h2 id="summary">Summary</h2>

* DNS is the Domain Name Service, the system responsible for translating human-readable domain names like `name.example` into IP addresses like `1.1.1.1`.

* A DNS Sinkhole is a configuration where a DNS query returns a false result. Instead of mapping `name.example` to the IP address `1.1.1.1`, it tells the client `name.example` is at `2.2.2.2`. 

* DNS sinkholing has several security applications: 
	* blocking known malicious sites
	* blocking malware distribution
	* blocking ads and spyware communications
	* blocking botnet command & control traffic
	* identifying infected machines attempting to reach malicious servers
