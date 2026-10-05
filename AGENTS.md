# SupraOS workflow delivery instructions

Read the current handoff, checklist, dependency plan and `workflow-plan.json` before planning work. The product repository has its own AGENTS.md/CONTEXT.md/build protocol; this documentation repository does not replace them.

## Required documentation workflow

- `workflow-plan.json` is the current status and execution-policy source. `scripts/render_plan.py` generates the handoff, checklist, dependency plan and evidence index. Do not hand-edit those generated views.
- Preserve all 33 task IDs and detailed acceptance/source/owner/dependency records, 16 behavior families and 12 surfaces. Historical baseline records and archived documents preserve previous evidence; they are not current release claims.
- Every generated handoff/checklist/plan must retain all EP01–EP13 principles, including failure-drain priority, parallel release feasibility, reusable harness/preflight, scoped evidence reuse, one-record documentation and delivery metrics.
- Before publication run `python3 scripts/render_plan.py` and `python3 scripts/render_plan.py --check`. Publish the record and generated views together. Secret-scan public files. Verify remote bytes and anonymous real-browser access/rendering. Keep receipts outside generated content to avoid a self-referencing publication loop.
- Scope changes or policy changes require explicit user direction; a partial milestone or a passing gate does not reduce the agreed project.

## Implementation discipline

- Finish the critical-failure drain and actual callers before starting another effect destination, unless it directly unblocks that contract. Root assigns one shared-file owner.
- Run three lanes around that delivery path: implementation/integration, release prerequisites, independent verification. Extra agents receive bounded dependency-closing tasks; honor actual capacity and host budgets.
- Reuse existing candidate, ledgers, receivers, schema packets, source manifests and SQL/REST harnesses. Missing live evidence is not missing implementation.
- Freeze exact qualification source. Preserve failures; admit only demonstrated blocker repairs with independent review. Preserve exact required final gates and permissions/resource limits.
- Track implementation, integration, tests, independent review, merge, deployment, activation and live acceptance separately. Do not turn acceptance/task counts into completion percentages.
- Respect current execution state and user pause/resume instructions. Documentation changes do not by themselves authorize product execution or install these rules into SupraOS Build agents.
