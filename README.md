# sccm

This repository contains Ansible playbooks to automate the process of joining Windows VMs to an Active Directory domain and installing the SCCM agent.

## Execution Sequence

The playbooks should be executed in the following sequence:

### 1. Pre-checks (`pre_checks_conn.yml`)
Validates the target environment before making any changes. It checks WinRM reachability, DNS resolution, Kerberos (port 88) and LDAP (port 389) connectivity, time synchronization, domain controller discovery, and current domain join status.

### 2. Join Domain (`ad_join_domain.yml`)
Configures the Windows VM to join the Active Directory domain. It sets the computer hostname to match the Ansible inventory name, performs the domain join operation using PowerShell credentials, and reboots the system if the domain join is successful.

### 3. Install SCCM Agent (`install_sccm_agent.yml`)
Automates the SCCM agent installation using the "Client Push" method. It delegates execution to the SCCM Primary Site Server, loads the Configuration Manager PowerShell module, triggers Active Directory System Discovery if the device is not yet known, and initiates the client push installation once the device is discovered in the SCCM database.
