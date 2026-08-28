<div align="center">
<img src="https://raw.githubusercontent.com/lucide-icons/lucide/main/icons/bar-chart-3.svg" width="80" height="80" alt="FieldLine Logo">
🏗️ FieldLine
Intelligent Data Capture & Schedule-Linking Layer for Infrastructure Project Management
Real-Time Actual Progress Tracking — Planning-to-Execution Bridge
https://sih.gov.in
https://sih.gov.in






</div>
🎯 The Problem
Large infrastructure projects — refineries, pipelines, bridges, roads, industrial facilities — are planned using Primavera P6, Microsoft Project, or Excel schedules.
But actual site progress is reported through messy, unstructured documents:
📄 PDF reports
📊 Excel / CSV files
📝 Free-text progress updates
🖼️ Site images
📋 Scanned documents
✍️ Handwritten site diaries
The gap: A supervisor writes "Pump P104 installation started yesterday. Base plate installed, motor alignment pending."
A normal database cannot understand which planned schedule activity this belongs to.
Project managers spend hours manually reconciling field updates with the master schedule.
💡 Our Solution
FieldLine is an AI-powered bridge between project planning and actual site execution.
plain
┌─────────────────────────────────────────────────────────────┐
│                      FIELDLINE PIPELINE                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   📋 PLANNED SCHEDULE          📂 FIELD EVIDENCE            │
│   (Primavera / Excel)          (Reports / Images / PDFs)    │
│          │                              │                   │
│          ▼                              ▼                   │
│   ┌──────────────┐              ┌──────────────┐           │
│   │  Schedule    │              │  Intelligent │           │
│   │  Database    │              │  AI Capture  │           │
│   └──────┬───────┘              └──────┬───────┘           │
│          │                              │                   │
│          └──────────────┬───────────────┘                   │
│                         ▼                                   │
│              ┌──────────────────┐                          │
│              │ Schedule Linking │                          │
│              │  + Confidence    │                          │
│              └────────┬─────────┘                          │
│                       ▼                                     │
│              ┌──────────────────┐                          │
│              │  Human Review    │                          │
│              └────────┬─────────┘                          │
│                       ▼                                     │
│              ┌──────────────────┐                          │
│              │ Verified Project │                          │
│              │     Status       │                          │
│              └──────────────────┘                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
✨ Key Features
Table
Feature	Description
📤 Schedule Upload	Import planned schedules from CSV, Excel, or Primavera exports
🤖 AI Data Capture	Extract structured project data from PDFs, images, text, and scanned documents
🔗 Intelligent Schedule Linking	Automatically match field reports to planned activities with confidence scores
👁️ Human Review	Review, edit, or reject AI matches before updating verified project data
📊 Planned vs Actual	Real-time progress comparison with variance detection
⚠️ Delay Detection	Automatic identification of delayed, at-risk, and ahead-of-schedule activities
🔍 Evidence Traceability	Every project status is traceable back to its original source evidence
🗣️ Voice Reporting (Future)	Field engineers report progress naturally through voice
🏗️ System Architecture
plain
                    ┌──────────────────────────────┐
                    │      CLIENT / FRONTEND       │
                    │   React + TypeScript + Vite  │
                    │                              │
                    │  • Dashboard                 │
                    │  • Schedule Upload           │
                    │  • Evidence Upload           │
                    │  • AI Review Interface       │
                    │  • Activity Detail View      │
                    └──────────────┬───────────────┘
                                   │
                          HTTP / WebSockets
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │    NGINX REVERSE PROXY       │
                    └──────────────┬───────────────┘
                                   │
              ┌────────────────────┴────────────────────┐
              │                                         │
              ▼                                         ▼
    ┌─────────────────────┐                 ┌─────────────────────┐
    │   Node.js API 1     │                 │   Node.js API 2     │
    │                     │                 │                     │
    │  • Schedule API     │                 │  • Evidence API     │
    │  • Activity API     │                 │  • Processing API   │
    └──────────┬──────────┘                 └──────────┬──────────┘
               │                                       │
               └───────────────────┬───────────────────┘
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
        ▼                          ▼                          ▼
