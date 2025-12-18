This project implements a real-time Bitcoin price tracker and logger. It fetches live market data from the CoinGecko API, records the data with timestamps into a local CSV file, and generates a visual trend line upon user termination.

---

## Bitcoin Real-Time Price Logger

This script provides a lightweight solution for monitoring cryptocurrency fluctuations and maintaining a historical record for later analysis.

### System Overview

The script operates on a continuous fetch-log-sleep cycle. It uses the `requests` library to interface with the CoinGecko REST API and `matplotlib` for time-series visualization.

### Mathematical Foundation

While this script is primarily an ETL (Extract, Transform, Load) tool, the price movement it tracks is often analyzed using the **Percentage Change** formula to determine volatility between intervals (t and t-1):

Where:

* P_t: Current price at time t.
* P_{t-1}: Previous price at the last recorded interval.

---

## Features

* **Live API Integration**: Fetches the current Bitcoin price in USD directly from CoinGecko.
* **Persistent Storage**: Automatically creates and appends data to `bitcoin_price_log.csv`.
* **Dynamic Plotting**: Generates a line chart showing price trends over the duration of the session.
* **Error Handling**: Includes try-except blocks to manage network interruptions or API downtime.

---

## Installation & Setup

### Prerequisites

Ensure you have Python installed, then install the necessary dependencies:

```bash
pip install requests matplotlib

```

### Usage

1. Run the script in your terminal or IDE.
2. The script will log the price every 60 seconds.
3. To stop tracking and view the graph, press **CTRL+C** (KeyboardInterrupt).

---

## File Documentation

### CSV Format

The data is stored in the following structure:

| timestamp | price_usd |
| --- | --- |
| 2025-12-18 16:00:00 | 98450.25 |
| 2025-12-18 16:01:00 | 98465.10 |

### Technical Details

* **Interval**: 60 seconds (configurable via `time.sleep()`).
* **API Endpoint**: `https://api.coingecko.com/api/v3/simple/price`.
* **Visualization**: Matplotlib with rotated X-axis labels for readability of timestamps.

---

## Future Improvements

* Add multi-currency support (e.g., Ethereum, Litecoin).
* Implement a Moving Average (SMA) calculation to smooth out the trend line.
* Integrate an email alert system if the price crosses a certain threshold.
* Implement a Frontend/Dashboard for easy visealization.

## Applying this code.
Remember to follow me and mention me before you clone this repository.
