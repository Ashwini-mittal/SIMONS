SIMONS is a real-time quantitative trading and market intelligence application built using Python and Streamlit.
It combines statistical mean reversion, institutional order flow, risk management, and bias-free backtesting into a single interactive interface.

This repository contains the entire base implementation of SIMONS.

1. Project Structure Overview
SIMONS is implemented as a single Streamlit application and organized logically into functional sections:
Page configuration
State management
Visual engine (UI & CSS)
Market data engine
Order flow & news engine

Alert system
Backtesting & reporting
Sidebar controls
Main application logic
Each section is clearly separated and documented in code.

2. Page Configuration
st.set_page_config(...)

This defines:
Wide layout for professional dashboards
Custom page title and icon
Expanded sidebar by default
This ensures SIMONS behaves like a trading terminal rather than a web app.

3. State Management & Auto-Fixes
SIMONS uses Streamlit session state to track:
Active trades
Alert history (spam protection)
Cached news
UI toggles
Selected trading symbol
An automatic symbol fix ensures compatibility between different exchange formats (e.g. Binance vs Kraken).
This allows persistent behavior across reruns, which is critical in live systems.

4. Visual Engine (UI & Styling)

The UI is built entirely with custom CSS injected via Streamlit.
Key design goals:
Dark, low-strain interface
High contrast for signals
Institutional / terminal-style layout
Clear visual hierarchy
This section defines:
Fonts
Colors
Cards
Buttons
Sidebar styling
Live news ticker
Order flow widgets
No external frontend framework is used.

5. Market Data Engine
get_market_data()

Fetches OHLCV data from Kraken via CCXT
Converts timestamps
Calculates:
Rolling mean
Standard deviation
Z-Score
Volatility expansion
This function forms the core quantitative engine of SIMONS.
Caching is used to respect API limits while maintaining responsiveness.

6. Institutional Order Flow Engine
get_order_book()

Fetches Level-2 order book data
Cleans inconsistent exchange formats
Calculates:
Bid & ask volumes
Buy/sell imbalance
Whale wall detection
This provides market structure confirmation for statistical signals.

7. Volume Profile Engine
calculate_volume_profile()
Buckets traded volume into price bins
Identifies high-interest price zones
Normalizes volume for visual scaling
This is used to visualize where the market accepts price, not just where price moves.
8. News Engine
get_crypto_news()

Pulls real-time crypto news from CryptoCompare
Caches results to avoid excessive requests
Displays headlines in a live ticker
This provides macro awareness without overloading the UI.

9. Alert System
send_telegram_alert()

Sends alerts via Telegram Bot API
Includes symbol, signal type, price, and Z-Score
Uses state-aware logic to prevent duplicate alerts
Alerts are triggered only on signal changes, not on every candle.

10. Visualization Engine

SIMONS uses Plotly to render:
Candlestick charts
Mean & deviation bands
Volume profile overlays
Entry, stop, and target levels
The charts update dynamically and are optimized for live use.

11. Backtesting Engine
run_backtest()

Iterative candle-by-candle simulation
No look-ahead bias
Supports long and short trades
Capital compounding enabled
Returns:
Trade log
Equity curve

12. Reporting Engine
generate_html_report()

Generates a professional HTML performance report
Includes trade history and metrics
Can be downloaded and archived
This mirrors institutional post-trade reporting.

13. Sidebar Controls

The sidebar acts as a control panel:
Strategy parameters
Order flow analysis
Asset selection
Telegram alerts
Live refresh toggle
Everything required to operate SIMONS is accessible here.

14. Main Application Logic

SIMONS is divided into three modes:
Live Feed → real-time monitoring & execution
Strategy Lab → backtesting & analytics
Tutorial → built-in system documentation
Each mode is conditionally rendered and fully isolated.

15. Design Philosophy

SIMONS is built on four principles:
Statistics over prediction
Confirmation over signals
Risk before returns
Transparency over complexity
This project is intended for education, research, and system design exploration.

Disclaimer

This software is not financial advice.
It is for educational and research purposes only.
