# SC4063 Network Security — Module Outline (0→100)

> **Code:** SC4063 (3 AU, MPE) · **Prereq:** SC3010 Computer Security (SC2008 Computer Network strongly recommended) · **Position:** MPE deep-dive beyond SC2008 Ch8 & SC3010 Ch6/8 · **Model:** muse-spark-1.2-contributor only (ox-alpha-free, retry 500/503, no fallback)

## Module Overview
SC4063 hardens **networks**, not just hosts or apps. SC2008 teaches *how packets move* (TCP/IP, routing, DNS, wireless); SC3010 teaches *CIA, crypto, auth, software/OS security* at foundation level. SC4063 is their intersection at depth: firewalls & segmentation, IDS/IPS, VPN tunnelling, DDoS defence, wireless/5G security, and monitoring/forensics — the toolkit that keeps an enterprise reachable under attack. From zero: every packet, handshake, and crypto primitive is re-derived on first use (intuition → picture → formal → runnable code). 0→100 flow is **threat → perimeter → detection → tunnel → availability → wireless → hunt → harden**: first model the adversary, then build walls, eyes, tunnels, and scrubbers before proving the whole fabric in a capstone audit. All diagrams are color TikZ; all code is highlighted `lstlisting`.

## Chapter Plan (8 chapters, 4–5 LOs each)

### Ch1 — Threat Models & Network Security Foundations (`ch01-threat`)
- model Dolev-Yao network adversary (eavesdrop/modify/inject/replay) vs. insider & APT;
- classify threats with STRIDE/CIA and map to OSI/TCP-IP layers and attack surfaces;
- apply defense-in-depth, least privilege, and zero-trust principles to a campus network;
- quantify risk (likelihood×impact, CVSS) and prioritise controls by cost/benefit.

### Ch2 — Firewalls & Network Segmentation (`ch02-firewall`)
- distinguish stateless packet filter vs. stateful vs. next-gen/application proxy (WAF);
- write and audit iptables/nftables ACLs and reason about rule order/shadowing;
- design DMZ, screened-subnet, and micro-segmentation with NAT/bastion hosts;
- evaluate firewall limits (encrypted traffic, insider, covert channels) and pair with IDS.

### Ch3 — Intrusion Detection & Prevention (`ch03-ids`)
- contrast signature (Snort/Suricata) vs. anomaly vs. hybrid detection and their ROC trade-offs;
- place NIDS/NIPS/HIDS at tap, inline, and host vantage points; explain fail-open vs. fail-closed;
- tune rules, suppress false positives, and correlate alerts via SIEM;
- measure IDS: TPR/FPR, base-rate fallacy, and evasion (fragmentation, encryption).

### Ch4 — VPNs & Secure Tunnelling (`ch04-vpn`)
- explain IPsec (AH/ESP, transport vs. tunnel, IKEv2) and TLS/WireGuard VPN trade-offs;
- walk through SA establishment, key exchange, and packet encapsulation overhead;
- configure split vs. full tunnel, remote-access vs. site-to-site, and kill-switch semantics;
- audit VPN for leakage (DNS, IPv6, reconnection) and performance vs. security.

### Ch5 — Denial-of-Service & Availability Defence (`ch05-ddos`)
- taxonomy: volumetric, protocol (SYN flood), and application-layer DDoS + amplification (DNS/NTP);
- explain botnets, reflectors, and pulsing attacks; compute bottleneck and amplification factor;
- deploy mitigations: SYN cookies, rate/bandwidth policing, scrubbing centre, Anycast/CDN, blackholing;
- plan an incident playbook: detect → classify → filter → scale → post-mortem.

### Ch6 — Wireless & Mobile Network Security (`ch06-wireless`)
- trace 802.11 evolution WEP→WPA2 (4-way handshake) →WPA3-SAE and why each step mattered;
- mount and foil evil-twin, deauth, KRACK-style, and rogue-AP attacks;
- extend to Bluetooth/BLE pairing and 5G AKA/IMSI-catcher intuition;
- design a hardened wireless deployment: 802.1X/EAP, PMF, and rogue-AP detection.

