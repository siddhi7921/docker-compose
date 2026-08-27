# 🚧 FieldLine

### Intelligent Data Capture & Schedule-Linking Layer for Infrastructure Project Management

**Smart India Hackathon 2026 | Problem Statement: SIH26122**

> FieldLine is an AI-powered planning-to-execution bridge for infrastructure projects. It captures messy field updates from documents and reports, converts them into structured project information, links them with planned schedule activities, and helps managers track actual progress, delays, and project risks.

---

## 🧠 The Problem

Large infrastructure projects such as refineries, pipelines, bridges, roads, and industrial facilities are planned using tools such as Primavera P6, Microsoft Project, Excel, or CSV-based schedules.

However, actual site progress is often reported through:

- PDF reports
- Excel and CSV files
- Free-text progress updates
- Site images
- Scanned documents
- Handwritten site diaries

Project managers must manually read these reports and compare them with the planned schedule.

For example, a supervisor may write:

> "Pump P104 installation started yesterday. Base plate installed, motor alignment pending."

A normal database cannot automatically understand which planned schedule activity this update belongs to.

---

## 💡 Our Solution

FieldLine acts as an intelligent bridge between **project planning** and **actual site execution**.

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
🏗️ System Architecture
                         ┌──────────────────────────┐
                         │   FIELDLINE FRONTEND     │
                         │  React + TypeScript      │
                         │                          │
                         │ • Dashboard              │
                         │ • Schedule Upload        │
                         │ • Evidence Upload        │
                         │ • AI Review              │
                         │ • Activity Details       │
                         └────────────┬─────────────┘
                                      │
                              HTTP / WebSockets
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │   NGINX REVERSE PROXY    │
                         └────────────┬─────────────┘
                                      │
                       ┌──────────────┴──────────────┐
                       ▼                             ▼
              ┌─────────────────┐           ┌─────────────────┐
              │  Node.js API 1 │           │  Node.js API 2 │
              │                 │           │                 │
              │ Schedule API    │           │ Evidence API    │
              │ Activity API    │           │ Processing API  │
              └────────┬────────┘           └────────┬────────┘
                       │                             │
                       └──────────────┬──────────────┘
                                      │
                  ┌───────────────────┼───────────────────┐
                  ▼                   ▼                   ▼
           ┌──────────────┐    ┌──────────────┐   ┌──────────────┐
           │ PostgreSQL   │    │ Redis        │   │ Message Queue│
           │              │    │              │   │              │
           │ Project Data │    │ Cache        │   │ Background   │
           │ Activities   │    │ Real-Time    │   │ Processing   │
           │ Evidence     │    │ Updates      │   │ Jobs         │
           └──────────────┘    └──────────────┘   └──────┬───────┘
                                                          │
                                                          ▼
                                               ┌──────────────────┐
                                               │  AI / OCR WORKER │
                                               │                  │
                                               │ • Text Extraction│
                                               │ • OCR Processing │
                                               │ • Activity Match │
                                               │ • Data Structuring│
                                               └─────────┬────────┘
                                                         │
                                                         ▼
                                                VERIFIED PROJECT
                                                    PROGRESS
⚙️ How It Works
1. Upload the Project Schedule

The project manager uploads the planned schedule containing:

Activity ID
Activity Name
WBS
Location
Planned Start Date
Planned Finish Date
Planned Quantity

Example:

Activity ID	Activity	Planned Dates
EXC-C-101	Excavation — Section C	10–14 August
FDN-B-023	Foundation — Block B	15–20 August
MECH-204	Install Pump P-104	15–20 August
2. Upload Field Evidence

Site engineers and supervisors can submit project updates through:

PDF documents
Excel files
CSV files
Text reports
Images
Scanned documents

Example:

"Foundation work completed today. 120 cubic metres concrete poured. Block B reinforcement still pending."

3. Intelligent Data Capture

The AI processing layer extracts useful project information.

Activity: Foundation Work
Location: Block B
Quantity: 120 m³
Status: In Progress
Pending Work: Reinforcement
4. Intelligent Schedule Linking

