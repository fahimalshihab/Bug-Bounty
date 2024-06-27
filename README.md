![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/fe4f34db-b49e-4210-9351-b9af60df28d1)# Bug Bounty

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
  

<b>Frist thing first to get the ip lets ping </b>

``` ping brac.ac.bd```

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/4c49ff42-5e5b-4123-a195-83285c4f4d2b)

<b> searchig IP in sodan </b>
![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/983b4202-85e0-4f26-9e65-9c846f3bdefc)

<b>Autonomous System Numbers </b>

We can do this using Autonomous System Numbers.

An autonomous system number (ASN) is a global identifier of a range of IP addresses. If you are an enormous company like Google you will likely have your own ASN for all of the IP addresses you own.

We can put the IP address into an ASN lookup tool such as https://asnlookup.com/,

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/b6c520da-d990-4989-9528-14fd4faba118)


Knowing the ASN is helpful, because we can search Shodan for things such as coffee makers or vulnerable computers within our ASN

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/617337e4-cff6-4049-b449-cefc124466bf)
