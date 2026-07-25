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