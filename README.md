<div align="center">

# 🚀 Nexus HQ

### Full Stack Management Dashboard

![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?style=for-the-badge&logo=express&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-5-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14+-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)

A production-ready full stack CRUD dashboard for managing **Users**, **Products**, and **Orders** — with live stats, dark/light mode, and a clean REST API.

</div>

---

## ✨ Features

- 📊 **Dashboard** — live stats, revenue, order status charts, stock levels
- 👥 **Users** — full CRUD with roles, status, and avatar initials
- 📦 **Products** — catalog management with auto stock status
- 🧾 **Orders** — order tracking linked to products
- 🔍 **Search** — live search filtering on every table
- 🌙 **Dark / Light mode** — toggle from the sidebar
- ✅ **Toast notifications** — on every create, update, delete
- 🔄 **REST API** — Express + Prisma + PostgreSQL

---

## 🗂 Project Structure

```
nexus-dashboard/
├── backend/
│   ├── prisma/
│   │   └── schema.prisma        # DB schema (User, Product, Order)
│   ├── src/
│   │   ├── routes/
│   │   │   ├── users.js         # CRUD  →  /api/users
│   │   │   ├── products.js      # CRUD  →  /api/products
│   │   │   ├── orders.js        # CRUD  →  /api/orders
│   │   │   └── stats.js         # Stats →  /api/stats
│   │   ├── index.js             # Express entry point
│   │   ├── prisma.js            # Prisma client singleton
│   │   └── seed.js              # Sample data seeder
│   ├── .env.example
│   └── package.json
│
└── frontend/
    ├── src/
    │   ├── App.jsx              # Full dashboard UI (single file)
    │   ├── api.js               # Fetch wrapper for all endpoints
    │   └── main.jsx             # React entry point
    ├── index.html
    ├── vite.config.js           # Vite + proxy to :5000
    └── package.json
```

---

## ⚙️ Prerequisites

Make sure these are installed:

| Tool | Version | Download |
|------|---------|----------|
| Node.js | 18+ | https://nodejs.org |
| PostgreSQL | 14+ | https://postgresql.org/download |
| Git | any | https://git-scm.com |

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/nexus-dashboard.git
cd nexus-dashboard
```

---

### 2. Set up PostgreSQL

**Option A — Local PostgreSQL**

Open `psql` or pgAdmin and run:

```sql
CREATE DATABASE nexus_dashboard;
```

**Option B — Docker** *(no local install needed)*

```bash
docker run --name nexus-pg \
  -e POSTGRES_PASSWORD=yourpassword \
  -e POSTGRES_DB=nexus_dashboard \
  -p 5432:5432 \
  -d postgres:16
```

---

### 3. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create your environment file
cp .env.example .env
```

Edit `.env` and fill in your database credentials:

```env
DATABASE_URL="postgresql://postgres:yourpassword@localhost:5432/nexus_dashboard"
PORT=5000
```

> ⚠️ Replace `yourpassword` with your actual PostgreSQL password.

```bash
# Create database tables
npx prisma migrate dev --name init

# Seed with sample data
npm run db:seed

# Start the API server
npm run dev
```

✅ API running at → `http://localhost:5000`  
🔍 Health check → `http://localhost:5000/api/health`

---

### 4. Frontend Setup

Open a **new terminal**:

```bash
cd frontend

# Install dependencies
npm install

# Start the dev server
npm run dev
```

✅ App running at → `http://localhost:5173`

---

## 🌐 API Reference

### Stats
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/health` | Health check |
| `GET` | `/api/stats` | Dashboard aggregate stats |

### Users `/api/users`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/users` | List all users (supports `?search=`) |
| `GET` | `/api/users/:id` | Get single user |
| `POST` | `/api/users` | Create user |
| `PUT` | `/api/users/:id` | Update user |
| `DELETE` | `/api/users/:id` | Delete user |

### Products `/api/products`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/products` | List all products (supports `?search=&category=`) |
| `GET` | `/api/products/:id` | Get single product |
| `POST` | `/api/products` | Create product |
| `PUT` | `/api/products/:id` | Update product |
| `DELETE` | `/api/products/:id` | Delete product |

### Orders `/api/orders`
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/orders` | List all orders (supports `?search=&status=`) |
| `GET` | `/api/orders/:id` | Get single order |
| `POST` | `/api/orders` | Create order |
| `PUT` | `/api/orders/:id` | Update order |
| `DELETE` | `/api/orders/:id` | Delete order |

---

## 🛠 Useful Commands

```bash
# Open Prisma Studio (visual DB browser)
cd backend && npx prisma studio

# Re-run seed data
cd backend && npm run db:seed

# Reset DB and re-migrate from scratch
cd backend && npx prisma migrate reset

# Build frontend for production
cd frontend && npm run build
```

---

## 🐛 Troubleshooting

<details>
<summary><strong>❌ "Can't connect to database"</strong></summary>

- Make sure PostgreSQL is running
- Double-check `DATABASE_URL` in `.env`
- Confirm the database `nexus_dashboard` exists: `psql -l`

</details>

<details>
<summary><strong>❌ "Port 5432 already in use"</strong></summary>

- Another Postgres instance is running
- Stop it: `sudo service postgresql stop` (Linux/Mac) or via Services (Windows)
- Or change the port in your `DATABASE_URL`

</details>

<details>
<summary><strong>❌ Frontend shows API errors</strong></summary>

- Make sure the backend is running on port `5000`
- Check Vite's proxy config in `frontend/vite.config.js`
- Look at the backend terminal for error messages

</details>

<details>
<summary><strong>❌ "prisma: command not found"</strong></summary>

Use `npx` prefix:

```bash
npx prisma migrate dev --name init
npx prisma studio
```

</details>

---

## 📄 License

MIT — free to use, modify, and distribute.

---

<div align="center">

Made with ☕ and a lot of `console.log`

</div>
