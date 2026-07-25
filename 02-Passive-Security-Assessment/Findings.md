# Passive Security Assessment Findings

## Target Information

| Item | Value |
|------|-------|
| Target Domain | torlegacy.com |
| Assessment Type | Passive Security Assessment |
| Assessment Method | Open Source Intelligence (OSINT) and Passive Reconnaissance |

---

# 1. WHOIS Analysis

## Observations

| Item | Finding |
|------|----------|
| Domain | torlegacy.com |
| Registrar | NameCheap, Inc. |
| Creation Date | 30 August 2022 |
| Last Updated | 17 January 2026 |
| Expiration Date | 30 August 2026 |
| Domain Status | clientTransferProhibited |
| Authoritative Name Servers | joyce.ns.cloudflare.com, oswald.ns.cloudflare.com |
| DNSSEC | Unsigned |
| WHOIS Privacy | Enabled (Withheld for Privacy ehf) |

---

## Security Assessment

### Positive Observations

- The domain is registered with NameCheap, a well-known ICANN-accredited registrar.
- Domain transfer protection is enabled through the `clientTransferProhibited` status, reducing the risk of unauthorised domain transfers.
- The domain uses Cloudflare authoritative name servers, indicating the organisation has delegated DNS management to a recognised DNS provider.
- WHOIS privacy protection is enabled, reducing exposure of registrant information.

### Potential Improvement

- DNSSEC is currently **not enabled** (`unsigned`). Enabling DNSSEC would provide cryptographic validation of DNS responses and help mitigate certain DNS spoofing and cache poisoning attacks.

---

## Risk Assessment

| Finding | Risk Level |
|----------|------------|
| Domain transfer protection enabled | Low Risk |
| WHOIS privacy enabled | Informational |
| DNSSEC not enabled | Medium Risk |

---

## Evidence

- Terminal output from `whois torlegacy.com`
- Screenshot: `Screenshots/WHOIS-01.png`

# 2. DNS Record Analysis

## A Record Lookup

### Observations

| Record Type | Value |
|-------------|-------|
| A Record | 104.21.51.90 |
| A Record | 172.67.177.252 |
| DNS Response Status | NOERROR |

---

## Security Assessment

### Positive Observations

- The domain successfully resolves to two IPv4 addresses.
- Multiple A records indicate that the domain is hosted behind Cloudflare's network, providing load balancing, redundancy, and additional protection against service disruption.
- DNS queries completed successfully with no resolution errors.

### Informational Observation

- The IP addresses belong to Cloudflare's reverse proxy infrastructure rather than the origin web server. This helps conceal the origin server's public IP address.

---

## Risk Assessment

| Finding | Risk Level |
|----------|------------|
| Multiple A records (Cloudflare) | Informational |
| DNS resolution successful | Low Risk |

---

## Evidence

- Terminal output from `dig torlegacy.com`
- Screenshot: `Screenshots/DNS-A-01.png`

## 3. Name Server (NS) Analysis

### Observations

| Record Type | Value |
|-------------|-------|
| NS Record | joyce.ns.cloudflare.com |
| NS Record | oswald.ns.cloudflare.com |
| DNS Response Status | NOERROR |

---

### Security Assessment

#### Positive Observations

- The domain uses two authoritative name servers.
- Both name servers are provided by Cloudflare, a widely used managed DNS provider.
- Using multiple authoritative name servers improves DNS availability and resilience.

#### Informational Observation

- Cloudflare manages the domain's authoritative DNS service, which can improve performance and reliability.

---

### Risk Assessment

| Finding | Risk Level |
|----------|------------|
| Cloudflare Authoritative Name Servers | Low Risk |
| Multiple Name Servers Configured | Low Risk |

---

### Evidence

- Terminal output from `dig NS torlegacy.com`
- Screenshot: `Screenshots/DNS-NS-01.png`

## 4. Mail Exchange (MX) Analysis

### Observations

| Priority | Mail Server |
|----------|-------------|
| 5 | mx1-hosting.jellyfish.systems |
| 10 | mx2-hosting.jellyfish.systems |
| 20 | mx3-hosting.jellyfish.systems |

