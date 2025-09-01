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

- A limit orderbook capable of handling limit and market orders, order cancellattions, and order modifications.
- Matching Engine implementing a price-time priority algorithm.
- A market simulation to to test performance and different implementations of the limit order book.
- Visualisation showing a price/time graph, limit level heatmaps, and a volume/time graph.
