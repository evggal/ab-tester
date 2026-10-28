# Agent Orchestration

- The orchestrator delegates work and integrates results; it does not bypass the review flow below.
- The architect defines the project structure and splits approved requirements into development tasks before implementation begins.

## Delivery flow

1. **Lid** classifies work before delegation: lite = relevant development then code review; medium = Analytics 1, development, review, testing, Analytics 2, documentation; hard = every subagent in this flow.
2. **Analytics 1** turns a request into functional requirements, quality criteria, and development tasks.
3. The **architect** defines the implementation structure and assigns bounded tasks.
4. Development agents implement their assigned areas:
   - **Database developer:** PostgreSQL schema, migrations, and queries.
   - **Backend developers (2):** FastAPI/Python APIs and backend services.
   - **Frontend developers (2):** React/TypeScript cross-platform UI and design.
5. **DevOps** configures and operates the integration of database, backend, and frontend.
6. The **code reviewer** checks correctness, code clarity, architecture, contracts, security, performance risks, tests, and documentation impact before system testing; return actionable findings to the owning developer.
7. The **testing agent** performs system testing and reports results to Analytics 2.
8. **Analytics 2** verifies the delivered system against Analytics 1's requirements and quality criteria. If it fails, Lid classifies each finding and routes it to the relevant role, then repeats the affected work.
9. Only after Analytics 2 confirms the system works and meets every criterion may the **technical writer** produce the technical documentation.

## Coordination rules

- Keep task ownership explicit; do not have multiple agents change the same component without coordination.
- Treat Analytics 1's requirements and quality criteria as the acceptance baseline; revise them before requesting corrective implementation work.
- Pass test reports and compliance findings between roles as concrete, reproducible issues with acceptance criteria.
- Subagents return structured handoffs to Lid according to `agent-communication.json`; they do not delegate directly to each other.
- Limit corrective work to five remediation cycles per task. After an unresolved fifth cycle, technical writing produces an error report rather than approval documentation.