┌───────────────┐      ┌───────────────┐      ┌───────────────┐
│  PostgreSQL   │      │    Redis      │      │ Message Queue │
│               │      │               │      │               │
│ • Project     │      │ • Feed Cache  │      │ • Background  │
│   Data        │      │ • Real-Time   │      │   Processing  │
│ • Activities  │      │   Updates     │      │   Jobs        │
│ • Evidence    │      │               │      │               │
└───────┬───────┘      └───────────────┘      └───────┬───────┘
        │                                              │
        │                                              ▼
        │                                   ┌──────────────────┐
        │                                   │  AI / OCR WORKER │
        │                                   │                  │
        │                                   │ • Text Extract   │
        │                                   │ • OCR Process    │
        │                                   │ • Activity Match │
        │                                   │ • Data Structure │
        │                                   └────────┬─────────┘
        │                                            │
        └────────────────────────────────────────────┘
                          │
                          ▼
                 VERIFIED PROJECT
                     PROGRESS
🎬 How It Works
1️⃣ Upload the Project Schedule
The manager uploads the planned schedule containing:
Table
Field	Example
Activity ID	EXC-C-101
Activity Name	Excavation — Section C
WBS	1.2.3
Location	Block C, Pipeline Route
Planned Start	2026-08-10
Planned End	2026-08-14
Planned Quantity	500 m³
2️⃣ Upload Field Evidence
Site engineers submit updates through:
plain
📄 PDF Documents    📊 Excel / CSV    🖼️ Site Images
📝 Text Reports     ✍️ Scanned Docs   🎤 Voice Notes (Future)
Example field report:
"Foundation work completed today. 120 cubic metres concrete poured. Block B reinforcement still pending."
3️⃣ Intelligent Data Capture
The AI extracts structured information:
JSON
{
  "activity": "Foundation Work",
  "location": "Block B",
  "quantity": "120 m³",
  "status": "In Progress",
  "pending": "Reinforcement"
}
4️⃣ Schedule Linking
FieldLine matches the report to the planned schedule:
plain
Field Report: "Pump P104 installation started."
              │
              ▼
       AI Schedule Matching
              │
              ▼
┌─────────────────────────────────────┐
│  Activity ID: MECH-204              │
│  Activity: Install Pump P-104       │
│  Location: Pump House, Unit 2       │
│  Confidence: 94%                    │
│  Status: In Progress (40%)          │
└─────────────────────────────────────┘
5️⃣ Human Review
Before updating verified project data, managers can:
✅ Confirm — Accept the AI match
✏️ Edit — Adjust the linked activity or extracted data
❌ Reject — Discard incorrect matches
6️⃣ Real-Time Project Status
Table
Activity	Planned	Actual	Variance	Status
Excavation — Section C	100%	100%	0%	✅ Completed
Foundation — Block B	80%	65%	-15%	🔴 Delayed
Install Pump P-104	100%	40%	-60%	🔴 Delayed
Pipeline Welding — Sec A	95%	110%	+15%	🟢 Ahead
Reinforcement — Block B	30%	0%	-30%	🟡 At Risk
🛠️ Tech Stack
Frontend
Table
Technology	Purpose
React 18	UI framework
TypeScript	Type safety
Vite	Build tool & dev server
React Router	Client-side routing
Lucide React	Icon library
SheetJS / PapaParse	CSV & Excel processing
Backend
Table
Technology	Purpose
Node.js	Runtime environment
TypeScript	Type-safe APIs
Express	Web framework
PostgreSQL	Relational database
Redis	Caching & real-time feeds
Message Queue	Background job processing
Nginx	Reverse proxy & load balancing
Docker	Containerization
AI / Processing
Table
Technology	Purpose
OCR	Text extraction from images & scans
NLP	Natural language understanding
Confidence Scoring	Match reliability assessment
Rule-Based Logic	Deterministic progress calculations
📁 Project Structure
plain
FieldLine/
│
├── 📂 frontend/                 # React + TypeScript + Vite
│   ├── 📂 src/
│   │   ├── 📂 components/       # Reusable UI components
│   │   │   ├── ActivityCard.tsx
│   │   │   ├── ConfidenceBar.tsx
│   │   │   ├── EvidenceViewer.tsx
│   │   │   ├── Header.tsx
│   │   │   ├── ProgressBar.tsx
│   │   │   └── StatusBadge.tsx
│   │   ├── 📂 pages/            # Route-level pages
│   │   │   ├── Dashboard.tsx
│   │   │   ├── Upload.tsx
│   │   │   └── ActivityDetail.tsx
│   │   ├── 📂 types/            # TypeScript interfaces
│   │   ├── 📂 utils/            # Helpers & mock data
│   │   ├── App.tsx
│   │   ├── index.css
│   │   └── main.tsx
│   ├── 📂 public/
│   ├── package.json
│   ├── vite.config.ts
│   └── tsconfig.json
│
├── 📂 backend/                  # Node.js + Express API
│   ├── 📂 src/
│   │   ├── 📂 routes/
│   │   ├── 📂 controllers/
│   │   ├── 📂 models/
│   │   ├── 📂 services/
│   │   ├── 📂 workers/
│   │   └── app.ts
│   ├── package.json
│   ├── Dockerfile
│   └── tsconfig.json
│
├── 📄 docker-compose.yml        # Full stack orchestration
├── 📄 .env.example              # Environment template
├── 📄 .gitignore
└── 📄 README.md                 # You are here!
🚀 Getting Started
Prerequisites
Node.js >= 18
npm or yarn
Docker (for full stack)
Option 1: Run Frontend Only
bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME

