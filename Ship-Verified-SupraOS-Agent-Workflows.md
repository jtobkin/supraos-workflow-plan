# Ship Verified SupraOS Agent Workflows

Working checkpoint: 2026-10-02 18:25 UTC. Execution is active. The owner requested an implementation pause at **2026-10-02 19:36:59 UTC / 2026-10-03 03:36:59 Hong Kong**, followed by an updated handoff and checklist. This checkpoint will be refreshed at that stop. The project is not complete.

This public document is intended to let a new session on a new computer understand the work. It contains no credentials. Public access to this document does **not** grant access to the private application repository, databases, providers, deployment accounts or original workstation. Use the owner's normal authorized access for those resources.

## 1. Goal and scope

Make SupraOS agents consistently private, authorized, context-aware, recoverable and truthful across personal chat, Telegram, voice, delegation, background agents, project/workspace execution, scheduled research, Rooms, Routines and System Workflows.

Agents must use current preferences and relevant bounded memory, skills and lessons; protect private information across audiences; enforce exact permissions; retain original execution identities; recover without repeating uncertain effects; and report outcomes backed by durable evidence. iMessage is deferred; WhatsApp is excluded.

The sixteen behavior goals remain in scope:

1. Quiet morning suggestions, or intentional silence when appropriate.
2. Drafts in the owner's voice, including edit/ignore paths and no implicit send.
3. Visible shopping and screenshots under exact permissions and history.
4. Approved real calls with correct recipient, speech and truthful outcome.
5. Useful initiative without silently broadening authority.
6. The same real computer across Telegram takeover, owner control and handback, with replay refusal.
7. A loose-end shelf supporting add, finish, dismiss and later suppression.
8. Mail retrieval, review, send/edit/snooze/ignore and suppression.
9. Two-owner consent for sharing, including revocation and concurrency.
10. A unique mailbox and inbound messages returning to the same conversation.
11. Purchases bound to exact shop, item, amount, payment instrument and receipt.
12. Truthful completion marks backed by checked history and context.
13. Current preferences and bounded relevant older memory across all surfaces.
14. Honest stops for unavailable sites/providers, missing evidence and uncertain commits.
15. Quiet hours, batching, cadence and urgency without duplicate work.
16. Tone and length appropriate to actual task, calendar and support context.

A partial release is useful progress; it does not redefine these goals.

## 2. What shipped, and what that evidence does not prove

PR6034, workflow dispatch identity and checkpoint concurrency, merged through the normal required-check guard as `2e061a2ec14abf58b63c6f68c925fdfe5ecafd0f`. Deployment was observed on 2026-10-02 at15:12:49 UTC. It derives grant identity from trusted dispatch options, persists the original principal and guards checkpoint writes against stale timestamp/configuration/lease state. No new SQL was applied for that release.

Independent deployed Chromium checked public rendering at390/1440 and unsigned run-list/detail denial. A later deployed-main regression at `e74e3a8961043483db9ceecc377dcfbc7f537b43` passed the same public checks. **Authenticated owner, foreign-owner and recovery acceptance remains open.** A public page loading and unsigned401 do not prove authenticated workflow correctness.

Earlier recorded privacy and deadline releases include PR6032 and PR6062. Their exact historical limits are preserved in the repository handoff. Do not infer completion of every behavior from these component releases.

## 3. Frozen release stack

