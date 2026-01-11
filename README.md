# SIEM Log Analysis Report – Log4j Exploitation & HTTP Data Exfiltration

## 📌 Project Overview

This project demonstrates **SOC-level log analysis and investigation skills** using a simulated environment.  
The focus is on detecting, investigating, and documenting two common attacker techniques involving HTTP traffic.

### Scenarios Analyzed
1. **Log4j vulnerability exploitation (Log4Shell)**
2. **Data exfiltration over HTTP**

All analysis was performed using anonymized training data adapted from SOC lab exercises.

👉 The completed SIEM Log Analysis Report can be downloaded via my cybersecurity blog, [Happy Bytes](https://happy-bytes.vercel.app/blogs/cybersec-lab-siem-log-analysis)

---

## 🛠 Tools & Technologies

- Wireshark  
- Splunk  
- CyberChef  
- HTTP & network protocol analysis  

---

## 🔎 Scenario 1: Log4j Vulnerability Analysis

**Objective:**  
Identify exploitation attempts targeting Log4j via malicious HTTP requests.

**Key Techniques:**
- Inspection of HTTP headers and payloads
- Detection of JNDI injection patterns
- Decoding obfuscated strings using CyberChef

Within Wireshark, we can use common search parameters to narrow our search, including:
- http.request.method == "POST"
- (ip contains "jndi") or (ip contains "Exploit")
- (frame contains "jndi") or ( frame contains "Exploit")
- (http.user_agent contains "$") or (http.user_agent contains "==")

---

- Image 1: Using these parameters, we identified a potentially suspicious packet within Wireshark. Investigating the HTTP stream of this packet, we identified the start of a "Log4j" attack phase. CyberChef was then used to decode and transform the obfuscated payload.

![Log4j HTTP JNDI injection observed in Wireshark](images/log4j_http_cleartext_02.png)


---

## 📤 Scenario 2: Data Exfiltration via HTTP

**Objective:**  
Detect and analyze suspicious outbound HTTP traffic indicating possible data exfiltration.

**Key Techniques:**
- Packet-level inspection in Wireshark
- Event correlation and timeline analysis in Splunk
- Identification of abnormal request frequency and payload size

---

- Image 1: Using Splunk, we could isolate a POST request with a large payload (600+ bytes, in this example) for further investigation.

![Data Exfiltration](images/data_exfil_1.png)


- Image 2: To correlate the findings, we successfully isolated the suspicious packet in Wireshark, and followed the HTTP stream to identify the exposed credentials and data being exfiltrated to the external IP.

![Data Exfiltration](images/data_exfil_3.png)

---

## 📄 Deliverables

👉 The completed SIEM Log Analysis Report can be downloaded via my cybersecurity blog, [Happy Bytes](https://happy-bytes.vercel.app/blogs/cybersec-lab-siem-log-analysis)

- Viewable on GitHub: [SIEM Log Analysis Report (PDF)](report/SIEM_Log_Analysis_Report_Complete.pdf)
- Detection queries
- Anonymized sample logs

---

## 🧠 Skills Demonstrated

- SIEM log analysis  
- Network traffic investigation  
- Threat detection & triage  
- Incident documentation  
- SOC-style remediation recommendations  

---

## ⚠️ Attribution

Data used in this project is derived from simulated SOC lab environments and re-analyzed independently for educational and portfolio purposes.

---

## 📬 Contact

Feel free to connect on [LinkedIn](https://www.linkedin.com/in/danchui/) or review my other security projects.
