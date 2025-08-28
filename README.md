# Explore Google hacking and enumeration 

# AIM:

To use Google for gathering information and perform enumeration of targets

## STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various Google hacking keywords and enumeration tools as follows:


### Step 3:
Open terminal and try execute some kali linux commands

## Pen Test Tools Categories:  

| Operator    | Description                        | Example Usage           |
| ----------- | ---------------------------------- | ----------------------- |
| `site:`     | Search within a specific domain    | `site:example.com`      |
| `inurl:`    | Search in URL                      | `inurl:admin`           |
| `intitle:`  | Search in page title               | `intitle:"index of"`    |
| `filetype:` | Search by file type                | `filetype:pdf`          |
| `intext:`   | Search inside page text            | `intext:"confidential"` |
| `link:`     | Pages that link to a specific site | `link:example.com`      |
| `cache:`    | View cached version of a site      | `cache:example.com`     |
| `ext:`      | Same as filetype                   | `ext:xls`               |

 ## Architecture 
 ```
+----------------------+
|   Attacker / Hacker  |
|   (Browser & Google) |
+----------+-----------+
           |
           | Google Dork Queries
           v
+---------------------------+
|       Google Search       |
+---------------------------+
           |
           | Indexed Public Content
           v
+---------------------------+
|   Target Websites / Data  |
| - Leaked files            |
| - Open directories        |
| - Sensitive info          |
+---------------------------+

```

# Output:

SITE:

<img width="1914" height="1076" alt="Screenshot 2025-08-25 085059" src="https://github.com/user-attachments/assets/eb8ec488-c856-4ace-ab74-ea1ee751df51" />

INURL:

<img width="1904" height="1077" alt="Screenshot 2025-08-25 085206" src="https://github.com/user-attachments/assets/e33a6d53-b7e4-426a-8277-42b2a5e8a48e" />

INTITLE:

<img width="1916" height="1075" alt="Screenshot 2025-08-25 085557" src="https://github.com/user-attachments/assets/ee4de0b6-dfa8-4801-a5a9-5949a365f415" />

FILETYPE.PDF:

<img width="1909" height="1056" alt="Screenshot 2025-08-25 085948" src="https://github.com/user-attachments/assets/72f5ddc3-1d19-4086-8b93-f67d9f39955b" />

INTEXT:

<img width="1902" height="1070" alt="Screenshot 2025-08-25 090039" src="https://github.com/user-attachments/assets/6bdbb54a-f030-47df-b442-767268fdc799" />

LINK:

<img width="1914" height="941" alt="Screenshot 2025-08-25 090412" src="https://github.com/user-attachments/assets/01ab3b8e-5b51-41d6-b157-52fc8a93b851" />

DNS Enumeration:

<img width="1348" height="740" alt="Screenshot 2025-08-25 092020" src="https://github.com/user-attachments/assets/a2b3b2b0-00db-409e-8e9b-f68ac66d4f9c" />


## DNS Recon

| Record Type | Meaning                        | Example Output                   |
| ----------- | ------------------------------ | -------------------------------- |
| A           | Host to IPv4 address           | `example.com -> 93.184.216.34`   |
| AAAA        | Host to IPv6 address           | `example.com -> ::1`             |
| MX          | Mail server info               | `mail.example.com`               |
| NS          | Name servers                   | `ns1.example.com`                |
| TXT         | Misc data (SPF, verifications) | `v=spf1 include:_spf.google.com` |
| CNAME       | Canonical names (aliases)      | `www -> example.com`             |

## Common Tools Used (Kali Linux)

