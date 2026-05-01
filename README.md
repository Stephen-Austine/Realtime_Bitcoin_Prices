# Real-Time Data Acquisition and Visualization using Python

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge)
![Requests](https://img.shields.io/badge/Requests-HTTP-FF6B35?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A Python project demonstrating real-time data acquisition from live APIs, continuous CSV logging, and dynamic data visualization using Matplotlib. The project contains two independent scripts — one tracking live Bitcoin prices via the CoinGecko API, and one tracking live temperature data for Nairobi via the OpenWeatherMap API.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Scripts](#scripts)
- [Project Structure](#project-structure)
- [Dependencies](#dependencies)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [How Each Script Works](#how-each-script-works)
- [Output](#output)
- [Possible Extensions](#possible-extensions)

---

## Project Overview

This project covers the full real-time data pipeline:

- **Acquisition** — Fetching live data from public REST APIs at defined intervals
- **Storage** — Appending each reading to a CSV log file as it arrives
- **Visualization** — Plotting the collected time-series data as a line chart with Matplotlib

Both scripts follow the same architectural pattern: fetch → log → wait → repeat, then plot on exit.

---

## Scripts

| File | Data Source | API | Interval | Runs |
|---|---|---|---|---|
| `Realtime-BTC-Tracker-and-Visualizer.py` | Bitcoin price (USD) | CoinGecko (free, no key) | 60 seconds | Indefinitely until `Ctrl+C` |
| `dynamic_data.py` | Nairobi temperature (°C) | OpenWeatherMap | 10 seconds | 10 iterations |

---

## Project Structure

```
Real-Time-Data-Acquisition-and-Visualization/
│
├── Realtime-BTC-Tracker-and-Visualizer.py   # Live Bitcoin price tracker
├── dynamic_data.py                           # Live Nairobi temperature tracker
├── bitcoin_price_log.csv                     # Auto-generated: Bitcoin price log
└── nairobi_temp_log.csv                      # Auto-generated: Temperature log
```

The CSV files are created automatically on first run. They do not need to exist beforehand.

---

## Dependencies

Both scripts use standard and widely available Python libraries:

```
requests
matplotlib
```

The `csv`, `time`, and `datetime` modules are part of the Python standard library and require no installation.

Install the external dependencies with:

```bash
pip install requests matplotlib
```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/Real-Time-Data-Acquisition-and-Visualization.git
cd Real-Time-Data-Acquisition-and-Visualization
```

### 2. Install dependencies

```bash
pip install requests matplotlib
```

### 3. Run the Bitcoin tracker

```bash
python Realtime-BTC-Tracker-and-Visualizer.py
```

The script runs indefinitely, printing a new price every 60 seconds. Press `Ctrl+C` to stop — the chart will render automatically on exit.

### 4. Run the temperature tracker

```bash
python dynamic_data.py
```

This runs for 10 iterations (one reading every 10 seconds), then prints a summary and renders the chart automatically.

---

## Configuration

### Bitcoin Tracker

No API key is required. The CoinGecko free tier is used. You can change the target coin or currency:

```python
COIN = 'bitcoin'       # e.g. 'ethereum', 'solana'
CURRENCY = 'usd'       # e.g. 'eur', 'gbp', 'kes'
```

### Temperature Tracker

An OpenWeatherMap API key is required. Register for a free key at [openweathermap.org](https://openweathermap.org/api) and set it as an environment variable:

```bash
# macOS / Linux
export OPENWEATHER_API_KEY='your_api_key_here'

# Windows
set OPENWEATHER_API_KEY=your_api_key_here
```

The script reads it with:

```python
import os
API_KEY = os.environ.get('OPENWEATHER_API_KEY')
```

You can also change the target city:

```python
CITY = 'Nairobi'       # Change to any city
```

---

## How Each Script Works

### Bitcoin Price Tracker (`Realtime-BTC-Tracker-and-Visualizer.py`)

1. Creates `bitcoin_price_log.csv` with headers on startup.
2. Enters an infinite loop — every 60 seconds it:
   - Makes a GET request to the CoinGecko `/simple/price` endpoint
   - Appends the price and timestamp to in-memory lists
   - Writes the row to the CSV file immediately
   - Prints the price to the console
3. On `Ctrl+C` (KeyboardInterrupt), exits the loop and renders a line chart of all collected prices.

### Temperature Tracker (`dynamic_data.py`)

1. Creates `nairobi_temp_log.csv` with headers on startup.
2. Loops for exactly 10 iterations — every 10 seconds it:
   - Makes a GET request to the OpenWeatherMap `/weather` endpoint
   - Appends the temperature and timestamp to in-memory lists
   - Writes the row to the CSV file immediately
   - Prints the temperature to the console
3. After all iterations, prints a full data summary and renders a line chart.

---

## Output

### Console output (Bitcoin tracker)

```
[2025-04-10 14:00:00] Bitcoin Price: $83,412.50
[2025-04-10 14:01:00] Bitcoin Price: $83,398.00
[2025-04-10 14:02:00] Bitcoin Price: $83,450.75
...
Stopped collecting data. Generating plot...
```

### Console output (Temperature tracker)

```
[2025-04-10 14:00:00] Temp: 19.4°C
[2025-04-10 14:00:10] Temp: 19.5°C
...
Data collection complete. Results:
[2025-04-10 14:00:00] Temperature: 19.4°C
```

### CSV log format (`bitcoin_price_log.csv`)

```
timestamp,price_usd
2025-04-10 14:00:00,83412.50
2025-04-10 14:01:00,83398.00
```

### CSV log format (`nairobi_temp_log.csv`)

```
timestamp,temperature
2025-04-10 14:00:00,19.4
2025-04-10 14:00:10,19.5
```

---

## Possible Extensions

- Add a moving average line to the chart for trend smoothing
- Use `matplotlib.animation` for a live-updating chart instead of a static end-of-run plot
- Track multiple coins or cities in a single run, plotting them on the same chart
- Add min/max/average annotations to the chart
- Schedule the Bitcoin tracker with `cron` or Windows Task Scheduler for automated background logging
- Load and plot historical data from an existing CSV file without re-fetching

---

## Author

**Stephen**

---

## License

This project is open source and available under the [MIT License](LICENSE).
