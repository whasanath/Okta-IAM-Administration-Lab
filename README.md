
# Okta Identity and Access Management (IAM) Home Lab

**Hands-on IAM Portfolio | Okta | Active Directory | Zendesk | Access Requests | Security Monitoring**

## Project Overview

This project documents hands-on Identity and Access Management (IAM) workflows explored in a personal Okta test environment.

The lab covers user and group administration, Microsoft Active Directory integration, application assignments, self-service access requests, approval workflows, and authentication and security activity monitoring.

The purpose of this project is to develop practical IAM administration skills and understand how organizations manage identities, control application access, and monitor security events.

> **Scope:** This is an educational home lab, not a production deployment. Screenshots document configuration steps and selected results. They do not demonstrate complete end-to-end provisioning or comprehensive security policy enforcement.

---

## Objectives

- Understand the relationship between on-premises Active Directory and cloud identity management.
- Explore directory imports, user matching, and assignment workflows.
- Review group-based application access using Zendesk.
- Configure application access requests and approval workflows.
- Examine Okta System Log events and security configuration features.
- Apply IAM security principles such as least privilege and separation of duties.
- Document technical configurations and troubleshooting observations.

---

## Tools and Technologies

| Technology | Purpose |
|---|---|
| Okta Workforce Identity | Cloud identity and access management |
| Microsoft Active Directory | On-premises directory and identity management |
| Okta AD Agent | Integration between Active Directory and Okta |
| Windows Server | Active Directory lab environment |
| VMware Workstation | Virtualized lab infrastructure |
| Zendesk | Application integration and access management |
| OIDC | Authentication and application integration concepts |
| Okta System Log | Audit and security event investigation |
| Okta HealthInsight | Security posture recommendations |

---

## Lab Walkthrough and Evidence

The following sections document the lab activities using **26 sanitized screenshots** stored in the `screenshots/` directory.

### Lab 1: Okta User and Group Management

**Objective:** Understand how Okta manages users, groups, and application access.

**Activities:**
- Reviewed existing Okta user accounts.
- Examined user account status.
- Explored directory groups and group membership.
- Reviewed how groups can be used for application assignments.

**Evidence:**

![Okta User Management](screenshots/01.png)

![Okta Group Management](screenshots/02.png)

**Key Learning:** Groups help simplify identity administration by allowing access to be managed collectively rather than assigning every application individually.

---

### Lab 2: Active Directory Integration

**Objective:** Explore integration between on-premises Active Directory and Okta.

**Activities:**
- Opened Okta Directory Integrations.
- Reviewed Active Directory integration requirements.
- Explored Okta AD Agent installation guidance.
- Reviewed the registered Active Directory integration.
- Examined organizational unit (OU) selection for synchronization.
- Reviewed an imported Active Directory user in the Okta assignment interface.

**Evidence:**

![Directory Integration](screenshots/03.png)

![Okta AD Agent Setup](screenshots/04.png)

![Active Directory Integration](screenshots/05.png)

![Organizational Unit Selection](screenshots/06.png)

![Imported Active Directory User](screenshots/07.png)

**Key Learning:** Integrating Active Directory with Okta allows organizations to connect on-premises identities with cloud-based identity management.

Directory import and user matching help organizations manage identity information across connected environments.

---

### Lab 3: Application Integration and Access Management

**Objective:** Understand application integration and group-based access assignment.

**Activities:**
- Explored the Okta application catalog.
- Reviewed the Zendesk application integration.
- Examined Zendesk user and group assignments.
- Reviewed an OIDC web application's configuration settings.

**Evidence:**

![Okta Application Catalog](screenshots/08.png)

![Zendesk Application Assignments](screenshots/09.png)

![OIDC Application Configuration](screenshots/10.png)

**Key Learning:** Okta supports centralized application assignment and authentication integration.

Group-based application assignments can reduce repetitive administrative tasks and improve consistency.

**Validation Note:** The screenshots show application settings and assignments, but do not establish successful downstream account provisioning.