| Tool           | Description                                | Usage Example                           |
| -------------- | ------------------------------------------ | --------------------------------------- |
| `nslookup`     | DNS lookup tool (simple queries)           | `nslookup example.com`                  |
| `dig`          | DNS lookup utility (detailed)              | `dig example.com any`                   |
| `host`         | Simple DNS querying tool                   | `host example.com`                      |
| `dnsenum`      | Perl script to enumerate DNS info          | `dnsenum example.com`                   |
| `fierce`       | DNS scanner to locate non-contiguous IPs   | `fierce -dns example.com`               |
| `dnsrecon`     | Powerful DNS enumeration script            | `dnsrecon -d example.com -a`            |
| `theHarvester` | Subdomain enumeration using search engines | `theHarvester -d example.com -b google` |


## OUTPUT:
NSLOOKUP:

<img width="558" height="292" alt="Screenshot 2025-08-25 092301" src="https://github.com/user-attachments/assets/df3c394d-2fc1-4fa8-8922-21950ac84df8" />

DIG:

<img width="603" height="679" alt="Screenshot 2025-08-25 092529" src="https://github.com/user-attachments/assets/64bd2049-f39d-4482-82ff-b1f4f65d1077" />

HOST:

<img width="522" height="220" alt="Screenshot 2025-08-25 092938" src="https://github.com/user-attachments/assets/feb0e068-de5c-406f-91c9-75b1562696f6" />

DNSENUM:

<img width="700" height="515" alt="Screenshot 2025-08-25 094152" src="https://github.com/user-attachments/assets/f2daeb5e-f576-472f-a687-b95e58ac772d" />

FIERCE:

<img width="562" height="599" alt="Screenshot 2025-08-25 094303" src="https://github.com/user-attachments/assets/2555bb03-0dc6-4be0-8119-043e416e36b7" />

theHarvester:

<img width="788" height="692" alt="Screenshot 2025-08-25 095107" src="https://github.com/user-attachments/assets/a356e22d-afd0-44ec-ab71-b0862bb9bbb9" />


## Architecture Diagram 
```
+-------------------+        +------------------+       +------------------+
|                   |        |                  |       |                  |
|   Attacker (You)  +------->|   Target Server   +<----->+    DNS Server    |
| Kali Linux / Parrot|       | (Mail / DNS Host) |       |  (Authoritative) |
+---------+---------+        +---------+--------+       +---------+--------+
          |                            ^                          ^
          |                            |                          |
          |                            |                          |
          |           +-----------------------------+            |
          |           |      Information Tools      |            |
          |           |-----------------------------|            |
          |           | smtp-user-enum              |            |
          |           | nmap --script smtp-enum-*   |            |
          |           | dnsenum                     |<-----------+
          |           +-----------------------------+
          |
          v
+-----------------------------+
|   Output/Report             |
|  - Usernames Found          |
|  - MX Records / Zones       |
|  - Subdomains / IPs         |
+-----------------------------+

```

## dnsenum
**Purpose:** A multithreaded Perl script to enumerate information from DNS servers.

**Use case:** Performs DNS zone transfers, brute force subdomains, and gather host IPs.

```
dnsenum example.com
```

## Output:
<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/595e0b6c-01d8-4ea4-9555-5bd478bc0dec" />



## smtp-user-enum
**Purpose:** Standalone tool used to enumerate valid users by using the VRFY, EXPN, or RCPT TO commands.

**Use case:** Brute-forces SMTP to find users.

```
smtp-user-enum -M VRFY -U users.txt -t <target-ip>
```
  
 ## Output
  <img width="920" height="385" alt="image" src="https://github.com/user-attachments/assets/fd8013e8-c6d0-44e6-84a9-5e101b09826c" />



## nmap –script smtp-enum-users.nse <hostname>

**Purpose:** Uses smtp-enum-users NSE script to enumerate valid users on an SMTP server.

**Use case:** Helps identify email accounts on mail servers.

```
nmap -p 25 --script smtp-enum-users.nse <target-ip>
```
## OUTPUT:
<img width="932" height="205" alt="image" src="https://github.com/user-attachments/assets/57626337-5202-4fb0-9802-248fd950024f" />
## RESULT:
The Google hacking keywords and enumeration tools were identified and executed successfully
