# 🏭 WMS Pro — Warehouse Management System

A full-featured, production-ready **Warehouse Management System (WMS)** built with a **React.js** frontend and **FastAPI** backend, powered by **MongoDB**. It supports end-to-end warehouse operations including inward/outward processing, bin management, stock tracking, role-based access control, and rich analytics.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Local Setup in VS Code](#local-setup-in-vs-code)
- [Environment Variables](#environment-variables)
- [Running the Application](#running-the-application)
- [Default Credentials](#default-credentials)
- [Modules & Roles](#modules--roles)
- [API Overview](#api-overview)
- [Database Collections](#database-collections)
- [Running Tests](#running-tests)
- [Roadmap](#roadmap)

---

## 🧭 Overview

WMS Pro is a warehouse operations platform designed for managing goods receipts, inventory, bin locations, putaway workflows, material issues, label printing, and comprehensive stock reporting — all backed by audit trails and fine-grained role-based access control.

---

## ✨ Features

### Core Modules
- **GRN (Goods Receipt Note)** — Create and process inward goods with batch tracking
- **Material Master** — Full CRUD with FIFO/LIFO inventory strategy support
- **Bin Location Management** — Create, organise, and monitor bin/zone utilisation
- **Putaway Workflow** — Assign and track stock to bin locations
- **Material Issue / Outward** — Process outward movements with approval workflow
- **Label / Sticker Generation** — QR-code sticker printing with reprint log
- **Stock Movement Tracking** — Full history of every movement

### Access Control
- **6 roles**: Admin, Warehouse Operator, Store In-Charge, Inventory Controller, Auditor, Management Viewer
- Route-level and action-level permission enforcement
- Complete **audit trail** for all changes (create/update/delete/role changes)

### Reports (14 Reports across 5 categories)
| Category | Reports |
|----------|---------|
| Inventory | GRN-wise Stock, Batch-wise Stock, Bin-wise Stock, Stock Summary, Stock Reconciliation |
| Movement | Material Movement History, Daily Inward/Outward Summary, Putaway Pending |
| Compliance | FIFO Compliance Report, Non-FIFO Exception Report |
| Stock Analysis | Stock Aging (0–30 / 31–60 / 61–90 / 90+ days), Dead/Slow Moving Stock |
| Audit & Activity | User Activity Log, Reprint Sticker Log |

- Excel & PDF export for all reports
- Date range, material code, batch number, bin code, and zone filters

### Stock Dashboard
- Real-time auto-refresh (every 30 seconds)
- Summary cards: Total Stock, Available, Blocked, Quality Hold, Overstock, Understock
- Interactive charts: Stock by Status (pie), Bin Utilisation (donut), Stock by Category (pie), Stock Aging (bar chart)
- Tabbed detail views: Alerts, Bin Zones, Top Materials, FIFO Status
- Expiring soon alert section

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 19, Tailwind CSS, Radix UI (shadcn/ui), Recharts, Axios |
| **Backend** | FastAPI (Python), Uvicorn |
| **Database** | MongoDB (via Motor async driver) |
| **Auth** | JWT-based local authentication (bcrypt password hashing) |
| **Reports** | openpyxl (Excel), ReportLab (PDF) |
| **Build** | CRACO (Create React App + custom webpack config) |

---

## 📁 Project Structure

```
WAP-PRO-FINAL-main/
│
├── backend/
│   ├── server.py                  # Main FastAPI application (all routes & logic)
│   ├── requirements.txt           # Python dependencies
│   ├── seed_sample_data.py        # Script to seed demo inventory data
│   ├── seed_users.py              # Script to seed demo users
│   ├── setup_solar_manufacturing.py # Industry-specific setup script
│   ├── create_sample_grns.py      # Script to generate sample GRN records
│   └── tests/
│       └── test_fifo_lifo.py      # Unit tests for FIFO/LIFO logic
│
├── frontend/
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── App.js                 # Root component with routing
│   │   ├── App.css
│   │   ├── index.js
│   │   ├── index.css
│   │   ├── components/
│   │   │   ├── Layout.js          # Main app shell (sidebar, navbar)
│   │   │   └── ui/                # shadcn/ui component library
│   │   ├── contexts/
│   │   │   └── AuthContext.js     # Global auth state & JWT management
│   │   ├── hooks/
│   │   │   └── use-toast.js       # Toast notification hook
│   │   ├── lib/
│   │   │   ├── api.js             # Axios API client & all API calls
│   │   │   └── utils.js           # Utility helpers
│   │   └── pages/
│   │       ├── Login.js
│   │       ├── Register.js
│   │       ├── Dashboard.js
│   │       ├── StockDashboard.js
│   │       ├── GRN.js
│   │       ├── Materials.js
│   │       ├── Bins.js
│   │       ├── Putaway.js
│   │       ├── Issues.js
│   │       ├── Labels.js
│   │       ├── Reports.js
│   │       ├── Users.js
│   │       └── AuthCallback.js
│   ├── package.json
│   ├── tailwind.config.js
│   ├── craco.config.js
│   └── components.json            # shadcn/ui config
│
├── memory/
│   └── PRD.md                     # Product Requirements Document
├── backend_test.py                # Integration tests for backend API
├── reports_backend_test.py        # Reports-specific backend tests
├── test_result.md                 # Latest test results
└── test_reports/                  # JSON test iteration reports
```

---

## ✅ Prerequisites

Make sure the following are installed before you begin:

| Tool | Version | Download |
|------|---------|---------|
| **Node.js** | v18 or higher | https://nodejs.org |
| **npm** | v9 or higher | Comes with Node.js |
| **Python** | 3.10 or higher | https://python.org |
| **pip** | Latest | Comes with Python |
| **MongoDB** | v6 or higher | https://www.mongodb.com/try/download/community |
| **Git** | Any | https://git-scm.com |
| **VS Code** | Latest | https://code.visualstudio.com |

---

## 💻 Local Setup in VS Code

### Step 1 — Clone or Extract the Project

If you downloaded the ZIP, extract it. If using git:
```bash
git clone https://github.com/your-username/WAP-PRO-FINAL.git
cd WAP-PRO-FINAL-main
```

Open the folder in VS Code:
```bash
code .
```

---

### Step 2 — Start MongoDB

Make sure MongoDB is running locally on the default port `27017`.

**On Windows:**
```bash
# If installed as a service, it may already be running.
# Otherwise, run:
"C:\Program Files\MongoDB\Server\6.0\bin\mongod.exe"
```

**On macOS (Homebrew):**
```bash
brew services start mongodb-community
```

**On Linux:**
```bash
sudo systemctl start mongod
```

You can verify it's running with:
```bash
mongosh
```

---

### Step 3 — Backend Setup

Open a **new terminal** in VS Code (`Ctrl+`` ` or Terminal → New Terminal`).

```bash
cd backend
```

**Create a virtual environment:**
```bash
python -m venv venv
```

**Activate the virtual environment:**

- Windows (PowerShell):
  ```powershell
  .\venv\Scripts\Activate.ps1
  ```
- Windows (CMD):
  ```cmd
  venv\Scripts\activate.bat
  ```
- macOS / Linux:
  ```bash
  source venv/bin/activate
  ```

**Install dependencies:**
```bash
pip install -r requirements.txt
```

**Create the backend `.env` file:**

Inside the `backend/` folder, create a file named `.env`:

```env
MONGO_URL=mongodb://localhost:27017/wms_pro
JWT_SECRET=your-super-secret-key-change-this
```

> ⚠️ Change `JWT_SECRET` to a strong random string before deploying.

---

### Step 4 — Seed Demo Data (Optional but Recommended)

With the virtual environment still active and inside `backend/`:

```bash
# Create demo users (admin + operator)
python seed_users.py

# Seed sample inventory data
python seed_sample_data.py

# (Optional) Create sample GRN records
python create_sample_grns.py
```

---

### Step 5 — Frontend Setup

Open a **second terminal** in VS Code:

```bash
cd frontend
```

**Install Node dependencies:**
```bash
npm install
```

**Create the frontend `.env` file:**

Inside the `frontend/` folder, create a file named `.env`:

```env
REACT_APP_BACKEND_URL=http://localhost:8001
```

---

## ▶️ Running the Application

You need **two terminals** running simultaneously — one for the backend, one for the frontend.

### Terminal 1 — Start the Backend

```bash
cd backend
source venv/bin/activate    # (or .\venv\Scripts\Activate.ps1 on Windows)
uvicorn server:app --host 0.0.0.0 --port 8001 --reload
```

Backend will be live at: **http://localhost:8001**  
API docs (Swagger UI): **http://localhost:8001/docs**

---

### Terminal 2 — Start the Frontend

```bash
cd frontend
npm start
```

Frontend will open at: **http://localhost:3000**

---

## 🔑 Default Credentials

| Role | Email | Password |
|------|-------|---------|
| Admin | `admin@warehouse.com` | `admin123` |
| Warehouse Operator | `operator@test.com` | `test123` |

> You can create additional users from the **Users** page once logged in as Admin.

---

## 👥 Modules & Roles

| Module | Admin | Warehouse Operator | Store In-Charge | Inventory Controller | Auditor | Mgmt Viewer |
|--------|-------|--------------------|-----------------|----------------------|---------|-------------|
| Dashboard | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ (Stock Dashboard) |
| GRN | ✅ | ✅ | ✅ | 👁️ | 👁️ | ❌ |
| Materials | ✅ (CRUD) | 👁️ | 👁️ | 👁️ | 👁️ | ❌ |
| Bins | ✅ (CRUD) | 👁️ | 👁️ | 👁️ | 👁️ | ❌ |
| Putaway | ✅ | ✅ | ✅ | 👁️ | 👁️ | ❌ |
| Issues | ✅ | ✅ | ✅ (+ approvals) | 👁️ | 👁️ | ❌ |
| Labels | ✅ | ✅ | ✅ | 👁️ | 👁️ | ❌ |
| Reports | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |
| Users | ✅ | ❌ | ❌ | ❌ | 👁️ | ❌ |
| Audit Trail | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ |

> 👁️ = Read-only access

---

## 🔌 API Overview

All API endpoints are prefixed with `/api`. Key endpoint groups:

| Prefix | Description |
|--------|-------------|
| `/api/auth/login` | User login → returns JWT token |
| `/api/auth/register` | Register new user |
| `/api/users` | User CRUD and role management |
| `/api/materials` | Material master CRUD |
| `/api/grn` | GRN creation and processing |
| `/api/bins` | Bin location management |
| `/api/putaway` | Putaway workflow |
| `/api/issues` | Material issue / outward |
| `/api/labels` | Label generation & print log |
| `/api/stock` | Stock inquiry and movements |
| `/api/reports/{report_type}` | All 14 reports with filters |
| `/api/audit-logs` | Full audit trail |

Full interactive docs available at **http://localhost:8001/docs** when the backend is running.

---

## 🗄️ Database Collections

MongoDB database: `wms_pro`

| Collection | Description |
|-----------|-------------|
| `users` | User accounts with roles and status |
| `materials` | Material master with FIFO/LIFO strategy |
| `grn` | Goods Receipt Notes |
| `bins` | Bin/rack location definitions |
| `putaway` | Putaway transaction records |
| `issues` | Material issue (outward) records |
| `stock_movements` | Full stock movement history |
| `labels` | Generated label records |
| `print_logs` | Label reprint audit log |
| `audit_logs` | System-wide audit trail |

---

## 🧪 Running Tests

### Backend Unit Tests (FIFO/LIFO logic)

```bash
cd backend
source venv/bin/activate
pytest tests/test_fifo_lifo.py -v
```

### Backend Integration Tests

From the project root:

```bash
python backend_test.py
python reports_backend_test.py
```

> Make sure the backend server is running on port 8001 before running integration tests.

---

## 🗺️ Roadmap

### High Priority (P1)
- [ ] Purchase Order integration
- [ ] Stock transfer between warehouses
- [ ] Inventory counting / cycle count module
- [ ] Barcode scanner integration

### Medium Priority (P2)
- [ ] Email notifications for low stock alerts
- [ ] Advanced analytics dashboard
- [ ] Multi-warehouse support
- [ ] API documentation improvements

### Future (P3)
- [ ] Mobile app for warehouse operations
- [ ] ERP system integrations
- [ ] AI-powered demand forecasting
- [ ] Voice-guided picking

---

## 📄 License

This project is proprietary. All rights reserved.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

---

> Built with ❤️ for efficient warehouse operations.
