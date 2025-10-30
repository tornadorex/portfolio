# DNS Sinkhole

A *DNS Sinkhole* is a security configuration for a DNS server or firewall that can be used for blocking ads, among other things. Read on to find out more about how a DNS Sinkhole works and its applications.

* [What is DNS?](#what-is-dns)
* [DNS Sinkholing](#dns-sinkholing)
* [Applications](#applications-for-dns-sinkholing)
* [Summary](#summary)

## What is DNS?

DNS stands for *Domain Name Service*.

There are two key points to understanding the Domain Name Service:

1. Computers communicate with one another using numerical identifiers (a.k.a an IP address) like `1.1.1.1`.
2. Human readable addresses like `name.example` are more intuitive and easier to remember.

The Domain Name Service is the system that translates human readable addresses like `name.example` to an IP address like `1.1.1.1`. Think of it as a phone book that a computer uses to reach the websites the user wants to browse.

When a user wants to connect to `name.example`, their web browser sends a query to the configured DNS server to find the stie's IP address. If the DNS server finds a match it will return the IP address. From there, the web browser sends a request to establish a connection with the website.

If the DNS server doesn't have `name.example` in its database, it forwards the request to other DNS servers in the chain and then caches the returning result.

## DNS Sinkholing

A DNS Sinkhole, also referred to as *Blackhole DNS*, is a configuration where the DNS server provides a false result for a domain name. This can be very useful in cases where the user is attempting to connect to a known malicious website or may be infected as part of a botnet.

There are several ways to create a DNS sinkhole:

* You can activate it as a security feature on some firewalls or proxies.
* You can alter the host files on a client machine.
* You can set up a [Pi-hole](https://docs.pi-hole.net/)
* Some ISPs and domain registrars configure their DNS servers to provide this service to protect their clients.

The result of any of these methods is that the request for the original website is diverted to another (often a controlled) IP address for security analysis.

> Let's look at a case where the `name.example` domain is known to be malicious. An ISP administrator has configured one of their high-level DNS servers to provide DNS sinkholing, and has included `name.example` as one of the websites to be sinkholed. Now, when the client computer queries the DNS server for the IP address of `name.example`, the DNS server returns a false result. The client computer connects to the sinkhole at `2.2.2.2` rather than `name.example` at `1.1.1.1`.

## Applications for DNS Sinkholing

DNS Sinkholing has several applications for which it proves useful.

1. **Blocking drive-by downloads**. A drive-by happens when an attacker has infected a legitimate website with a malicious hidden link that forces the user's browser to download and execute malicious code without their knowledge or permission. All it takes to become infected is to access the website in question. DNS sinkholing can block the malicious hidden link and protect the client computer from becoming infected by a drive-by download.

2. **Blocking ads, adware, spyware, and other unwanted traffic** by redirecting that traffic elsewhere.

3. **Blocking command & control traffic for botnets**. If a computer is infected, it will try to connect to a C&C server for further malicious commands. By using a DNS Sinkhole to redirect traffic, the connection is never established. An organization can not only prevent the botnet from infecting more systems, but they can also consult system logs and identify the infected machines trying to make C&C connections.

## Summary

* DNS is the Domain Name Service, the system responsible for translating human-readable domain names like `name.example` into IP addresses like `1.1.1.1`.

* A DNS Sinkhole is a configuration where a DNS query returns a false result. Instead of mapping `name.example` to the IP address `1.1.1.1`, it tells the client `name.example` is at `2.2.2.2`.

* DNS sinkholing has several security applications:
  * blocking known malicious sites
  * blocking malware distribution
  * blocking ads and spyware communications
  * blocking botnet command & control traffic
  * identifying infected machines attempting to reach malicious servers
