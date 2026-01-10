# Creda AI

Creda AI is a personal finance assistant that blends Splitwise-style group expenses, Venmo-style wallet transfers, and Rocket Money-style transaction insights into one app. It pairs a fast, secure backend with a polished React Native experience and a ChatGPT-style multimodal (text + voice) assistant backed by an MCP server so users can perform app actions by voice.

## Highlights

- Send and receive money with wallet transfers and requests.
- Create groups, split expenses, track settlements, and maintain full audit history.
- Ingest bank data via Plaid Link and Transactions Sync; normalize and persist to PostgreSQL.
- Analyze spend trends and subscriptions with AI-assisted categorization.
- Real-time activity and timeline updates via WebSockets.
- Multimodal chatbot (text + voice) with streaming LLM output, STT, and TTS.

## Product Capabilities

### Money Management

- Wallet transfers and payment requests with transactional integrity.
- Group expense workflows with comments, locks, flags, and history.
- Settlement tracking with clear status and reconciliation.

### Bank Insights

- Bank sync with Plaid Link + Transactions Sync.
- Categorized transactions and subscription detection.
- Trend analytics and user-friendly insights.

### AI Assistant (Voice + Text)

- ChatGPT-style conversational UX with live voice toggle in the same thread.
- WebSocket multiplexing for user messages, STT partial/final transcripts, and streaming LLM output.
- Tool-enabled assistant backed by an MCP server, so app functions can be invoked by voice.

## Architecture Overview

- Mobile app: React Native (0.82), React 19, TypeScript, React Navigation.
- Backend: FastAPI + Python, PostgreSQL, SQLAlchemy.
- Realtime: FastAPI WebSockets with user-scoped connection management.
- AI: Vertex AI Gemini for chat generation (streaming), Google Cloud STT (batch + streaming), and Google Cloud TTS (single-shot + streaming).
- Storage: Cloud Storage for audio artifacts and receipts; GCS or local filesystem with signed URLs.
- Auth: JWT access/refresh tokens, bcrypt password hashing, Google OAuth sign-in.
- Cloud: Cloud Run deployment, Secret Manager for sensitive config, Firestore/Cloud SQL for conversation history, Cloud Logging for observability.

## Backend Features (FastAPI)

- Plaid integration for account linking and transaction ingestion.
- Secure auth with JWT, bcrypt, and role-aware authorization.
- Split-expense and group workflows with transactional DB logic.
- Receipt ingestion pipeline with image parsing via Gemini.
- Transaction categorization via YAML-driven prompts.
- WebSocket events for wallet, expenses, groups, and activity feeds.
- Dockerized services orchestrated with docker-compose.

## Mobile App Features (React Native)

- Cross-platform experience with robust error handling.
- Secure auth flows with token refresh and encrypted local storage.
- Plaid integration and receipt/expense tooling.
- Realtime updates via WebSockets across wallet and group flows.
- Voice assistant UX with push-to-talk and streaming responses.
- Code quality with TypeScript types, Jest, and ESLint.

## Tech Stack

- Mobile: React Native, React 19, TypeScript, React Navigation.
- Backend: FastAPI, Python, SQLAlchemy, PostgreSQL.
- Realtime: WebSockets.
- AI: Vertex AI Gemini, Google Cloud STT/TTS.
- Auth: JWT, OAuth, bcrypt.
- Infra: Docker, docker-compose, Cloud Run, Secret Manager, Firestore/Cloud SQL, Cloud Storage, Cloud Logging.
- Integrations: Plaid Link + Transactions Sync.

## Data Flow (High Level)

1. User connects a bank via Plaid Link.
2. Transactions Sync ingests data -> normalization -> PostgreSQL.
3. Categorization and insights are generated with AI assistance.
4. Groups and expenses are created, settled, and tracked in real time.
5. Voice assistant interacts via WebSockets, with tool calls handled by an MCP server.

## Local Development

Note: The following is a suggested structure. Adjust to match your repo layout.

```bash
# Backend
cd backend
cp .env.example .env
docker-compose up --build

# Mobile app
cd mobile
yarn install
yarn ios # or yarn android
```

## Environment Variables (Suggested)

- `DATABASE_URL`
- `JWT_SECRET`
- `JWT_REFRESH_SECRET`
- `GOOGLE_OAUTH_CLIENT_ID`
- `PLAID_CLIENT_ID`
- `PLAID_SECRET`
- `PLAID_ENV`
- `GEMINI_API_KEY`
- `GCS_BUCKET`
- `CLOUD_RUN_SERVICE`

## Security

- JWT access/refresh flow with rotation.
- bcrypt password hashing.
- Role-aware authorization checks.
- Secret Manager for sensitive config.

## Roadmap Ideas

- Budgeting goals and alerts.
- Automated subscription renegotiation insights.
- Multi-currency support with live FX.

## License

Private or TBD.
