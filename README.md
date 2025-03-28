# OpenGoPoker

A high-performance, distributed poker server built in Go, designed to handle millions of concurrent game tables with high availability, resilience, and crash recovery. Inspired by Erlang’s concurrency and fault-tolerance strengths (e.g., the *OpenPoker* project), *OpenGoPoker* leverages Go’s goroutines, gRPC, and Cassandra to deliver a modern, scalable poker platform.

## Features
- **Massive Concurrency**: Supports millions of game tables using Go’s lightweight goroutines and the Actor Model, inspired by Erlang’s process-per-entity design.
- **High Availability**: Distributed architecture with no single point of failure, powered by Cassandra and Kubernetes.
- **Resilience**: Game state snapshots and event sourcing ensure crash recovery and consistency, adapting Erlang’s fault-tolerance ethos.
- **Real-Time Communication**: gRPC for low-latency client-server and inter-service interactions.
- **Event Sourcing**: Stores all game actions as events for replay, auditing, and state reconstruction.

## Tech Stack
- **Golang**: Core language for performance and concurrency.
- **Actor Model**: Implemented via goroutines and channels (or Proto Actor) for game table management.
- **gRPC**: High-performance RPC for client and server communication.
- **Cassandra**: Distributed database for game states, events, and player data.
- **Event Sourcing**: Persists game history with periodic snapshots.
- **Docker/Kubernetes**: Deployment and orchestration for scalability.

## Architecture
- **Game Tables as Actors**: Each table runs as an independent goroutine, processing player actions and maintaining state, echoing Erlang’s lightweight process model.
- **gRPC Services**: Manage client connections, game logic, and inter-service communication (e.g., matchmaking).
- **Cassandra DB**: Stores events, snapshots, and player data in a fault-tolerant, distributed system.
- **Event Sourcing + Snapshots**: Rebuilds game state from events, with snapshots for quick recovery.
- **Load Balancing**: Distributed across nodes with Kubernetes, inspired by Erlang’s cluster scalability.

## Prerequisites
- Go 1.21+
- Docker
- Cassandra 4.x
- gRPC and Protocol Buffers
- Kubernetes (optional, for production)

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/jamie0xgitc0decat/OpenGoPoker.git
   cd opengopoker
   ```

Copy

cd opengopoker
Install dependencies:
bash

Collapse

Wrap

Copy
go mod tidy
Set up Cassandra:
bash

Collapse

Wrap

Copy
docker run --name cassandra -p 9042:9042 -d cassandra:latest
Build and run:
bash

Collapse

Wrap

Copy
go build -o opengopoker
./opengopoker
Usage
Start the server:
bash

Collapse

Wrap

Copy
./opengopoker --config config.yaml
Connect via a gRPC client (example client TBD).
Configuration
Edit config.yaml:

yaml

Collapse

Wrap

Copy
grpc:
  port: 50051
cassandra:
  hosts: ["localhost:9042"]
  keyspace: opengopoker
server:
  snapshot_interval: 100 # Events before a snapshot
Project Roadmap
Phase 1: Core Infrastructure (Q2 2025)
 Set up Go project with gRPC server and client stubs.
 Implement Actor Model for game tables using goroutines and channels.
 Integrate Cassandra for event storage and schema design.
 Define core poker logic (e.g., Texas Hold’em).
 Basic event sourcing for game actions (e.g., bet, fold).
Phase 2: Game State & Recovery (Q3 2025)
 Add snapshots every N events or on game end.
 Implement crash recovery from snapshots + events.
 Test 10,000 concurrent tables on a single node.
 Add player authentication and profiles in Cassandra.
Phase 3: Scalability & Resilience (Q4 2025)
 Distribute actors across nodes with Proto Actor or custom sharding.
 Deploy with Kubernetes for orchestration and auto-scaling.
 Load test 1 million concurrent tables.
 Implement failover: Actors restart on another node post-crash.
Phase 4: Features & Polish (Q1 2026)
 Add matchmaking service via gRPC.
 Implement leaderboards and stats.
 Optimize snapshot frequency and event pruning.
 Build a simple gRPC client (CLI or GUI) for testing.
Phase 5: Production Ready (Q2 2026)
 Add TLS for gRPC and authentication tokens.
 Integrate Prometheus/Grafana for monitoring.
 Stress test 5 million concurrent tables.
 Release v1.0 with full documentation.
Why OpenGoPoker?
OpenGoPoker draws inspiration from Erlang-based systems like OpenPoker, which demonstrated massive scalability (800,000 processes on a laptop) and fault tolerance. By using Go, we bring these principles into a modern ecosystem with gRPC and Cassandra, targeting millions of tables while keeping development accessible and efficient.

Contributing
Pull requests are welcome! Please open an issue to discuss changes.

License
MIT License - see  for details.
