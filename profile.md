# Hamza Alkoozy — Software Engineer & Component Lead | AI-Native Full Stack Developer | PHP, Laravel, React.js | FinTech & Payments

hamza.alkoozy@outlook.com · https://www.linkedin.com/in/hamza-alkoozy-05603b126 · Dubai, UAE · GMT +4

## Summary

I am a backend-focused full stack developer with 6+ years of experience in PHP, Laravel, MongoDB, SQL and React. Today I build and maintain backend services for a high-volume, multi-brand platform for wallets, payments, rewards and marketing automation. The data runs to billions of rows, with millions of new rows a day, so I design every query, job and write for that scale. My focus is money correctness: a customer must never be paid twice or paid more than they should, across retries, crashes and parallel workers. I also run a governed AI engineering workflow, with rules, review gates and memory, that keeps AI-written code safe on money and load.

## Top strengths

- **Money correctness at scale (hard skill)** — I build wallet, reward and commission logic that stays correct across retries, parallel workers and crashes, without database transactions. I root-caused a silent bug where wallet balances stopped saving after a framework upgrade, and I run a money-safety review on every change that touches a money path.
- **High-volume data and performance (hard skill)** — I set query and index rules for MongoDB collections with billions of rows: indexed date bounds, no unbounded queries, and reports from a read replica, ClickHouse or snapshots. I found and fixed an O(n²) hot path that pushed a production server to full CPU load.
- **Governed AI engineering (hard skill)** — I designed my own AI coding workflow: rule files with reasons, hard limits, required money and performance reviews, memory, a task board and reusable skills.
- **Turning incidents into rules (soft skill)** — After each incident I fix the root cause and then fix the process. The CPU incident and the silent save bug each became a standing rule with its reason and date.
- **Clear ownership of decisions (soft skill)** — I stop and ask on every business decision instead of guessing. I state the question in plain words, list the options, give a recommendation, and log the answer in a decision register.

## Experience

### Full Stack Web Developer — Modsoft Technology AI Applications and Services Co. L.L.C. · Aug 2024 – Present · Dubai, UAE

- Build and maintain PHP and Laravel services for a high-volume, multi-brand platform for wallets, payments, rewards and marketing automation.
- Built asynchronous job pipelines with queues and Supervisor for reliable high-volume financial transactions and wallet operations.
- Developed crypto wallet systems for deposits, withdrawals, balance reconciliation and transactional consistency.
- Designed MongoDB schemas, aggregation pipelines and statistical snapshot systems. Keep heavy reporting on a read replica, ClickHouse or pre-built snapshots instead of live aggregation on collections with billions of rows.
- Ship every behavior change as an operator option whose default is today's behavior, so no brand sees a surprise.
- Run a governed AI coding workflow for my own work, with required money-safety and performance reviews before any task closes.

### Full Stack Developer — ASTUDIO · Apr 2024 – Aug 2024 · Dubai, UAE

- Optimized SQL queries to speed up search in the ERP system.
- Integrated OpenAI ChatGPT to parse emails into deals automatically.
- Built backend form-builder logic to add or remove fields dynamically, using the EAV model for the job module.

### Full Stack Web Developer | Component Lead — Veer UAE · Jun 2022 – Dec 2023 · Dubai, UAE

- Led the Digital Monitoring and Scraper component team in the integration and validation of data sources.
- Set up a task scheduler for the Scraper component on Google Cloud to improve its efficiency and reliability.
- Built a user authentication and authorization microservice with PHP and JWT.
- Improved the Scraper with a content-extraction microservice written in Python.

### Full Stack Web Developer — Veer UAE · Oct 2020 – Jun 2022 · Dubai, UAE

- Upgraded the client dashboard with bar and pie charts (Chart.js), responsive on all platforms.
- Built complex reports exported to Excel, with multi-table queries, filters and aggregations.
- Worked with cross-functional teams in agile, using Git, Jira and Bitbucket.

### Front-End Web Developer — Freelance · Oct 2019 – Aug 2020

- Designed and built web app interfaces with React and Next.js.
- Built responsive features with HTML, CSS, JavaScript and Bootstrap.

## Key projects

### Silent balance saves after a framework upgrade

- **Problem:** After a framework upgrade, affiliate wallet balances and cached stats on existing records stopped saving. There was no error and no log.
- **What I built:** I traced it into the MongoDB ORM. It compared Decimal128 values with `==`, and any two Decimal128 values are equal that way, so every change looked like "no change". I added a shared compare method for every cast of this kind. I also added a rule that tests must check a fresh read from the database, not the model in memory.
- **Why it mattered:** Balances save again. The same bug can no longer hide in tests that only check the in-memory model.

### CPU saturation on a high-traffic endpoint

