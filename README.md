# SemarangUniversity-Bug

# Security Research Portfolio: Universitas Semarang (USM) Subdomains

**Author:** [Rully Miftahur Rozaq]  
**Role:** Security Researcher / Student at Universitas Semarang  
**Date:** March 2026  

---

## Overview
This repository contains a collection of responsibly disclosed vulnerabilities found within the digital infrastructure of Universitas Semarang.  

The goal of this research is to assist the IT department (Puskom) in securing student and faculty data while demonstrating technical proficiency in penetration testing.

---

## Toolset & Methodology

My research follows a structured methodology:

1. **Reconnaissance**
   - Subdomain enumeration using `Subfinder` and `Amass`.

2. **Analysis**
   - Parameter discovery with `Arjun`
   - Service fingerprinting via `Nmap`.

3. **Vulnerability Assessment**
   - Manual testing for **Broken Access Control (IDOR)**
   - Automated testing for **Injection flaws using `sqlmap`**

4. **Reporting**
   - Documentation and responsible disclosure to the relevant authorities.

---

## Findings Summary

### 1. SQL Injection (Error-Based) - `isdm.usm.ac.id`

- **Severity:** Critical (CVSS 9.8)
- **Vulnerability:** Unauthenticated SQL Injection in the login module.
- **Impact:** Potential full database takeover and authentication bypass.
- **Status:** Reported / Patched
- **Write-up:** [isdm-sqli.md](./writeups/isdm-sqli.md)

---

### 2. IDOR (Insecure Direct Object Reference) - `elearning.usm.ac.id`

- **Severity:** High (Privacy / PII Leak)
- **Vulnerability:** Lack of authorization checks on user profile parameters.
- **Impact:** Unauthorized access to student PII (Email, City, Enrollment data) for **~40,000+ users**.
- **Status:** Reported
- **Write-up:** [elearning-idor.md](./writeups/elearning-idor.md)

---

### 3. Hidden Parameter Discovery & XSS Filtering - `conference.usm.ac.id`

- **Severity:** Informational / Low
- **Vulnerability:** Discovery of hidden parameters (`support`, `repeat`) reflecting input in the UI.
- **Observation:** Advanced **Cloudflare WAF** implementation prevents standard XSS payloads, demonstrating active defense-in-depth.
- **Tools Used:** `Arjun`, `Dalfox`

---

## Detailed Write-ups

### Finding 1: IDOR on Student Profiles

By manipulating the `id` parameter in the profile URL, I could view private data of any registered student.

**Proof of Concept**
