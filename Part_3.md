# DNS (Domain Name System)

## Introduction

Imagine you want to visit a website like:

```text
www.google.com
```

Computers do not understand domain names such as Google, Facebook, or Amazon.

They communicate using **IP Addresses** such as:

```text
142.250.195.78
```

Remembering IP addresses for every website would be difficult.

This is where **DNS (Domain Name System)** helps.

DNS acts like the **phonebook of the internet**.

It converts human-friendly domain names into machine-friendly IP addresses.

---

# What is DNS?

## Definition

DNS (Domain Name System) is a distributed system that translates domain names into IP addresses.

### Example

When you type:

```text
www.google.com
```

DNS finds Google's IP address:

```text
142.250.xxx.xxx
```

and allows your browser to connect to Google's servers.

---

# How Websites Actually Work

Many beginners think that visiting a website directly opens a webpage.

In reality, several steps happen behind the scenes.

## Simplified Flow

```text
User Types URL
        ↓
DNS Lookup
        ↓
Get IP Address
        ↓
Browser Connects to Server
        ↓
Server Sends Response
        ↓
Web Page Displays
```

### Example

You enter:

```text
www.instagram.com
```

The browser first asks DNS:

> "What is the IP address of instagram.com?"

DNS returns the IP address.

Then the browser connects to Instagram's server and downloads the webpage.

---

# Why DNS Is Needed

Without DNS:

```text
https://142.250.195.78
```

Instead of:

```text
https://www.google.com
```

Every website would need to be remembered using its IP address.

DNS makes the internet user-friendly.

---

# DNS Hierarchy

DNS follows a hierarchical structure.

```text
Root Server
     ↓
TLD Server
     ↓
Authoritative Name Server
     ↓
IP Address
```

Each layer has a specific responsibility.

---

# Root Server

## Definition

Root Servers are the highest level in the DNS hierarchy.

They know where Top-Level Domain (TLD) servers are located.

## Example

Suppose a user requests:

```text
www.google.com
```

The Root Server does not know Google's IP address.

Instead, it knows:

> "For .com domains, ask the .com TLD server."

### Root Server Response

```text
Ask .com TLD Server
```

Think of Root Servers as the directory of all TLD servers.

---

# TLD (Top-Level Domain) Server

## Definition

TLD Servers manage domain extensions such as:

* .com
* .org
* .net
* .edu
* .gov
* .in

## Example

For:

```text
www.google.com
```

The TLD server handles:

```text
.com
```

The TLD server does not know Google's IP address directly.

Instead, it knows which Name Server manages google.com.

### TLD Response

```text
Ask Google's Name Server
```

---

# Name Server

## Definition

A Name Server contains the actual DNS records of a domain.

It knows the exact IP address associated with the domain.

## Example

For:

```text
google.com
```

The Name Server may return:

```text
142.250.xxx.xxx
```

This is the final answer needed by the browser.

---

# DNS Resolution Process Explained Step-by-Step

DNS Resolution is the process of converting a domain name into an IP address.

Let's understand it using:

```text
www.google.com
```

---

## Step 1: User Enters Domain Name

The user types:

```text
www.google.com
```

into the browser.

---

## Step 2: Browser Cache Check

The browser first checks its local cache.

```text
Browser Cache
       ↓
IP Found?
```

If the IP already exists, the process ends here.

Otherwise, continue.

---

## Step 3: Operating System Cache Check

The operating system checks its DNS cache.

```text
OS DNS Cache
       ↓
IP Found?
```

If found, it returns the IP address.

Otherwise, continue.

---

## Step 4: DNS Resolver Receives Request

The request is sent to a DNS Resolver.

Usually provided by:

* ISP
* Google DNS
* Cloudflare DNS

Examples:

```text
8.8.8.8
1.1.1.1
```

The resolver starts searching for the IP address.

---

## Step 5: Resolver Contacts Root Server

The resolver asks:

```text
Where can I find google.com?
```

Root Server replies:

```text
Ask .com TLD Server
```

---

## Step 6: Resolver Contacts TLD Server

The resolver asks the .com TLD Server:

```text
Where can I find google.com?
```

The TLD Server replies:

```text
Ask Google's Name Server
```

---

## Step 7: Resolver Contacts Name Server

The resolver asks Google's Name Server:

```text
What is the IP address of google.com?
```

The Name Server replies:

```text
142.250.xxx.xxx
```

---

## Step 8: Resolver Returns IP Address

The resolver sends the IP address back to the browser.

```text
google.com
        ↓
142.250.xxx.xxx
```

---

## Step 9: Browser Connects to Server

The browser uses the IP address to connect to Google's web server.

```text
Browser
      ↓
Google Server
```

---

## Step 10: Web Page Loads

The server sends:

* HTML
* CSS
* JavaScript
* Images

The browser renders the webpage.

The user sees:

```text
Google Homepage
```

---

# Complete DNS Resolution Flow

```text
User Types google.com
           ↓
Browser Cache
           ↓
OS Cache
           ↓
DNS Resolver
           ↓
Root Server
           ↓
TLD Server (.com)
           ↓
Google Name Server
           ↓
Returns IP Address
           ↓
Browser Connects to Server
           ↓
Website Loads
```

---

# DNS Caching

DNS lookups are expensive if performed repeatedly.

To improve performance, DNS responses are cached.

## Cache Locations

### Browser Cache

Stores recently visited domain IPs.

### Operating System Cache

Stores DNS records locally.

### DNS Resolver Cache

Stores responses for many users.

---

## Benefits of Caching

* Faster website loading
* Reduced DNS traffic
* Lower latency
* Better scalability

---

# Common DNS Record Types

## A Record

Maps domain name to IPv4 address.

### Example

```text
google.com → 142.250.xxx.xxx
```

---

## AAAA Record

Maps domain name to IPv6 address.

---

## CNAME Record

Maps one domain to another domain.

### Example

```text
www.example.com
        ↓
example.com
```

---

## MX Record

Used for email servers.

### Example

```text
gmail.com
        ↓
Mail Server
```

---

# DNS in System Design Interviews

DNS is important because it helps:

* Route users to servers
* Improve scalability
* Reduce latency
* Support global applications
* Enable load balancing
* Support CDNs

Almost every large-scale application uses DNS before any request reaches the application server.

---

# Key Takeaways

## DNS

* DNS stands for Domain Name System.
* It converts domain names into IP addresses.
* DNS acts as the phonebook of the internet.

## Root Server

* Highest level in DNS hierarchy.
* Directs requests to TLD servers.

## TLD Server

* Manages domain extensions such as .com, .org, and .in.
* Directs requests to the correct Name Server.

## Name Server

* Stores actual DNS records.
* Returns the final IP address.

## DNS Resolution Process

```text
Domain Name
      ↓
Root Server
      ↓
TLD Server
      ↓
Name Server
      ↓
IP Address
      ↓
Web Server
```

## Final Note

Every time you open a website, DNS works behind the scenes to translate a human-readable domain name into an IP address, allowing your browser to communicate with the correct server on the internet.
