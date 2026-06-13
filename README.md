# Suricata-Detection-Engineering-Lab

# Suricata Detection Engineering Lab

## Overview

This project demonstrates the deployment, configuration, and operation of a network-based Intrusion Detection System (IDS) using Suricata in a controlled cybersecurity laboratory environment.

The objective was to develop practical detection engineering skills by creating custom signatures, generating malicious and benign network traffic, validating detections, and performing alert investigations. The lab simulates common Security Operations Center (SOC) workflows including monitoring, threat detection, incident analysis, and MITRE ATT&CK mapping.

---

## Key Achievements

* Deployed and configured Suricata IDS on Kali Linux
* Developed custom detection signatures for reconnaissance and network activity
* Detected ICMP reconnaissance and TCP scanning activity
* Validated Suricata alerts using simulated attack traffic
* Analyzed EVE JSON and Fast Log telemetry
* Performed alert investigations and event correlation
* Mapped detections to the MITRE ATT&CK framework
* Documented SOC investigation workflows

---

## Lab Architecture

```text
                    +------------------+
                    |  Windows Server  |
                    | Target Host      |
                    | 192.168.56.102   |
                    +---------+--------+
                              |
                              |
                       Virtual Network
                              |
                              |
                    +---------+--------+
                    | Kali Linux       |
                    | Suricata IDS     |
                    | 192.168.56.101   |
                    +------------------+
```

---

## Technologies Used

| Component      | Purpose                      |
| -------------- | ---------------------------- |
| Kali Linux     | Security Monitoring Platform |
| Suricata IDS   | Network Intrusion Detection  |
| Nmap           | Attack Simulation            |
| Windows Server | Target System                |
| EVE JSON       | Structured Alert Logging     |
| Fast Log       | Real-Time Alert Monitoring   |

---

## Detection Engineering

Custom detection rules were created to identify suspicious network activity and reconnaissance techniques.

### ICMP Reconnaissance Detection

```text
alert icmp any any -> $HOME_NET any (msg:"SOC-LAB ICMP Ping Detected"; sid:1000001; rev:1;)
```

### SSH Activity Detection

```text
alert tcp any any -> $HOME_NET 22 (msg:"SOC-LAB SSH Connection"; sid:1000002; rev:1;)
```

### HTTP Traffic Detection

```text
alert tcp any any -> $HOME_NET 80 (msg:"SOC-LAB HTTP Traffic"; sid:1000003; rev:1;)
```

### SMB Activity Detection

```text
alert tcp any any -> $HOME_NET 445 (msg:"SOC-LAB SMB Connection"; sid:1000004; rev:1;)
```

### RDP Activity Detection

```text
alert tcp any any -> $HOME_NET 3389 (msg:"SOC-LAB RDP Connection"; sid:1000005; rev:1;)
```

### Port Scan Detection

```text
alert tcp any any -> $HOME_NET any (msg:"SOC-LAB Possible Nmap Scan"; flags:S; threshold:type both, track by_src, count 10, seconds 5; sid:1000006; rev:1;)
```

---

## Attack Simulation

The following activities were performed to generate network telemetry and validate detections.

### ICMP Network Discovery

```bash
ping 192.168.56.101
```

### SYN Port Scan

```bash
nmap -sS 192.168.56.102
```

### Service Enumeration

```bash
nmap -sV 192.168.56.102
```

### Aggressive Enumeration

```bash
nmap -A 192.168.56.102
```

---

## Detection Results

### ICMP Reconnaissance

The IDS successfully generated alerts when ICMP traffic was observed between hosts.

**Evidence**

![ICMP Detection](screenshots/icmp-detection.png)

**Analysis**

* Source Host: Windows Server
* Destination Host: Suricata Sensor
* Detection: Network Discovery Activity

---

### Port Scan Detection

Suricata identified repeated SYN packets indicative of reconnaissance activity.

**Evidence**

![Nmap Detection](screenshots/nmap-detection.png)

**Analysis**

* Scan Type: SYN Scan
* Tool: Nmap
* Detection Method: Threshold-Based Rule

---

## Alert Investigation

### Sample Alert

```json
{
  "event_type": "alert",
  "src_ip": "192.168.56.102",
  "dest_ip": "192.168.56.101",
  "alert": {
    "signature": "SOC-LAB ICMP Ping Detected"
  }
}
```

### Investigation Workflow

1. Alert Generation
2. Alert Validation
3. Source IP Analysis
4. Destination Analysis
5. Timeline Reconstruction
6. MITRE ATT&CK Mapping
7. Risk Assessment
8. Documentation

---

## Threat Hunting Activities

The following threat hunting scenarios were investigated:

### Network Reconnaissance

Detection of ICMP and TCP scanning activity.

### Service Enumeration

Detection of unauthorized service discovery attempts.

### Remote Access Monitoring

Monitoring SSH and RDP connections.

### SMB Activity Monitoring

Identification of file-sharing activity and potential lateral movement behavior.

### File Transfer Activity

Inspection of HTTP-based file downloads.

---

## MITRE ATT&CK Mapping

| Detection           | ATT&CK Technique                   |
| ------------------- | ---------------------------------- |
| ICMP Reconnaissance | T1046 Network Service Discovery    |
| Port Scanning       | T1046 Network Service Discovery    |
| SMB Activity        | T1021.002 SMB/Windows Admin Shares |
| RDP Activity        | T1021.001 Remote Desktop Protocol  |
| File Transfer       | T1105 Ingress Tool Transfer        |

---

## Skills Demonstrated

### Detection Engineering

* Signature Development
* Alert Validation
* Rule Testing

### Security Monitoring

* Network Traffic Analysis
* IDS Operations
* Event Correlation

### Threat Hunting

* Reconnaissance Detection
* Service Enumeration Analysis
* Alert Investigation

### Incident Response

* Alert Triage
* Event Analysis
* ATT&CK Mapping

---

## Lessons Learned

This project reinforced key blue-team concepts including network monitoring, intrusion detection, alert investigation, and detection engineering. It also provided practical experience analyzing network telemetry and mapping observed activity to adversary behaviors described in the MITRE ATT&CK framework.

---

## Future Enhancements

* Splunk Integration
* Sysmon Integration
* Sigma Rule Development
* Detection-as-Code
* Malware Traffic Analysis
* Threat Intelligence Enrichment
* Automated Alerting Workflows

---

## Conclusion

This lab demonstrates practical experience deploying and operating Suricata IDS in a blue-team environment. Through custom rule development, attack simulation, alert analysis, and threat hunting, the project showcases foundational SOC analyst and detection engineering skills applicable to real-world security operations.
