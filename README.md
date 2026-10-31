# Northstar IAM Lab

**Enterprise Identity & Access Management | Active Directory | Windows Server 2025 | RBAC | Least Privilege**

## Project Overview

Northstar IAM Lab is a self-directed, hands-on Identity and Access Management project designed to simulate identity administration and access control within a fictional enterprise environment.

I built a virtual Windows Server domain infrastructure using Microsoft Hyper-V, configured Active Directory Domain Services (AD DS), provisioned employee accounts, created department-based organizational units and security groups, and implemented group-based permissions for confidential network resources.

The objective is to develop practical IAM skills through real-world scenarios involving authentication, authorization, employee access management, and identity lifecycle administration.

## Technologies Used

- Windows Server 2025
- Windows 11 Enterprise Evaluation
- Microsoft Hyper-V
- Active Directory Domain Services (AD DS)
- Windows DNS Server
- Active Directory Users and Computers (ADUC)
- SMB File Sharing
- NTFS Permissions
- Windows Command Prompt

## Lab Architecture

| Component | Configuration |
|---|---|
| Domain Controller | NS-DC01 |
| Client Workstation | NS-CLIENT01 |
| Active Directory Domain | ad.northstar.test |
| Domain Controller IP | 10.10.10.10 |
| Workstation IP | 10.10.10.20 |
| Virtual Network | Northstar-Lab (Private Hyper-V Switch) |
| Server Operating System | Windows Server 2025 |
| Client Operating System | Windows 11 Enterprise Evaluation |

Both virtual machines communicate through an isolated Hyper-V network.

## Phase 1: Active Directory Infrastructure

**Status: Completed**

- Deployed a Windows Server 2025 virtual machine.
- Installed and configured Active Directory Domain Services and DNS.
- Promoted NS-DC01 to a domain controller.
- Created the ad.northstar.test Active Directory domain.
- Established a private virtual network for isolated testing.
- Created the Northstar-Technologies organizational unit with departmental OUs for Human Resources, Finance, Information Technology, and Sales.

## Phase 2: Identity Provisioning and Group Management

**Status: Completed**

Provisioned simulated employee accounts within Active Directory and assigned them to appropriate organizational units.

Configured the GG_HR_Employees global security group and added Jordan Mitchell, an HR employee, as a member.

Configured temporary credentials and a first-logon password-change requirement to simulate a new employee onboarding process.

### Test Accounts

| Employee | Username | Department | HR Group Membership |
|---|---|---|---|
| Jordan Mitchell | jmitchell | Human Resources | Yes |
| Alex Carter | acarter | Sales | No |

## Phase 3: Role-Based Access Control (RBAC)

**Status: Completed**

Created a confidential HR network share on NS-DC01:

`\\NS-DC01\HR-Confidential`

Configured NTFS and SMB share permissions to allow the HR security group to access the protected resource while excluding unauthorized employees.

This exercise demonstrates how Active Directory security groups can be used to manage access based on job responsibilities instead of granting permissions individually.

## Phase 4: Domain Authentication and Access Validation

**Status: Completed**

Deployed a Windows 11 Enterprise workstation, configured static IPv4 and DNS settings, and successfully joined NS-CLIENT01 to the Active Directory domain.

Authenticated using the HR employee's domain account and verified the account identity and group membership using:

```cmd
whoami
whoami /groups
```

### Access-Control Test Results

| Test Scenario | Expected Result | Actual Result |
|---|---|---|
| Jordan authenticates to AD | Successful login | PASS |
| Jordan's HR group membership | GG_HR_Employees present | PASS |
| Jordan opens HR-Confidential | Access granted | PASS |
| Jordan creates a text file in HR share | File creation successful | PASS |
| Alex attempts to open HR-Confidential | Access denied | PASS |

The authorized HR employee successfully accessed the network share and created `HR-Access-Test.txt`.

The Sales employee was denied access to the same resource, demonstrating that the configured permissions enforce department-based access restrictions.

## Phase 5: Identity Lifecycle Management (Planned)

Upcoming scenarios will cover:

- Joiner: Provisioning a new employee identity and assigning access.
- Mover: Transferring an employee between departments and updating group memberships.
- Leaver: Disabling employee accounts and revoking access during offboarding.
- Access reviews: Validating employee permissions against business responsibilities.

These scenarios will be documented after testing.

## Skills Demonstrated

- Active Directory administration
- Identity provisioning
- Domain authentication
- Security group management
- Role-based access control (RBAC)
- Least-privilege access enforcement
- NTFS and SMB permission configuration
- Windows Server and Hyper-V administration
- DNS and IPv4 troubleshooting
- Access validation and testing

## Project Scope

This is a simulated enterprise environment created for independent technical training and portfolio development. It does not represent production infrastructure or professional employer systems.
