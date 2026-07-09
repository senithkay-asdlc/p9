---
skillsApplied:
  - high-level-architecture
  - go
  - openapi-conventions
---

# Design — Hello World API

## 1. Overview

The system is a single minimal HTTP API service that returns a greeting
message and exposes a health check. It has no persistence, no auth, and no
other components — a single Go service satisfies every requirement.

## 2. Components

- **hello-api** (`service`) — HTTP API serving the greeting endpoint and the
  health check.

## 3. Capabilities

### hello-api

- **Greeting** — `GET /hello`, optionally accepting a `name` query parameter,
  returns `{ "message": "Hello, World!" }` or a personalized greeting.
- **Health check** — `GET /health` returns `200 OK` for liveness monitoring.
- **Request logging** — basic logging of incoming requests for observability.

## 4. Data model

None. The service is stateless and holds no persistent entities.

## 5. Roles & access

No authentication or roles — the API is open/public per requirements
(non-goal: no auth or user accounts).

## 6. Interactions

None — `hello-api` is a standalone service with no dependencies on other
components or external systems.

## 7. Data flow

1. Client sends `GET /hello` (optionally with `?name=Alice`).
2. `hello-api` builds the greeting message (personalized if `name` is
   present, default otherwise) and returns it as JSON with `200 OK`.
3. Monitoring systems poll `GET /health`, which returns `200 OK` when the
   service is running.
