# Curiosity Report: Understanding SSL Certificates in DevOps

## Why I Chose This Topic

During our deployment exercises and service integration work in this course, I noticed that SSL certificates are extremely important, but I didn’t have a clear mental model for how SSL actually works, what certificates do, and how they’re managed in real-world DevOps workflows. This made me curious, so I dug in.

## What is an SSL Certificate?

An SSL (Secure Sockets Layer) certificate is a digital certificate that authenticates a website's identity and enables an encrypted connection. It’s what turns `http://` into `https://`.
- Proves identity: Shows users that your server is who it claims to be.
- Encrypts traffic: Protects data in transit (e.g., login info, personal data).
- Issued by CAs: Certificates are issued by trusted Certificate Authorities (CAs) like Let's Encrypt, DigiCert, or GoDaddy.

## How SSL Fits into DevOps

I learned that SSL certificates show up all over modern DevOps pipelines. For example:

### 1. In CI/CD Pipelines
- During deployment, services like NGINX or AWS ELB are often configured to use an SSL cert.
- Certificate rotation (especially with Let's Encrypt) needs automation.
- Some CI workflows validate the certificate chain before deploying updates.

### 2. In Load Balancers
- SSL termination is commonly done at the load balancer (e.g., AWS ALB, NGINX, Cloudflare).
- DevOps teams must handle both internal and public SSL traffic properly.

### 3. In Containerized Applications
- Services inside containers (like Express.js apps) might run on HTTP but get wrapped in SSL by a reverse proxy.
- Managing certs for containers at scale often involves sidecars or secrets managers.

## The Certificate Lifecycle 

1. Generate a key pair (public/private)
2. Create a CSR (Certificate Signing Request)
3. Send CSR to a CA
4. Get certificate back and install it on your server
5. Configure your web server (NGINX, Apache, etc.)
6. Auto-renew (for Let's Encrypt, usually every 90 days)

## Tools & Services

This is a table of some of the tools and services that I researched a bit while I was digging around.

| Tool | What it does |
|------|--------------|
| Let's Encrypt | Free CA that issues SSL certs |
| Certbot | Automates Let's Encrypt cert issuance/renewal |
| OpenSSL | CLI tool for generating keys/CSRs and inspecting certs |
| AWS ACM | Manages certs in AWS, integrates with ELB |
| NGINX | Common server for configuring SSL manually |
| Traefik | Reverse proxy that auto-manages certs using Let's Encrypt |

## Common Gotchas

- Mixed content: Serving some assets over HTTP breaks the padlock.
- Expired certs: Can cause outages — hence, auto-renewal is 🔑.
- Wildcard certs: Useful for subdomains, but trickier to manage.
- Self-signed certs: Good for dev, but not for public-facing apps.
- Certificate chains: Browsers must trust the full chain, not just your leaf cert.

## Cool Facts That Surprised Me

- SSL is actually deprecated; most use TLS 1.2+, but we still call them "SSL certs."
- You can inspect any website's cert!
- SSL certificates are just base64-encoded text files with a specific structure.


## Conclusion

Exploring SSL certificates gave me a deeper appreciation for web security in DevOps. It’s not just “turning HTTPS on” — it’s a complex process involving cryptography, trust models, automation, and tooling. Next time I see an SSL error or a CI pipeline deploying to production, I’ll have a much better idea of what’s going on under the hood.
