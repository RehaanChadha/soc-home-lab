# Project Analysis

## Summary
The SOC home lab successfully demonstrated endpoint-based threat detection using Wazuh SIEM. The environment consisted of an Ubuntu-based SIEM server, a Windows victim machine, and a Kali attacker machine.

## What Worked
### Wazuh Deployment
Wazuh Manager, Indexer, and Dashboard were successfully installed and configured on Ubuntu. The dashboard became accessible through the browser and displayed security events in real time.

### Agent Integration
The Windows endpoint was connected to Wazuh using the Windows agent. Logs began flowing into the SIEM, confirming proper data ingestion.

### Brute Force Detection
Authentication abuse was simulated through repeated failed login attempts and Hydra-based brute-force behavior. Wazuh successfully detected authentication failures and visualized them in the dashboard. MITRE ATT&CK mappings related to brute force and account access were shown.

## What Did Not Work Well
### Nmap Detection
Nmap scanning from Kali did not produce strong default detection in Wazuh. This highlighted an important limitation:
- Wazuh is primarily host-based
- Nmap is a reconnaissance tool that often generates weak endpoint visibility by default
- Additional network logging or IDS tools would improve detection

## Key Lessons Learned
- SIEM availability is critical; attacks are not detected if the monitoring server is offline
- Host-based monitoring is effective for authentication abuse
- Network reconnaissance may require firewall logging, IDS tools, or custom rules for clear detection
- Service dependencies matter when starting Wazuh components

## Security Conclusion
The lab proved that Wazuh can detect endpoint-based attacks such as failed logins and brute-force attempts. It also showed that default host-based monitoring has gaps in detecting network reconnaissance. A more mature SOC design would combine SIEM with IDS or expanded logging to improve visibility.
