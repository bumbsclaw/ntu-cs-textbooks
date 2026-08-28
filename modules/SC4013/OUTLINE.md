# SC4013 Application Security — Textbook Outline (0→100)

**Code:** SC4013 · **AU:** 3 · **Type:** MPE (≥4× SC4xxx) · **Prereq:** SC3010 Computer Security
**Focus:** OWASP Top 10, threat modeling, secure SDLC, pentesting — application-layer defense.
**Position:** Builds on SC3010 (CIA, crypto, auth, software/network/OS security) and zooms into code.
**Sources:** NTU CCDS MPE catalogue, NTUMods SC3010/SC4012, OWASP Top 10 2021/2025, OWASP ASVS/SAMM, NIST SSDF.

## Overview
SC4013 hardens web, mobile and API applications against the OWASP Top 10 (2021/2025:
A01 Broken Access Control, A02 Cryptographic Failures, A03 Injection, A04 Insecure Design,
A05 Security Misconfiguration, A06 Vulnerable Components, A07 Auth Failures, A08 Integrity
Failures, A09 Logging Failures, A10 SSRF). SC3010 gives foundations — CIA triad, threat
modeling basics, crypto primitives, auth and software security. SC4013 applies them to
application code: threat-model a feature, code/review a fix, and pentest-verify it.
From zero: HTTP, cookies, SQL and DOM are defined on first use; intuition (attacker
story) → formal model (STRIDE, DREAD) → fix (defense pattern) → verify (SAST/DAST/ZAP).
Graduates can own secure SDLC for a full feature. Aligns 1-to-1 with `main.tex` 8-chapter
scaffold `ch01-owasp` … `ch08-sdlc`.

## Chapter Breakdown (8 chapters, 0→100)

### Ch1 — OWASP Top 10 & Risk Taxonomy (`ch01-owasp`)
Outcomes: (1) map OWASP A01–A10 to CIA/STRIDE; (2) score risk qualitatively and via
  CVSS/DREAD; (3) distinguish design vs. implementation vs. configuration flaws.
TikZ: (1) OWASP 2021 sunflower/heatmap — color fills blue!15/orange!15/red!15 by rank
  with legend; (2) STRIDE↔OWASP bipartite mapping; (3) Risk matrix (likelihood×impact)
  with CVSS vector overlay.
lstlisting: Python — OWASP dependency-check + CVSS calculator (`cvss` lib) snippet.
Exercises: classify Juice Shop bugs to OWASP IDs; CVSS scoring debate; risk-matrix triage.

### Ch2 — Authentication, Session & Identity (`ch02-auth`, OWASP A07)
Outcomes: (1) design password hashing + MFA (TOTP/WebAuthn); (2) implement OAuth2/OIDC
  and JWT validation; (3) prevent session fixation/hijack (SameSite, HttpOnly, Secure).
TikZ: (1) OAuth2 authorization-code flow — swimlane user/browser/AS/RS color-coded
  green!15/blue!12/orange!15; (2) JWT anatomy (header.payload.signature) + validation
  timeline with `alg:none` attack branch; (3) Session lifecycle state machine.
lstlisting: Java (Spring Security) — `BCryptPasswordEncoder` + JWT filter; JS — `fetch`
  with `SameSite=Lax` cookie handling and CSRF double-submit demo.
Exercises: crack weak hashes (John/Hashcat), audit JWT `none` confusion, Burp session lab.

### Ch3 — Injection: SQLi, XSS, Command & Template (`ch03-injection`, A03)
Outcomes: (1) explain code-data confusion; (2) build parameterized queries and contextual
  output encoding; (3) block SSTI/CMDi/LDAPi via allow-listing and sandboxing.
TikZ: (1) SQL parse-tree vs. string-concatenation fork — green safe / red injected;
  (2) XSS reflected→stored→DOM flow across trust boundary violet!10; (3) Template
  injection (SSTI) sandbox escape with Jinja2/Thymeleaf.
lstlisting: Java — `PreparedStatement` vs. concat; Python — Jinja2 autoescape + safe
  `subprocess`/`shlex`; JS — `DOMPurify.sanitize()` vs. `innerHTML`.
Exercises: Juice Shop SQLi/XSS labs, payload crafting, fix-diff code review.

### Ch4 — Access Control & Authorization (`ch04-access`, A01)
Outcomes: (1) model RBAC/ABAC/ReBAC (PEP/PDP); (2) detect IDOR/BOLA/BFLA, path traversal,
  privilege escalation; (3) enforce server-side checks and deny-by-default.
TikZ: (1) RBAC matrix + ABAC policy-decision tree (PEP/PDP with xcolor fills);
  (2) IDOR/BOLA sequence — attacker swaps `id=...`, color highlight red!15;
  (3) Directory-traversal lattice and canonicalization.
lstlisting: Python (Flask) — `@require_role` decorator; Java — Spring `@PreAuthorize`;
  JS — API gateway authorization middleware.
Exercises: IDOR hunt via Burp Intruder/Repeater, broken-access CTF, policy unit tests.