---

### Lab 4: Okta System Log Monitoring

**Objective:** Understand how IAM administrators investigate administrative and authentication activity.

**Activities:**
- Opened Okta System Log.
- Reviewed available search and filtering capabilities.
- Examined recorded events.
- Reviewed event information, including actors, targets, timestamps, and outcomes.

**Evidence:**

![Okta System Log Search](screenshots/11.png)

![Okta System Log Events](screenshots/12.png)

**Key Learning:** Okta System Log provides audit records that support troubleshooting, security investigations, and monitoring of identity-related activities.

---

### Lab 5: Self-Service Application Access

**Objective:** Configure an application access-request workflow using Okta Self Service.

**Activities:**
- Reviewed organization-level self-service settings.
- Opened the Zendesk application configuration.
- Enabled users to request Zendesk access.
- Configured the application to require approval before access assignment.

**Evidence:**

![Okta Self Service Settings](screenshots/13.png)

![Zendesk Self Service Configuration](screenshots/14.png)

![Zendesk Approval Required](screenshots/15.png)

**Key Learning:** Self-service access requests allow employees to request applications without requiring administrators to manually initiate every assignment.

Approval workflows introduce an authorization checkpoint before access is granted.

---

### Lab 6: Access Approval Workflow Configuration

**Objective:** Configure approval requirements, notifications, and expiration settings.

**Activities:**
- Enabled required approval for Zendesk.
- Reviewed approval notification options.
- Configured a two-day approval response window.
- Added a named approver.
- Reviewed the expected application assignment behavior after approval.

**Evidence:**

![Approval Notification Settings](screenshots/16.png)

![Assigned Application Approver](screenshots/17.png)

**Key Learning:** Approval workflows help organizations establish controlled application access.

The approval process should be designed so that an authorized person reviews the request before access is granted.

---

### Lab 7: Self-Service Request Verification

**Objective:** Verify that Zendesk appears in the application catalog and that access requests can be submitted.

**Activities:**
- Confirmed Zendesk displayed self-service requests enabled.
- Confirmed approval was required.
- Opened the end-user application catalog.
- Located Zendesk with the Request option.
- Submitted an application access request.
- Located the pending request in the Okta administration interface.

**Evidence:**

![Zendesk Self Service Enabled](screenshots/18.png)

![Zendesk Application Request](screenshots/19.png)

![Pending Application Requests](screenshots/20.png)

![Request and Approver Details](screenshots/21.png)

**Observed Result:**

The application request successfully appeared in the pending-request queue.

The request details displayed:
- Requester
- Next approver
- Request expiration period

**Validation Limitation:** The screenshots do not demonstrate a completed approval or successful Zendesk account provisioning.

---

## Example Access Request Workflow

1. An employee signs in to the Okta end-user dashboard.
2. The employee opens the application catalog.
3. The employee selects **Request** for Zendesk.
4. Okta creates a pending access request.
5. The configured approver reviews the request.
6. If approved, Okta assigns the application according to its configured settings.
7. Account provisioning depends on the application's provisioning configuration.

**Observed in this lab:** Request submission and pending-request visibility.

**Not yet verified:** Completed approval, successful downstream provisioning, and application sign-in after approval.

---

## IAM Security Finding: Separation of Duties

During testing, the same lab account appeared as both the requester and the next approver.

This highlighted an important IAM governance consideration.

**Security Risk:**

Allowing employees to approve their own access requests can weaken access governance and create opportunities for unauthorized privilege assignment.

**Recommended Improvement:**

Use separate requester and approver accounts.

For example:

- **Employee:** Requests Zendesk access.
- **Application Owner:** Reviews the business justification.
- **Okta:** Assigns the application after approval.
- **IAM Administrator:** Reviews access records and investigates exceptions.

This approach supports separation of duties and appropriate access governance.

---

### Lab 8: Okta HealthInsight Review

**Objective:** Review security posture recommendations within Okta.

