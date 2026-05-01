# 💰 WealthTrack — Family Portfolio Tracker

A **self-contained, zero-backend** wealth tracker for couples managing assets across multiple countries and currencies. Tracks progress toward a **₹100 Cr retirement goal** with snapshots, projections, and what-if scenarios.

## ✨ Features

| Feature | Details |
|---|---|
| 🔐 Auth | Sign up / Sign in with 5-step onboarding |
| 👫 Dual profiles | Full profile for both partners (DOB, country, occupation, income) |
| 💱 Multi-currency | INR, USD, SGD with live-editable exchange rates |
| 📊 Dashboard | Overview, breakdown by owner, charts, goal bar |
| 🎯 Goal tracking | Real-time progress toward ₹100 Cr retirement |
| 🔮 Projections | Compound growth calculator with sliders |
| 🤔 What-if | Sell assets, market moves, FX sensitivity |
| 📸 Snapshots | Save portfolio state over time, chart history |
| 💾 Savings plan | Monthly target calculator with A/B split |
| ☁️ Drive export | Downloads 2 CSVs (portfolio + tracking history) to save in Google Drive |
| 📤 Import CSV | Load your own spreadsheet CSV directly |

---

## 🚀 Deploy in 2 minutes (GitHub Pages)

### 1. Fork or clone

```bash
git clone https://github.com/YOUR_USERNAME/wealth-tracker.git
cd wealth-tracker
```

### 2. Enable GitHub Pages

Go to **Settings → Pages → Source: main branch / root folder** → Save.

Your app will be live at:
```
https://YOUR_USERNAME.github.io/wealth-tracker/login.html
```

### 3. Share with your partner

Just send the link. Each person signs up with their own email — profiles are stored in the browser's `localStorage`.

---

## 📁 File structure

```
wealth-tracker/
├── index.html        ← Main dashboard (requires login)
├── login.html        ← Sign in page
├── signup.html       ← 5-step onboarding form
└── README.md
```

---

## ☁️ Google Drive integration

WealthTrack does **not** use a cloud database. Instead, it downloads two CSVs to your device — you drag them into a shared Google Drive folder yourself.

### How to use Drive sync:

1. Create a shared folder: `Google Drive → New Folder → "WealthTrack"`
2. Share it with your partner
3. Click **☁ Save to Drive** in the app header
4. Two files download automatically:
   - `wealthtrack-portfolio-YYYY-MM-DD.csv` — full portfolio snapshot with profile
   - `wealthtrack-tracking-history-YYYY-MM-DD.csv` — time series of all snapshots
5. Drag both files into your Google Drive folder

### Load partner's data:

1. Partner downloads their CSV from Drive
2. Go to **Import / Export → Import from CSV**
3. Upload the assets CSV to merge

---

## 📋 CSV formats

### Portfolio CSV (auto-generated)
```
## HOUSEHOLD PROFILE
field,person_a,person_b
"Name","Priya Sharma","Raj Sharma"
...

## ASSETS
name,owner,type,currency,value,institution,value_inr
"Chase Checking","Person A","Bank Account","USD","8000","Chase","668000"
...

## SUMMARY
metric,value_inr,value_display
"Total Portfolio","45000000","₹4.50 Cr"
```

### Assets import CSV
Your CSV must have these columns (header row required):

| Column | Required | Values |
|---|---|---|
| `name` | ✅ | Any text |
| `owner` | ✅ | `Person A`, `Person B`, or `Joint` |
| `type` | — | `Bank Account`, `Retirement Plan`, `Stocks / Brokerage`, `Real Estate`, `Mutual Fund`, `Fixed Deposit`, `Other` |
| `currency` | ✅ | `INR`, `USD`, or `SGD` |
| `value` | ✅ | Number (no commas) |
| `institution` | — | Any text |

**Example:**
```csv
name,owner,type,currency,value,institution
Chase Checking,Person A,Bank Account,USD,8000,Chase
HDFC Savings,Person B,Bank Account,INR,800000,HDFC
House equity,Joint,Real Estate,INR,8500000,—
```

---

## 🔐 Authentication notes

- Credentials are stored in `localStorage` (browser-only, no server)
- Passwords are base64-encoded (not production-grade — see below)
- Sessions live in `sessionStorage` (cleared on tab close)
- For production security, replace with a real auth provider (see below)

### 🔒 Production upgrade path

For real security, replace the localStorage auth with one of:

| Provider | Free tier | Setup |
|---|---|---|
| [Supabase](https://supabase.com) | Yes | Drop-in Postgres + Auth |
| [Firebase Auth](https://firebase.google.com) | Yes | Google-backed, easy |
| [Clerk](https://clerk.com) | Yes | Best DX, social logins |
| [Auth0](https://auth0.com) | Yes | Enterprise-grade |

---

## 🛠️ Local development

No build step needed. Just open with any static file server:

```bash
# Python
python3 -m http.server 3000

# Node
npx serve .

# VS Code
# Install "Live Server" extension → right-click index.html → Open with Live Server
```

Then visit `http://localhost:3000/login.html`

---

## 📈 Roadmap

- [ ] Google OAuth + real Drive API (auto-upload without download)
- [ ] Supabase backend for multi-device sync
- [ ] PWA / installable app
- [ ] Real-time exchange rates (via ExchangeRate-API)
- [ ] Mobile app (Capacitor)
- [ ] Shared link to view partner's portfolio read-only

---

## 📄 License

MIT — use freely, modify as you like.
