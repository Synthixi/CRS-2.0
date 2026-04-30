# The Long Awaited CRS 2.0 is Here!

## Overview
CRS 2.0 is a redesigned version of the University of the Philippines Visayas Course Registration System (CRS). The update aims to improve usability, performance, and reliability by introducing a more modern web-based platform that supports faster transactions and improved user experience.

### Team Members
- Justin Lauricio — Product Owner  
- Samantha Mok — Frontend Designer  
- Jhon Chriztopher Nice — Backend Developer  
- Aleighia Keith Reyes — Database Manager  

---

## Table of Contents
 
- [The Long Awaited CRS 2.0 is Here!](#the-long-awaited-crs-20-is-here)
  - [Overview](#overview)
    - [Team Members](#team-members)
  - [Table of Contents](#table-of-contents)
  - [System Summary](#system-summary)
    - [New Features](#new-features)
    - [Fixes](#fixes)
  - [🛠️ CRS 2.0 — Tech Stack](#️-crs-20--tech-stack)
    - [🎨 Frontend Tools](#-frontend-tools)
    - [Backend Tools](#backend-tools)
    - [Database](#database)
    - [Other Tools](#other-tools)
  - [Hosting](#hosting)
  - [Mockups](#mockups)
  - [System Architecture](#system-architecture)
    - [Direct Payment Process](#direct-payment-process)
    - [CRS 2.0 Simple Sitemap](#crs-20-simple-sitemap)
    - [Course Enlistment Flowchart](#course-enlistment-flowchart)
---
## System Summary

### New Features
- Students can now see during course enlistment whether taking a course would cause a conflict with their current schedule
- Direct payment of tuition and other fees through the portal (no more separate Maya QR workaround)

### Fixes
- Improved UI and placements of navigation elements (— replaced the outdated newspaper layout)
- Unified portal experience — document requests, schedules, grades, and payments in one place instead of scattered across separate pages
- Bigger text and visual weight to improve visual hierarchy, making key information easier to scan


## 🛠️ CRS 2.0 — Tech Stack

### 🎨 Frontend Tools

The frontend is primary built with **Next.js**, a modern React-based framework that supports Server-Side Rendering (SSR) and Static Site Generation (SSG) — ensuring fast, reliable page loads even during peak enrollment periods. The stack is designed for type safety, consistent UI, and real-time data updates, making it ideal for a high-traffic university system.

| Logo | Technology | Role | Why We Chose It |
|:----:|------------|------|-----------------|
| <img src="https://cdn.simpleicons.org/nextdotjs/000000" width="24"/> | **Next.js** | Core Framework | Provides SSR and SSG for fast page loads during enrollment peaks. File-based routing maps cleanly to pages. |
| <img src="https://cdn.simpleicons.org/typescript/3178C6" width="24"/> | **TypeScript** | Language | Enforces strict type checking across the codebase — prevents passing wrong data types for student records, course codes, and IDs. |
| <img src="https://cdn.simpleicons.org/tailwindcss/06B6D4" width="24"/> | **Tailwind CSS** | Styling | Utility-first CSS that ensures UI consistency across all pages — components built quickly and uniformly without custom CSS. |
| <img src="https://cdn.simpleicons.org/reactquery/FF4154" width="24"/> | **React Query** | Data Fetching & Caching | Manages server state with intelligent caching and background refetching — students always see up-to-date enrollment data without full page reloads. |
| <img src="https://cdn.simpleicons.org/zod/3E67B1" width="24"/> | **Zod** | Form Validation | Validates form inputs on the frontend before they reach the backend — ensures malformed enrollment or document data is rejected early. |
| <img src="https://authjs.dev/img/logo-sm.png" width="24"/> | **Auth.js** | Authentication | Handles authentication, session management, and OAuth 2.0 integration with UP SSO providers. Supports secure role-aware access flows for students, faculty, and administrators. |
 
### Backend Tools
 
<!-- Backend tools here -->
 
### Database
 
<!-- Database here -->
 
### Other Tools
 
<!-- Other tool if any -->

## Hosting
<!-- Hostings -->

## Mockups
<!-- Screenshots -->

## System Architecture 

The following diagrams illustrates the workflows and structure of CRS 2.0

### Direct Payment Process


```mermaid
sequenceDiagram
    participant Student
    participant CRS as CRS Portal
    participant Payment as Payment Gateway
    participant DB as Database

    Student->>CRS: View balance and click "Pay Now"
    CRS->>DB: Get outstanding balance
    DB-->>CRS: Return balance
    CRS-->>Student: Display payment page
    
    Student->>CRS: Enter payment details
    CRS->>Payment: Process direct payment
    
    Note over Payment,Student: If successful
    Payment-->>CRS: Payment confirmed
    CRS->>DB: Update payment status
    CRS-->>Student:  Success + Receipt
    
    Note over Payment,Student: If failed
    Payment-->>CRS: Payment failed
    CRS-->>Student:  Error - Retry
```


---


### CRS 2.0 Simple Sitemap
```mermaid
flowchart LR
    Home["CRS 2.0 Homepage"]
    
    Home --> Logins["Logins"]
    Home --> Forms["Forms"]
    Home --> Colleges["Colleges"]
    Home --> Campuses["Campuses"]
    Home --> Contacts["Contacts"]
    
    Logins --> Student["Student"]
    Logins --> Admin["Admin"]
    Logins --> Faculty["Faculty"]
    
    Student --> Grades["Grades"]
    Student --> Accountability["Accountability"]
    Student --> Schedule["Schedule"]
    Student --> Enrollment["Enrollment"]

    Admin --> ADashboard["..."]
    Faculty -->FDashboard["..."]
    
    Forms --> Graduates["Graduates"]
    Forms --> Undergrads["Undergrads"]
    Forms --> Downloadable["Downloadable"]
    
    Colleges --> CAS["Arts & Sciences"]
    Colleges --> CBA["Business"]
    Colleges --> CFOS["Fisheries & Ocean Sciences"]
    Colleges --> CM["Management"]
    Colleges --> SoTech["School of Technology"]
    
    Campuses --> DILIMAN["Diliman"]
    Campuses --> VISAYAS["Visayas"]
    Campuses --> MINDANAO["Mindanao"]
    Campuses --> ETC["OTHER"]
    
    Contacts --> Email["Email"]
    Contacts --> Registrar["Registrar"]
```


---


### Course Enlistment Flowchart
```mermaid
flowchart TD
    Start([Student logs in]) --> Dashboard[Dashboard]
    Dashboard --> Enlist[Click Enlistment]
    Enlist --> Browse[Browse courses]
    Browse --> Select[Select course]
    Select --> Check{Check conflict}
    Check -->|Conflict found| Warn[Show warning]
    Warn --> Modify[Modify schedule]
    Modify --> Check
    Check -->|No conflict| Add[Add to enlistment]
    Add --> More{More courses?}
    More -->|Yes| Browse
    More -->|No| Finalize[Finalize enlistment]
    Finalize --> End([Done])
    
```

