# Pharmacast

Pharmacy inventory management with demand forecasting. Pure Python, SQLite, no runtime dependencies.

## Features
- Medicine catalogue with reorder levels
- Batch tracking with expiry dates
- **FEFO** selling (first-expiry-first-out); expired stock is never sold
- Alerts: low stock, expiring soon, expired
- Demand forecasting (exponential smoothing) with safety-stock reorder suggestions

## Setup
```bash
pip install -e ".[dev]"
pytest
```

## Usage
```bash
pharmacast add-medicine Paracetamol --strength 500mg --price 2.5 --reorder-level 20
pharmacast receive Paracetamol B1 200 2027-06-30
pharmacast sell Paracetamol 15
pharmacast stock
pharmacast alerts --days 45
pharmacast forecast Paracetamol --lead-time 7 --cover 30
```

## Layout
```
src/pharmacast/
  db.py         SQLite schema/connection
  inventory.py  stock, FEFO sales, alerts
  forecast.py   demand forecast + reorder maths
  cli.py        argparse command line
tests/          pytest suite
```

## Ideas to extend
FastAPI REST layer, prescriptions & patients, supplier orders, seasonal forecasting (Holt-Winters).
