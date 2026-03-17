# OrderBook

**OrderBook** is a high-performance, concurrent order book engine implemented in **C++**, designed with a focus on **low-latency trading** and **scalable order processing**. The project explores core mechanisms used in modern financial exchange systems, emphasizing concurrency, correctness, and performance.

## Key Features

### Low Latency Matching
Benchmarked across **16,000 samples**:
| Metric | Latency |
|--------|---------|
| Median | 10 µs |
| Average | 2,089 µs |
| p99 | 9,250 µs |

### Intel TBB Integration
Leverages TBB's concurrent containers — `tbb::concurrent_hash_map` and 
`tbb::concurrent_queue` — for high-throughput, thread-safe order processing 
without coarse-grained locking.

### Asynchronous Matching Engine
Dedicated threads for buy and sell queues process orders independently, 
reducing lock contention and improving overall throughput under load.

### Multiple Order Types
| Order Type | Behavior |
|------------|----------|
| Limit | Rests in book at specified price |
| Market | Executes immediately at best available price |
| IOC | Fills what it can, cancels residual quantity |
| Stop | Stubbed — planned for future implementation |

### Modular & Extensible
Clean separation of matching logic, order lifecycle, and queue management 
enables straightforward extension for partial fills, advanced order types, 
and custom matching rules.

## Design Overview
- `std::map`-based bid/ask price levels
- `tbb::concurrent_hash_map` and `tbb::concurrent_queue` for parallel ingestion and matching
- Modular architecture enabling future extensions (partial fills, advanced order types, improved matching)

## Use Cases
- Experimentation with high-performance trading system components
- Educational reference for order book mechanics and concurrent C++ design
- Foundation for advanced matching engines or trading simulators

## Contents
- Core order book and scheduler implementation
- Example main driver
- Comprehensive test suite
- Catch-based unit tests


## Build and Run

### Prerequisites

- C++ compiler with C++17/C++20 support  
  (GCC ≥ 10 / Clang ≥ 10 / MSVC ≥ 2019)
- CMake ≥ 3.10
- make or ninja

---

### Clone Repository

```bash
git clone https://github.com/STARSHIP2006/High-Performance-Stop-Order-Scheduler-for-Order-Book-.git
cd High-Performance-Stop-Order-Scheduler-for-Order-Book-
```

##  Compile

```bash
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
cmake --build . --config Release
```

## Run

```bash
./StopOrderScheduler
```

If the executable is generated inside the build directory:
```bash
./build/StopOrderScheduler
```

## Example Run With Arguments

```bash
./build/StopOrderScheduler \
  --input examples/orders.csv \
  --config examples/config.json \
  --threads 4
```

## Command Line Options

```bash
--input <file>     Input order stream  
--config <file>    Scheduler configuration  
--threads <n>      Number of worker threads  
--help             Display usage information  
```

## Clean Build

```bash
rm -rf build
```

> This repository is a personal project focused on concurrency, data structures, and performance engineering in quantitative systems.
