# ShiftSync — Domain Microservices

**Student Name:** Chamith Bhanuka Widanapathirana  
**Student ID / Number:** 241711051  
**Slack Handle:** Chamith Bhanuka  
**GCP Project ID:** project-a58ee7a4-4913-4af2-a6d  
**Course:** ITS 2130 — Enterprise Cloud Architecture  

---

## Description

Parent repository for the ShiftSync domain microservices suite:

1. **[shiftsync-scheduling-service](./shiftsync-scheduling-service)**: Shift scheduling, open-shift claims, and peer-to-peer swap workflows backed by Cloud SQL PostgreSQL.
2. **[shiftsync-notification-service](./shiftsync-notification-service)**: Activity event auditing, unread tracking, and real-time STOMP WebSocket notifications backed by MongoDB Atlas.
3. **[shiftsync-credential-service](./shiftsync-credential-service)**: Employee credential upload, compliance reviews, and secure Google Cloud Storage (GCS) document streaming.

---

## Microservices Architecture

```
                      ┌──────────────────────┐
                      │     API Gateway      │
                      └──────────┬───────────┘
                                 │
     ┌───────────────────────────┼───────────────────────────┐
     ▼                           ▼                           ▼
┌──────────────┐          ┌──────────────┐          ┌──────────────┐
│  Scheduling  │ ───────► │ Notification │          │  Credential  │
│   Service    │ (Events) │   Service    │          │   Service    │
└──────┬───────┘          └──────┬───────┘          └──────┬───────┘
       │                         │                         │
       ▼                         ▼                         ▼
┌──────────────┐          ┌──────────────┐          ┌──────────────┐
│  Cloud SQL   │          │   MongoDB    │          │ Cloud SQL +  │
│ (PostgreSQL) │          │    Atlas     │          │  GCS Bucket  │
└──────────────┘          └──────────────┘          └──────────────┘
```

---

## Deployment Architecture

Domain microservices run on Google Cloud Platform (GCP) Compute Engine Managed Instance Groups (`mig-services`) in `asia-southeast1`. Each service dynamically registers with Eureka Server and pulls configuration from Config Server.
