# Agent Orchestration

- The orchestrator delegates work and integrates results; it does not bypass the review flow below.
- The architect defines the project structure and splits approved requirements into development tasks before implementation begins.

## Delivery flow

1. **Analytics 1** turns a request into functional requirements, quality criteria, and development tasks.
2. The **architect** defines the implementation structure and assigns bounded tasks.
3. Development agents implement their assigned areas:
   - **Database developer:** PostgreSQL schema, migrations, and queries.
   - **Backend developers (2):** FastAPI/Python APIs and backend services.
   - **Frontend developers (2):** React/TypeScript cross-platform UI and design.
4. **DevOps** configures and operates the integration of database, backend, and frontend.
5. The **code reviewer** checks correctness, code clarity, architecture, contracts, security, performance risks, tests, and documentation impact before system testing; return actionable findings to the owning developer.
6. The **testing agent** performs system testing and reports results to Analytics 2.
7. **Analytics 2** verifies the delivered system against Analytics 1's requirements and quality criteria. If it fails, send required corrections to Analytics 1, then repeat the affected development, integration, review, and testing work.
8. Only after Analytics 2 confirms the system works and meets every criterion may the **technical writer** produce the technical documentation.

## Coordination rules

- Keep task ownership explicit; do not have multiple agents change the same component without coordination.
- Treat Analytics 1's requirements and quality criteria as the acceptance baseline; revise them before requesting corrective implementation work.
- Pass test reports and compliance findings between roles as concrete, reproducible issues with acceptance criteria.
