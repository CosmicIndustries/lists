# Allow Lists

This folder contains several allow lists used to manage and filter access to specific services or content platforms. Each file within this folder represents a list of domains, IPs, or other identifiers that are approved for access, grouped by service or platform. Below is a description of each file:

## Files

### 1. [`allowList.txt`](https://github.com/CosmicIndustries/lists/blob/main/allowList.txt)
This is the general allow list containing a broad set of approved domains that can be accessed across various services and platforms. It includes general-purpose entries for day-to-day use.

### 2. [`disney.txt`](https://github.com/CosmicIndustries/lists/blob/main/disney.txt)
This allow list specifically includes domains related to **Disney** services, such as Disney+, ESPN+, and other Disney-owned platforms. It ensures that traffic to these services is not blocked or filtered.

### 3. [`list2mrg.txt`](https://github.com/CosmicIndustries/lists/blob/main/list2mrg.txt)
This file contains an allow list intended to be merged with others. It can be combined with the general allow list or other specific platform lists to expand or update approved domains.

### 4. [`netflix.txt`](https://github.com/CosmicIndustries/lists/blob/main/netflix.txt)
This allow list is dedicated to **Netflix** and related services. It ensures that all necessary Netflix domains and subdomains are permitted, allowing smooth access to the streaming service.

### 5. [`roku.txt`](https://github.com/CosmicIndustries/lists/blob/main/roku.txt)
This allow list is designed for **Roku** devices, allowing them to access the necessary domains for updates, streaming, and other Roku services.

## Usage
These allow lists can be imported or used within firewall configurations, content filters, or any other system that requires a domain-based allow list. Each file can be used individually for its respective service or merged with others for a more comprehensive list.

### Merging Lists
To combine multiple lists into one (e.g., `list2mrg.txt`), simply use the following command (Linux/MacOS):

```bash
cat allowList.txt disney.txt netflix.txt roku.txt > mergedAllowList.txt
```

On Windows, you can use:

```bash
type allowList.txt disney.txt netflix.txt roku.txt > mergedAllowList.txt
```

This will create a new file `mergedAllowList.txt` containing the entries from all specified lists.

## Optional: Allowing Everything Except Certain Domains (DenyList)

To allow everything except certain domains, you would essentially need to create a **denylist** (blacklist) that blocks specific domains while allowing all other traffic. This can be achieved by configuring a firewall, DNS filtering, or a proxy server to block only the domains you specify. Here's how you can implement this concept:

### 1. **Using Firewall Rules**

Most firewalls can be configured to block specific domains or IPs while allowing all other traffic. However, blocking domains directly requires domain resolution (DNS) to map those domains to their IP addresses, as firewalls typically operate at the network layer. Below is an example using a firewall setup like **iptables** on Linux.

#### Example: Blocking Specific Domains with `iptables`

1. **Step 1**: Create a rule to block traffic to the IPs associated with the domain you want to block.

```bash
# Block traffic to a specific domain (e.g., www.example.com)
iptables -A OUTPUT -p tcp -d <IP_ADDRESS> -j REJECT
```

For example, if you wanted to block `www.netflix.com`, you would first resolve the IP address for Netflix:

```bash
# Resolve the IP address
nslookup www.netflix.com
```

Then, use the resolved IP address in your `iptables` command:

```bash
# Block Netflix's IP address
iptables -A OUTPUT -p tcp -d 52.42.125.93 -j REJECT
```

Repeat this for all IP addresses you want to block.

2. **Step 2**: Ensure that all other traffic is allowed:

```bash
# Allow all other outbound traffic
iptables -P OUTPUT ACCEPT
```

In this setup, all traffic is allowed except for traffic to the domains/IPs you’ve blocked.

### 2. **Using DNS Filtering**

A more domain-friendly approach is to use a DNS-based filtering system like **Pi-hole**, **OpenDNS**, or **pfSense** with DNS filtering. These tools operate at the DNS level, allowing you to block specific domains while allowing all other traffic. This method is much easier for handling domain-based restrictions.

#### Example: Blocking Specific Domains with Pi-hole

1. **Step 1**: Install and configure **Pi-hole** on your network. Pi-hole acts as a DNS sinkhole, filtering queries based on a denylist.

2. **Step 2**: Add domains you want to block to the Pi-hole's blacklist:

   - Access the Pi-hole admin interface.
   - Go to **Group Management > Blacklist**.
   - Add the domains you want to block (e.g., `netflix.com`, `disney.com`).
   
   Pi-hole will prevent these domains from resolving, effectively blocking access to the sites, while all other domains are allowed.

### 3. **Using a Proxy Server**

A **proxy server** like **Squid** can also be used to block specific domains. The proxy server can be configured to deny requests for specific domains while allowing all others.

#### Example: Blocking Specific Domains with Squid Proxy

1. **Step 1**: Install and configure **Squid**.

2. **Step 2**: In the Squid configuration file (`/etc/squid/squid.conf`), you can define ACLs (Access Control Lists) to block specific domains:

```bash
# Define the domains to block
acl blocked_domains dstdomain .netflix.com .disney.com

# Deny access to the blocked domains
http_access deny blocked_domains

# Allow all other traffic
http_access allow all
```

This setup will block access to Netflix and Disney domains while allowing all other traffic.

### 4. **Using `hosts` File**

If you're looking for a simple solution on individual machines, you can edit the `hosts` file to block specific domains by redirecting them to `localhost` or a non-existent IP address.

#### Example: Blocking Specific Domains with `hosts` File

1. **Step 1**: Open the `hosts` file on your system:
   - **Linux/macOS**: `/etc/hosts`
   - **Windows**: `C:\Windows\System32\drivers\etc\hosts`

2. **Step 2**: Add entries for the domains you want to block by mapping them to `127.0.0.1` (localhost):

```bash
127.0.0.1   netflix.com
127.0.0.1   www.netflix.com
127.0.0.1   disney.com
127.0.0.1   www.disney.com
```

This method effectively blocks the domains by preventing the system from resolving their real IP addresses. However, it only works on the machine where the `hosts` file is edited.

### Summary of Approaches

1. **Firewall-based solution**: Block specific domains' IP addresses using firewall rules (e.g., `iptables`).
2. **DNS-based filtering**: Use a DNS filtering tool like Pi-hole to block specific domains.
3. **Proxy-based solution**: Use a proxy server like Squid to block requests to specific domains.
4. **Hosts file solution**: Edit the `hosts` file to block specific domains by redirecting them to `localhost`.

Each of these methods allows you to block specific domains while allowing everything else, depending on the network infrastructure or use case you prefer.
```
👋
Let me know if you'd like help setting up one of these methods!
```