### Ch7 — Monitoring, Forensics & Zero Trust (`ch07-monitor`)
- capture and dissect traffic (tcpdump/Wireshark, NetFlow/IPFIX) and build visibility baselines;
- deploy honeypots/honeynets and DNS/BGP hardening (DNSSEC, RPKI) as network sensors;
- run a forensics workflow: preserve → timeline → IoC hunt → attribute;
- apply zero-trust network access (ZTNA) vs. perimeter model and map to NIST 800-207.

### Ch8 — Studio: Hardened Enterprise Network Capstone (`ch08-capstone`)
- compose Ch1–7 into a segmented enterprise (WAN→DMZ→core→wireless) with firewall/IDS/VPN/DDoS controls;
- pen-test the design (port scan, spoof, IDS evasion, VPN leak, deauth) and close findings;
- write a monitoring dashboard + SIEM detection rules and run a tabletop IR exercise;
- reflect on cost, usability, and residual risk; argue when controls hurt availability more than they help.

## TikZ Diagram Plan (2–3 per chapter, color where useful)

- **Ch1:** (1) Dolev-Yao attacker on a pipe: Alice→[Eve controls network, red!15]→Bob with CIA labels (blue!12/green!12/orange!12); (2) OSI stack with threat badges per layer + legend; (3) Defense-in-depth concentric rings (perimeter blue!12 → segment green!12 → host orange!12 → data violet!12)
- **Ch2:** (1) Firewall generations timeline: packet filter→stateful→proxy→NGFW (blue→green→orange→violet); (2) Screened-subnet DMZ topology (Internet red!12 | bastion orange!15 | DMZ yellow!12 | LAN green!12, rule arrows); (3) ACL shadowing Venn: overlapping CIDR blocks with first-match highlight
- **Ch3:** (1) NIDS tap vs. NIPS inline placement (mirror port vs. inline diamond gate, blue!12/red!12); (2) Signature vs. anomaly ROC curves with threshold slider; (3) SIEM correlation funnel: raw alerts→aggregate→incident (funnel fills orange!12→red!12)
- **Ch4:** (1) IPsec ESP tunnel encapsulation: original IP (blue!12) wrapped in ESP (green!15) → new IP (violet!12) with AH/ESP legend; (2) IKEv2 + TLS 1.3 vs. WireGuard handshake swimlanes; (3) Split-tunnel vs. full-tunnel flow map with DNS-leak red branch
- **Ch5:** (1) DDoS kill-chain: botnet (red!12) → reflector amplification (orange!15, ×factor label) → victim; (2) SYN-flood half-open backlog vs. SYN-cookie rescue (red→green); (3) Scrubbing centre + Anycast/CDN diversion topology (grey→green scrub, blue Anycast PoPs)
- **Ch6:** (1) WPA2 4-way handshake ladder with nonce/MIC labels + KRACK reinstall red fork; (2) Evil-twin/rogue-AP topology: client torn between legit (green!12) and evil (red!15) with RSSI bars; (3) 802.1X/EAP-TLS enterprise auth swimlane (supplicant/authenticator/RADIUS, fills blue/green/orange)
- **Ch7:** (1) Visibility pipeline: tap→NetFlow→collector→SIEM dashboard (blue!12→teal!12→orange!12→violet!12); (2) Honeypot vs. production honeynet with attacker diverted (red path → yellow honey); (3) Zero-trust vs. perimeter: castle-moat (grey) vs. identity-aware micro-perimeters (green mesh)
- **Ch8:** (1) Enterprise reference topology: WAN→DMZ→core→wireless with firewall/IDS/VPN badges per zone; (2) Attack→detect→respond swimlane (red attack→blue detect→green respond→violet lessons); (3) Risk heatmap residual after controls (likelihood×impact, red→amber→green shift)

