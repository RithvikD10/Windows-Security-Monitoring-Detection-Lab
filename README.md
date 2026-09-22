# Windows Security Monitoring & Detection Lab

## Overview

This project is an isolated Windows 11 Enterprise security lab built using VMware Workstation Pro. The lab is designed to practice endpoint monitoring, Windows event analysis, detection engineering, and incident investigation.

## Lab Environment

- VMware Workstation Pro
- Windows 11 Enterprise
- Microsoft Sysmon
- Windows Event Viewer
- Windows Security Auditing
- PowerShell Script Block Logging

## Objectives

- Configure endpoint telemetry using Sysmon
- Analyze Windows and Sysmon event logs
- Generate controlled security events
- Investigate authentication and process activity
- Monitor account and privilege changes
- Monitor PowerShell activity
- Detect service creation
- Correlate events from multiple Windows logging sources
- Document simulated security incidents

## Progress

### 1. Sysmon Installation

Installed Microsoft Sysmon as a Windows service and verified that the service was actively running.

![Sysmon Service Running](screenshots/01-sysmon-service-running.png)

### 2. Sysmon Event Collection

Verified that Sysmon was generating telemetry in the Sysmon Operational event log.

![Sysmon Operational Log](screenshots/02-sysmon-operational-log.png)

### 3. Process Creation Monitoring

Generated a controlled Notepad process and identified the corresponding Sysmon Event ID 1 process creation event.

![Notepad Process Creation](screenshots/03-notepad-process-create.png)

### 4. Custom Sysmon Configuration

Created and applied a custom Sysmon XML configuration for process creation, network connections, file creation, and DNS queries.

![Sysmon Configuration Applied](screenshots/04-custom-sysmon-config-applied.png)

### 5. Sysmon Telemetry Testing

Successfully generated and identified multiple Sysmon event types:

- Event ID 1 - Process Creation
- Event ID 3 - Network Connection
- Event ID 11 - File Creation
- Event ID 22 - DNS Query

![Process Creation](screenshots/05a-sysmon-process-create.png)

![Network Connection](screenshots/05b-sysmon-network-connection.png)

![File Creation](screenshots/05c-sysmon-file-create.png)

![DNS Query](screenshots/05d-sysmon-dns-query.png)

### 6. Failed Authentication Monitoring

Enabled Windows auditing for successful and failed logon attempts.

![Logon Auditing Enabled](screenshots/06a-logon-auditing-enabled.png)

Generated multiple controlled failed authentication attempts against the `labuser` account and identified Windows Security Event ID 4625.

![Failed Logon Event](screenshots/06b-failed-logon-event-4625.png)

### 7. Local User Account Creation

Enabled User Account Management auditing and created a controlled local test account named `testuser`.

Windows Security Event ID 4720 recorded the creation of the account.

![User Account Auditing Enabled](screenshots/07a-user-account-auditing-enabled.png)

![User Account Created](screenshots/07b-user-account-created-4720.png)

### 8. Administrator Group Membership Monitoring

Added the controlled `testuser` account to the local Administrators group.

Windows Security Event ID 4732 recorded the security group membership change.

![Administrator Group Change](screenshots/08-admin-group-member-added-4732.png)

### 9. PowerShell Monitoring

Enabled PowerShell Script Block Logging.

![PowerShell Script Block Logging Enabled](screenshots/09a-powershell-script-block-logging-enabled.png)

Generated a controlled PowerShell command and identified PowerShell Event ID 4104.

![PowerShell Script Block Event](screenshots/09b-powershell-script-block-event-4104.png)

The same activity was correlated with Sysmon Event ID 1, which recorded the PowerShell process, command line, user, executable hash, and parent process.

![PowerShell Sysmon Process Creation](screenshots/09c-powershell-sysmon-process-create.png)

### 10. Windows Service Creation Monitoring

Created a controlled Windows service named `CyberLabService`.

Windows System Event ID 7045 recorded the service installation, including the service name, executable path, start type, and service account.

![Service Creation Event](screenshots/10a-service-created-7045.png)

## Current Findings

The lab successfully captured several types of security-relevant Windows activity.

- Event ID 4625 captured repeated failed interactive logon attempts
- Event ID 4720 captured local user account creation
- Event ID 4732 captured a user being added to the Administrators group
- Event ID 4104 captured PowerShell script block activity
- Sysmon Event ID 1 captured PowerShell process creation and command-line information
- Event ID 7045 captured Windows service creation

These events demonstrated how Windows Security logs, PowerShell logs, and Sysmon can provide different pieces of information about the same system activity.

## Skills Demonstrated

- Windows security monitoring
- Microsoft Sysmon
- Windows Event Viewer
- Windows Security auditing
- Process monitoring
- Network monitoring
- File monitoring
- DNS monitoring
- Authentication monitoring
- Account and privilege change monitoring
- PowerShell logging
- Service creation monitoring
- Event correlation
- Detection analysis
- Incident investigation
- Security documentation

## Incident Reports

- [Incident 001: Repeated Failed Logon Attempts](incident-reports/incident-001-failed-logons.md)

## Next Steps

The Windows endpoint monitoring phase of this lab is complete.

Future expansions will include:

- Deploying a Wazuh SIEM server
- Connecting the Windows endpoint to Wazuh
- Centralizing Windows and Sysmon telemetry
- Building SIEM detection rules and alerts
- Expanding the environment with Active Directory
- Generating controlled attack simulations
- Investigating and correlating alerts across multiple systems
