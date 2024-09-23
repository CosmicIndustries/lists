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