DNS Response Status: **NOERROR**

---

### Security Assessment

#### Positive Observations

- The domain has three MX records configured for email delivery.
- Multiple MX records provide redundancy, allowing email delivery to continue if one mail server becomes unavailable.
- The MX records use priority values (5, 10, and 20), enabling mail servers to be contacted in the correct order.

#### Informational Observation

- The domain's email service is hosted by **jellyfish.systems** rather than on the web server itself.

---

### Risk Assessment

| Finding | Risk Level |
|----------|------------|
| Multiple MX Records Configured | Low Risk |
| Priority-Based Mail Routing | Low Risk |

---

### Evidence

- Terminal output from `dig MX torlegacy.com`
- Screenshot: `Screenshots/DNS-MX-01.png`

## 5. TXT Record Analysis

### Observations

| TXT Record | Purpose |
|------------|---------|
| google-site-verification=... | Google site ownership verification |
| mailerlite-domain-verification=... | MailerLite domain verification |
| v=spf1 include:_spf.mlsend.com +a +mx +ip4:198.54.114.25 include:spf.web-hosting.com include:sendersrv.com ~all | SPF record for email sender authorization |

---

### Security Assessment

#### Positive Observations

- An SPF (Sender Policy Framework) record is configured.
- The SPF record authorizes multiple legitimate email sending services, helping to reduce email spoofing.
- Google Site Verification and MailerLite verification records are present, confirming ownership for those services.

#### Informational Observation

- The SPF policy ends with `~all` (SoftFail). This means email from unauthorized senders is marked as suspicious rather than being outright rejected.

---

### Risk Assessment

| Finding | Risk Level |
|----------|------------|
| SPF Record Present | Low Risk |
| Google and MailerLite Verification Records | Informational |
| SPF SoftFail (`~all`) | Low Risk |

---

### Evidence

- Terminal output from `dig TXT torlegacy.com`
- Screenshot: `Screenshots/DNS-TXT-01.png`

## 6. DMARC Analysis

### Observations

| DMARC Record | Value |
|--------------|-------|
| DMARC Policy | v=DMARC1; p=none; |

---

### Security Assessment

#### Positive Observations

- A DMARC (Domain-based Message Authentication, Reporting and Conformance) record is configured.
- The presence of a DMARC record demonstrates that the domain has implemented email authentication monitoring.

#### Potential Improvement

- The DMARC policy is currently set to **p=none**, which only monitors email authentication results.
- The domain has implemented DMARC with a monitoring-only (`p=none`) policy. Organizations commonly use this policy during deployment before moving to stricter enforcement such as `quarantine` or `reject`.

---

### Risk Assessment

| Finding | Risk Level |
|----------|------------|
| DMARC Record Present | Low Risk |
| Policy set to `p=none` | Informational / Low |

---

### Evidence

- Terminal output from `dig TXT _dmarc.torlegacy.com`
- Screenshot: `Screenshots/DNS-DMARC-01.png`

## 7. DKIM Analysis

### Observations

| DKIM Selector | Status |
|---------------|--------|
| default | DKIM record present |

| Attribute | Value |
|-----------|-------|
| Version | DKIM1 |
| Key Type | RSA |
| Public Key | Present |

---

### Security Assessment

#### Positive Observations

- A DKIM (DomainKeys Identified Mail) record is configured using the `default` selector.
- The domain publishes a valid RSA public key for email signature verification.
- DKIM helps receiving mail servers verify that outgoing email has not been altered in transit and was sent by an authorized source.

#### Informational Observation

- The public key is published in DNS as expected for DKIM authentication.

---

### Risk Assessment

| Finding | Risk Level |
|----------|------------|
| DKIM Record Present | Low Risk |
| RSA Public Key Published | Low Risk |

---

### Evidence

- Terminal output from `dig TXT default._domainkey.torlegacy.com`
- Screenshot: `Screenshots/DNS-DKIM-01.png`