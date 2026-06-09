# Software Requirements Specification

## Computerized Maintenance Management System (CMMS)

**Document Version:** 1.1.0
**Status:** Draft
**Date:** 2026-06-09
**Classification:** Internal — Requirements Phase

---

## Table of Contents

- [Software Requirements Specification](#software-requirements-specification)
  - [Computerized Maintenance Management System (CMMS)](#computerized-maintenance-management-system-cmms)
  - [Table of Contents](#table-of-contents)
  - [1. Introduction](#1-introduction)
    - [1.1 Purpose](#11-purpose)
    - [1.2 Scope](#12-scope)
    - [1.3 Definitions, Acronyms, and Abbreviations](#13-definitions-acronyms-and-abbreviations)
    - [1.4 Document Conventions](#14-document-conventions)
  - [2. System Overview](#2-system-overview)
    - [2.1 Product Perspective](#21-product-perspective)
    - [2.2 Deployment Model and SaaS Context](#22-deployment-model-and-saas-context)
    - [2.3 System Actors](#23-system-actors)
      - [2.3.1 Company Administrator](#231-company-administrator)
      - [2.3.2 Technician](#232-technician)
      - [2.3.3 Client](#233-client)
    - [2.4 Key Entities and Relationships](#24-key-entities-and-relationships)
    - [2.5 Assumptions and Dependencies](#25-assumptions-and-dependencies)
    - [2.6 Constraints](#26-constraints)
  - [3. Functional Requirements](#3-functional-requirements)
    - [3.1 User Management and Authentication](#31-user-management-and-authentication)
    - [3.2 Client Onboarding and Account Management](#32-client-onboarding-and-account-management)
    - [3.3 Role and Permission Management](#33-role-and-permission-management)
    - [3.4 Service Management](#34-service-management)
    - [3.5 Incident Management](#35-incident-management)
    - [3.6 Invoice Management](#36-invoice-management)
    - [3.7 Calendar and Scheduling](#37-calendar-and-scheduling)
    - [3.8 Notification System](#38-notification-system)
    - [3.9 Reporting and Visibility](#39-reporting-and-visibility)
    - [3.10 Activity Lifecycle and Status Management](#310-activity-lifecycle-and-status-management)
    - [3.11 Asset Management](#311-asset-management)
  - [4. Non-Functional Requirements](#4-non-functional-requirements)
    - [4.1 Performance](#41-performance)
    - [4.2 Scalability](#42-scalability)
    - [4.3 Security](#43-security)
    - [4.4 Usability and Accessibility](#44-usability-and-accessibility)
    - [4.5 Availability and Reliability](#45-availability-and-reliability)
    - [4.6 Maintainability](#46-maintainability)
    - [4.7 Portability and Cross-Platform Support](#47-portability-and-cross-platform-support)
    - [4.8 Extensibility and Future-Proofing](#48-extensibility-and-future-proofing)
    - [4.9 Compliance and Data Privacy](#49-compliance-and-data-privacy)
  - [5. Technical Requirements](#5-technical-requirements)
    - [5.1 Architecture](#51-architecture)
    - [5.2 Cross-Platform Application](#52-cross-platform-application)
    - [5.3 Authentication and Identity](#53-authentication-and-identity)
    - [5.4 Data Storage and Persistence](#54-data-storage-and-persistence)
    - [5.5 File and Media Handling](#55-file-and-media-handling)
    - [5.6 API Design and Integration](#56-api-design-and-integration)
    - [5.7 Notification Infrastructure](#57-notification-infrastructure)
    - [5.8 Multi-Tenancy](#58-multi-tenancy)
    - [5.9 DevOps and Deployment](#59-devops-and-deployment)
  - [6. Use Cases](#6-use-cases)
    - [UC-001: Client Reports an Incident](#uc-001-client-reports-an-incident)
    - [UC-002: Technician Resolves an Incident](#uc-002-technician-resolves-an-incident)
    - [UC-003: Technician Creates a Service Record](#uc-003-technician-creates-a-service-record)
    - [UC-004: Technician Completes a Scheduled Service](#uc-004-technician-completes-a-scheduled-service)
    - [UC-005: Client Views Service Calendar](#uc-005-client-views-service-calendar)
    - [UC-006: Employee Views Pending Incidents Dashboard](#uc-006-employee-views-pending-incidents-dashboard)
    - [UC-007: User Authenticates into the System](#uc-007-user-authenticates-into-the-system)
    - [UC-008: Administrator Invites a New Client](#uc-008-administrator-invites-a-new-client)
    - [UC-009: Client Completes First-Time Registration](#uc-009-client-completes-first-time-registration)
    - [UC-010: Client Requests Account Recovery](#uc-010-client-requests-account-recovery)
    - [UC-011: Administrator Manages User Accounts](#uc-011-administrator-manages-user-accounts)
    - [UC-012: Employee Adds an Invoice to a Charge](#uc-012-employee-adds-an-invoice-to-a-charge)
    - [UC-013: Client Views Invoices](#uc-013-client-views-invoices)
    - [UC-014: Administrator Updates Incident Priority](#uc-014-administrator-updates-incident-priority)
    - [UC-015: System Issues a Service Due-Date Notification](#uc-015-system-issues-a-service-due-date-notification)
    - [UC-016: Client Requests an Early Service Appointment](#uc-016-client-requests-an-early-service-appointment)
  - [Appendix A — Requirement Traceability Matrix](#appendix-a--requirement-traceability-matrix)
  - [Appendix B — Glossary of Priority Levels](#appendix-b--glossary-of-priority-levels)
  - [Appendix C — Revision History](#appendix-c--revision-history)

---

## 1. Introduction

### 1.1 Purpose

This document constitutes the Software Requirements Specification (SRS) for the **Computerized Maintenance Management System (CMMS)**, a cloud-based, multi-tenant Software-as-a-Service (SaaS) platform designed to enable small companies to manage preventive maintenance services, corrective incidents, workforce coordination, and client communications without requiring significant technical infrastructure or operational overhead.

The purpose of this SRS is to formally define, in a complete and unambiguous manner, the functional, non-functional, and technical requirements that govern the design, development, testing, and delivery of the CMMS platform. This document serves as the primary contractual and architectural reference between stakeholders, product management, and the engineering team throughout the software development lifecycle.

### 1.2 Scope

The system described herein is the **CMMS SaaS Platform**, hereafter referred to as "the System" or "the Platform." The Platform encompasses:

- A **cross-platform client application** (desktop and mobile) as the primary interface for all user roles.
- A companion **web application** providing equivalent functionality through a modern browser.
- A **backend composed of loosely coupled microservices** responsible for identity, service management, incident tracking, invoicing, notifications, and data persistence.
- An **API Gateway** acting as a unified, secure entry point for all client-facing communications.

The scope of this version (v1.0) covers the initial production-ready release, which includes the three primary actor roles (Company Administrator, Technician, and Client), credential-based authentication, service and incident lifecycle management, invoice handling, calendar views, and notification of approaching service due dates.

The following capabilities are **explicitly outside the scope of v1.0** but are architecturally anticipated for future releases:

- Automatic priority escalation based on elapsed time.
- Two-Factor Authentication (2FA) via Time-based One-Time Passwords (TOTP).
- OAuth2 / OpenID Connect and Active Directory integration for administrator login.
- Digital document signing for PDF invoices.
- Additional employee categories and extended client tiers.
- Automatic priority assignment for incidents via business rules or AI.

### 1.3 Definitions, Acronyms, and Abbreviations

| Term | Definition |
|---|---|
| **CMMS** | Computerized Maintenance Management System |
| **SaaS** | Software as a Service — a software licensing model in which the software is centrally hosted and licensed on a subscription basis |
| **Tenant** | A company or organisation registered in the Platform that uses the service; each tenant's data is logically isolated from all others |
| **Administrator** | A user with the highest-privilege role within a tenant; may also act as a Technician |
| **Technician** | An employee user responsible for executing and recording service work and resolving incidents |
| **Client** | An end-user of the tenant company who submits incidents and views service and invoice information |
| **Service** | A scheduled or completed maintenance task assigned to an item or asset owned by a client |
| **Incident** | An unplanned problem reported by a client or employee, requiring corrective action |
| **Resolution** | The structured record documenting how a Service or Incident was addressed |
| **Invoice** | A financial document (PDF or image) attached to a Service or Incident resolution, detailing charges |
| **API** | Application Programming Interface |
| **API Gateway** | A service that acts as a single entry point for requests from clients to backend microservices |
| **JWT** | JSON Web Token — a compact, URL-safe token used for authentication and authorization |
| **OAuth2** | An open standard for access delegation, commonly used for token-based authentication |
| **OIDC** | OpenID Connect — an identity layer built on top of the OAuth2 protocol |
| **LDAP** | Lightweight Directory Access Protocol |
| **AD** | Active Directory — Microsoft's directory service for identity and access management |
| **TOTP** | Time-based One-Time Password — a form of 2FA defined in RFC 6238 |
| **2FA** | Two-Factor Authentication |
| **RBAC** | Role-Based Access Control |
| **SRS** | Software Requirements Specification |
| **RPO** | Recovery Point Objective — maximum acceptable period of data loss |
| **RTO** | Recovery Time Objective — maximum acceptable downtime after a failure |
| **CI/CD** | Continuous Integration / Continuous Delivery |
| **TLS** | Transport Layer Security |
| **OWASP** | Open Web Application Security Project |
| **FR** | Functional Requirement |
| **NFR** | Non-Functional Requirement |
| **TR** | Technical Requirement |
| **UC** | Use Case |
| **Asset** | A physical item, piece of equipment, or installation for which maintenance activities (Services and Incidents) are tracked within a tenant |
| **ActivityStatusTransition** | An immutable record of a single operational-status change on a ManagementActivity; an ordered sequence of these records forms the complete lifecycle history of an activity |
| **ActivityStatus** | The operational state of a ManagementActivity at a given point in time (e.g., SCHEDULED, IN_PROGRESS, AWAITING_PARTS, COMPLETED) |
| **FileAsset** | A reference to a binary file (image or document) stored externally; may be attached directly to a ManagementActivity, to a Resolution, or to an Invoice |

### 1.4 Document Conventions

- **Requirement identifiers** follow the format `FR-XXX`, `NFR-XXX`, and `TR-XXX`, where `XXX` is a three-digit zero-padded integer.
- **Use case identifiers** follow the format `UC-XXX`.
- The keyword **shall** denotes a mandatory requirement.
- The keyword **should** denotes a recommended but non-mandatory requirement.
- The keyword **may** denotes an optional or aspirational requirement.
- Requirements marked with *(Future)* are out of scope for v1.0 but are included to document architectural intent and ensure the system is designed for extensibility.
- All dates and timestamps in the system shall conform to ISO 8601 (UTC).

---

## 2. System Overview

### 2.1 Product Perspective

The CMMS Platform is a greenfield SaaS product positioned to serve small and medium-sized enterprises (SMEs) operating in service-oriented industries — including, but not limited to, facilities management, equipment maintenance, building services, and technical support operations. The Platform is intended to replace fragmented, manual, or spreadsheet-based maintenance tracking workflows with a centralised, role-aware, and mobile-accessible solution.

The Platform is not an enterprise resource planning (ERP) system and does not aspire to replace accounting, HR, or asset management suites. Its primary domain is the **maintenance service lifecycle**: from the scheduling of recurring services and the reporting of client incidents, through to resolution, documentation, invoicing, and archival.

Ease of onboarding is a first-class design principle. A company administrator should be able to register a new tenant, configure roles, invite clients, and have the system operational within a single working session, without requiring IT consultancy, database administration, or server provisioning.

### 2.2 Deployment Model and SaaS Context

The Platform shall be operated under a **multi-tenant SaaS model**, whereby a single deployment of the backend infrastructure serves multiple independent tenants. Tenants are logically isolated; no tenant shall have any visibility into, or access to, data belonging to another tenant.

The Platform shall be offered as a hosted service managed by the Platform operator. Tenants subscribe to the service and interact with it exclusively through the provided client application and web application. Tenants do not manage their own infrastructure.

### 2.3 System Actors

The initial version of the Platform recognises three primary actor roles. The role model is designed to be extended in future versions.

#### 2.3.1 Company Administrator

The Company Administrator (hereafter "Administrator") is the most privileged role within a tenant. The Administrator is responsible for the overall configuration and oversight of the tenant's operations within the Platform. An Administrator may simultaneously hold the Technician role. Capabilities exclusive to this role include user management, permission configuration, incident priority management, and account recovery approval. At least one Administrator must always exist within a tenant.

#### 2.3.2 Technician

The Technician is an employee user responsible for the operational execution of maintenance services and the resolution of client-reported incidents. Technicians create, document, and close service records and incident records. They attach resolution reports, images, and invoices to completed work. A Technician may be elevated to also hold the Administrator role; however, a Technician can never hold the Client role within the same tenant.

#### 2.3.3 Client

The Client is an external-facing user representing the company's customer. Clients interact with the Platform to report incidents, provide supplementary information (descriptions, images), view their service calendar, track the status of their incidents, and access their invoices. Clients cannot self-register; they are exclusively onboarded via an invitation mechanism initiated by an Administrator. A Client can never hold an employee role (Technician or Administrator) within the same tenant.

### 2.4 Key Entities and Relationships

The following summarises the core domain entities of the System and their principal relationships.

```
Tenant
  ├── Users (Administrator, Technician, Client)
  │
  ├── Assets
  │     ├── Name
  │     ├── Description
  │     ├── Category / Type
  │     ├── Serial Number / External Reference
  │     ├── Installation Date
  │     └── Associated Client
  │
  ├── Services  [ManagementActivity]
  │     ├── Title
  │     ├── Description
  │     ├── Service Date (actual)
  │     ├── Next Service Date (scheduled)
  │     ├── Technical Notes
  │     ├── Asset Reference (optional)
  │     ├── File Assets (images or documents attached at any lifecycle point, optional)
  │     ├── Status Transitions  [ActivityStatusTransition history]
  │     │     └── Status (SCHEDULED | IN_PROGRESS | AWAITING_PARTS | COMPLETED | CANCELLED)
  │     │           Timestamp, Actor, Notes
  │     └── Resolution
  │           ├── Resolution Date
  │           ├── Technician Reference
  │           ├── Description of work done
  │           ├── Images (optional)
  │           ├── Price Charged
  │           └── Discount (optional)
  │
  ├── Incidents  [ManagementActivity]
  │     ├── Title
  │     ├── Priority
  │     ├── Report Date
  │     ├── Description
  │     ├── Asset Reference (optional)
  │     ├── File Assets (images or documents attached at any lifecycle point, optional)
  │     ├── Status Transitions  [ActivityStatusTransition history]
  │     │     └── Status (OPEN | IN_PROGRESS | AWAITING_PARTS | CLOSED)
  │     │           Timestamp, Actor, Notes
  │     └── Resolution
  │           ├── Resolution Date
  │           ├── Resolution Outcome (Resolved / Pending Parts / Unable to Resolve)
  │           ├── Technician Reference
  │           ├── Description of work done
  │           ├── Images (optional)
  │           ├── Price Charged
  │           └── Discount (optional)
  │
  └── Invoices
        ├── Associated Resolution (Service or Incident)
        ├── Document (PDF or Image)
        └── Metadata (date, amount, discount)
```

### 2.5 Assumptions and Dependencies

- **A1:** The Platform operator provides and maintains the cloud infrastructure (compute, storage, networking) required to host the backend services.
- **A2:** Tenants have access to a reliable internet connection for using the application, as the Platform is cloud-hosted.
- **A3:** End-user devices (desktop, mobile) satisfy the minimum operating system versions supported by the chosen cross-platform framework.
- **A4:** Email delivery infrastructure (SMTP or transactional email provider) is available and configured for invitation and notification workflows.
- **A5:** In v1.0, all authentication is performed via the Platform's own credential store; integration with external identity providers (OAuth2, LDAP/AD) is deferred.
- **A6:** Incident priority is a single configurable attribute managed manually; automated escalation is deferred.

### 2.6 Constraints

- **C1:** The initial release must operate with no requirement for the tenant to manage or provision any server infrastructure.
- **C2:** The system must be operable by non-technical company administrators; no command-line tools or manual configuration files shall be required for day-to-day operation.
- **C3:** All personal data handling must be compliant with applicable data protection regulations (e.g., GDPR for European tenants).
- **C4:** The architecture must not introduce vendor lock-in to a degree that would prevent migration between cloud providers in the future.

---

## 3. Functional Requirements

### 3.1 User Management and Authentication

| ID | Requirement |
|---|---|
| **FR-001** | The System shall support credential-based authentication (email address and password) as the primary login method for all user roles in v1.0. |
| **FR-002** | The System shall support OAuth2 / OpenID Connect authentication as an additional login method for Administrator accounts. *(Future — architecture must support it from v1.0)* |
| **FR-003** | The System shall support Active Directory (LDAP) authentication as an additional login method for Administrator accounts. *(Future — architecture must support it from v1.0)* |
| **FR-004** | The System shall be architected to support Two-Factor Authentication (2FA) via Time-based One-Time Passwords (TOTP) as an additional security layer for all roles. *(Future — architecture must support it from v1.0)* |
| **FR-005** | Upon credential-based login, the System shall issue a session token (JWT) to the authenticating user, valid for a configurable duration. |
| **FR-006** | The System shall allow authenticated users to explicitly log out, invalidating their active session token. |
| **FR-007** | The System shall enforce configurable password policies, including minimum length and complexity rules, at the time of password creation and change. |
| **FR-008** | The System shall provide a self-service password reset flow for employees (Administrator and Technician) via an email-based verification link. |

### 3.2 Client Onboarding and Account Management

| ID | Requirement |
|---|---|
| **FR-009** | Clients shall not be able to self-register on the Platform. Client accounts may only be created through an invitation process initiated by an Administrator. |
| **FR-010** | The System shall generate a unique, time-limited invitation link upon Administrator request, which is delivered to the client's email address. |
| **FR-011** | Upon first accessing the invitation link, the client shall be required to complete a registration flow in which they create their credentials (password) before gaining access to the application. |
| **FR-012** | Following successful first-time registration, the client shall be granted access to the application using their established credentials on all subsequent sessions. |
| **FR-013** | The System shall provide a client account recovery option, whereby a client may request access restoration. This request shall require explicit approval from a tenant Administrator before access is re-enabled. |
| **FR-014** | The System shall notify the Administrator of a pending client account recovery request, awaiting their approval or rejection. |
| **FR-015** | Invitation links shall expire after a configurable period; the Administrator shall be able to reissue a new invitation link for a given client if the original has expired. |

### 3.3 Role and Permission Management

| ID | Requirement |
|---|---|
| **FR-016** | The System shall implement Role-Based Access Control (RBAC), where access to system functions and data is governed by the role(s) assigned to a user. |
| **FR-017** | The System shall define three initial roles: Administrator, Technician, and Client. |
| **FR-018** | An Administrator may simultaneously be assigned the Technician role, thereby inheriting all Technician capabilities in addition to their own. |
| **FR-019** | A Technician may be elevated to hold the Administrator role at the discretion of an existing Administrator. |
| **FR-020** | An employee user (a user holding either the Administrator or Technician role) shall never hold the Client role within the same tenant, and vice versa. |
| **FR-021** | At least one user with the Administrator role must always exist within a tenant. The System shall prevent the demotion or deletion of the last Administrator in a tenant. |
| **FR-022** | Administrators shall be able to view a list of all users registered within their tenant, including their assigned roles and account status. |
| **FR-023** | Administrators shall be able to modify the roles and permissions of any user within their tenant, subject to the constraint in FR-021. |
| **FR-024** | Administrators shall be able to deactivate user accounts. Deactivated users shall not be able to authenticate or access the System. |
| **FR-025** | Administrators shall be able to reactivate previously deactivated user accounts. |
| **FR-026** | The role model shall be architecturally designed to support additional role definitions in future versions of the Platform, without requiring structural redesign. |

### 3.4 Service Management

| ID | Requirement |
|---|---|
| **FR-027** | Technicians and Administrators shall be able to create Service records within the System. Clients shall not have the ability to create Service records. |
| **FR-028** | A Service record shall contain the following mandatory fields: (a) Title; (b) Description of the maintenance work to be performed; (c) Date of actual service execution; (d) Date of the next scheduled service; (e) A free-text area for technical notes, difficulties, or observations encountered during the service. |
| **FR-029** | A Service record shall be associated with a specific client within the tenant. |
| **FR-030** | Upon completing a service, the responsible Technician shall record a Resolution against the Service record. |
| **FR-031** | A Service Resolution shall contain the following fields: (a) Resolution date (mandatory); (b) Technician reference (the identity of the resolving Technician, mandatory); (c) Brief description of the work performed (mandatory); (d) Optional photographic evidence (one or more images); (e) Price charged for the service (mandatory); (f) Discount applied, if any (optional). |
| **FR-032** | Clients shall be able to request that a service be performed before the scheduled next service date. Such requests shall be visible to Technicians and Administrators and shall not automatically create or modify a Service record; a Technician must create the Service record. |
| **FR-033** | Technicians and Administrators shall be able to edit the fields of a Service record prior to its resolution. |
| **FR-034** | Technicians and Administrators shall be able to view all Service records within their tenant. |
| **FR-035** | Clients shall be able to view Service records associated with their own account. |
| **FR-036** | The resolution status categories for a Service shall be extensible in future versions to support additional resolution outcomes beyond the initial set. |
| **FR-073** | Technicians and Administrators shall be able to attach file assets (images or documents) directly to a Service record at any point in its lifecycle, independently of any files attached within a Resolution record. |

### 3.5 Incident Management

| ID | Requirement |
|---|---|
| **FR-037** | Clients shall be able to create Incident records to report problems or unplanned failures requiring attention. |
| **FR-038** | Technicians and Administrators shall also be able to create Incident records on behalf of a client. |
| **FR-039** | An Incident record shall contain the following fields: (a) Title (mandatory); (b) Priority level (mandatory, assigned to the system-defined default priority upon creation in v1.0); (c) Incident report date (mandatory, automatically set to the date and time of submission); (d) Description of the problem (mandatory); (e) Optional file assets (images) submitted by the reporting party (Client or employee) at the time of initial submission. |
| **FR-040** | Incident priority shall be a configurable attribute. In v1.0, all newly created incidents shall be assigned a system-defined default priority value. |
| **FR-041** | Administrators shall be able to manually update the priority of any Incident at any time. |
| **FR-042** | The System shall be designed to support automated priority escalation based on the time elapsed since incident creation and the initial priority value, as a future capability. *(Future)* |
| **FR-043** | Upon addressing an Incident, the responsible Technician shall record a Resolution against the Incident record. |
| **FR-044** | An Incident Resolution shall contain the following fields: (a) Resolution date (mandatory); (b) Resolution outcome status, which shall be one of: *Resolved*, *Pending Parts*, or *Unable to Resolve* (mandatory). This status captures the formal closure outcome and is distinct from the operational status transitions tracked via ActivityStatusTransition (see Section 3.10); (c) Technician reference (mandatory); (d) Brief description of the corrective action taken (mandatory); (e) Optional photographic evidence (one or more images); (f) Price charged for the service (mandatory for "Resolved" status; optional for others); (g) Discount applied, if any (optional). |
| **FR-045** | An Incident record shall record two distinct dates: the date the incident was reported (set automatically at creation) and the date the incident was resolved (set at resolution time). |
| **FR-046** | Unresolved incidents shall not have a resolution date. |
| **FR-047** | Clients shall be able to view Incident records associated with their own account, including the status of their resolution. |
| **FR-048** | Technicians and Administrators shall be able to view all Incident records within their tenant. |
| **FR-049** | The resolution status categories for an Incident shall be extensible in future versions without requiring structural changes to the data model. |
| **FR-074** | After creation, Clients, Technicians, and Administrators shall be able to attach additional file assets (images or documents) to an open or in-progress Incident record at any point prior to its final closure, independently of any files attached within a Resolution record. |

### 3.6 Invoice Management

| ID | Requirement |
|---|---|
| **FR-050** | Technicians and Administrators shall be able to attach one or more invoice documents to the Resolution of a Service or an Incident. |
| **FR-051** | An invoice document shall be accepted in one of the following formats: (a) A PDF file; (b) An image file (JPEG, PNG) representing a photographed printed invoice. |
| **FR-052** | PDF invoices shall be the preferred format and the System shall be designed to support future integration of digital signature verification and generation for PDF documents. *(Future for signing)* |
| **FR-053** | Each invoice shall be associated with the following metadata: (a) The associated entity (Service or Incident); (b) The date of issuance; (c) The total amount charged; (d) Any discount applied. |
| **FR-054** | Clients shall be able to view and download all invoices associated with their own Service and Incident records. |
| **FR-055** | Employees (Technicians and Administrators) shall be able to view and download all invoices within their tenant. |
| **FR-056** | The System shall not expose invoice documents of one client to another client, even within the same tenant. |

### 3.7 Calendar and Scheduling

| ID | Requirement |
|---|---|
| **FR-057** | The System shall provide a calendar view for Clients displaying: (a) Upcoming scheduled services (next service date in the future); (b) Overdue services (next service date in the past without a completed service record). |
| **FR-058** | The System shall provide a calendar view for Technicians and Administrators displaying all pending (scheduled and unresolved) services within their tenant. |
| **FR-059** | The calendar view shall clearly distinguish between upcoming, overdue, and completed service entries. |
| **FR-060** | The calendar view for Clients shall be filtered to display only services associated with the logged-in client. |
| **FR-061** | The calendar shall allow navigation between months and display individual service entries on their scheduled dates. |

### 3.8 Notification System

| ID | Requirement |
|---|---|
| **FR-062** | The System shall monitor the scheduled next service date of all active Service records within all tenants. |
| **FR-063** | When a service is approaching its scheduled next service date within a configurable advance notice period (e.g., a defined number of days before the due date), the System shall generate a notification for the responsible Technicians and Administrators of that tenant. |
| **FR-064** | The notification shall convey that the service is due and prompt the recipient to contact the relevant client to arrange an appointment. |
| **FR-065** | Notifications shall be delivered within the application (in-app notification) as a minimum delivery channel. |
| **FR-066** | The notification delivery infrastructure shall be architected to support additional delivery channels (e.g., email, push notification, SMS) in future versions. |
| **FR-067** | The advance notice period for service due-date notifications shall be configurable at the tenant level by the Administrator. |
| **FR-075** | The System shall maintain a persistent, immutable audit log of all notifications dispatched, recording for each entry: (a) Notification type and subject; (b) Recipient user(s); (c) Delivery channel(s) used; (d) Timestamp of dispatch; (e) Delivery status per channel (delivered, failed, or pending); (f) The domain event or triggering action that caused the notification to be issued. |
| **FR-076** | Administrators shall be able to query the notification dispatch audit log for their tenant, with filtering by date range, notification type, recipient, and delivery status. |
| **FR-077** | Notification audit log entries shall be retained for a minimum configurable period (default: 12 months) and shall not be editable or deletable by any user role. |

### 3.9 Reporting and Visibility

| ID | Requirement |
|---|---|
| **FR-068** | The System shall provide Technicians and Administrators with a dedicated screen displaying all pending (unresolved) Incident records within their tenant, ordered by priority (highest priority first). |
| **FR-069** | Within the same priority level, pending incidents shall be further ordered by report date (oldest first) as a secondary sort key. |
| **FR-070** | The System shall provide Technicians and Administrators with a dedicated screen displaying all resolved Incident records within their tenant, ordered by resolution date (most recently resolved first). |
| **FR-071** | Each incident entry in the pending and resolved screens shall display, at minimum: title, priority, report date, associated client, and (for resolved) resolution date and status. |
| **FR-072** | Administrators shall be able to filter the incident lists by client, priority, status, and date range. |

### 3.10 Activity Lifecycle and Status Management

| ID | Requirement |
|---|---|
| **FR-078** | The System shall track the complete operational status lifecycle of every ManagementActivity (Service and Incident) through an ordered, append-only sequence of ActivityStatusTransition records. |
| **FR-079** | Each ActivityStatusTransition record shall contain: (a) The new operational status value (mandatory); (b) Timestamp of the transition, automatically set to the recording time (mandatory); (c) Identity of the actor recording the transition (mandatory); (d) Optional free-text notes explaining the reason for the transition. |
| **FR-080** | The operational status lifecycle for a Service shall support the following statuses: (a) *SCHEDULED* — initial status set automatically upon creation; (b) *IN_PROGRESS* — a Technician has commenced work; (c) *AWAITING_PARTS* — work is blocked pending availability of a required material or component; (d) *COMPLETED* — work finished and formally closed through a ServiceResolution record. A Service shall only enter *COMPLETED* status when a ServiceResolution has been recorded; (e) *CANCELLED* — the service was cancelled without completion. |
| **FR-081** | The operational status lifecycle for an Incident shall support the following statuses: (a) *OPEN* — initial status set automatically upon creation; (b) *IN_PROGRESS* — a Technician has begun addressing the incident; (c) *AWAITING_PARTS* — work is blocked pending availability of a required material or component; (d) *CLOSED* — final status, applied automatically when an IncidentResolution is recorded regardless of resolution outcome. The specific closure outcome (Resolved, Pending Parts, or Unable to Resolve) is captured in the IncidentResolution record; the *CLOSED* operational status signals that no further transitions are expected. |
| **FR-082** | Technicians and Administrators shall be able to record a new ActivityStatusTransition on a Service or Incident at any point until the activity reaches its terminal status (*COMPLETED* or *CANCELLED* for Services; *CLOSED* for Incidents). |
| **FR-083** | The complete ActivityStatusTransition history for a Service or Incident shall be visible to all authorised users (Technicians, Administrators, and the associated Client) on the activity detail view, presented as a chronological timeline. |
| **FR-084** | The operational status values for Services and Incidents shall be stored in a configurable manner (e.g., database-driven enumeration), allowing the addition of new intermediate status values at the tenant or platform level without requiring code deployment. |

### 3.11 Asset Management

| ID | Requirement |
|---|---|
| **FR-085** | Technicians and Administrators shall be able to create, view, edit, and deactivate Asset records within the tenant. An Asset represents a physical item, piece of equipment, or installation against which maintenance activities are tracked. |
| **FR-086** | An Asset record shall contain the following fields: (a) Name (mandatory); (b) Description (optional); (c) Asset category or type (optional); (d) Serial number or external reference (optional); (e) Installation or commissioning date (optional); (f) Associated Client (mandatory — each asset belongs to a specific client within the tenant). |
| **FR-087** | A Service record may optionally reference an Asset, indicating which physical item the service was performed on or scheduled for. |
| **FR-088** | An Incident record may optionally reference an Asset, indicating which physical item the incident concerns. |
| **FR-089** | The System shall provide an Asset detail view listing all Service and Incident records associated with a given Asset, in reverse chronological order, forming a complete maintenance and fault history for that asset. |
| **FR-090** | Clients shall be able to view Asset records and their associated maintenance history for assets linked to their own account. |

---

## 4. Non-Functional Requirements

### 4.1 Performance

| ID | Requirement |
|---|---|
| **NFR-001** | The System shall respond to standard user interface interactions (page loads, list fetches, record creation) within **2 seconds** under normal operating load, measured at the API Gateway. |
| **NFR-002** | File upload operations (images, PDFs) shall complete within **10 seconds** for files up to the defined maximum size under normal network conditions. |
| **NFR-003** | The System shall sustain the expected concurrent user load without degradation in response time, as validated by load testing prior to production release. |
| **NFR-004** | Background processes (e.g., due-date monitoring, notification dispatch) shall not negatively impact the responsiveness of user-facing API calls. |

### 4.2 Scalability

| ID | Requirement |
|---|---|
| **NFR-005** | The System shall support **horizontal scaling** of individual microservices to accommodate growth in tenant count, user volume, and data size, without requiring architectural changes. |
| **NFR-006** | The database layer shall be designed to support read replicas and sharding strategies to accommodate growing data volumes in future. |
| **NFR-007** | The System shall be capable of onboarding new tenants without changes to the deployed codebase or infrastructure topology. |
| **NFR-008** | File storage shall leverage a scalable object storage service capable of storing unlimited volumes of image and document assets. |

### 4.3 Security

| ID | Requirement |
|---|---|
| **NFR-009** | All data in transit between clients and the Platform shall be encrypted using **TLS 1.2 or higher**. Unencrypted HTTP connections shall be rejected or redirected. |
| **NFR-010** | All data at rest (databases, file storage) shall be encrypted using industry-standard encryption algorithms. |
| **NFR-011** | User passwords shall never be stored in plaintext. They shall be hashed using a memory-hard, cryptographically suitable algorithm (e.g., **Argon2id** or **bcrypt** with an appropriate work factor). |
| **NFR-012** | The System shall implement protection against the **OWASP Top 10** web application security risks, including but not limited to injection attacks, broken authentication, cross-site scripting (XSS), and insecure direct object references (IDOR). |
| **NFR-013** | Access control shall be enforced at the **API level** on every request, irrespective of client-side role checks. No resource shall be accessible without proper authorisation validation at the backend. |
| **NFR-014** | JWT session tokens shall have a configurable expiry period. The System shall support token revocation via a deny-list or token rotation mechanism. |
| **NFR-015** | Invitation links and account recovery links shall be time-limited, single-use, and cryptographically unguessable. |
| **NFR-016** | Multi-tenant data isolation shall be enforced at both the application and database layers. A request originating from one tenant shall never be able to access data belonging to another tenant, regardless of the resource identifier used. |
| **NFR-017** | All security-relevant events (authentication attempts, authorisation failures, administrative actions) shall be recorded in an immutable audit log. |
| **NFR-018** | The System shall implement rate limiting on authentication endpoints to mitigate brute-force and credential-stuffing attacks. |

### 4.4 Usability and Accessibility

| ID | Requirement |
|---|---|
| **NFR-019** | The System shall provide an intuitive user interface operable by non-technical users (Clients and Technicians) without requiring product training beyond a brief onboarding guide. |
| **NFR-020** | A new Administrator shall be able to configure their tenant, create employee accounts, and invite at least one client within **one working session** without requiring external technical assistance. |
| **NFR-021** | Error messages presented to the user shall be descriptive, clearly indicating what went wrong and, where possible, providing actionable guidance for resolution. Internal stack traces or system errors shall not be exposed to end users. |
| **NFR-022** | The application shall conform to **WCAG 2.1 Level AA** accessibility guidelines for colour contrast, keyboard navigation, and screen reader support where technically feasible within the chosen framework. |
| **NFR-023** | The user interface shall support **internationalisation (i18n)** from the outset, allowing the addition of new language translations without code changes. |

### 4.5 Availability and Reliability

| ID | Requirement |
|---|---|
| **NFR-024** | The Platform shall target a minimum uptime of **99.9%** (equivalent to approximately 8.7 hours of downtime per year), measured on a rolling monthly basis. |
| **NFR-025** | The System shall implement graceful degradation; where an individual microservice is temporarily unavailable, the impact on unrelated features shall be minimised and users shall receive informative status feedback. |
| **NFR-026** | The System shall implement automated health checks for all services, with alerting to the operations team upon detection of service failure or degradation. |
| **NFR-027** | The System shall define and meet a **Recovery Point Objective (RPO)** of no more than **24 hours** and a **Recovery Time Objective (RTO)** of no more than **4 hours** in the event of a critical service failure. |

### 4.6 Maintainability

| ID | Requirement |
|---|---|
| **NFR-028** | All source code shall adhere to documented coding standards and style guides appropriate to each technology used. Code review shall be a mandatory step in the development workflow. |
| **NFR-029** | Each microservice shall be independently deployable; deploying an update to one service shall not require downtime or redeployment of other services. |
| **NFR-030** | All public APIs shall be versioned to allow backward-compatible changes and to provide a deprecation path for breaking changes. |
| **NFR-031** | The System shall maintain a **minimum test coverage threshold** of 80% (unit and integration tests combined) for all critical business logic components. |
| **NFR-032** | The System shall produce structured logs in a machine-readable format (e.g., JSON), suitable for ingestion into a centralised log aggregation and monitoring platform. |

### 4.7 Portability and Cross-Platform Support

| ID | Requirement |
|---|---|
| **NFR-033** | The primary client application shall operate natively on the following platforms: **Windows**, **macOS**, **Linux**, **iOS**, and **Android**. |
| **NFR-034** | A **web application** providing equivalent functionality shall be accessible from all major modern browsers (Chrome, Firefox, Safari, Edge) without the installation of additional plugins or extensions. |
| **NFR-035** | The user interface shall be **responsive**, adapting appropriately to different screen sizes, from smartphone displays (minimum 360px width) to desktop screens. |
| **NFR-036** | The Platform backend shall be deployable on any major cloud provider (AWS, Azure, GCP) or on-premise infrastructure using standard containerisation tooling, without modification to the application code. |

### 4.8 Extensibility and Future-Proofing

| ID | Requirement |
|---|---|
| **NFR-037** | The role and permission model shall be designed such that new roles (both employee and client categories) can be added through configuration and data changes, without requiring structural code modifications to the authorisation layer. |
| **NFR-038** | The incident and service resolution status enumeration, and the operational activity status values used by ActivityStatusTransition, shall be stored in a configurable manner (e.g., database-driven) to allow the addition of new categories without requiring code deployments. |
| **NFR-039** | The authentication service shall expose a plugin or adapter interface to allow the integration of additional identity providers (OAuth2 providers, LDAP/AD, TOTP) without modifying the core authentication flow. |
| **NFR-040** | The notification service shall be designed with a channel abstraction layer, enabling the addition of new delivery channels (email, SMS, push) by implementing a defined interface, without modifying existing channel logic. |
| **NFR-041** | The invoice handling module shall be architected to allow the future integration of a document signing service (e.g., a PKI-based PDF signing service) without requiring changes to the invoice storage or retrieval logic. |

### 4.9 Compliance and Data Privacy

| ID | Requirement |
|---|---|
| **NFR-042** | The System shall comply with applicable data protection legislation, including the **General Data Protection Regulation (GDPR)** for tenants operating within the European Economic Area, as a minimum baseline. |
| **NFR-043** | The System shall support the right to erasure ("right to be forgotten") by providing a mechanism to permanently delete a user's personal data upon a validated request, subject to any legal retention obligations. |
| **NFR-044** | Personal data shall be processed and stored only to the extent necessary for the provision of the service (data minimisation principle). |
| **NFR-045** | The System shall maintain an audit trail of data access and modification events for personal data, sufficient to support data breach investigation and regulatory reporting. |

---

## 5. Technical Requirements

### 5.1 Architecture

| ID | Requirement |
|---|---|
| **TR-001** | The backend of the System shall be built upon a **microservice architecture**, with each service encapsulating a distinct bounded domain context (e.g., Identity, Services, Incidents, Invoicing, Notifications, Calendar). |
| **TR-002** | Microservices shall communicate with each other via two defined patterns: **synchronous REST over HTTPS** for request/response interactions, and **asynchronous message passing** (via a message broker) for event-driven interactions (e.g., notifications triggered by state changes). |
| **TR-003** | An **API Gateway** shall be deployed as the single, externally accessible entry point for all client applications. The API Gateway shall be responsible for request routing, authentication token validation, rate limiting, and TLS termination. |
| **TR-004** | Each microservice shall own and encapsulate its own data store (**database-per-service pattern**). Direct database access between services is prohibited; all cross-service data access shall occur through defined service APIs or events. |
| **TR-005** | All services shall be packaged as **Docker container images** and shall declare their dependencies through a container specification. |
| **TR-006** | The deployment configuration shall support orchestration via **Kubernetes** or an equivalent container orchestration platform for production environments. |
| **TR-007** | A **service discovery mechanism** shall be in place to allow microservices and the API Gateway to locate each other without hardcoded network addresses. |

### 5.2 Cross-Platform Application

| ID | Requirement |
|---|---|
| **TR-008** | The client application shall be developed using a **cross-platform framework** that supports native or near-native compilation for desktop (Windows, macOS, Linux) and mobile (iOS, Android) from a single shared codebase. Recommended frameworks include Flutter or React Native (for mobile-first) or Electron paired with a modern JavaScript framework (for desktop-first). The final framework selection shall be documented in the Technical Design Document. |
| **TR-009** | The web application shall be developed using a **modern JavaScript single-page application (SPA) framework** (e.g., React, Vue, or Angular), sharing business logic and API client code with the cross-platform application where the chosen framework permits. |
| **TR-010** | The application shall implement **offline-aware UI states** where applicable, informing the user when connectivity is unavailable and indicating which operations require connectivity. |
| **TR-011** | Application assets shall be versioned, and the application shall support **over-the-air (OTA) update mechanisms** where the target platform permits, to allow prompt delivery of bug fixes and security patches. |

### 5.3 Authentication and Identity

| ID | Requirement |
|---|---|
| **TR-012** | A dedicated **Identity Service** (microservice) shall be responsible for all authentication and authorisation logic. No other service shall contain primary authentication logic. |
| **TR-013** | The Identity Service shall implement credential-based authentication using **email address and password**, issuing signed **JWT (JSON Web Tokens)** upon successful authentication. |
| **TR-014** | Issued JWTs shall be **short-lived access tokens** (configurable, e.g., 15–60 minutes) paired with **longer-lived refresh tokens**, following the OAuth2 token refresh pattern. Refresh tokens shall be rotated on each use and stored server-side for revocation capability. |
| **TR-015** | The Identity Service shall be designed with an **adapter/provider pattern** to enable future integration of OAuth2/OIDC providers, LDAP/Active Directory, and TOTP 2FA, without modification to the token issuance or validation logic. |
| **TR-016** | Password hashing shall use **Argon2id** as the preferred algorithm, with fallback to bcrypt (minimum cost factor 12) if Argon2id is not available in the target runtime. |
| **TR-017** | Password reset and account invitation tokens shall be generated using a **cryptographically secure random number generator**, stored as a one-way hash on the server, and shall expire within a configurable period (default: 24 hours for invitations, 1 hour for password resets). |
| **TR-018** | All downstream microservices shall validate the JWT signature and claims on every inbound request, using a shared public key distributed from the Identity Service. |

### 5.4 Data Storage and Persistence

| ID | Requirement |
|---|---|
| **TR-019** | A **relational database** (PostgreSQL 14+ is the recommended choice) shall be used as the primary data store for structured domain data: users, roles, tenants, services, incidents, and invoice metadata. |
| **TR-020** | Each microservice's database shall be managed independently, with schema migrations handled via a version-controlled migration tool (e.g., Flyway or Liquibase). |
| **TR-021** | Binary and large file assets (uploaded images, PDF invoices) shall be stored in an **S3-compatible object storage service** (e.g., AWS S3, MinIO), referenced by URI from the relational database. Object storage buckets shall be configured with access policies restricting direct public access. |
| **TR-022** | All object storage assets shall be served to authorised clients via **pre-signed URLs** with a short validity period, generated on demand by the appropriate service, to prevent unauthorised direct access to stored files. |
| **TR-023** | Database backups shall be performed at minimum **daily**, with backup files stored in a geographically separated location. Backup integrity shall be verified regularly through restoration tests. |
| **TR-024** | Database connections shall be managed through a **connection pool** to optimise resource utilisation under concurrent load. |

### 5.5 File and Media Handling

| ID | Requirement |
|---|---|
| **TR-025** | All file uploads shall be validated server-side for: (a) **MIME type** (accepted types: `image/jpeg`, `image/png`, `application/pdf`); (b) **file size** (maximum configurable limit, default: 20 MB per file); (c) **absence of malicious content** (basic antivirus or hash-based scanning where feasible). |
| **TR-026** | Uploaded images shall be processed server-side to generate **thumbnail variants** for efficient display in list views, reducing bandwidth consumption on mobile clients. |
| **TR-027** | The file upload API shall support **multipart/form-data** uploads and shall respond with a stable asset reference upon successful upload. |
| **TR-028** | The System shall be architected to integrate a **PDF signing service** (e.g., a PKI-based digital signature library or third-party signing API) in the future, without requiring changes to the invoice storage model. *(Architecture requirement for v1.0; signing capability is future)* |

### 5.6 API Design and Integration

| ID | Requirement |
|---|---|
| **TR-029** | All external-facing APIs (exposed through the API Gateway) shall conform to **RESTful design principles** and shall use JSON as the primary data serialisation format. |
| **TR-030** | All APIs shall be fully documented using the **OpenAPI 3.x specification**. API documentation shall be automatically generated from code annotations or a schema-first approach, and shall be kept in synchronisation with the implementation. |
| **TR-031** | APIs shall implement **URL-based versioning** (e.g., `/api/v1/...`) to ensure backward compatibility when introducing breaking changes. |
| **TR-032** | All API responses shall include appropriate **HTTP status codes** and structured error bodies conforming to a defined error schema (e.g., RFC 7807 Problem Details). |
| **TR-033** | The API Gateway shall enforce **request rate limiting** per authenticated user or per tenant to protect backend services from overload and abuse. |

### 5.7 Notification Infrastructure

| ID | Requirement |
|---|---|
| **TR-034** | A dedicated **Notification Service** shall be responsible for all outbound notification logic, decoupled from the domain services that trigger notifications. |
| **TR-035** | Notification events shall be published to a **message broker** (e.g., RabbitMQ or Apache Kafka) by originating domain services, and consumed asynchronously by the Notification Service. |
| **TR-036** | The Notification Service shall implement a **channel abstraction interface** with pluggable channel adapters. The v1.0 implementation shall include an **in-app notification adapter** and an **email adapter**. |
| **TR-037** | The Notification Service shall maintain a persistent record of dispatched notifications and their delivery status, to support retry logic and audit purposes. |
| **TR-038** | A scheduled **background job** (cron-based or event-driven) shall periodically evaluate service due dates and publish notification events to the message broker when services are within the configured advance notice window. |

### 5.8 Multi-Tenancy

| ID | Requirement |
|---|---|
| **TR-039** | The System shall implement a **shared-database, schema-per-tenant** or **shared-schema with tenant discriminator column** multi-tenancy model. The chosen model shall ensure that tenant data is isolated at the query level on every operation. |
| **TR-040** | The **tenant identifier** shall be embedded in the JWT of every authenticated session and validated by the API Gateway and each downstream service on every request. |
| **TR-041** | Object storage assets shall be organised using a **tenant-scoped key prefix** (e.g., `/{tenant_id}/{entity_type}/{entity_id}/{filename}`) to facilitate logical isolation and potential per-tenant storage policies. |
| **TR-042** | Tenant provisioning (onboarding a new company) shall be automated through an administrative API, completing all required setup (database schema initialisation, default role configuration, default priority definition) within a single transactional operation. |

### 5.9 DevOps and Deployment

| ID | Requirement |
|---|---|
| **TR-043** | The System shall support a **CI/CD pipeline** providing: automated unit and integration test execution on every code change; automated build and container image creation; and automated deployment to staging and production environments upon successful test passage. |
| **TR-044** | All environment-specific configuration (database credentials, API keys, feature flags) shall be managed via **environment variables** or a dedicated secrets management service (e.g., HashiCorp Vault, AWS Secrets Manager). No secrets shall be committed to source control. |
| **TR-045** | **Infrastructure-as-Code (IaC)** tooling (e.g., Terraform, Pulumi) shall be used to define and provision all cloud infrastructure resources, ensuring reproducibility and version control of the infrastructure state. |
| **TR-046** | Deployment to production shall use a **blue-green** or **rolling update** strategy to achieve zero-downtime deployments. |
| **TR-047** | A centralised **observability stack** (logging, metrics, distributed tracing) shall be deployed alongside the application services. Recommended tools include the ELK stack or Grafana Loki for logs, Prometheus + Grafana for metrics, and Jaeger or Tempo for tracing. |

---

## 6. Use Cases

> **Format Note:** Each use case follows the standard IEEE 830-derived template. The *Main Flow* represents the happy-path scenario. *Alternative Flows* represent valid deviations. *Exceptions* represent error conditions.

---

### UC-001: Client Reports an Incident

| Field | Detail |
|---|---|
| **Use Case ID** | UC-001 |
| **Title** | Client Reports an Incident |
| **Primary Actor** | Client |
| **Secondary Actors** | Notification Service, Technician (notified) |
| **Related Requirements** | FR-037, FR-038, FR-039, FR-040, FR-065 |
| **Description** | A Client identifies a problem and submits an incident report through the application. |
| **Preconditions** | The Client is authenticated. The Client has an active account within the tenant. |
| **Postconditions** | A new Incident record exists in the system with status "Open" and default priority. The Incident is visible to Technicians and Administrators of the tenant. An in-app notification is dispatched to the tenant's Technicians and Administrators. |

**Main Flow:**
1. The Client navigates to the "Report Incident" section of the application.
2. The System presents a form with fields: Title, Description, and an optional image upload control.
3. The Client enters a title and a description of the problem.
4. (Optional) The Client attaches one or more photographs of the problem.
5. The Client submits the form.
6. The System validates the submitted data (required fields present; file types and sizes valid if images are attached).
7. The System creates an Incident record with: the provided title and description, the current timestamp as the report date, the default system priority, and the client's identity as the reporting party.
8. The System dispatches an in-app notification to all Technicians and Administrators of the tenant, indicating a new incident has been reported.
9. The System displays a confirmation to the Client, showing the newly created Incident record with its assigned identifier.

**Alternative Flows:**
- **AF-001-A (No images):** The Client does not attach any images (step 4 is skipped). The Incident is created without image attachments; all other steps proceed normally.
- **AF-001-B (Employee reports on behalf of client):** A Technician or Administrator initiates the incident creation on behalf of the Client (FR-038). The flow is identical, but the creating employee selects the relevant Client from a list in step 2, and the creating employee's identity is recorded separately from the Client's identity as the reporting party.

**Exceptions:**
- **EX-001-A:** If required fields (Title or Description) are missing, the System displays inline validation errors and does not submit the form. The Client must correct the errors and resubmit.
- **EX-001-B:** If an attached file exceeds the permitted size or is of an invalid type, the System rejects the file, displays an error message, and allows the Client to remove the invalid file and resubmit.

---

### UC-002: Technician Resolves an Incident

| Field | Detail |
|---|---|
| **Use Case ID** | UC-002 |
| **Title** | Technician Resolves an Incident |
| **Primary Actor** | Technician |
| **Secondary Actors** | Administrator (optional reviewer) |
| **Related Requirements** | FR-043, FR-044, FR-045, FR-046 |
| **Description** | A Technician addresses an open incident and records a resolution against it, including their report, status, and any charges. |
| **Preconditions** | The Technician is authenticated. At least one open Incident record exists in the tenant. |
| **Postconditions** | The Incident record is updated with a Resolution. If status is "Resolved," the resolution date is set. The Incident moves from the pending list to the resolved list. The Client associated with the Incident can view the resolution. |

**Main Flow:**
1. The Technician navigates to the "Pending Incidents" screen.
2. The Technician selects an open Incident from the list.
3. The System displays the Incident detail view, showing the title, description, priority, report date, client information, and any images submitted by the client.
4. The Technician selects "Add Resolution."
5. The System presents a resolution form with fields: Resolution Status (Resolved / Pending Parts / Unable to Resolve), Description of work performed, Price Charged, Discount (optional), and an image upload control.
6. The Technician selects "Resolved" as the resolution status, enters a description of the corrective action taken, enters the price charged, and optionally enters a discount and attaches images.
7. The Technician submits the resolution form.
8. The System validates the submitted data.
9. The System saves the Resolution against the Incident record, recording the current timestamp as the resolution date and associating the Technician's identity with the resolution.
10. The Incident record is removed from the pending list and appears in the resolved list.
11. The Client associated with the Incident receives an in-app notification that their incident has been resolved.

**Alternative Flows:**
- **AF-002-A (Pending Parts):** In step 6, the Technician selects "Pending Parts" as the status and provides an explanatory description. Price Charged is optional. The resolution date is recorded but the incident remains in a "Pending Parts" sub-state and may be visible in a filtered pending view.
- **AF-002-B (Unable to Resolve):** In step 6, the Technician selects "Unable to Resolve." The Technician provides a mandatory explanation. The resolution date is recorded and the incident is closed with this status.
- **AF-002-C (Administrator resolves):** An Administrator may perform the same flow, as Administrators may hold the Technician role.

**Exceptions:**
- **EX-002-A:** If required fields (Status or Description) are missing, the System displays validation errors and does not save the resolution.
- **EX-002-B:** If the Incident record has already been resolved, the System displays a read-only view of the existing resolution and does not allow a second resolution to be recorded.

---

### UC-003: Technician Creates a Service Record

| Field | Detail |
|---|---|
| **Use Case ID** | UC-003 |
| **Title** | Technician Creates a Service Record |
| **Primary Actor** | Technician |
| **Secondary Actors** | Client (associated), Administrator (optional reviewer) |
| **Related Requirements** | FR-027, FR-028, FR-029 |
| **Description** | A Technician creates a new scheduled or recently performed maintenance service record for a specific client. |
| **Preconditions** | The Technician is authenticated. At least one Client exists within the tenant. |
| **Postconditions** | A new Service record exists in the system, associated with the specified Client. The service date appears in the relevant Calendar views. |

**Main Flow:**
1. The Technician navigates to the "Services" section and selects "New Service."
2. The System presents a service creation form.
3. The Technician fills in: (a) Title; (b) Description of work to be performed or performed; (c) Date of actual service execution; (d) Date of next scheduled service; (e) Technical notes (optional free-text); (f) Associated Client (selected from a list of tenant clients).
4. The Technician submits the form.
5. The System validates all mandatory fields.
6. The System creates and persists the Service record, associating it with the selected Client.
7. The System confirms creation and navigates the Technician to the Service detail view.

**Exceptions:**
- **EX-003-A:** If any mandatory field is missing, the System displays validation errors and does not create the record.
- **EX-003-B:** If the "Next Service Date" is earlier than the "Actual Service Date," the System displays a validation warning. The Technician must confirm the intent or correct the value before proceeding.

---

### UC-004: Technician Completes a Scheduled Service

| Field | Detail |
|---|---|
| **Use Case ID** | UC-004 |
| **Title** | Technician Completes a Scheduled Service |
| **Primary Actor** | Technician |
| **Related Requirements** | FR-030, FR-031 |
| **Description** | A Technician records the completion of a scheduled maintenance service by adding a resolution to an existing Service record. |
| **Preconditions** | The Technician is authenticated. A Service record without an existing Resolution exists in the tenant. |
| **Postconditions** | The Service record is updated with a Resolution. The Service is marked as completed in the calendar and service list views. |

**Main Flow:**
1. The Technician navigates to the pending services view or calendar and selects the relevant Service record.
2. The Technician selects "Record Completion."
3. The System presents a resolution form: Resolution Date, Description of work performed, Price Charged, Discount (optional), and an image upload control.
4. The Technician completes all fields, optionally attaches images, and submits.
5. The System validates the form.
6. The System saves the Resolution to the Service record, associating the Technician's identity with the completion record.
7. The Service is updated to "Completed" status in all views.

**Exceptions:**
- **EX-004-A:** If required fields are missing, validation errors are shown and the record is not saved.

---

### UC-005: Client Views Service Calendar

| Field | Detail |
|---|---|
| **Use Case ID** | UC-005 |
| **Title** | Client Views Service Calendar |
| **Primary Actor** | Client |
| **Related Requirements** | FR-057, FR-059, FR-060, FR-061 |
| **Description** | A Client views a calendar displaying the dates of their upcoming, overdue, and completed services. |
| **Preconditions** | The Client is authenticated. At least one Service record exists that is associated with the Client. |
| **Postconditions** | No state change. The Client has received visibility into their service schedule. |

**Main Flow:**
1. The Client navigates to the "Calendar" section.
2. The System retrieves all Service records associated with the authenticated Client.
3. The System renders a monthly calendar view, placing service entries on their respective service or scheduled dates.
4. Upcoming services (next service date in the future, no resolution) are visually indicated as "Upcoming."
5. Overdue services (next service date in the past, no resolution) are visually indicated as "Overdue."
6. Completed services are visually indicated as "Completed."
7. The Client may navigate to previous or subsequent months.
8. Selecting a calendar entry navigates the Client to the full detail view of that Service record.

**Alternative Flows:**
- **AF-005-A (No services):** If no services are associated with the Client, the System renders an empty calendar with a message indicating no services are scheduled.

---

### UC-006: Employee Views Pending Incidents Dashboard

| Field | Detail |
|---|---|
| **Use Case ID** | UC-006 |
| **Title** | Employee Views Pending Incidents Dashboard |
| **Primary Actor** | Technician / Administrator |
| **Related Requirements** | FR-068, FR-069, FR-071, FR-072 |
| **Description** | A Technician or Administrator views the list of all open incidents within the tenant, ordered by priority and then by report date, in order to triage and act on them. |
| **Preconditions** | The employee is authenticated. |
| **Postconditions** | No state change. The employee has visibility into the current incident backlog. |

**Main Flow:**
1. The Technician navigates to the "Incident Dashboard" or "Pending Incidents" screen.
2. The System retrieves all Incident records within the tenant where the resolution status is "Open" (no resolution recorded) or "Pending Parts."
3. The System renders a list ordered by priority (highest first) and, within equal priority, by report date (oldest first).
4. Each list entry displays: Incident title, priority indicator, report date, associated client name, and time elapsed since report.
5. The employee may apply filters (by client, priority, date range) to narrow the view.
6. Selecting an entry navigates to the full Incident detail view.

---

### UC-007: User Authenticates into the System

| Field | Detail |
|---|---|
| **Use Case ID** | UC-007 |
| **Title** | User Authenticates into the System |
| **Primary Actor** | Any User (Client, Technician, Administrator) |
| **Related Requirements** | FR-001, FR-005, FR-006, TR-013, TR-014 |
| **Description** | A registered user provides their credentials to authenticate and obtain an active session. |
| **Preconditions** | The user has a registered account within the tenant. The application is running. |
| **Postconditions** | The user holds a valid session (JWT access token and refresh token) and is directed to their role-appropriate home screen. |

**Main Flow:**
1. The user launches the application or navigates to the login screen.
2. The System presents the login form with fields for email address and password.
3. The user enters their email address and password and submits.
4. The System forwards the credentials to the Identity Service.
5. The Identity Service looks up the user record by email address within the tenant context.
6. The Identity Service verifies the submitted password against the stored hash.
7. Upon successful verification, the Identity Service issues a signed JWT access token and a refresh token.
8. The System stores the tokens securely on the client device and redirects the user to their role-appropriate home screen.

**Alternative Flows:**
- **AF-007-A (Expired access token):** If the access token has expired during a session, the client application silently uses the refresh token to obtain a new access token from the Identity Service, without requiring the user to log in again, provided the refresh token remains valid.

**Exceptions:**
- **EX-007-A (Invalid credentials):** If the email address is not found or the password is incorrect, the Identity Service returns a generic authentication failure. The System displays a non-specific error message ("Invalid email address or password") to prevent user enumeration. After a configurable number of consecutive failed attempts, the account is temporarily locked and the user is notified.
- **EX-007-B (Deactivated account):** If the user's account is deactivated, the System displays a message indicating that the account is inactive and advises the user to contact their Administrator.

---

### UC-008: Administrator Invites a New Client

| Field | Detail |
|---|---|
| **Use Case ID** | UC-008 |
| **Title** | Administrator Invites a New Client |
| **Primary Actor** | Administrator |
| **Secondary Actors** | Email Delivery Service |
| **Related Requirements** | FR-009, FR-010, FR-015 |
| **Description** | An Administrator creates a client account and dispatches an invitation email so the client can complete their own registration. |
| **Preconditions** | The Administrator is authenticated. The intended client does not already have an account in the tenant. |
| **Postconditions** | A pending client account record exists in the system. An invitation email with a unique, time-limited link has been sent to the client's email address. |

**Main Flow:**
1. The Administrator navigates to "User Management" and selects "Invite Client."
2. The System presents a form requesting the client's name and email address.
3. The Administrator enters the client's details and submits.
4. The System checks that the email address is not already in use within the tenant.
5. The System creates a pending client account record associated with the tenant.
6. The System generates a cryptographically secure, unique, time-limited invitation token and stores its hash.
7. The System dispatches an email to the provided address containing the invitation link embedding the token.
8. The System confirms to the Administrator that the invitation has been sent.

**Exceptions:**
- **EX-008-A:** If the email address is already associated with an account in the tenant, the System displays an error and does not send a duplicate invitation.
- **EX-008-B:** If email delivery fails, the System records the failure and notifies the Administrator. The Administrator may retry the invitation dispatch from the User Management screen.

---

### UC-009: Client Completes First-Time Registration

| Field | Detail |
|---|---|
| **Use Case ID** | UC-009 |
| **Title** | Client Completes First-Time Registration |
| **Primary Actor** | Client (prospective) |
| **Related Requirements** | FR-011, FR-012, FR-007 |
| **Description** | A client who has received an invitation link uses it to complete their account setup by creating credentials. |
| **Preconditions** | A valid, non-expired invitation link has been sent to the client. The client accesses the link within the validity period. |
| **Postconditions** | The client account is activated. The client can authenticate using their newly set credentials. The invitation token is invalidated. |

**Main Flow:**
1. The client opens the invitation link in the application or a browser.
2. The System validates the invitation token: it exists, has not been used, and has not expired.
3. The System presents a registration completion form showing the client's name and email (pre-filled, read-only) and requesting a new password (with confirmation).
4. The client enters and confirms a password meeting the System's password policy.
5. The client submits the form.
6. The System validates the password against the configured policy.
7. The System hashes the password and activates the client account.
8. The invitation token is marked as used and invalidated.
9. The System authenticates the client automatically and navigates them to the client home screen.

**Exceptions:**
- **EX-009-A (Expired link):** If the token has expired, the System displays an informative message and provides a link for the client to request a new invitation (triggering UC-010 workflow with Administrator approval).
- **EX-009-B (Password policy violation):** If the entered password does not meet the policy, the System displays specific guidance and does not activate the account until a compliant password is provided.

---

### UC-010: Client Requests Account Recovery

| Field | Detail |
|---|---|
| **Use Case ID** | UC-010 |
| **Title** | Client Requests Account Recovery |
| **Primary Actor** | Client |
| **Secondary Actors** | Administrator |
| **Related Requirements** | FR-013, FR-014 |
| **Description** | A Client who has lost access to their account (e.g., forgotten password, expired invitation) requests recovery, which must be approved by an Administrator. |
| **Preconditions** | A client account exists for the requesting user but the client cannot authenticate. |
| **Postconditions (pending approval):** | An account recovery request is recorded. The tenant Administrator(s) receive a notification of the pending request. |
| **Postconditions (upon approval):** | The Administrator approves the request, triggering dispatch of a new invitation-style reset link to the client's registered email address. The client can complete registration/password reset via UC-009. |

**Main Flow:**
1. The client navigates to the login screen and selects "Account Recovery" or "Can't log in."
2. The System presents a form requesting the client's registered email address.
3. The client enters their email address and submits.
4. The System verifies that an account exists for the email address within a tenant context.
5. The System creates an account recovery request record and dispatches an in-app notification to all Administrators of the tenant.
6. The System informs the client that their request has been submitted and is awaiting Administrator approval.
7. The Administrator reviews the request in the User Management section and approves or rejects it.
8. Upon approval, the System generates a new time-limited recovery link and dispatches it to the client's registered email address.
9. The client follows the link to complete the password reset (following the flow of UC-009 from step 3).

**Exceptions:**
- **EX-010-A:** If no account is found for the submitted email address, the System displays a generic message ("If an account exists for this email, a recovery request will be submitted") to prevent account enumeration.
- **EX-010-B:** If the Administrator rejects the request, the client receives an email informing them that the recovery request was denied, with guidance to contact the company directly.

---

### UC-011: Administrator Manages User Accounts

| Field | Detail |
|---|---|
| **Use Case ID** | UC-011 |
| **Title** | Administrator Manages User Accounts |
| **Primary Actor** | Administrator |
| **Related Requirements** | FR-022, FR-023, FR-024, FR-025, FR-021 |
| **Description** | An Administrator views, modifies, activates, deactivates, or changes the roles of user accounts within their tenant. |
| **Preconditions** | The Administrator is authenticated. |
| **Postconditions** | Any modifications to user accounts are persisted and take effect immediately on subsequent requests from the affected users. |

**Main Flow:**
1. The Administrator navigates to "User Management."
2. The System displays a paginated list of all user accounts in the tenant, showing: name, email, roles, account status (active/deactivated), and last login date.
3. The Administrator selects a specific user account.
4. The System displays the account detail view.
5. The Administrator performs one or more of the following actions: (a) Modify roles (assign or revoke the Technician or Administrator role); (b) Deactivate the account; (c) Reactivate a deactivated account.
6. The Administrator confirms the change.
7. The System validates the change (e.g., preventing removal of the last Administrator per FR-021).
8. The System persists the change and immediately reflects it in the user's access rights on subsequent API calls.

**Exceptions:**
- **EX-011-A:** If the Administrator attempts to remove the last Administrator role within the tenant (including from their own account), the System rejects the operation with an explanatory error message.
- **EX-011-B:** If the Administrator attempts to assign the Client role to an employee, or the Technician/Administrator role to a Client, the System rejects the operation with an explanatory error message.

---

### UC-012: Employee Adds an Invoice to a Charge

| Field | Detail |
|---|---|
| **Use Case ID** | UC-012 |
| **Title** | Employee Adds an Invoice to a Charge |
| **Primary Actor** | Technician / Administrator |
| **Related Requirements** | FR-050, FR-051, FR-052, FR-053 |
| **Description** | After recording a resolution for a Service or Incident, an employee attaches an invoice document and associated financial metadata to the resolution. |
| **Preconditions** | The employee is authenticated. A Service or Incident Resolution record exists that does not yet have an invoice attached. The employee has an invoice document (PDF or image) available. |
| **Postconditions** | The invoice document is stored and associated with the resolution. The Client can view and download the invoice. |

**Main Flow:**
1. The employee navigates to the relevant Service or Incident resolution detail.
2. The employee selects "Add Invoice."
3. The System presents an invoice upload form with fields: Invoice Date, Amount, Discount (optional), and a file upload control.
4. The employee completes the metadata fields and selects the invoice file (PDF or image).
5. The employee submits the form.
6. The System validates the file type and size.
7. The System uploads the file to object storage and generates a persistent reference URI.
8. The System creates an Invoice metadata record, associating it with the resolution and storing the URI, date, amount, and discount.
9. The System confirms the upload and displays the invoice in the resolution detail view.

**Exceptions:**
- **EX-012-A:** If the file type is not accepted or the file size exceeds the limit, the System rejects the file and displays an appropriate error. The employee must select a valid file.

---

### UC-013: Client Views Invoices

| Field | Detail |
|---|---|
| **Use Case ID** | UC-013 |
| **Title** | Client Views Invoices |
| **Primary Actor** | Client |
| **Related Requirements** | FR-054, FR-056 |
| **Description** | A Client views a list of all invoices associated with their Services and Incidents and downloads specific invoice documents. |
| **Preconditions** | The Client is authenticated. At least one invoice exists associated with the Client's records. |
| **Postconditions** | No state change. The Client has retrieved and viewed or downloaded an invoice document. |

**Main Flow:**
1. The Client navigates to the "Invoices" section.
2. The System retrieves all Invoice records associated with the authenticated Client's Service and Incident records.
3. The System displays a list of invoices showing: associated service/incident title, invoice date, amount, and discount.
4. The Client selects a specific invoice.
5. The System requests a pre-signed URL for the invoice document from the storage service.
6. The System presents the invoice document to the Client (inline preview for PDFs and images, with a download option).

**Exceptions:**
- **EX-013-A:** If no invoices exist for the Client, the System displays an empty state with a message indicating no invoices are available.
- **EX-013-B:** If the pre-signed URL generation fails (e.g., storage service unavailable), the System displays an error message and advises the Client to retry.

---

### UC-014: Administrator Updates Incident Priority

| Field | Detail |
|---|---|
| **Use Case ID** | UC-014 |
| **Title** | Administrator Updates Incident Priority |
| **Primary Actor** | Administrator |
| **Related Requirements** | FR-041, FR-040 |
| **Description** | An Administrator manually changes the priority level of an open incident, for example to escalate an urgent issue or to downgrade a low-impact report. |
| **Preconditions** | The Administrator is authenticated. At least one open Incident record exists in the tenant. |
| **Postconditions** | The Incident's priority is updated and the incident list is re-sorted accordingly. The change is recorded in the incident's audit history. |

**Main Flow:**
1. The Administrator navigates to the Incident detail view of the target incident.
2. The Administrator selects "Edit Priority."
3. The System presents the current priority value and a selector showing all available priority levels.
4. The Administrator selects the new priority level.
5. The Administrator confirms the change.
6. The System persists the updated priority, records the change event (including the Administrator's identity, previous value, new value, and timestamp) in the incident's audit log.
7. The Incident's position in the pending incidents list is updated to reflect the new priority.

---

### UC-015: System Issues a Service Due-Date Notification

| Field | Detail |
|---|---|
| **Use Case ID** | UC-015 |
| **Title** | System Issues a Service Due-Date Notification |
| **Primary Actor** | System (Scheduler) |
| **Secondary Actors** | Technician, Administrator (recipients) |
| **Related Requirements** | FR-062, FR-063, FR-064, FR-065, FR-067, TR-038 |
| **Description** | The system automatically detects services approaching their scheduled next service date and dispatches notifications to the responsible employees. |
| **Preconditions** | At least one Service record exists with a next service date within the configured advance notice window and without a completed resolution for that period. |
| **Postconditions** | In-app notifications are delivered to all Technicians and Administrators of the tenant to which the service belongs. |

**Main Flow:**
1. The background scheduler executes the due-date check job at the configured interval (e.g., daily at a set time).
2. The System queries all Service records across all tenants where: (a) the next service date falls within the configured advance notice period; (b) no completed Resolution has been recorded against the current service cycle.
3. For each qualifying Service record, the System publishes a "ServiceDueSoon" event to the message broker, including the tenant identifier, service identifier, associated client, and the next service date.
4. The Notification Service consumes the event and retrieves the relevant Technicians and Administrators for the tenant.
5. The Notification Service dispatches an in-app notification to each recipient, indicating that a service for a named client is due within the advance notice period.
6. The notification includes the service title, the client name, and the scheduled next service date.
7. The dispatched notifications are recorded with their delivery status.

**Exceptions:**
- **EX-015-A:** If the message broker is unavailable, the event publication fails. The scheduler shall retry with exponential backoff. Persistent failures are logged and trigger an operational alert.
- **EX-015-B:** If no qualifying services exist, the job completes without publishing events.

---

### UC-016: Client Requests an Early Service Appointment

| Field | Detail |
|---|---|
| **Use Case ID** | UC-016 |
| **Title** | Client Requests an Early Service Appointment |
| **Primary Actor** | Client |
| **Secondary Actors** | Technician, Administrator (notified) |
| **Related Requirements** | FR-032 |
| **Description** | A Client requests that a maintenance service be performed sooner than the currently scheduled next service date. |
| **Preconditions** | The Client is authenticated. At least one Service record with a future next service date exists associated with the Client. |
| **Postconditions** | An early appointment request is recorded and Technicians and Administrators are notified. The Service record is not modified; the Technician must create a new Service record upon scheduling the early appointment. |

**Main Flow:**
1. The Client navigates to the Service detail view of the relevant service (accessible from the calendar or service list).
2. The Client selects "Request Early Appointment."
3. The System presents a form with a free-text field for the Client to describe the reason for the early request (optional).
4. The Client submits the request.
5. The System creates an early appointment request record linked to the Service record.
6. The System dispatches an in-app notification to the tenant's Technicians and Administrators, indicating that a client has requested an early service appointment.
7. The System confirms the request to the Client and indicates that the team has been notified.
8. A Technician reviews the request and, upon agreeing to schedule the appointment, creates a new Service record with the appropriate dates.

**Exceptions:**
- **EX-016-A:** If the Client has already submitted a pending early appointment request for the same service, the System notifies the Client that a request is already pending and does not create a duplicate.

---

## Appendix A — Requirement Traceability Matrix

The following table provides a high-level mapping between Use Cases and the Functional Requirements they exercise, supporting traceability from requirements to test design.

| Use Case | Primary Functional Requirements |
|---|---|
| UC-001 | FR-037, FR-038, FR-039, FR-040, FR-065 |
| UC-002 | FR-043, FR-044, FR-045, FR-046, FR-049 |
| UC-003 | FR-027, FR-028, FR-029 |
| UC-004 | FR-030, FR-031 |
| UC-005 | FR-057, FR-059, FR-060, FR-061 |
| UC-006 | FR-068, FR-069, FR-071, FR-072 |
| UC-007 | FR-001, FR-005, FR-006, FR-007 |
| UC-008 | FR-009, FR-010, FR-015 |
| UC-009 | FR-011, FR-012 |
| UC-010 | FR-013, FR-014 |
| UC-011 | FR-022, FR-023, FR-024, FR-025 |
| UC-012 | FR-050, FR-051, FR-053 |
| UC-013 | FR-054, FR-056 |
| UC-014 | FR-040, FR-041 |
| UC-015 | FR-062, FR-063, FR-064, FR-065, FR-067 |
| UC-016 | FR-032 |

---

## Appendix B — Glossary of Priority Levels

The following priority levels are defined for the initial version of the Platform. Priority level definitions may be configured at the tenant level in future versions.

| Priority Level | Label | Description |
|---|---|---|
| P1 | Critical | Requires immediate attention; the affected asset or service is completely non-functional and is causing significant operational impact. |
| P2 | High | Significant degradation of the asset or service; urgent attention required within the same working day. |
| P3 | Medium | Partial degradation or non-critical fault; attention required within a defined service window. |
| P4 | Low | Minor issue or cosmetic fault; no immediate operational impact; to be addressed in the next available maintenance slot. |

> In v1.0, all newly created incidents shall be assigned a default priority of **P3 (Medium)** unless manually changed by an Administrator.

---

## Appendix C — Revision History

| Version | Date | Author | Description of Change |
|---|---|---|---|
| 1.0.0 | 2026-06-08 | — | Initial release of the Software Requirements Specification. |
| 1.1.0 | 2026-06-09 | — | Added requirements derived from the updated domain class diagram: Asset entity (FR-085–FR-090, Section 3.11); ActivityStatusTransition lifecycle tracking with SCHEDULED/IN_PROGRESS/AWAITING_PARTS/COMPLETED/CANCELLED/OPEN/CLOSED statuses (FR-078–FR-084, Section 3.10); file asset attachment at ManagementActivity level for both Services and Incidents (FR-073, FR-074); notification dispatch audit log (FR-075–FR-077, added to Section 3.8). Updated Section 2.4 entity overview. Amended FR-039 (file assets at creation time), FR-044 (resolution outcome status distinguished from operational status), and NFR-038 (ActivityStatusTransition status extensibility). |

---

*End of Document*

---

> **Document Control Notice:** This document is a living specification. Any changes to requirements subsequent to this version must be formally reviewed, assigned a new version number, and appended to Appendix C. All affected downstream documents (Technical Design Document, Test Plan, Acceptance Criteria) must be updated in concert to maintain traceability and consistency.
