# 🛡️ SIEM Lab: Brute Force Attack Detection

## 1. Project Overview
**Objective:** To detect identity-based attacks using Splunk Enterprise and Windows Event Logs.
**Scenario:** A threat actor attempts to guess user credentials (Brute Force/Dictionary Attack).
**Data Source:** Windows Security Event Log (Event ID 4625).
**Tools Used:** Splunk

## 2. Technical Configuration
* **Ingestion:** Configured Splunk to monitor the local `Security` log channel.
* **Normalization:** Mapped raw Windows Event Logs to Splunk's Common Information Model (CIM) fields.

## 3. Detection Logic (The SPL Workflow)

### Phase 1: Discovery (Raw Logs)
First, I searched for the specific Windows Event Code for "Logon Failure" to validate that Splunk was ingesting the attack data correctly.

```splunk
index=* EventCode=4625

index=* EventCode=4625
| stats count by Account_Name
| where count > 5
