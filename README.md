# 📊 MT5 Performance Dashboard

A real-time performance monitoring dashboard for MetaTrader 5 trading accounts — tracks live and demo account results, displays per-model metrics, and allows dynamic management of active ML trading models.

---

## 🏗️ Overview

This dashboard is part of the [XGBoost Forex Trading System](https://github.com/hiltontrip/xgboost-forex-system). It connects directly to MT5 accounts via API, ingests trade data in real time, and provides a web interface to monitor and control which ML models are actively trading.

```
MetaTrader 5 Accounts (demo/live)
    │
    │  Trade data via API/webhook
    ▼
┌─────────────────────────────┐
│       report_api.py         │
│  REST API endpoints         │
│  Receives MT5 trade events  │
│  Stores in SQLite           │
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│     report_dashboard.py     │
│  Web dashboard              │
│  Per-model performance      │
│  Model management UI        │
│  Real-time updates          │
└─────────────────────────────┘
             │
             ▼
        Browser UI
  (metrics, charts, controls)
```

---

## ✨ Features

- **Real-time MT5 account monitoring** — connects to multiple demo/live accounts simultaneously
- **Per-model performance metrics:**
  - Net P&L, Return %
  - Sharpe Ratio
  - Max Drawdown ($  and %)
  - Win Rate
  - Profit Factor
  - Average Win / Average Loss
  - Streak Win / Streak Loss
  - Trades per day
- **Model management** — add, remove, or set models to idle directly from the dashboard
- **Magic Number tracking** — each MT5 EA magic number maps to a trained ML model
- **Multi-account support** — view and filter by account
- **Period filtering** — filter metrics by custom date ranges
- **Persistent storage** — SQLite database with automatic backups

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python |
| API | REST (report_api.py) |
| Database | SQLite |
| Dashboard | Python web framework |
| MT5 Integration | MetaTrader 5 API / webhook |
| Infrastructure | Ubuntu VPS |

---

## 📁 Project Structure

```
├── report_dashboard.py     # Main dashboard application
├── report_api.py           # REST API for MT5 data ingestion
├── database.py             # SQLite interface and queries
├── dashboard_prefs.json    # User preferences (visible accounts, layout)
├── mt5report.db            # SQLite database (trade history)
└── modelos.txt             # Model registry reference
```

---

## ⚙️ Configuration

```json
// dashboard_prefs.json
{
  "visible_accounts": ["198223063"],
  "default_period": "2026-01-01/2026-12-31"
}
```

---

## 🚀 Usage

**1. Start the API server**
```bash
python report_api.py
```

**2. Start the dashboard**
```bash
python report_dashboard.py
```

**3. Configure MT5 EA to send trade data**
```
Point your MT5 Expert Advisor webhook URL to:
http://your-server:PORT/api/trade
```

---

## 📊 Dashboard Preview

| Magic | P&L | Trades | Win Rate | Sharpe | Max DD | Status |
|---|---|---|---|---|---|---|
| 15002001 | +$19.25 | 5 | 40.0% | 2.03 | 22.4% | ✅ Active |
| 41731001 | +$15.75 | 3 | 33.3% | 2.59 | 19.8% | ✅ Active |
| 220908002 | +$8.90 | 2 | 50.0% | 4.79 | 3.8% | ✅ Active |
| 191848001 | -$1.18 | 1 | 0.0% | 0.00 | 2.4% | ⏸ Idle |

---

## 👤 Author

**Hilton Paz** — [github.com/hiltontrip](https://github.com/hiltontrip) · [linkedin.com/in/hilton-júnior-b1544927](https://linkedin.com/in/hilton-júnior-b1544927)
