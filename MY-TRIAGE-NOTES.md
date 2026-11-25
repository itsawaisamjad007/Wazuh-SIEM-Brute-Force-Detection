# My Triage Notes - SSH Brute Force Detection

## Project: Wazuh SIEM - SSH Brute Force Detection

### 1. Alert Received
- Rule ID: 40111 - Multiple Authentication Failures
- Rule ID: 5712 - sshd: authentication failed
- Severity: Level 10
- Source: Ubuntu Server (Agent) - 10.0.2.3

### 2. Investigation
- I checked the alert details in the Wazuh Dashboard.
- Attacker IP: 10.0.2.15 (Kali Linux)
- Targeted User: analyst
- Attack Method: Hydra used to try multiple passwords via SSH
- MITRE ATT&CK: T1110.001 - Brute Force: Password Guessing

### 3. Decision: True Positive or False Positive?
- **Verdict: True Positive**
- Reason: More than 20 failed login attempts in a short time from a single IP. This is not normal user behavior.

### 4. Response / Action Taken
- Wazuh Active Response was NOT configured in this lab, so auto-blocking did not happen.
- I blocked the attacker IP manually on the Ubuntu Server using CLI.
- This completed the SOC workflow: Detection -> Investigation -> Response

### 5. Verification
- I launched the attack again from Kali Linux after blocking.
- Result: No new alerts were generated in Wazuh.
- Conclusion: The block was successful.

### What I Learned
Wazuh only detects and alerts by default. For automatic blocking, Active Response must be configured in ossec.conf and linked with Rule 40111. In a real SOC, this blocking happens automatically.
