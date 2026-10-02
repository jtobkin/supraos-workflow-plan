# Ship Verified SupraOS Agent Workflows

Working checkpoint: 2026-10-02 17:44 UTC. Execution is active. The owner requested an implementation pause at **2026-10-02 19:36:59 UTC / 2026-10-03 03:36:59 Hong Kong**, followed by an updated handoff and checklist. This checkpoint will be refreshed at that stop. The project is not complete.

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

The three Sol6 agents are now working on the existing W7 workflow-tool retry dependency:

- Implementation owns a separate composition worktree based on frozen email candidate227de. Existing frozen release branches remain unchanged.
- Native verification owns preserved retry failures, real database admission and changed-target/concurrent retry tests.
- Independent review owns the production caller/identity/provenance map, authority boundaries and final source audit.

Exact227de tests reproduced two effects for one repeated execute_workflow request, including a lost provider acknowledgment. The update_node extension similarly repeated a save after success or an uncertain save reply. Those tests inject a server coordinate: they expose the admission gap but do not prove that real callers already propagate that coordinate.

Code review found the historical W7 source depends on a trusted ToolContext and durable input-provenance chain absent from227de. A wrapper-only port would cause existing production calls to refuse. The successor must carry the complete supported caller chain and preserve the original input/target; the target-keyed W6 receipt alone may not prevent changing targets under one call coordinate. Independent PostgreSQL/PostgREST tests on an explicitly recorded historical source overlay confirmed that changed-target and concurrent A/B requests can both save. This is diagnosis of the existing helper/SQL contract, not full historical-source or trusted-caller qualification. No W7 successor is release-ready at this checkpoint.

## 6. Production blockers and exact next actions

1. Keep PR6141 frozen while required CI runs. Finish W7 trusted caller/provenance composition and independent positive, denial, changed-target and uncertain-outcome qualification. Preserve failure evidence; do not ship wrappers without usable production callers.
2. Monitor existing required CI without cancelling it for unrelated source advances. At the last census two jobs were running and92 queued; a queued check is not a pass. Do not change budgets, queue priority or release controls.
3. Release ready no-new-SQL candidates through `scripts/ci/box-ci/merge-if-green.sh`, observe the actual deployed commit, then independently verify relevant deployed behavior.
4. Build/qualify the actual workflow operation in the release operator. The current Money-specific operator does not install these workflow packets. An unused descriptor or a wrapper that merely reaches a refusal is not completion.
5. Establish verified target/CA, one continuous REST/direct-PostgreSQL/Docker/effect exclusion window, old web/cron/external invocation drainage and faithful backup/restore. Wrapper locks alone do not close direct privileged connections or raw Docker writers.
6. Apply only reviewed uninstalled packets, in the qualified operation/order, with same-target ledger/catalog/RLS/ACL/cache readback and compatible web/cron activation. Installed packets must never be replayed.
7. Obtain normal authenticated QA admission through an existing member. The QA wallet cannot sponsor itself; no bypass is authorized. Prior Claude CLI access was signed out. Do not request or paste credentials into chat.
8. Complete independently verified live positive/denied/revoked/failure/recovery journeys and the all-path16-behavior matrix. Provider configuration, including the pending Stripe configuration, remains an explicit external dependency.

Workflow candidate prerequisites include private bucket packet `20261001014500_workflow_files_bucket` plus five ordered workflow packets: `20261001020000_workflow_grant_atomic_admission`, `20261001110000_scheduled_workflow_occurrences`, `20261002100000_scheduled_terminal_approval`, `20261002120000_scheduled_approval_continuation`, and `20261002160000_scheduled_approved_selected_pure`, each with VERIFY. They remain uninstalled at this checkpoint. The project candidate has a separate seven-packet contract; consult its exact source and operator contract rather than combining lists blindly.

W6 is used by manual effects, so default-off scheduling does not make a schema-dependent image a transparent code-only release. Retained originals or grant receipts forbid destructive reverse SQL. Preserve history and a compatible hold-capable image. Never delete history, objects or files to force rollback to pass.

## 7. Code map and fresh-computer bootstrap

Start from authenticated Git access, not copied credentials:

```sh
git clone https://github.com/jtobkin/suprafx-platform.git
cd suprafx-platform
git fetch origin
# Example: inspect the frozen email candidate in an isolated checkout.
git worktree add --detach ../supraos-email-review 227de4f57e35cf111788f8bfca4e50a7d75342f5
```

If an exact object is absent, fetch its recorded branch or PR head first and verify the full SHA. Do not substitute whatever main contains today. Read `AGENTS.md`, `CONTEXT.md`, `docs/AI_BUILD_PROTOCOL.md`, relevant `docs/PLATFORM_ARCHITECTURE.md` sections and `docs/DOC_MAINTENANCE.md` before editing. The atlas is large; use targeted sections and actual source callers. Use the recorded lockfile/dependency versions and Node22 environment; do not perform an unrelated dependency upgrade.

| Area | Repository paths |
| --- | --- |
| Workflow runtime and original authority | `lib/vms/workflows/execution-engine.ts`; adjacent checkpoint, grants, scheduling and continuation modules |
| Exact ordinary email | `lib/vms/workflows/notification-recipients.ts`, `notification-grant-requests.ts`, `outcome-delivery.ts` |
| Permission API and mounted owner UI | `app/api/approvals/route.ts`; `app/vms/settings/grants/PendingRequestsSection.tsx`; page metadata in `lib/vms/page-registry.ts` |
| Workflow tool callers and pending identity integration | `core-extensions/workflows/src/tools/{execute_workflow,update_node}.ts`; `lib/vms/workflows/workspace-tools.ts`; pending trusted `ToolContext.toolExecution` and `lib/harness/tool-execution-identity.ts`/tool provenance producers |
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
- W7 baseline and composition: `qa-evidence/w7-tool-identity-red-20261003/receipt.md`, `qa-evidence/w7-source-audit-20261003.md`, and unpublished worktree `qa-lanes/w7-tool-original-admission-20261003/`. Its state must be frozen and inventoried at pause; do not infer a published branch.
- Project recipient proof: `qa-evidence/c2-recipient-native-20261003/`; implementation worktree `qa-lanes/c2-recipient-eligible-20261003/`.
- Interactive plan source: `qa-evidence/supraos-execution-plan-20261001/index.html` and `plan.json`. Publication package: `qa-evidence/handoff-20261002/docs-package/`.
- Timed stop receipt: `qa-evidence/pr6034-release-20261002/scheduled-pause.json`; ongoing coordination: `ROOT-CONTINUATION.md` beside it.

Git-published source is portable. Some raw screenshots/logs, incremental Git bundles and disposable verification checkouts are only on the original workstation or authorized Linux verification host. A new computer must obtain those through the owner's authorized artifact transfer or reproduce them from exact source; do not claim that a local path in this document is downloadable or already present. Published test source and receipt hashes identify what to reproduce. No production/customer data was exported into this public handoff.

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