# Navigate to frontend
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
Open http://localhost:3000 in your browser.
Option 2: Run Full Stack with Docker
bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME

# Start all services
# (PostgreSQL, Redis, Backend APIs, Frontend)
docker-compose up --build
Access the application at http://localhost:80
🧪 Demo Data
The frontend includes realistic mock data for demonstration:
Table
Activity	Status	Actual	Planned	Confidence
Excavation — Section C	✅ Completed	100%	100%	95%
Foundation Work — Block B	🔴 Delayed	65%	80%	88%
Reinforcement — Block B	🟡 At Risk	0%	30%	—
Concrete Pouring — Block B	🔵 On Track	0%	0%	—
Install Pump P-104	🔴 Delayed	40%	100%	92%
Pipeline Welding — Section A	🟢 Ahead	110%	95%	90%
🎨 UI Highlights
Dashboard
📊 Real-time stats cards (overall progress, delayed count, ahead count)
⚠️ Automatic delayed activity alerts
🔍 Status filters + search
📋 Activity cards with progress bars & confidence scores
Upload
📤 Drag-and-drop schedule upload (CSV / Excel)
📂 Multi-file field report upload (PDF, images, text, scans)
📋 Live CSV preview with validation
🤖 Simulated AI processing with loading state
Activity Detail
📈 Large dual progress bar (actual vs planned)
📅 Planned start / end dates
📏 Quantity breakdown (planned / actual / remaining)
🎯 AI confidence score with color coding
🔗 Traceable source evidence — every status links back to original documents
🔮 Future Scope
[ ] 🎤 Voice-based field reporting — Engineers report progress naturally
[ ] 📱 Mobile application — Native app for site engineers
[ ] 🤖 Conversational project assistant — Ask questions about project status
[ ] 📊 Advanced analytics dashboard — Visual monitoring across all dimensions
[ ] 🔔 Real-time risk notifications — Push alerts for delays and risks
[ ] 📍 Location-based tracking — GPS-tagged activity updates
[ ] 🔮 Predictive delay analysis — AI-powered delay forecasting
[ ] 👥 Role-based approval workflow — Multi-level review and sign-off
🏆 Smart India Hackathon 2026
<div align="center">
Table
Problem Statement ID	SIH26122
Problem Statement Title	Intelligent Data Capture & Schedule-Linking Layer for Infrastructure Project Management: Real-Time Actual Progress Tracking (Planning-to-Execution Bridge)
Theme	Smart Automation
Category	Software
Organization	Oil India Limited
</div>
👥 Team AI Builders
Table
Role	Responsibility
Frontend Developer	UI, Dashboard, Upload System, AI Review Interface
Backend Developer	APIs, Database, Redis, Queue, WebSockets
AI / ML Developer	OCR, Data Extraction, Activity Matching
DevOps / Database	Docker, Deployment, Database Infrastructure
📄 License
This project was developed for Smart India Hackathon 2026 under Problem Statement SIH26122.
<div align="center">
🏗️ FieldLine — Transforming scattered field evidence into a clear, traceable picture of project execution.
⬆ Back to Top
</div>
