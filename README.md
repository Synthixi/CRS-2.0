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
 
- [System Summary](#system-summary)
- [Tech Stack](#tech-stack)
    - [Frontend Tools](#frontend-tools)
    - [Backend Tools](#backend-tools)
    - [Database](#database)
    - [Other Tools](#other-tools)
- [Hosting](#hosting)
- [Mockups](#mockups)
- [System Architecture](#system-architecture)
---
## System Summary

### New Features
- Students can now see during course enlistment whether taking a course would cause a conflict with their current schedule
- Direct payment of tuition and other fees through the portal (no more separate Maya QR workaround)

### Fixes
- Improved UI and placements of navigation elements (— replaced the outdated newspaper layout)
- Unified portal experience — document requests, schedules, grades, and payments in one place instead of scattered across separate pages
- Bigger text and visual weight to improve visual hierarchy, making key information easier to scan


## Tech Stack
 
### Frontend Tools
 
<!-- Front end Tools here -->
 
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

