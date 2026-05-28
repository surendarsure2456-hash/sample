# 🏪 New Krishna Sweets — Smart Billing System

> **Powered by Sai Shuru Nexus**

A full-stack mobile-first billing system with MongoDB backend, React frontend, smart QR customer portal, analytics dashboard, and PDF/JPG download.

---

## 📁 Project Structure

```
nks-billing/
├── backend/
│   ├── server.js          ← Express + MongoDB API
│   ├── package.json
│   └── .env.example       ← Copy to .env and fill MongoDB URI
│
└── frontend/
    ├── src/
    │   ├── App.jsx        ← Full React app
    │   └── main.jsx       ← Entry point
    ├── index.html
    ├── package.json
    └── vite.config.js
```

---

## 🚀 Setup Instructions

### 1. MongoDB Atlas (Database)

1. Go to [https://cloud.mongodb.com](https://cloud.mongodb.com) and create a free account
2. Create a new **Cluster** (free M0 tier)
3. Under **Database Access** → Add user (username + password)
4. Under **Network Access** → Allow from anywhere (`0.0.0.0/0`)
5. Click **Connect** → **Drivers** → Copy the connection string

It looks like:
```
mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/nks_billing?retryWrites=true&w=majority
```

---

### 2. Backend Setup

```bash
cd nks-billing/backend

# Install dependencies
npm install

# Create .env file
cp .env.example .env
# Edit .env and paste your MongoDB URI:
# MONGO_URI=mongodb+srv://...

# Start server
npm start
# or for development with auto-reload:
npm run dev
```

Server runs on: `http://localhost:5000`

---

### 3. Frontend Setup

```bash
cd nks-billing/frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

App runs on: `http://localhost:3000`

---

## 🔐 Login

| Role     | URL                        | Password   |
|----------|----------------------------|------------|
| Staff    | `http://localhost:3000/`   | `nks2026`  |
| Customer | `http://localhost:3000/customer` | *(no password)* |

---

## 📱 Bill Number Format

```
NKS-YYYYMMDD-XXXX
     │         └── 4-digit unique number (e.g. 3456)
     └── Date (e.g. 20260526)

Example: NKS-20260526-3456
```

**Customer flow:**
1. Customer scans shop QR code → opens `/customer` page
2. Enters only the **last 4 digits** (e.g. `3456`)
3. Today's date is auto-prefixed: `NKS-20260526-3456`
4. Bill appears with download options (JPG / PDF / Print / Share)

---

## 🌐 API Endpoints

### Categories
| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/categories` | Get all categories |
| POST | `/api/categories` | Add new category `{label, emoji, color}` |
| DELETE | `/api/categories/:id` | Delete category (and its products) |

### Products
| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/products` | Get all products grouped by category |
| POST | `/api/products` | Add product `{name, ta, price, unit, catId}` |
| DELETE | `/api/products/:id` | Delete product |

### Bills
| Method | Route | Description |
|--------|-------|-------------|
| POST | `/api/bills` | Create bill `{items, total}` |
| GET | `/api/bills` | Get bills (query: `?filter=today/week/month/all`) |
| GET | `/api/bills/:billId` | Get bill by full ID |
| GET | `/api/bills/lookup/:last4` | Customer lookup by last 4 digits |

### Analytics
| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/analytics/daily?days=7` | Daily sales data for last N days |

---

## 🚀 Deployment

### Deploy Backend (Render / Railway / Heroku)

**Render.com (recommended, free tier):**
1. Push backend to GitHub
2. New Web Service → connect repo → `nks-billing/backend`
3. Build command: `npm install`
4. Start command: `node server.js`
5. Add environment variable: `MONGO_URI=mongodb+srv://...`
6. Note the deployed URL (e.g. `https://nks-billing.onrender.com`)

### Deploy Frontend (Vercel / Netlify)

**Vercel (recommended, free):**
1. Push frontend to GitHub
2. Import project on vercel.com
3. Framework: Vite
4. Add environment variable:
   ```
   VITE_API_URL=https://nks-billing.onrender.com/api
   ```
5. Deploy!

### Physical QR Code

After deploying, your customer portal URL will be:
```
https://your-app.vercel.app/customer
```

Print this URL as a **QR code** using any QR generator (e.g. qr-code-generator.com) and place it at your shop counter. One QR code works for ALL bills forever.

---

## 📲 Customer Portal Features

- Enter **last 4 digits** of bill number
- Today's date is auto-filled as prefix
- ⬇️ **Download JPG** — saves bill as image
- 📄 **Download PDF** — saves bill as A5 PDF
- 🖨️ **Print** — clean print layout
- 📤 **Share** — native share / copy to clipboard

---

## 🧾 Staff Billing App Features

- **Password protected** (password: `nks2026`)
- Select items from 6+ categories
- Click items → weight/qty picker
- Custom weight (e.g. 750g) or custom amount
- Generate bill → auto-saved to MongoDB
- **Bill ID shown** with 4-digit customer code highlighted
- Download / Print / Share from invoice screen
- **Analytics:** Daily bar chart, top items, category breakdown
- **History:** Filter by today/week/month/all, expand bills, download old bills
- **Add Items:** Add new products and categories from within the app

---

## ⚙️ Default Categories

| Category | Emoji | 
|----------|-------|
| Sweets | 🍬 |
| Mixture | 🥨 |
| Cake & Bread | 🍰🍞 |
| Puffs & Roll | 🥐 |
| Ice & Juice | 🍨🍹 |
| Biscuits & Choc | 🍪🍫 |

---

## 🛠 Technologies

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Vite |
| Backend | Node.js + Express |
| Database | MongoDB Atlas + Mongoose |
| PDF | jsPDF |
| Image | html2canvas |
| Styling | Inline styles (mobile-first) |

---

## 📞 Support

**New Krishna Sweets**  
📞 +91 978 968 3468

---

> Powered by **Sai Shuru Nexus**
