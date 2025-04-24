# 🚨 Network Attack Analysis: SYN Flood DoS Attack  
*A cybersecurity project analyzing Wireshark logs to diagnose a web server outage*

[Wireshark TCP/HTTP Log For Reference](https://docs.google.com/spreadsheets/d/1enpRzrIao3J2Lp2tOI0hmu1Cu7D7CjLGhFAiTiR9J64/edit?gid=1522826613#gid=1522826613)

## 📝 Cybersecurity Incident Report  

### **Section 1: Attack Identification**  
**One potential explanation for the website's connection timeout error message is:**  
A **SYN Flood Denial-of-Service (DoS) attack** targeting TCP port 443 (HTTPS).  

**The logs show that:**  
- A single IP (`203.0.113.0`) sent **214+ SYN packets** (highlighted in red) to the server (`192.0.2.1`) within minutes.  
- Legitimate user requests (green) were interrupted or reset (yellow) due to server resource exhaustion.  
- No completed handshakes from the malicious IP, confirming spoofed SYN packets.  

**This event could be:**  
- A deliberate DoS attack to disrupt business operations.  
- An attempt to exploit the server’s TCP/IP stack vulnerability.  

---

### **Section 2: Attack Mechanism & Impact**  
**Normal TCP Three-Way Handshake:**  
1. **SYN**: Client sends SYN to initiate connection.  
2. **SYN-ACK**: Server acknowledges and reserves resources.  
3. **ACK**: Client confirms, establishing the connection.  

**Malicious SYN Flood Behavior:**  
- The attacker sends **high-volume SYN packets** without completing handshakes.  
- The server allocates resources to each half-open connection, exhausting memory/CPU.  
- Legitimate users (e.g., `198.51.100.x`) receive **RST (reset)** or **504 Timeout** errors (logs #73, #77, #121).  

**Log Analysis:**  
- **Pattern**: 214+ SYN packets from `203.0.113.0` (logs #52–214).  
- **Impact**: Server becomes unresponsive, failing to process legitimate HTTPS requests (e.g., `GET /sales.html`).  

---

## 🔧 Recommended Mitigations  
1. **Immediate Actions**:  
   - **Rate limiting**: Block >5 SYN/sec per IP.  
   - **Firewall rules**: Drop packets from `203.0.113.0`.  
2. **Long-Term Solutions**:  
   - **SYN Cookies**: Prevent resource exhaustion.  
   - **Cloudflare/DDoS Protection**: Filter malicious traffic upstream.  
   - **IDS/IPS**: Detect and block future attacks automatically.  

---

## 🌟 Why This Matters  
- **Business Impact**: DoS attacks can cost multiple figures of $ in downtime.  
- **Security Fundamentals**: Demonstrates analysis of **TCP/IP vulnerabilities** and **defense strategies**.  
- **Compliance**: Mitigating DoS aligns with **NIST CSF PR.AC-4** (access control) and **PCI DSS 11.4** (network resilience).  

---

## 📂 How to Use This Project  
- **For Recruiters**: Showcases **log analysis**, **attack pattern recognition**, and **incident response** skills.  
- **For Learners**: [Template](https://docs.google.com/document/d/1xEk_arFwlQOto7KEM6gN-sIYriXhP9-lY2ftpBXhS4M/template/preview?resourcekey=0-_ODneeo__mDgK7BTE1FkVA) for analyzing SYN floods using Wireshark/tcpdump. [Document](https://docs.google.com/document/d/1JYyUPhfm2gwDellGRIcgItA3cZ7kz29xdYpVr1L_o9c/template/preview) on how to read a Wireshark TCP/HTTP log.  

**Tools Used**: Wireshark, tcpdump.  
**Frameworks**: NIST CSF, MITRE ATT&CK (T1498: Network Denial of Service).  

### 📜 License  
This project is part of the [Google Cybersecurity Certificate](https://www.coursera.org/professional-certificates/google-cybersecurity).  

---