- **Problem:** One high-traffic endpoint pushed all CPU cores of a production server to full load.
- **What I built:** I found an O(n²) loop over a large catalog and replaced the nested scan with a linear pass. I then made it a standing rule: every change states its complexity, has no collection calls inside loops, and never loads the full catalog per request.
- **Why it mattered:** CPU went back to normal. The rule now runs on every change as part of my performance review.

### Self-healing analytics sync between MongoDB and ClickHouse

- **Problem:** Analytics data copied from MongoDB to ClickHouse for reports could drift from the source or arrive twice.
- **What I built:** Drift self-repair for the synced data, a sync that removes duplicates, an alert when duplicates appear, query performance logging, and a short-lived read cache for report queries.
- **Why it mattered:** Drift is found and repaired by the system. Duplicates raise an alert instead of passing silently into reports.

### Marketing automation engine

- **Problem:** Operators needed automated customer journeys and audience segments that send rewards safely, at scale.
- **What I built:** A journey engine with trigger, profile check, action, delay, stop and conversion steps. Scheduled triggers with caps and paced sending. Pause and resume that fully freezes a journey. Customer segmentation with change tracking, showing who was added and removed.
- **Why it mattered:** Scheduled sends are capped and paced, and each reward is paid once.

## Skills

| Area | Strong (proven) | Growing |
|---|---|---|
| Backend | PHP 8, Laravel, REST APIs, queues and jobs, RabbitMQ, Redis, Supervisor, JWT authentication, microservices, Python (content extraction) | Go, gRPC |
| Data and databases | MongoDB (schema design, aggregation pipelines, index design, query optimization, read replicas), ClickHouse, snapshots and pre-aggregation, backfills, reconciliation, SQL, EAV model | PostgreSQL, transaction isolation, partitioning |
| Money and payments correctness | Wallets, crypto wallet deposits and withdrawals, idempotency, paid-once effects, locks without database transactions, race conditions, Decimal128 and BigDecimal precision, per-currency sums, affiliate commission | Double-entry ledger, outbox pattern, sagas |
| Performance and reliability | Big-O analysis, N+1 removal, write counting on unchanged runs, caching, incident response, root cause analysis, safe rollout with operator options, multi-tenant SaaS | Load testing (k6), profiling in production, OpenTelemetry, Prometheus, Grafana, SLO / SLI, AWS / GCP, Docker, Kubernetes |
| AI engineering | Claude Code, agentic coding, context engineering, agent rule files, custom skills, hooks, agent memory, AI code review gates, human-in-the-loop, code knowledge graph, OpenAI ChatGPT integration | Building MCP servers, RAG, evals, agent security |
| Frontend | React, Next.js, Vite, Chart.js, HTML, CSS, JavaScript, Bootstrap, responsive design | — |
| Leadership and communication | Component team lead, code review standards, decision register, rollout runbooks, client, operator and frontend guides, Postman collections | Design docs, mentoring, spoken presentations |

## AI engineering

I run AI coding agents in my own work as a governed system, not as a shortcut.

- **Rules with reasons:** My rule files work at three levels: personal, platform and service. Each rule carries its reason and often the incident date, so the agent can apply it to cases the rule does not name.
- **Learning loop:** Every incident becomes a rule the same day. Examples are the CPU hot path, the silent Decimal128 save, and a stale code comment that was trusted over the code.
- **Hard limits:** The agent works under hard limits on commits, servers and private data.
- **Stop and ask:** On any business or money decision, the agent stops, states the question in plain words, lists the options with a recommendation, and builds nothing until I answer.
- **Review gates:** A money-safety review checks retries, redelivered messages, two workers at once, crashes between writes and reverse paths. A performance review checks reads, writes, CPU and memory per run and per day. No task closes without both.
- **Memory and task board:** A curated memory index with topic notes. A task board the agent updates through a command-line tool and hooks, with plans, small reviewable chunks, rollout steps and open questions.
- **Reusable skills:** Custom skills for reviews, guides, API explorers, handoffs and backups.
- **Testing the tool:** I checked which sub-agents load my rules and changed how I brief the ones that do not.

## Soft skills

- **Escalates business decisions instead of guessing.** I keep code choices and business meaning apart, and I log every business decision per area in a decision register.
- **Writes for every audience.** I write client guides, operator guides, frontend guides and Postman collections for the features I ship.
- **Leads a component team.** At Veer UAE I led the Digital Monitoring and Scraper component team through data source integration and validation.
- **Turns incidents into rules.** I fix the root cause, then fix the process so the same bug cannot come back.
- **Keeps work reviewable.** I plan first, deliver one logical change per chunk, and put a short summary with file references on top of each one.
- **Verifies instead of trusting.** I treat code as the only source of truth and checked my own AI tooling before relying on it.

## Education and languages

- Bachelor's degree, Information Technology (Software Engineering and Information), Tishreen University, 2013 – 2019
- Arabic — native
- English — professional (B2)

Source: https://hamzaalkoozy1.github.io/
© 2026 Hamza Alkoozy · All rights reserved
