# LimitOrderBook & MatchingEngine
- Limit Orderbook &amp; Matching Engine   + market simulation &amp; visualsation written in c++.
- Design Document [here](https://github.com/jxm35/LimitOrderBook-MatchingEngine/wiki/Design-Document).

## Preview
[here](https://www.youtube.com/watch?v=aIDbPyKnSMg)

## Benchmarks

Benchmark methodology explained [here](https://github.com/jxm35/LimitOrderBook-MatchingEngine/wiki/Design-Document#213-benchmarking).
In a [simulation of market trading](https://github.com/jxm35/LimitOrderBook-MatchingEngine/wiki/Design-Document#23-market-simulation) the application was able to place and match orders at an average rate of <strong>14 Million orders per second</strong>.

| Function | Time (ns) | Implied rate per second |
| --- | --- | --- |
| Get Order | 17.7 | 56,642,000 |
| Get Best Bid Price | 17.6 | 56,665,000 |
| Place Limit Order (New Price Level) | 81.7 | 12,238,000 |
| Place Limit Order (Existing Price Level) | 73.4 | 13,615,000 |
| Place Market Order (Crossing Single Bid) | 43.0 | 23,257,000 |
| Place Market Order (Crossing 3 Bids) | 116.0 | 8,634,000 |
| Remove Order | 74.0 | 13,506,000 |


## Features

- **Limit Orderbook**: Price-time priority orderbook supporting limit/market orders, cancellations, and modifications with O(1) best price access.
- **Matching Engine**: High-frequency matching engine with sub-microsecond latency and automatic trade execution.
- **Market Data Feed**: Low-latency multicast UDP publisher broadcasting price level updates, trades, book clear events, and heartbeats.
- **Order Entry Gateway**: Multi-client TCP server handling FIX-style order messages with real-time acknowledgments and execution reports.
- **Python Integration**: pybind11 bindings exposing the C++ orderbook to Python for analysis and tooling.
- **Market Simulation**: To test performance and different implementations of the limit order book.
- **Visualisation**: Showing a price/time graph, limit level heatmaps, and a volume/time graph.

## Applications

### Exchange Server (`exchange`)

Full-featured multi-instrument exchange with dual operating modes:

- **Simulation Mode**: Generates realistic synthetic trading activity using normal distributions for price/quantity
- **Client Mode**: Order gateway accepting live client connections with market data broadcasting
- **Market Data**: Real-time UDP multicast feed (configurable IP/port) publishing all order book events
- **Order Entry**: TCP server (default port 8080) handling concurrent client connections

**Usage**: `./exchange --mode [simulation|client] --md-ip 239.1.1.1 --md-port 9999 --oe-port 8080`

### Market Data Client (`client`)

- UDP multicast receiver with sequence gap detection
- Configurable logging (console/file) and statistics reporting
- Message validation and real-time latency monitoring

**Usage**: `./client --ip 239.1.1.1 --port 9999 --logfile market_data.log`

### Order Entry Client (`order_client`)

- Interactive command-line interface for manual order entry
- Supports limit orders and cancellations with real-time feedback
- Direct TCP connection to exchange or standalone order server

**Usage**:

```bash
./order_client --server 127.0.0.1 --port 8080
> new AAPL buy 150.50 100
> cancel 12345 AAPL
```

### Order Entry Server (`order_server`)

- Standalone TCP server for testing order message protocols
- Processes NEW_ORDER and CANCEL_ORDER messages with detailed logging

---
### Python Market Simulation (`src/simulation_python/`)

Real-time trading visualization combining C++ performance with Python flexibility:

- **Live Charts**: Price/time series, order book depth visualisation, and volume analysis
- **Interactive Controls**: Buy/sell pressure buttons for market stress testing
- **Market Simulation**: Autonomous trading bot generating realistic order flow
- **Performance**: C++ orderbook backend with PyQt6 frontend for sub-microsecond order processing

**Requirements**: PyQt6, pyqtgraph, numpy