### Ch5 — Cryptographic Failures & Secrets (`ch05-crypto`, A02)
Outcomes: (1) select TLS 1.3 ciphers, encrypt at rest (AES-GCM); (2) manage secrets/keys
  (Vault/KMS, rotation); (3) prevent leakage via logs, URLs, Git (OWASP Crypto Cheat Sheet).
TikZ: (1) TLS 1.3 handshake — color stages ClientHello→Finished (blue→green);
  (2) Secrets-vault architecture app→Vault→KMS→DB with rotation timeline orange!15;
  (3) Failure gallery — ECB penguin vs. GCM, hard-coded key red box.
lstlisting: Python — `cryptography.fernet` + `os.urandom`; Java — JCA
  `AES/GCM/NoPadding` + KeyStore; JS — WebCrypto `subtle.encrypt`.
Exercises: decrypt ECB penguin, scan repo with TruffleHog/gitleaks, http→https+HSTS fix.

### Ch6 — API & Client-Side Security (`ch06-api-client`, A08 + A04)
Outcomes: (1) secure REST/GraphQL (mass assignment, BOLA, rate-limit, schema validation);
  (2) harden DOM, CSP, SRI, CORS; (3) prevent insecure deserialization / prototype pollution.
TikZ: (1) REST→API gateway→microservice validation layers (blue!12/green!15);
  (2) CSP policy tree + blocked-inline-script flow with `script-src` directive;
  (3) CORS preflight + `Origin` check and deserialization gadget chain.
lstlisting: JS — CSP header + `TrustedTypes` + SRI `integrity`; Python — Pydantic strict
  model vs. mass-assignment; Java — Jackson `@JsonIgnore` + bucket4j throttling.
Exercises: mass-assignment exploit, CSP bypass lab, GraphQL introspection audit.

### Ch7 — SSRF, Misconfig & Vulnerable Components (`ch07-ssrf-http`, A05/A06/A10)
Outcomes: (1) block SSRF via allow-lists, URL parsing, egress rules; (2) harden headers,
  containers, IaC (CIS benchmarks); (3) manage SBOM, SCA and supply-chain integrity.
TikZ: (1) SSRF kill-chain → internal metadata `169.254.169.254` (red!15 target);
  (2) Misconfig checklist tree (headers/CORS/debug/cloud bucket) with green/red leaves;
  (3) Dependency graph with CVE blast radius and SBOM (CycloneDX) overlay.
lstlisting: Python — `requests` SSRF deny-list + `urllib.parse` validation; Java —
  `SecurityFilter` security headers; JS/YAML — `npm audit`/`pip-audit` CI gate.
Exercises: SSRF lab (port-scan via `url=`), Docker/K8s hardening, CycloneDX SBOM gen.

### Ch8 — Secure SDLC, DevSecOps & Pentesting (`ch08-sdlc`, A04/A09)
Outcomes: (1) run STRIDE/DREAD threat modeling in sprints; (2) wire SAST/DAST/IAST/SCA
  and IaC scanning into CI/CD; (3) plan pentest, logging/monitoring (A09) and IR.
TikZ: (1) Secure SDLC spiral — threat-model→code→test→deploy with gates violet!10;
  (2) CI/CD pipeline with SAST/DAST/IaC scan gates (green check / red block);
  (3) Pentest methodology + SIEM logging/monitoring flow (ELK/Splunk).
lstlisting: Python — `Bandit`/`Semgrep` pre-commit hook; Java — OWASP ZAP API scan
  script (`zaproxy`); YAML/JS — GitHub Actions with `zaproxy` + `npm audit` gates.
Exercises: threat-model a new feature end-to-end, wire ZAP into pipeline, write SIEM
  detection rule + post-mortem.

## TikZ Plan Summary (2–3/ch, 20 total, color + legend)
Scale 0.70–0.82, fills blue!15/green!20/orange!15/violet!10/red!12 where useful; every
figure labeled, 0 `pgfkeys` errors. Heatmap, swimlanes, parse trees, RBAC matrices, TLS
stages, API layers, SSRF kill-chains, SDLC spiral.

## lstlisting Plan (Python/Java/JS + YAML)
Ch1 Python · Ch2 Java/JS · Ch3 Java/Python/JS · Ch4 Python/Java/JS · Ch5 Python/Java/JS
· Ch6 JS/Python/Java · Ch7 Python/Java/YAML · Ch8 Python/Java/JS/YAML via
`\begin{lstlisting}[language=...]` with `lstset` colors (keyword blue!70!black, comment
green!50!black, string orange!70!black), `xleftmargin=1.0em` — never `verbatim`.

## Exercise Themes
Juice Shop/WebGoat labs; Burp/ZAP proxy; vulnerable→fixed diffs; CTF flags; CVSS/DREAD
worksheets; CI gate authoring; threat-model tabletop + post-mortem.

## Build Invariants & QA
0→100 ground-up (HTTP/SQL/DOM first, intuition→formal→example→exercise); color TikZ +
highlighted `lstlisting`; small-screen 1.3/1.2 cm, `setstretch 1.20`; `pdflatex ×2` →
0 `!` 0 `pgfkeys` 0 `Overfull>15pt`; adversarial QA compile-checks all figures/code.