**Activities:**
- Opened Okta HealthInsight.
- Reviewed security recommendations.
- Examined available remediation guidance.
- Identified areas where security configuration could be improved.

**Evidence:**

![Okta HealthInsight](screenshots/22.png)

**Key Learning:** HealthInsight helps administrators identify potential security configuration improvements.

Reviewing recommendations does not mean the identified issues have been remediated.

---

### Lab 9: Authentication and Security Configuration

**Objective:** Explore authentication and security controls available in Okta.

**Activities:**
- Reviewed configured authenticators.
- Examined authentication factor options.
- Explored network zone configuration.
- Reviewed behavior detection settings.

**Evidence:**

![Okta Authenticators](screenshots/23.png)

![Okta Network Zones](screenshots/24.png)

![Okta Behavior Detection](screenshots/25.png)

**Key Learning:** Authentication factors, network zones, and behavior detection can support risk-based access decisions when appropriately configured and enforced.

**Validation Note:** These screenshots document configuration views rather than successful policy enforcement tests.

---

### Lab 10: Additional System Log Investigation

**Objective:** Review additional identity-related security events.

**Activities:**
- Returned to Okta System Log.
- Reviewed recorded authentication-related events.
- Examined event outcomes and available audit information.

**Evidence:**

![Additional Okta System Log Events](screenshots/26.png)

**Key Learning:** Audit logs provide visibility into identity-related events and help analysts investigate access issues and potentially suspicious activity.

---

## Key Findings

1. Explored user and group administration in Okta.
2. Reviewed Active Directory integration and directory import workflows.
3. Examined Zendesk application assignments and OIDC application settings.
4. Configured a Zendesk self-service request workflow requiring approval.
5. Confirmed that an application request appeared in the pending-request queue.
6. Identified a separation-of-duties concern involving the requester and approver.
7. Reviewed Okta System Log and security configuration features.
8. Gained experience documenting IAM configurations and validation limitations.

---

## Challenges and Lessons Learned

### Challenge 1: Understanding AD and Okta Integration

**Lesson:** Active Directory and Okta serve different but complementary roles in identity management.

Active Directory manages directory identities within an organization's environment, while Okta provides cloud-based identity and application access management capabilities.

### Challenge 2: Configuring Application Approval

**Challenge:** An approval workflow requires at least one designated approver.

**Lesson:** Access request workflows must include appropriate approval routing and notification configuration.

### Challenge 3: Requester and Approver Separation

**Challenge:** The same test account was configured as both requester and approver.

**Lesson:** Separate accounts should be used to demonstrate proper approval governance.

### Challenge 4: Verifying Application Access

**Lesson:** A pending request does not mean that application access has been granted.

Successful approval, application assignment, provisioning, and sign-in should be validated separately.

---

## Future Improvements

- Complete an approval test using separate requester and approver accounts.
- Test approved and denied requests.
- Verify notification delivery.
- Validate Zendesk application assignment after approval.
- Test downstream account provisioning where supported.
- Perform controlled authentication policy testing.
- Document an example System Log investigation.
- Add an IAM architecture diagram.

---

## Skills Demonstrated

- Identity and Access Management (IAM)
- Okta Administration
- Active Directory Integration Concepts
- Directory Import and User Matching
- User and Group Management
- Application Access Management
- Self-Service Access Requests
- Approval Workflow Configuration
- Least Privilege and Separation of Duties
- Audit Log Review
- IAM Security Configuration Review
- Technical Documentation

---

## Screenshot Privacy

The screenshots in this repository are intended to be privacy-reduced copies of the original lab evidence.

Some identifying information and sensitive configuration areas have been covered using opaque masks.

**Important:** All screenshots should be manually reviewed before public publication. Automated masking cannot guarantee that every sensitive value has been removed.

Do not publish passwords, API tokens, private credentials, tenant secrets, or unredacted personal information.

---

## Disclaimer

This is an independent educational project created for hands-on IAM learning and professional portfolio development.

It is not affiliated with or endorsed by Okta, Zendesk, or any employer.
