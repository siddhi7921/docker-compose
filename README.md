<div align="center">

# 🚧 FieldLine

### Intelligent Data Capture & Schedule-Linking Layer for Infrastructure Project Management

**The Planning-to-Execution Bridge for Large-Scale Infrastructure Projects**

[![SIH 2026](https://img.shields.io/badge/Smart%20India%20Hackathon-2026-orange?style=for-the-badge)](https://sih.gov.in/)
[![Problem Statement](https://img.shields.io/badge/Problem%20Statement-SIH26122-blue?style=for-the-badge)](#-smart-india-hackathon)
[![Theme](https://img.shields.io/badge/Theme-Smart%20Automation-green?style=for-the-badge)](#-smart-india-hackathon)
[![Category](https://img.shields.io/badge/Category-Software-purple?style=for-the-badge)](#-smart-india-hackathon)

[![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)](https://redis.io/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)

*Turning scattered site reports into structured, schedule-linked, real-time project intelligence.*

[Overview](#-the-problem) •
[Solution](#-our-solution) •
[Architecture](#%EF%B8%8F-system-architecture) •
[How It Works](#%EF%B8%8F-how-it-works) •
[Tech Stack](#-tech-stack) •
[Getting Started](#-getting-started) •
[Team](#-team)

</div>

---

## 📖 Table of Contents

- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [System Architecture](#%EF%B8%8F-system-architecture)
- [How It Works](#%EF%B8%8F-how-it-works)
- [Planned vs. Actual Progress](#-planned-vs-actual-progress)
- [Frontend](#-frontend)
- [Backend Infrastructure](#%EF%B8%8F-backend-infrastructure)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Smart India Hackathon](#-smart-india-hackathon)
- [Team](#-team)
- [Future Scope](#-future-scope)
- [Vision](#-vision)

---

## 🧠 The Problem

Large infrastructure projects — refineries, pipelines, bridges, roads, and industrial facilities — are planned using tools like **Primavera P6**, **Microsoft Project**, **Excel**, or **CSV-based schedules**.

But actual site progress is reported through a completely different, messy channel:

| Source Type | Examples |
|---|---|
| 📄 Documents | PDF reports, scanned documents |
| 📊 Spreadsheets | Excel and CSV files |
| ✍️ Free text | Site updates, WhatsApp-style notes |
| 🖼️ Images | Site photos, handwritten diaries |

Project managers are left to **manually read** these reports and cross-check them against the planned schedule — a slow, error-prone, and unscalable process.

> **Example field note:**
> *"Pump P104 installation started yesterday. Base plate installed, motor alignment pending."*

A standard database has no way of knowing which planned schedule activity this update actually belongs to.

---

## 💡 Our Solution

**FieldLine** acts as an intelligent bridge between **project planning** and **actual site execution** — automatically capturing field evidence, extracting structured meaning from it, and linking it back to the right activity in the plan.

```text
PROJECT PLANNING
Primavera / MS Project / Excel
              │
              ▼
       PLANNED SCHEDULE
              │
              ▼
     ┌───────────────────┐
     │     FIELDLINE     │
     │                   │
     │ Intelligent Data  │
     │ Capture &         │
     │ Schedule Linking  │
     └─────────┬─────────┘
               │
        Field Evidence
               │
     ┌─────────┼─────────┐
     ▼         ▼         ▼
    PDF      Excel     Images
   Reports   / CSV    / Scans
     │         │         │
     └─────────┼─────────┘
               │
               ▼
      AI INFORMATION EXTRACTION
               │
               ▼
        SCHEDULE MATCHING
               │
               ▼
        PROGRESS ANALYSIS
               │
               ▼
      REAL-TIME PROJECT STATUS
```

---

## 🏗️ System Architecture

```text
                         ┌──────────────────────────┐
                         │    FIELDLINE FRONTEND     │
                         │   React + TypeScript      │
                         │                           │
                         │ • Dashboard               │
                         │ • Schedule Upload         │
                         │ • Evidence Upload         │
                         │ • AI Review               │
                         │ • Activity Details        │
                         └────────────┬──────────────┘
                                      │
                              HTTP / WebSockets
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │   NGINX REVERSE PROXY     │
                         └────────────┬──────────────┘
                                      │
                       ┌──────────────┴──────────────┐
                       ▼                             ▼
              ┌─────────────────┐           ┌─────────────────┐
              │  Node.js API 1  │           │  Node.js API 2  │
              │                 │           │                 │
              │ Schedule API    │           │ Evidence API    │
              │ Activity API    │           │ Processing API  │
              └────────┬────────┘           └────────┬────────┘
                       │                              │
                       └──────────────┬───────────────┘
                                      │
                  ┌───────────────────┼───────────────────┐
                  ▼                   ▼                   ▼
           ┌──────────────┐    ┌──────────────┐   ┌──────────────┐
           │  PostgreSQL  │    │    Redis     │   │Message Queue │
           │              │    │              │   │              │
           │ Project Data │    │    Cache     │   │  Background  │
           │  Activities  │    │  Real-Time   │   │  Processing  │
           │   Evidence   │    │   Updates    │   │     Jobs     │
           └──────────────┘    └──────────────┘   └──────┬───────┘
                                                          │
                                                          ▼
                                               ┌──────────────────┐
                                               │  AI / OCR WORKER │
                                               │                  │
                                               │ • Text Extraction│
                                               │ • OCR Processing │
                                               │ • Activity Match │
                                               │ • Data Structure │
                                               └─────────┬────────┘
                                                          │
                                                          ▼
                                                VERIFIED PROJECT
                                                    PROGRESS
```

---

## ⚙️ How It Works

### 1️⃣ Upload the Project Schedule

The project manager uploads the planned schedule containing:

- Activity ID
- Activity Name
- WBS
- Location
- Planned Start Date
- Planned Finish Date
- Planned Quantity

| Activity ID | Activity | Planned Dates |
|---|---|---|
| `EXC-C-101` | Excavation — Section C | 10–14 August |
| `FDN-B-023` | Foundation — Block B | 15–20 August |
| `MECH-204` | Install Pump P-104 | 15–20 August |

### 2️⃣ Upload Field Evidence

Site engineers and supervisors submit updates through PDFs, Excel/CSV files, text reports, images, or scanned documents.

> *"Foundation work completed today. 120 cubic metres concrete poured. Block B reinforcement still pending."*

### 3️⃣ Intelligent Data Capture

The AI processing layer extracts structured, useful project information from unstructured input:

```yaml
Activity:      Foundation Work
Location:      Block B
Quantity:      120 m³
Status:        In Progress
Pending Work:  Reinforcement
```

### 4️⃣ Intelligent Schedule Linking

FieldLine compares the extracted information with the planned project schedule and finds the best match.

```text
Field Report:
"Pump P104 installation started."
              ↓
       Schedule Matching
              ↓
   Activity ID:  MECH-204
   Activity:     Install Pump P-104
   Confidence:   94%
```

### 5️⃣ Human Review

AI-generated results are always reviewed by a human before they update verified project data:

```text
AI Extraction
      │
      ▼
Schedule Match
      │
      ▼
Confidence Score
      │
      ▼
┌──────────────────┐
│ ✅ Confirm         │
│ ✏️ Edit            │
│ ❌ Reject          │
└──────────────────┘
      │
      ▼
Verified Project Data
```

---

## 📊 Planned vs. Actual Progress

FieldLine continuously compares planned progress against actual site execution.

**Foundation — Block B**

| Metric | Value |
|---|---|
| Planned Progress | 80% |
| Actual Progress | 65% |
| Variance | −15% |
| Status | 🔴 **DELAYED** |

This helps project managers instantly identify:

| Indicator | Meaning |
|---|---|
| 🟢 | Completed activities |
| 🔵 | Activities on track |
| 🟡 | Activities at risk |
| 🔴 | Delayed activities |

---

## 💻 Frontend

The frontend provides the primary interface for interacting with the FieldLine platform.

**Features**
- Project Dashboard
- Schedule Upload
- Evidence Upload
- CSV & Excel Processing
- AI Extraction Results
- Activity Matching
- Planned vs. Actual Progress
- Delay Detection
- Activity Detail View
- Source Evidence Traceability
- AI Review & Confirmation

**Technologies**

`React` · `TypeScript` · `Vite` · `React Router` · `SheetJS` · `PapaParse` · `Lucide Icons`

---

## ⚙️ Backend Infrastructure

The backend is designed for scalable project data processing and real-time updates.

**Core Components**

`Node.js` · `TypeScript` · `PostgreSQL` · `Redis` · `Message Queue` · `Docker` · `Docker Compose` · `Nginx` · `WebSockets`

**Responsibilities**
- Schedule Management
- Activity Management
- Evidence Processing
- Background Job Processing
- Database Operations
- Caching
- Real-Time Updates
- AI & OCR Processing Integration

```text
       [Client / Frontend]
               │
        (HTTP / WebSockets)
               ▼
     [ Nginx Reverse Proxy ]
               │
       ┌───────┴───────┐
       ▼               ▼
 [ Node.js API 1 ] [ Node.js API 2 ]   ← Horizontal Scaling
       │               │
       ├───────────────┼───────────────┐
       ▼               ▼               ▼
 [ PostgreSQL ]    [  Redis  ]   [ Message Queue ]
  (Relational)     (Cache)       (Background Jobs)
```

---

## 📁 Project Structure

```text
FieldLine/
│
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
│
├── backend/
│   ├── src/
│   ├── package.json
│   └── Dockerfile
│
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js (LTS)
- Docker & Docker Compose
- Git

### Run the Frontend

```bash
cd frontend
npm install
npm run dev
```

### Run the Full Project with Docker

```bash
docker-compose up --build
```

---

## 🎯 Smart India Hackathon

| Detail | Description |
|---|---|
| **Problem Statement ID** | SIH26122 |
| **Problem Statement Title** | Intelligent Data Capture & Schedule-Linking Layer for Infrastructure Project Management: Real-Time Actual Progress Tracking (Planning-to-Execution Bridge) |
| **Theme** | Smart Automation |
| **Category** | Software |

---

## 👥 Team

**Team Name:** AI Builders

| Role | Responsibility |
|---|---|
| 🎨 Frontend Developer | UI, Dashboard, Upload System, AI Review |
| 🔧 Backend Developer | APIs, Database, Redis, Queue, WebSockets |
| 🤖 AI/ML Developer | OCR, Data Extraction, Activity Matching |
| 🐳 DevOps / Database | Docker, Deployment, Database Infrastructure |

---

## 🔮 Future Scope

- 🎙️ Voice-based field reporting
- 📱 Mobile application for site engineers
- 💬 Conversational project assistant
- 📈 Advanced analytics dashboard
- 🔔 Real-time risk notifications
- 📍 Location-based activity tracking
- 🔮 Predictive delay analysis
- ✅ Role-based approval workflow

---

## 🏆 Vision

> **FieldLine transforms scattered field evidence into a structured, traceable, and real-time picture of infrastructure project execution.**

<div align="center">

---

Made with ❤️ by **Team AI Builders** for Smart India Hackathon 2026

</div>
