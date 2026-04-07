# Pollution Monitoring System

> Real-time indoor environment monitoring via gRPC streaming — track temperature, humidity, air quality, and noise level across multiple location types.

![Node.js](https://img.shields.io/badge/Node.js-20%2B-339933?logo=nodedotjs)
![gRPC](https://img.shields.io/badge/gRPC-Enabled-4285F4?logo=google)
![Protocol Buffers](https://img.shields.io/badge/Protobuf-proto3-blueviolet?logo=googlechrome)
![License](https://img.shields.io/badge/License-ISC-yellow)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running Locally](#running-locally)
- [gRPC Services](#grpc-services)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

The **Pollution Monitoring System** is a client-server application that streams simulated environmental sensor data in real time using **gRPC**. It targets indoor environments — hospitals, commercial buildings, and offices — and continuously reports metrics such as temperature, humidity, air quality index, and noise level.

Data is generated server-side through a random-value simulation, enabling demonstration of the full streaming pipeline without physical hardware.

---

## Features

- **Real-time data streaming** using gRPC server-side streaming (proto3)
- **Three environment service types**: Hospital, Building, and Office
- **CLI-driven client** with interactive service selection and continuous-query support
- **Client metadata propagation** — client IP, selected service, and timestamp are forwarded to the server on every call
- **Graceful error handling** on both client and server sides
- **Four query modes**: monitor individual services or all three at once

---

## Tech Stack

| Technology | Purpose |
|---|---|
| [Node.js](https://nodejs.org/) | Runtime for both server and client |
| [@grpc/grpc-js](https://www.npmjs.com/package/@grpc/grpc-js) | gRPC implementation for Node.js |
| [@grpc/proto-loader](https://www.npmjs.com/package/@grpc/proto-loader) | Dynamic `.proto` file loading |
| Protocol Buffers (proto3) | Service and message definitions |
| nodemon | Development server auto-reload |

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/en/download) v18 or higher
- npm (bundled with Node.js)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/flaviu-vanca/Pollution-Monitoring-System.git
   cd Pollution-Monitoring-System
   ```

2. **Install server dependencies**

   ```bash
   cd server
   npm install
   ```

3. **Install client dependencies**

   ```bash
   cd ../client
   npm install
   ```

### Running Locally

> Open two separate terminal windows.

**Terminal 1 — Start the server**

```bash
cd server
node server.js
```

The server binds to `127.0.0.1:50051` and logs its address on startup.

**Terminal 2 — Start the client**

```bash
cd client
node client.js
```

Follow the interactive CLI prompts to select a monitoring service.

---

## gRPC Services

All services are defined in [`protos/pollution_tracker.proto`](protos/pollution_tracker.proto) under the `pollution` package.

**Service:** `EnvironmentServices`

| RPC Method | Type | Description |
|---|---|---|
| `HospitalEnvironmentService` | Server-side streaming | Streams environment data for a hospital location |
| `BuildingEnvironmentService` | Server-side streaming | Streams environment data for a building location |
| `OfficeEnvironmentService` | Server-side streaming | Streams environment data for an office location |

**`EnvironmentData` message fields:**

| Field | Type | Description |
|---|---|---|
| `locationId` | `string` | Simulated GPS-style coordinates |
| `temperature` | `double` | Temperature reading (°C, range 10–60) |
| `humidity` | `double` | Relative humidity (%, range 0–100) |
| `air_quality` | `double` | Air quality index (range 0–100) |
| `noiseLevel` | `double` | Noise level (range 0–100) |

---

## Project Structure

```
Pollution-Monitoring-System/
├── client/
│   ├── client.js            # Interactive CLI gRPC client
│   ├── package.json
│   └── package-lock.json
├── server/
│   ├── server.js            # gRPC server with three environment services
│   ├── package.json
│   └── package-lock.json
├── protos/
│   └── pollution_tracker.proto  # Protobuf service and message definitions
└── README.md
```

---

## Contributing

Contributions are welcome. To contribute:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "feat: describe your change"`
4. Push to your fork: `git push origin feature/your-feature`
5. Open a pull request against `main`

Please follow the existing code style and keep pull requests focused on a single concern.

---

## License

This project is licensed under the **ISC License**.

---

> **Disclaimer:** This project is for educational purposes only. It is not intended for production deployment in critical environments without proper validation, testing, and integration with real sensor hardware.