## lstlisting Plan (listings with language=, colors keyword blue!60!black, comment green!50!black, string orange!60!black, numbers gray, xleftmargin 1em)

- **Python (primary, all chapters):** Scapy packet crafting/sniffing, SYN-flood & amplification demo, IDS rule test harness, IPsec/WireGuard config generation, WPA2 handshake parser, tcpdump/Wireshark automation with `pyshark`, NetFlow aggregation, SIEM rule stub. Every block `\\begin{lstlisting}[language=Python]` with caption + numbers.
- **C (secondary, Ch2, Ch3, Ch5, Ch7):** raw-socket packet filter, state-table sketch, eBPF/XDP drop program stub, SYN-cookie kernel intuition, libpcap capture loop. Shows SC1008→SC4063 transfer (same C packet structs filtered in Ch2, inspected in Ch3, rate-limited in Ch5).
- **Bash/YAML (inline, Ch2 & Ch4 & Ch7):** `iptables`/`nft` rule sets, `wg-quick`/`strongSwan` configs, Suricata `suricata.yaml` + rule, Zeek/SIEM pipeline YAML — rendered as `language=bash` lstlisting, never verbatim.

## Exercise Themes (per chapter, 4–6 items)

- Ch1: STRIDE on a campus Wi-Fi + CVSS scoring & risk-prioritisation table; Dolev-Yao trace analysis.
- Ch2: write/audit an iptables ruleset (find shadowed rule); design a DMZ for a 3-tier web app; NAT traversal trace.
- Ch3: author a Suricata rule, measure TPR/FPR on a pcap, tune away a false positive, evade via fragmentation.
- Ch4: bring up a WireGuard/IPsec tunnel pair, prove no DNS/IPv6 leak, benchmark overhead vs. TLS VPN.
- Ch5: craft SYN-flood with Scapy in a lab netns, enable SYN cookies and re-measure backlog; compute DNS amplification factor.
- Ch6: crack WEP toy (why it fails), run a deauth/evil-twin lab (contained), audit a WPA3-SAE capture.
- Ch7: build a NetFlow baseline, hunt an IoC in a pcap timeline, deploy a cowrie honeypot and triage hits.
- Ch8: capstone audit — harden → pen-test → SIEM-alert → IR report for the enterprise topology; residual-risk memo.

## Prerequisite Graph

```
MH1812/SC1123 ──┐
                ├─→ SC1008 (C) ──────────────┐
SC1003 ─────────┘                            │
                                             ▼
SC2000 (prob) + SC1004 ──→ SC2008 (TCP/IP, routing, DNS, wireless, Ch8 security intro)
                              │                    │
SC1005→SC1006→SC2005 (OS) ─────┤                    │
                              ▼                    ▼
                          SC3010 (CIA, crypto, auth, software/OS sec, Ch6 net-sec foundations)
                              │                    │
                              └────────┬───────────┘
                                       ▼
                                   SC4063 (firewall→IDS→VPN→DDoS→wireless→monitor→capstone)
                                       │
                              ┌────────┴────────┐
                              ▼                 ▼
                          SC4012/SC4013     SC4051/SC4050
                     (sibling app/sec)   (dist/parallel — shares threat-model maturity)
```

SC4063 formally requires SC3010; SC2008 is strongly recommended — without it students lack subnetting/TCP/DNS/wireless intuition that Ch1–6 re-derive only briefly. SC4012/4013 are siblings, not prerequisites.

## Build Invariants & Pedagogy

Book class `11pt a4paper`, geometry `1.3/1.2cm includeheadfoot`, `setstretch 1.20`, `parskip 0.70em`, TikZ `scale 0.82–0.88`, `lstset` coloured above, `hyperref` links, `pdflatex×2` → `grep -c "! " 0`, `pgfkeys 0`, `Overfull>15pt 0`. 0→100 law: intuition→picture→formal→worked example→runnable code→exercise; small-screen verified. Aligns 1-to-1 with `main.tex` 8-chapter scaffold `ch01-threat … ch08-capstone`.
