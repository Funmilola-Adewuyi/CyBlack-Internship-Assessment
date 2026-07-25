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