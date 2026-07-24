# 🚀 High-Scale Distributed Twitter / X Clone

[![Node.js](https://img.shields.io/badge/Node.js-20.x-green.svg)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue.svg)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue.svg)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7-red.svg)](https://redis.io/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED.svg)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A production-grade, high-throughput micro-blogging backend architecture designed to handle high-concurrency feeds, real-time WebSockets, and caching patterns for scale.

---

## 🏗️ System Architecture

```text
       [Client / Frontend]
               │
        (HTTP / WebSockets)
               ▼
     [ Nginx Reverse Proxy ]
               │
       ┌───────┴───────┐
       ▼               ▼
 [ Node.js API 1 ] [ Node.js API 2 ]  <── (Horizontal Scaling)
       │               │
       ├───────────────┼───────────────┐
       ▼               ▼               ▼
 [ PostgreSQL ]   [  Redis  ]   [ Message Queue ]
  (Relational)    (Feed Cache)   (Background Jobs)
