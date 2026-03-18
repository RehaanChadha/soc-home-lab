#  Project Analysis – SOC Home Lab

##  Overview

This project involved building and operating a simulated Security Operations Center (SOC) using Wazuh SIEM to detect and analyze cyber attack activity. The environment consisted of a Kali Linux attacker machine, a Windows victim endpoint, and an Ubuntu-based SIEM server.

The objective was to validate whether real-world attack techniques could be detected and analyzed through endpoint log collection and SIEM correlation.

---

##  System Implementation

### SIEM Deployment

Wazuh Manager, Indexer, and Dashboard were successfully installed and configured on an Ubuntu server. All core services were validated to be operational, and the dashboard was accessible via a web interface.

### Agent Integration

A Wazuh agent was installed on the Windows machine, enabling log forwarding to the SIEM. The agent remained active and consistently transmitted system and security logs.

### Data Pipeline

```id="qj3g5k"
Windows Logs → Wazuh Agent → Wazuh Manager → Wazuh Dashboard
```

This confirmed that the log ingestion and processing pipeline was functioning correctly.

---

##  Attack Simulation Analysis

###  Reconnaissance (Nmap)

An advanced Nmap scan was executed to identify exposed services and system details.

**Observations:**

* Port 3389 (RDP) was discovered open
* OS and service fingerprinting identified Windows environment
* Provided actionable intelligence for further attack phases

**Analysis:**
This phase accurately represents the reconnaissance stage of the cyber kill chain. The attacker was able to identify a viable entry point for exploitation.

---

###  Brute Force Attack (Hydra)

A brute-force attack was launched against the RDP service using Hydra and a password wordlist.

**Observations:**

* Multiple login attempts were generated in parallel
* Authentication failures were recorded on the Windows system
* Attack terminated due to connection errors and rate limiting

**Analysis:**
This simulation reflects real-world credential access attacks. The rate limiting and connection failures indicate the presence of defensive mechanisms, highlighting the effectiveness of basic protections against sustained brute-force attempts.

---

###  Failed Login Simulation

Manual login failures were generated using command-line tools on Windows.

**Observations:**

* Consistent authentication failure logs were created
* Events were captured in Windows Event Logs

**Analysis:**
This step ensured reliable log generation for SIEM validation and confirmed that authentication-related events are highly visible at the endpoint level.

---

##  Detection Effectiveness

### Successful Detection

Wazuh successfully detected:

* Repeated authentication failures
* Patterns consistent with brute-force behavior
* Event spikes corresponding to attack timing

###  MITRE ATT&CK Classification

Detected events were mapped to relevant MITRE ATT&CK techniques:

* T1110 – Brute Force
* Valid Accounts
* Account Manipulation

**Analysis:**
This demonstrates the SIEM’s ability to translate raw log data into structured threat intelligence, enabling faster incident understanding.

---

##  Detection Gaps

###  Limited Detection of Nmap Scans

Nmap-based reconnaissance activity did not generate strong alerts within Wazuh.

**Reason:**

* Wazuh is primarily a host-based SIEM
* Network scans generate minimal endpoint-level logs
* Default logging configurations do not capture detailed scan activity

**Impact:**

* Reduced visibility into early-stage attacks
* Potential blind spot in reconnaissance detection

---

## Key Insights

### 1. Importance of Log Visibility

Detection is highly dependent on the availability and quality of logs. Without sufficient logging, even active attacks may go undetected.

---

### 2. Strength of Host-Based Monitoring

Authentication-based attacks (e.g., brute force) are highly detectable due to detailed endpoint logging.

---

### 3. Need for Layered Security

A complete SOC requires multiple layers of visibility:

* Endpoint monitoring (Wazuh)
* Network monitoring (IDS/IPS tools)

---

### 4. Service Dependency Challenges

Wazuh services required proper startup sequencing and sufficient system resources. Misconfiguration or resource limitations can disrupt detection capabilities.

---

##  Recommendations

To improve detection coverage and realism:

* Integrate **Sysmon** for enhanced Windows telemetry
* Deploy **Suricata or Zeek** for network-level monitoring
* Enable detailed firewall logging
* Develop custom Wazuh detection rules
* Implement alert correlation and tuning

---

##  Conclusion

The SOC home lab successfully demonstrated the ability to detect and analyze authentication-based attacks using Wazuh SIEM. While brute-force activity was clearly identified and classified, reconnaissance detection remained limited, highlighting the need for additional monitoring layers.

This project reinforces the importance of combining endpoint and network visibility to achieve comprehensive threat detection in modern SOC environments.

