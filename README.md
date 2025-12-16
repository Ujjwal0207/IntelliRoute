# IntelliRoute

AI-powered query assignment system built as a Spring Boot (MongoDB) backend with built-in complexity scoring powered by Google Gemini, plus a heuristic Java fallback.

## Backend (Spring Boot)
- Java 17, Spring Boot 3, MongoDB.
- Key modules: web, data-mongodb, validation, actuator, webflux (WebClient).
- Scheduling enabled for periodic assignment runs and SLA checks.

### Config
- `backend/IntelliRoute/src/main/resources/application.yml` uses env overrides:
  - `MONGODB_URI` (default `mongodb://localhost:27017/intelliroute`)
  - `GEMINI_API_KEY` / `GEMINI_MODEL` / `GEMINI_ENDPOINT`
  - `ASSIGNMENT_SCHEDULER_DELAY_MS` / `SLA_CHECK_MS`
- Adjust logging via `logging.level.com.intelliroute`.

### Run
Option A: environment variables (recommended for prod)
```bash
cd backend/IntelliRoute
export MONGODB_URI=...
export MONGODB_DATABASE=...
export GEMINI_API_KEY=...
mvn spring-boot:run
```

Option B: .env file (auto-loaded)
```bash
cd backend/IntelliRoute
cp config/env.sample .env   # edit with real values (URL-encode @ as %40)
mvn spring-boot:run
```
API samples:
- `POST /api/engineers` body `{"name":"Alex","designation":"SENIOR","capacity":3,"skills":["kafka","react"]}`
- `POST /api/queries` body `{"description":"Kafka consumer lag on prod","priority":"P1","tags":["kafka","infra"]}`
- `POST /api/assignments/run` to trigger manual assignment (scheduler runs automatically).

## Deployment Notes
- Provide MongoDB credentials via env vars/secret store.
- Provide `GEMINI_API_KEY` in a secure way (env vars/secret manager).
- Actuator enabled for health/metrics; wire to monitoring (Prometheus/Grafana).


