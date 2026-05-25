# PowerDNS Stack Implementation Guide

This repository shares practical experiences and configurations for setting up a lightweight and efficient DNS management stack using the following tools:

- **PowerDNS**: The core authoritative DNS server.
- **PDNS Manager**: A simple and lightweight web-based control panel for PowerDNS.
- **PDNS-ACME**: A tool for managing Let's Encrypt SSL certificates (ACME) via PowerDNS.

---

## Technical Insights & Tips

During the implementation of this stack, several challenges were encountered and resolved. Below are the key takeaways:

### 1. Database Compatibility
The default databases for these tools are not fully synchronized out-of-the-box. You must manually update/migrate the database schema to ensure seamless integration between PowerDNS and the management panel.

### 2. Development Environment (PDNS Manager)
Please note that **PDNS Manager** has not received official updates for a few years. If you plan to modify or develop the codebase:
- You must use **Node.js v12** to build the environment and handle dependencies.

### 3. PDNS-ACME & Wildcard SSL Challenges
The **PDNS-ACME** tool operates in a semi-automatic manner. One of the main challenges was configuring the JSON file for **Wildcard Certificates**. 
To issue a wildcard certificate, you must have two separate ACME records for each domain and map them correctly in the JSON configuration.

#### Example JSON Configuration:
```json
{
  "config": {
"server": "https://your-api-endpoint.com/",
"deploy-wait": 120
  },
  "domains": {
"example.com": 371,
"*.example.com": 372,
"another-domain.ir": 352,
"*.another-domain.ir": 353
  },
  "certs": {
"example.com": {
"alias": [
"*.example.com"
]
},
"another-domain.ir": {
"alias": [
"*.another-domain.ir"
]
}
  }
}
```

### 3. UI/UX Bugs

The PDNS Manager web interface is built with Angular. Due to its lack of recent updates, there are several UI bugs and functional inconsistencies. You will likely need to debug and patch these manually within the frontend code to suit your needs.

---------------
Good luck with your implementation!