Repository: [jtobkin/suprafx-platform](https://github.com/jtobkin/suprafx-platform), private. PR/source links require repository access.

| Candidate | Exact source | Purpose and status |
| --- | --- | --- |
| [PR6124](https://github.com/jtobkin/suprafx-platform/pull/6124) | `2e7d34c79b77ddbeb4fc74e14681de37c37d096a` | Original outcome holds; next no-new-SQL release milestone. Required CI pending at this checkpoint. |
| [PR6127](https://github.com/jtobkin/suprafx-platform/pull/6127) | `00cb9c8e9b97ea53b7e6c5c623579121a5b5705a` | Pause receipts; draft stacked after6124. |
| [PR6123](https://github.com/jtobkin/suprafx-platform/pull/6123) | `8415b13a51751928529a27d54b2b8490ff2bfa4f` | Original scheduled approvals, including a narrow demonstrated main-conflict repair. Draft; schema-first release prerequisites open. |
| [PR6129](https://github.com/jtobkin/suprafx-platform/pull/6129) | `9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365` | Actual API/bot/child authority and approved selected pure continuation. Draft stacked on6123. |
| [PR6132](https://github.com/jtobkin/suprafx-platform/pull/6132) | `2b68ff4d0dbeb15032cb7b03fa1cabd4ef406350` | Owner-private workflow storage, exact operation permissions and uncertain upload recovery. Draft stacked on6129. |
| [PR6138](https://github.com/jtobkin/suprafx-platform/pull/6138) | `227de4f57e35cf111788f8bfca4e50a7d75342f5` | Ordinary email recipient authority, owner-only output destination and approval recovery. Draft stacked on6132; source qualified, required CI enqueued once. |
| [PR6141](https://github.com/jtobkin/suprafx-platform/pull/6141) | `c8d5bbaaffb59115d78bf2ca5a29ea1c3e6a0b40` | Eligible project recipient selection; qualified draft successor to6118. Required CI queued; inherited rollout prerequisites open. |
| [PR6118](https://github.com/jtobkin/suprafx-platform/pull/6118) | `d82464efd076c707760e0809f4aa3dccd0150bba` | Separate project dispatch/schema candidate. Not part of the workflow stack above. Seven project packets and operator/client rollout remain prerequisites. |

Other ready candidates6053/6066/6107/6121 remain in the canonical checklist. Re-read live GitHub state before any release action: the table is a timestamped checkpoint, not permission to assume a check passed.

**Never merge a stacked PR into another frozen candidate branch.** Release the predecessor, retarget the successor to main, independently inspect any real conflict, and require the unchanged normal release gates.

## 4. Current email and storage work

Storage candidate6132 restricts actual file-read/file-write to the owner's private `vms-workflow-files` namespace and exact operation grants. Foreign owner/bucket, traversal/encoded aliases and oversized destinations refuse before Storage. W6 receipts bind admission to the original trusted principal. A lost upload reply or in-flight deadline holds an unknown outcome and stops downstream execution; it does not replay the upload. Permission approval does not execute the workflow. The actual Settings card wraps long destinations on phones.

Email candidate6138 resolves interpolated To/Cc/Bcc before exact W6 recipient admission. It passes the actual Gmail attempt callback, holds uncertain sends and stops downstream edges, while retaining existing scheduled-continuation behavior. Its actual owner Settings/API saves exact recipient permission without sending. Read-only status recovers an uncertain decision. Owner-only Resend output rejects a stale saved recipient override; this does not claim exactly-once Resend recovery.

Email source qualification:152 mixed PostgreSQL/PostgREST, unit, local Gmail SDK and mounted browser checks across11 suites. The final changed11-case approval suite was replayed on exact227de; other ten suites retain identical runtime/test blobs. A separate independent13-case run overlaps that set and must not be added as13 new unique tests. Final scoped types114, focused16 and pinned Gitleaks full publication range106 commits passed. Browser checks use actual mounted Settings at320/390/1440, actual Bcc visibility before and absence after account switch, committed database acknowledgment loss, application acknowledgment loss and every HTTP reply dropped after durable approval.

The socket-loss browser case observed multiple raw POST attempts from transport retransmission, but one application dispatch and one new durable grant. Status-only recovery did not issue another application decision. This is real local transport/database/browser evidence, **not** authenticated live Gmail or deployed wallet proof.

## 5. Immediate parallel lanes

The recipient-selection repair is now frozen and published as PR6141, exact `c8d5bbaaffb59115d78bf2ca5a29ea1c3e6a0b40`, on project predecessor6118. It filters connected project-capable relays before ordering and excludes null heartbeat/empty token entries. Ordinary dispatch remains unchanged; SQL retains final server-clock freshness and authorization. Runtime bytes are unchanged since2c40; the final commits add complete producer tests and a narrow test-only typing repair.

The final source has13/13 captured PostgreSQL/PostgREST controls,20/20 canonical tickPlan tests,52 affected types and a75-commit publication secret scan. The actual extracted deliverDispatch producer seals the original reviewed payload and recipient through real SQL before a synthetic Realtime acknowledgment. Denial and post-selection revocation cause no broadcast. These tests do not establish mounted Realtime or live project delivery. Source, schema, operator, client rollout and live acceptance are tracked separately.

W7 now has a complete selective source composition, but remains blocked for release. Runtime `9070a51d5236515429db08551473066f81d7d850` adds retained original execution identity and a target-independent input-provenance claim before the existing exact W6 target admission. It covers both generated registry and legacy MCP shim, supported Chat/headless/Routine callers, and saved project-task claim producers. Chat stops after an uncertain workflow result and replaces premature completion text. Headless execution reports failure; Routines do not re-offer an uncertain tool through AI fallback. Missing original identity holds instead of inventing a new attempt.

Qualification of those exact bytes: independent native registry/MCP30/30 and compatibility128/128, including real mounted Chromium; canonical Chat117/117; a real Chromium case at390/1440 consumes the actual route-produced failed SSE and shows the original reference without false completion or automatic retry. Chat authentication, provider and tool outcome are synthetic in that fixture. Native tests use real disposable PostgreSQL/PostgREST with a reduced schema and synthetic owner/grants. No live authenticated W7 acceptance is claimed. The test-only successor c1f passed651 affected types; full publication secret scanning passed.

A later review found a distinct **project-task settlement race**. An old execution result may arrive after a new executor claims the task. `onTaskFailed` and `onTaskCompleted` do not receive the executed claim identity; they can change the newer task, and completion emits some effects before durable plan settlement. A route reread is insufficient because another writer can win after the reread. Preserved actual cron and owner-route tests fail2/2. This defect also reproduces on exact PR6124, but its implicated production blobs are unchanged from that PR's main baseline and none of PR6124's changed runtime paths calls these handlers. It remains a full-project and W7 blocker; it does not by itself disqualify the separately scoped System Workflow release6124.

The safe partial pre-dispatch fix is frozen at `678d437c009f6cc071e858377551b125a9158a07`: if the saved claim cannot be verified before execution, neither dispatch nor task settlement runs. Focused5/5 route controls and651 affected types pass. Its changed owner waiting UI still needs exact browser proof. The diagnostic successor `3f5da6c261ae0a56ddd6e6dcb3114c7c675fa4f8` preserves the post-dispatch RED. These are blocked work-in-progress source, not qualified releases. Neither is merged, deployed, activated, or authenticated-live verified.

Required next repair: a server-retained original claim token, owner-bound atomic settlement with idempotent receipts, and durable recovery for post-settlement effects. Cover cron, owner project execute, `runExecutionCycle`, and direct authenticated workspace plan actions. Unknown outcome, definite failure, successful completion, head-review revision and plan completion all need positive and superseded-claim tests. Do not claim that a new unused helper or an additional read closes the race.

## 6. Production blockers and exact next actions

1. Keep PR6141 and existing release candidates frozen. Close the demonstrated W7/project-task settlement dependency with claim-bound atomic persistence and recoverable post-commit effects; preserve all RED evidence. W7 caller/provenance composition already has scoped qualification, but settlement and full supported-caller live acceptance remain open.
2. Restore CI disk capacity safely: PR6107 security qualification encountered ENOSPC while writing G10 logs, so infrastructure capacity is now a concrete blocker, not merely queue backlog. Preserve failed evidence; only remove verified disposable owned artifacts, never running containers or another lane. Then rerun infrastructure-failed gates on the same immutable source as needed. Do not change budgets, queue priority or release controls.
3. Release ready no-new-SQL candidates through `scripts/ci/box-ci/merge-if-green.sh`, observe the actual deployed commit, then independently verify relevant deployed behavior.
4. Build/qualify the actual workflow operation in the release operator. The current Money-specific operator does not install these workflow packets. An unused descriptor or a wrapper that merely reaches a refusal is not completion.
5. Establish verified target/CA, one continuous REST/direct-PostgreSQL/Docker/effect exclusion window, old web/cron/external invocation drainage and faithful backup/restore. Wrapper locks alone do not close direct privileged connections or raw Docker writers.
6. Apply only reviewed uninstalled packets, in the qualified operation/order, with same-target ledger/catalog/RLS/ACL/cache readback and compatible web/cron activation. Installed packets must never be replayed.
7. Obtain normal authenticated QA admission through an existing member. The QA wallet cannot sponsor itself; no bypass is authorized. Prior Claude CLI access was signed out. Do not request or paste credentials into chat.
8. Complete independently verified live positive/denied/revoked/failure/recovery journeys and the all-path16-behavior matrix. Provider configuration, including the pending Stripe configuration, remains an explicit external dependency.

Workflow candidate prerequisites include private bucket packet `20261001014500_workflow_files_bucket` plus five ordered workflow packets: `20261001020000_workflow_grant_atomic_admission`, `20261001110000_scheduled_workflow_occurrences`, `20261002100000_scheduled_terminal_approval`, `20261002120000_scheduled_approval_continuation`, and `20261002160000_scheduled_approved_selected_pure`, each with VERIFY. They remain uninstalled at this checkpoint. The project candidate has a separate seven-packet contract; consult its exact source and operator contract rather than combining lists blindly.

W6 is used by manual effects, so default-off scheduling does not make a schema-dependent image a transparent code-only release. Retained originals or grant receipts forbid destructive reverse SQL. Preserve history and a compatible hold-capable image. Never delete history, objects or files to force rollback to pass.

## Broader project work still required

The release stack above is only part of the full plan. The canonical private JSON tracks 33 dependency nodes and 16 behavior goals; node labels such as “complete” can describe a source component, so read its separate release stages before making a project claim.

| Workstream | Current boundary | What closes it |
| --- | --- | --- |
| C1 client context isolation | Reviewed project/personal workspace isolation and installed Claude loopback tests exist. Codex startup failed managed-preferences synchronization before reaching the test provider; Grok/native and real subscription paths remain unqualified. | Qualify managed configuration, real authenticated clients, resume identity, safe file tools, hooks/skills isolation and personal positive controls. Keep unqualified project execution disabled. |
| B1/B2, M1/M2 audience and background privacy | Component source and scoped checks exist; do not equate guarded pages with direct API or background producer coverage. | Compose exact source, verify all direct readers/producers and prove owner/member/private audience behavior on deployed paths. |
| M3 and J1 real transport | Captured native database and client fixtures cover bounded contracts. Synthetic broadcast acknowledgment is not mounted Realtime proof. | Exercise actual authenticated relay/Realtime enqueue, claim, result, reconnect and original-output recovery across cloud and desktop clients. |
| X1 and A1 every execution entry | Entry census and attention/context components remain incomplete as a joined release. | Prove preferences, bounded memory/skills/lessons, permission/audience, cancellation, truthful outcomes and recovery through each named production caller, including background and System Workflows. |
| R2/R3/R3B/C2S production readiness | Runtime-role, Docker and database observer components exist in separate candidates. The actual continuous workflow/project operation is not qualified. | Target/CA provenance, installed catalog/ACL checks, continuous direct-PG/REST/Docker/effect exclusion, drain, faithful restore, ordered schema and compatible rollout. |
| P1 provider/computer readiness | Stripe configuration is still pending. Mail/DNS, calls, real browser worker and Telegram takeover need actual configured acceptance. | Use approved inputs and normal account permissions to verify real provider effects and recovery; preserve originals and avoid duplicate calls, sends or purchases. |
| V1/U1 final acceptance | Full live matrix and owner confirmation are open. | Independently pass all supported paths and all sixteen behaviors, then give the owner precise confirmation tests with expected results and recovery instructions. |

These are retained scope, not optional follow-up improvements. A new session should use the canonical JSON and exact candidate source to determine what is code, evidence, access, approval or deployment work.

## 7. Code map and fresh-computer bootstrap

Start from authenticated Git access, not copied credentials:

```sh
git clone https://github.com/jtobkin/suprafx-platform.git
cd suprafx-platform
git fetch origin
# Example: inspect the frozen email candidate in an isolated checkout.
git worktree add --detach ../supraos-email-review 227de4f57e35cf111788f8bfca4e50a7d75342f5
```

If an exact object is absent, fetch its recorded branch or PR head first and verify the full SHA. For the blocked W7 source, use:

```sh
git fetch origin wip/w7-settlement-blocked-partial-20261003
git worktree add --detach ../supraos-w7-review 678d437c009f6cc071e858377551b125a9158a07
# Separate diagnostic branch includes intentional failing regression tests.
git fetch origin wip/w7-settlement-blocked-red-20261003
```

Do not interpret a published WIP branch or intentionally failing regression as a deployable candidate. Do not substitute whatever main contains today. Read `AGENTS.md`, `CONTEXT.md`, `docs/AI_BUILD_PROTOCOL.md`, relevant `docs/PLATFORM_ARCHITECTURE.md` sections and `docs/DOC_MAINTENANCE.md` before editing. The atlas is large; use targeted sections and actual source callers. Use the recorded lockfile/dependency versions and Node22 environment; do not perform an unrelated dependency upgrade.

| Area | Repository paths |
| --- | --- |
| Workflow runtime and original authority | `lib/vms/workflows/execution-engine.ts`; adjacent checkpoint, grants, scheduling and continuation modules |
| Exact ordinary email | `lib/vms/workflows/notification-recipients.ts`, `notification-grant-requests.ts`, `outcome-delivery.ts` |
| Permission API and mounted owner UI | `app/api/approvals/route.ts`; `app/vms/settings/grants/PendingRequestsSection.tsx`; page metadata in `lib/vms/page-registry.ts` |
| Workflow tool callers and pending identity integration | `core-extensions/workflows/src/tools/{execute_workflow,update_node}.ts`; `lib/vms/workflows/workspace-tools.ts`; `ToolContext.toolExecution`, `lib/harness/tool-execution-identity.ts`, `lib/harness/tool-provenance.ts`, `lib/extensions/tool-provenance.ts`, `lib/security/retained-chain-payload.ts`; inspect blocked W7 branch, not main |
| Project plan execution and settlement | `lib/vms/workflows/plan-orchestrator.ts`; `app/api/cron/mc-coordinator/route.ts`; `app/api/projects/[id]/execute/route.ts`; `app/api/workspace/plan/execute/route.ts` |
| Project dispatch producer | `lib/supraos-build/plan-coordinator.ts`, especially `deliverDispatch`, recipient selection and broadcast |
| Database authority | `supabase/migrations/`; use exact candidate forward/VERIFY packets and the reviewed operator contract |
| Required release guard/CI | `scripts/ci/box-ci/merge-if-green.sh`, `box-ci.mjs` and adjacent library/runner code |
| Current operator foundation | `scripts/qa/money-release-operator.py`; separate C2 candidates contain additional unmerged controls. Do not assume those exist on main. |
| Canonical status and handoff | Branch `docs/paused-workflow-handoff-20261002`, directory `docs/agent-run/handoffs/` |
| Executable regression suites | `tests/unit/*workflow*postgrest.test.ts`, scheduled-approval suites, project dispatch/recovery suites; inspect each test's native/browser opt-in environment |

Canonical private documents: `Ship-Verified-SupraOS-Agent-Workflows.md`, `SupraOS-Workflow-Plan-Checklist.md`, `SupraOS-Workflow-Plan.json`, `Workflow-Production-Operator-Release-Contract.md`, `Client-Isolation-Managed-Preferences-Blocker.md`, and `Signed-Owner-Workflow-Browser-Verification.md`. Older sections are historical; the newest checkpoint supersedes conflicting old status. Some historical component “complete” labels mean implementation only; consult separate release stages.

## 8. Where evidence and data currently live

These original workstation paths are **locations, not portable dependencies**:

- Main Git object store/worktrees: `/Users/joshuatobkin/suprafx-platform` and `/Users/joshuatobkin/qa-lanes/`.
- Workflow release proof: `/Users/joshuatobkin/qa-evidence/pr6034-release-20261002/`.
- Email source publication and scan: `qa-evidence/w2-qualified-release-20261003/`; transport receipt `qa-evidence/w2-email-native-20261003/independent-receipt.md`; final browser receipt `qa-evidence/w2-independent-approval-20261003/final-227/receipt.md`.
- Storage proof: `qa-evidence/w3-selective-composition-20261003/` and `qa-evidence/w3-independent-acceptance-20261003/`.
- W7 baseline and composition: `qa-evidence/w7-tool-identity-red-20261003/receipt.md`, `qa-evidence/w7-source-audit-20261003.md`, and unpublished worktree `qa-lanes/w7-tool-original-admission-20261003/`. Frozen partial678d is published at `wip/w7-settlement-blocked-partial-20261003`; diagnostic3f5 at `wip/w7-settlement-blocked-red-20261003` in the private application repository. These branches were independently fetched/pushed with full publication-range secret scans (114/115 commits); neither has a release PR. Neither is release-qualified.
- W7 claim-settlement design and frozen bundle receipts: `qa-evidence/w7-settlement-20261003/settlement-blocker.md`; caller matrix `qa-evidence/w7-supported-callers-20261003.md`; exact PR6124 inherited-RED receipt `qa-evidence/x2-postdispatch-red-20261003/receipt.md`. Chat/browser evidence is `qa-evidence/w7-held-chat-browser-20261003/receipt.md`.
- Project recipient proof: `qa-evidence/c2-recipient-native-20261003/`; implementation worktree `qa-lanes/c2-recipient-eligible-20261003/`.
- Interactive plan source: `qa-evidence/supraos-execution-plan-20261001/index.html` and `plan.json`. Publication package: `qa-evidence/handoff-20261002/docs-package/`.
- Timed stop receipt: `qa-evidence/pr6034-release-20261002/scheduled-pause.json`; ongoing coordination: `ROOT-CONTINUATION.md` beside it.

Git-published source is portable. Some raw screenshots/logs, incremental Git bundles and disposable verification checkouts are only on the original workstation or authorized Linux verification host. A new computer must obtain those through the owner's authorized artifact transfer or reproduce them from exact source; do not claim that a local path in this document is downloadable or already present. Published test source and receipt hashes identify what to reproduce. No production/customer data was exported into this public handoff.

Production data is separate from Git. The selected authorized Supabase project holds workflow definitions (`vms_workflows`), workflow results (`vms_workflow_run_results`), durable checkpoints (`vms_execution_checkpoints`), project plans (`vms_execution_plans`, including task claims and version), original hash-chain records (`vms_hash_chain`) and signing-key history. The pending migrations add grant-admission receipts, scheduled occurrence/continuation records and the private workflow Storage bucket. Project relay tables and completion queues live in the same source-defined data layer. Consult the exact migration/operator contract for installed versus pending tables; this list is a code map, not an installed-schema claim.

A new computer gets database and provider access through normal authorized account/configuration setup. Locate the selected project via the existing deployment configuration and verify its identity and certificate provenance; do not infer it from a similar hostname or this document. Production rows, credentials, wallet signing material, provider mail/payment data and customer files are not copied into Git or this handoff. Disposable native test databases contain synthetic fixtures and are not production backups. Existing production backup authority and a role/grant-faithful restore rehearsal remain open.

Native verification used PostgreSQL17.11, PostgREST14.18, cached real Chromium/Playwright and synthetic provider endpoints. The verification host has isolated checkouts under `/opt/box-ci/`; host identity/access comes from existing authorized configuration, not this public document. Retain pinned SSH host verification. Never disable TLS/host checks to regain access. Original macOS Chromium/account issues do not justify skipping browser acceptance.

Representative exact email suite invocation in an isolated checkout with those tools installed:

```sh
CI=1 PG_BIN=/usr/lib/postgresql/17/bin \
POSTGREST_BIN=/path/to/pinned/postgrest \
PLAYWRIGHT_BROWSERS_PATH=/path/to/browser/cache \
node node_modules/vitest/vitest.mjs run \
  tests/unit/workflow-notification-actual-caller-boundary.test.ts \
  tests/unit/workflow-notification-request-postgrest.test.ts --maxWorkers=1
```

Read each suite before running: missing opt-in variables may skip native tests. A green command with skipped required cases is not acceptance. Use scoped changed-types and tests; local full builds have caused memory exhaustion. Required hosted production build remains a separate gate.

## 9. Execution and cleanup rules

Keep one coherent candidate frozen. Change it only for a demonstrated release blocker; preserve the failure, narrowly repair it, independently review and verify affected behavior. Give parallel lanes clear file/checkout ownership. New work must close a named delivery dependency, not accumulate unused helpers.

Track implemented, integrated, tested, independently audited, merged, deployed and verified-live separately. Never turn acceptance counts into code-completion or effort percentages. Continue useful independent work while external approvals remain pending; elapsed time does not grant approval.

The merger removes only its own clean, idle, merged worktree using `git worktree remove` without `--force`. Confirm the PR is merged or HEAD is in fresh main, status is empty and no process runs there. Never delete another agent's folder or use blanket pruning. Preserve raw failed evidence and do not kill processes without verified ownership.

## 10. Definition of finished

Every supported execution path and all sixteen behaviors have sufficient positive, denied, revoked, failure and recovery evidence. Required CI passes on the exact released source. Necessary schemas and capabilities are safely installed and activated. Recovery/rollback is tested without deleting retained history. Actual deployed journeys work without privacy leaks, unauthorized actions, duplicate effects or unsupported success claims.

Only after independent live verification provide the owner specific confirmation tests and the final handoff. Missing provider configuration, normal QA access and release authority remain unfinished dependencies. The timed pause is a handoff boundary, not project completion.
