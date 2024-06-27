# Bug Bounty

# ALL about Recon

## Passive Reconnaissance

### WHOIS and DNS Queries

We can use the following command-line tools to gather information about our target without alerting it:

* **whois**: to query WHOIS servers
* **nslookup**: to query DNS servers
* **dig**: to query DNS servers

These tools allow us to access publicly available records, including WHOIS records and DNS database records.

### Online Services

We will also explore the usage of two online services that enable us to collect information about our target without directly connecting to it:

* **DNSDumpster**: a online tool for DNS reconnaissance
* **Shodan.io**: a search engine for internet-connected devices

These services provide valuable insights into our target's infrastructure without triggering any alerts.

#### whois
```whois abcd.com```
#### nslookup
``` nslookup -type=a xyz.com 1.1.1.1```

Here type = a  8.8.8.8 googl local dns server 
| Query Type | Result |
| --- | --- |
| A | IPv4 Addresses |
| AAAA | IPv6 Addresses |
| CNAME | Canonical Name |
| MX | Mail Servers |
| SOA | Start of Authority |
| TXT | TXT Records |
#### dig 
```
dig xyz.com MX
```
- For more advanced DNS queries and additional functionality, you can use dig
-  dig returned more information thn nslookup
  
#### For sub domains

[DNSDumpster](https://dnsdumpster.com/)
#### Shodan
[Shodan.io](https://www.shodan.io/)
- Shodan.io collects information related to any device it can find connected online
- Shodan.io is a search engine for the Internet of Things.
