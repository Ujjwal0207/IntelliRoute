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


## Frontend
<img width="1240" height="649" alt="Screenshot 2025-12-16 at 9 02 36 PM" src="https://github.com/user-attachments/assets/826c338c-af8b-4c4c-98c4-3042fd0f448f" />
<img width="1259" height="686" alt="Screenshot 2025-12-16 at 9 02 47 PM" src="https://github.com/user-attachments/assets/2f351c0e-1366-46d6-a041-cf240ce58111" />
<img width="1267" height="691" alt="Screenshot 2025-12-16 at 9 03 46 PM" src="https://github.com/user-attachments/assets/b4c136fc-e93b-48e9-b97e-5fccbb4ea468" />
<img width="1277" height="707" alt="Screenshot 2025-12-16 at 9 33 12 PM" src="https://github.com/user-attachments/assets/96021fa6-ba44-4904-b03a-4deb8817647e" />