FieldLine compares the extracted information with the planned project schedule.

Field Report:
"Pump P104 installation started."

              ↓

       Schedule Matching

              ↓

Activity ID: MECH-204
Activity: Install Pump P-104
Confidence: 94%
5. Human Review

AI-generated results can be reviewed before updating verified project information.

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
│ Confirm          │
│ Edit             │
│ Reject           │
└──────────────────┘
      │
      ▼
Verified Project Data
📊 Planned vs Actual Progress

FieldLine compares planned progress with actual site execution.

Foundation — Block B

Planned Progress: 80%
Actual Progress: 65%

Variance: -15%

Status: DELAYED

This helps managers identify:

🟢 Completed activities
🔵 Activities on track
🟡 Activities at risk
🔴 Delayed activities
💻 Frontend

The frontend provides the main interface for interacting with the FieldLine platform.

Features
Project Dashboard
Schedule Upload
Evidence Upload
CSV and Excel Processing
AI Extraction Results
Activity Matching
Planned vs Actual Progress
Delay Detection
Activity Detail View
Source Evidence Traceability
AI Review and Confirmation
Technologies
React
TypeScript
Vite
React Router
SheetJS
PapaParse
Lucide Icons
⚙️ Backend Infrastructure

The backend is designed to support scalable project data processing and real-time updates.

Core Components
Node.js
TypeScript
PostgreSQL
Redis
Message Queue
Docker
Docker Compose
Nginx
WebSockets
Responsibilities
Schedule Management
Activity Management
Evidence Processing
Background Job Processing
Database Operations
Caching
Real-Time Updates
AI and OCR Processing Integration
🔄 Complete Data Flow
SITE ENGINEER / SUPERVISOR
            │
            │ Upload Report
            ▼
┌────────────────────────────┐
│     FIELDLINE FRONTEND     │
└──────────────┬─────────────┘
               │
               ▼
┌────────────────────────────┐
│        NODE.JS API         │
└──────────────┬─────────────┘
               │
               ▼
┌────────────────────────────┐
│       MESSAGE QUEUE        │
└──────────────┬─────────────┘
               │
               ▼
┌────────────────────────────┐
│       AI / OCR WORKER      │
│                            │
│ Extracts:                  │
│ • Activity                 │
│ • Location                 │
│ • Quantity                 │
│ • Status                   │
│ • Issues                   │
└──────────────┬─────────────┘
               │
               ▼
┌────────────────────────────┐
│      SCHEDULE MATCHING     │
└──────────────┬─────────────┘
               │
               ▼
┌────────────────────────────┐
│     HUMAN / AI REVIEW      │
└──────────────┬─────────────┘
               │
               ▼
     VERIFIED PROJECT DATA
               │
               ▼
       PROJECT DASHBOARD
📁 Project Structure
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
🚀 Getting Started
Clone the Repository
git clone https://github.com/siddhi7921/docker-compose.git
cd docker-compose
Run the Frontend
cd frontend
npm install
npm run dev
Run the Full Project with Docker
docker-compose up --build
🎯 Smart India Hackathon

Problem Statement ID: SIH26122

Problem Statement Title:

Intelligent Data Capture & Schedule-Linking Layer for Infrastructure Project Management: Real-Time Actual Progress Tracking (Planning-to-Execution Bridge)

Theme: Smart Automation

Category: Software

👥 Team
Team Name: AI Builders
Role	Responsibility
Frontend Developer	UI, Dashboard, Upload System, AI Review
Backend Developer	APIs, Database, Redis, Queue, WebSockets
AI/ML Developer	OCR, Data Extraction, Activity Matching
DevOps / Database	Docker, Deployment, Database Infrastructure
🔮 Future Scope
Voice-based field reporting
Mobile application for site engineers
Conversational project assistant
Advanced analytics dashboard
Real-time risk notifications
Location-based activity tracking
Predictive delay analysis
Role-based approval workflow
🏆 Vision

FieldLine transforms scattered field evidence into a structured, traceable, and real-time picture of infrastructure project execution.
