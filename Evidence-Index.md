# SupraOS Workflow Evidence Index

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-05T00:53:37.755392+00:00**. Canonical record SHA-256: `437343b4070e88ac2d35cb0f3d78cd922100b51983b9338f221e8305b2a65e18`.

**Execution state:** Owner authorized an eight-hour implementation run after this documentation rewrite is published and verified. Product edits have not resumed yet; start/deadline will be recorded at activation of the run..

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current candidate record:** `ad2ee680464217fd1b00883bf7ea9fc917ed3140`, tree `d646dcd04525189171ee67fc83098667cac6d290`. Security: PASS 51 steps; build: PASS 7 steps; macOS Native Land: Not run. Merged: False; deployed: False; activated: False; verified live: False. Scope: Qualified partial W7 checkpoint; full scope open. Observed: 2026-10-04T23:50:26Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.

## Reuse before writing code

Missing deployment or live evidence does not mean the implementation is absent. Verify source and authority before extending these assets.

| Existing component | Source / location | Proven scope | What NOT to rebuild |
| --- | --- | --- | --- |
| Partial release baseline | `ad2ee680464217fd1b00883bf7ea9fc917ed3140`; `PR6190; feat/w7-guard-manual-notification-compose-20261005` | Required security51/build7 PASS, source reviewed; Native Land not run | Branch from exact candidate; do not rebuild or discard its passing source merely because main advanced. Full W7 remains open. |
| Original operation ledger and receivers | `ad2ee680464217fd1b00883bf7ea9fc917ed3140`; `lib/vms/workflows/mc-*-effect.ts; claim/effect SQL; actual settler and coordinator` | Original finalization, retry/replay guards, terminal events, retro, estimation and notification have scoped evidence | Extend existing ledger and receiver contracts. Do not introduce another scheduler, effect queue or memory writer. |
| Task admission guard | `cb727d09f964d461942b06aca4bbee0047a2d719`; `20261005220000_mc_task_claim_admission_guard*; fixtures/mc-claim-admission-guard` | 22 native phases/49 outputs PASS c566a19c | Guard is built. Missing work is failure drain/closure, not a replacement guard. |
| Manual notification | `a97bc98bd1cc40e3b3ba079b67d22ea1d2c112be`; `mc-owner-manual-action.ts and existing notification receiver` | 26 unit tests;15 actual manual SQL cases baeb5066; provider/config stubbed | Reuse notification intent after parent; actual TS caller has unit evidence only. Missing manual terminal/retro parity remains. |
| Retro original memory | `2c3e4e996aafbab198c688fa2569dacf481e9b98`; `Original-bound readback and mc-plan-retro-agent-effect.ts` | Exact1c0 import-closure REST af423ff2,10 cases/4 ACK faults | Preserve original public/mapped namespace; broad mapped SELECT remains denied. |
| Estimation and notification recovery | `604ab88d95390d0df8248cfda3d1426333bd619c / 8fd64af7c043f8855449ba5a6c89e6e0cd15f530`; `Actual settlement/cron → parent → original receivers` | Estimation eed6aa56 10 cases/4 ACK faults; notification c593b19b12 cases/2 faults | Reuse existing receiver/harness. Stubbed provider evidence is not real email/Telegram delivery. |
| Projectless and idle cancellation | `301dfc3ed4edcae1251381a959efbc6a36723d6c / 4f7d2ef29ab6a7bcb7613be79d92e96a00181012`; `Existing projectless finalization and cancellation routes` | Projectless18 native cases and scoped idle-cancel/native/browser evidence | Do not rebuild these slices; active cancellation and real L1 remain separate. |
| Wider held source | `PR6129 / PR6132 / PR6138 / PR6118 / PR6141`; `OAuth/child/limits; file authority; notification permissions; exact-workspace commands` | Preserved source/native/browser evidence in baseline task records | Fetch and inspect existing branches and latest dependencies. Do not infer missing code from an unmerged PR or missing live proof. |
| Qualification infrastructure | `Private evidence04795ddf0c18af8d40960ea29993fbf93535f5de`; `root/, sql/, integration/, verification/ reconstructed folders` | Frozen manifests, preserved RED runs, green receipts, cleanup and independent audits | Extract reusable preflight/harness behavior; never rerun archived launchers, consumed claims or stale host snapshots blindly. |

## Evidence reuse and qualification ladder

The complete five-child selected settlement SQL suite passes **38 ordered phases / 81 saved outputs** on exact preserved `3e27866a` source (receipt **d771f442**). Actual failed-task REST (**04bcceb4**) and coordinator-adjustment REST (**fd1edcaf**) pass with real private PostgREST `service_role` transport and committed-ACK recovery. Terminal direct SQL (**1b9e3cb8**), estimation direct SQL (**56b0a323**) and notification direct SQL are separately qualified. These are dated private schemas and synthetic identities, not production installation, JWT/signer, live cron or real L1 evidence.

Preserved failures include legitimate host-inventory refusal, malformed synthetic fixture rows, a timestamp bind-type conflict, and three `.status` assertions against an actual `Promise<void>` finalizer. Corrected fixtures inspect the durable original parent row/receipt and replay equality instead. A new real-TypeScript preflight catches all three old void-return mistakes and passes the corrected fixtures before another native allocation. Esbuild success alone was insufficient. No permissions, rejection assertions, resource floors or required gates were relaxed.

Native source, stage, one-use claim, terminal output, cleanup and independent audit are distinct receipts. Socket-only PostgreSQL and private internal Docker networks avoid production writes; no published fixture ports. Consumed or uncertain attempts are never replayed. Stopped owned scratch retained for later exact cleanup is listed in the private lifecycle handoff. No blanket Docker cleanup, worktree pruning or deletion of another agent's folder occurred.

For each receipt record: exact source commit/tree and imported-file hashes; schema/role/config/runtime fingerprints; test command/version and input identity; positive/negative/recovery scope; outcome and failed evidence; cleanup; independent reviewer; invalidating changes. Mark reuse as scoped parity, never a new execution.

Run in this order when applicable: source/caller inspection → focused regression/types/fixture checks → SQL parse/load and no-host checks → bounded native SQL/REST → independent actual caller and browser review → required exact-source CI → guarded rollout → authenticated live acceptance and tested recovery. Setup failure is not product failure; preserve and diagnose it without weakening budgets. A passing lower step does not substitute for a higher one.

The existing manifests and private packet are the starting point. Consolidation means parameterizing proven harness components during needed work; it is not a separate harness rewrite project. Keep native runs within existing resource controls and distinct owned scratch. Preserve one-use attempt semantics.


## Recovery and source locations

The public plan repository is `jtobkin/supraos-workflow-plan`, branch `main`. Start with the [detailed handoff](https://github.com/jtobkin/supraos-workflow-plan/blob/main/Ship-Verified-SupraOS-Agent-Workflows.md), [full checklist](https://github.com/jtobkin/supraos-workflow-plan/blob/main/SupraOS-Workflow-Plan-Checklist.md), and [dependency plan](https://github.com/jtobkin/supraos-workflow-plan/blob/main/Delivery-Path-Release-Plan.md). These documents are intended to be readable without sign-in. The baseline84f9 documents were anonymously browser-verified. Every new publication requires its own access/rendering check.

Product code is in **private `jtobkin/suprafx-platform`**. A new account needs normal collaborator/team access. Public documentation does not confer product/host/account access, and no credentials should be copied from the old computer.

| Saved branch | Exact local source commit at closeout inventory | Old computer path (not required on a new computer) |
| --- | --- | --- |
| `feat/w7-r1-main-composition-20261005` | `1c0e12c00717ff94572f64f821ab0663aeb54d28` | `/Users/joshuatobkin/qa-lanes/w7-r1-main-composition-20261005` |
| `fix/w7-claim-admission-guard-20261005` | `cb727d09f964d461942b06aca4bbee0047a2d719` | `/Users/joshuatobkin/qa-lanes/w7-claim-admission-guard-20261005` |
| `feat/w7-estimation-retro-notification-composed-20261005` | `e9689db0a52fe690edfe5bb40b85b926affc138c` | `/Users/joshuatobkin/qa-lanes/w7-estimation-retro-notification-composed-20261005` |
| `feat/w7-plan-estimation-reconcile-20261005` | `604ab88d95390d0df8248cfda3d1426333bd619c` | `/Users/joshuatobkin/qa-lanes/w7-plan-estimation-reconcile-20261005` |
| `feat/w7-plan-notification-recovery-20261005` | `8fd64af7c043f8855449ba5a6c89e6e0cd15f530` | `/Users/joshuatobkin/qa-lanes/w7-plan-notification-recovery-20261005` |
| `fix/w7-retro-bound-readback-20261005` | `2c3e4e996aafbab198c688fa2569dacf481e9b98` | `/Users/joshuatobkin/qa-lanes/w7-retro-bound-readback-20261005` |
| `fix/w7-recovery-writer-catalog-e968-20261005` | `87e5cb00064b39d9fdb27799129026b25395d2dc` | `/Users/joshuatobkin/qa-lanes/w7-recovery-writer-catalog-e968-20261005` |
| `feat/w7-projectless-finalization-20261005` | `301dfc3ed4edcae1251381a959efbc6a36723d6c` | `/Users/joshuatobkin/qa-lanes/w7-projectless-finalization-20261005` |
| `feat/w7-project-cancel-atomic-20261005` | `4f7d2ef29ab6a7bcb7613be79d92e96a00181012` | `/Users/joshuatobkin/qa-lanes/w7-project-cancel-atomic-20261005` |
| `feat/w7-plan-retro-agent-effect-20261005` | `6951a00f3d020862a3b53c5b3f9b6eb02590ec56` | `/Users/joshuatobkin/qa-lanes/w7-plan-retro-agent-effect-20261005` |
| `feat/w7-mc-critical-escalation-effect-20261004` | `3e27866a5d880eaa32375a857ffa0ca67d0341c1` | `/Users/joshuatobkin/qa-lanes/w7-mc-task-failed-effect-20261004` |
| `fix/w7-telegram-gate-durable-notification-20261005` | `53840e26a20c903ca816fe229477e38f579b5499` | `/Users/joshuatobkin/qa-lanes/w7-manual-plan-notification-20261005` |
| `feat/w7-guard-manual-notification-compose-20261005` | `82838240d57ce81d26a5bdda723c0f38f5a5a8d7` | `/Users/joshuatobkin/qa-lanes/w7-guard-manual-compose-20261005` |
| `fix/guard-catalog-blocker-20261005` | `ad2ee680464217fd1b00883bf7ea9fc917ed3140` | `/Users/joshuatobkin/qa-lanes/w7-guard-catalog-blocker-20261005` |

Fourteen selected local lane heads were inventoried and exact remote refs verified at the prior closeout; recheck before execution. The `w7-guard-manual-compose` worktree remains at `828` while its GitHub candidate branch advances to `ad2`; `w7-r1-main-composition` remains at `1c0`. No worktree was deleted.

Core code map:

- `lib/vms/workflows/plan-orchestrator.ts`: actual task claims, settlement, effect dispatch and integration; `mc-plan-finish-intents.ts`, `mc-manual-transition.ts`, `mc-owner-manual-action.ts`: terminal/manual intent construction and caller behavior.
- `lib/vms/workflows/mc-*-effect.ts`: original-operation finalization, estimation, notification, retrospective, terminal event and other durable receivers/reconciliation.
- `app/api/cron/mc-coordinator/route.ts`, `app/api/workspace/plan/execute/route.ts`, `app/api/workspace/plan/route.ts`, `app/api/projects/[id]/execute/route.ts`: real server entry points and recovery callers.
- `components/vms/workflow/ParallelDashboard.tsx` and the actual workspace page: mounted user behavior; source and browser tests under `tests/unit/`.
- `supabase/migrations/20261003120000_mc_task_claim_settlement*` and ordered 20261004/20261005 forward/VERIFY/ROLLBACK packets: authority, original claims/results and receiver SQL. Never install a directory glob as migration order; verifier and rollback files coexist with forwards.
- `supabase/migrations/20261005220000_mc_task_claim_admission_guard*` and `tests/fixtures/mc-claim-admission-guard/contract.cjs`: new admission policy and real lock/recovery contract.
- `lib/db-as-owner.ts`, `lib/vms-config.ts`, original-bound retrospective readback and integrity gateway: original memory namespace and narrow authority; broad mapped-schema SELECT intentionally remains denied.
- `scripts/qa/w7-operation-gate.py`, `w7-bootstrap-install.js`, `w7-proxy-hold.py`, and `docs/agent-run/w7-operation-bound-release-admission.md`: release controls and guarded operator packets. Read repository `AGENTS.md`, `CONTEXT.md`, build protocol and `docs/PLATFORM_ARCHITECTURE.md` before editing.

Old evidence root: `/Users/joshuatobkin/qa-evidence/resume-delivery-20261005/`. It contains `root/` fixtures, `integration/` code/CI evidence, `sql/` host lifecycle and native receipts, `verification/` independent audits/screenshots, `grok/` read-only results/adjudications, and `closeout-status/` transfer records. The old local machine plan is `/Users/joshuatobkin/qa-evidence/supraos-execution-plan-20261001/plan.json`. It and reconstructed snapshots are historical inputs after this documentation rewrite. Current documentation authority is public `workflow-plan.json`, with generated views and explicit evidence limits.

The final additive private packet is saved at commit **`04795ddf0c18af8d40960ea29993fbf93535f5de`**, [five-hour closeout evidence](https://github.com/jtobkin/suprafx-platform/tree/04795ddf0c18af8d40960ea29993fbf93535f5de/docs/agent-run/evidence/five-hour-workflow-closeout-20261005). All 1,036 transport files were remotely byte-verified. Independent reconstruction verified 2,291 original files and 957 content objects across 55 evidence roots; plaintext scans passed with zero unresolved findings. The immutable archive was frozen before the final CI/public-document checkpoint, so this public handoff records later results. Product/evidence access requires normal private-repository permission.

The earlier base packet remains at `316999ab481ab57c582dd45ee7e1f4be4378898f`, private branch `docs/paused-workflow-handoff-20261002`, directory `docs/agent-run/evidence/five-hour-workflow-qualification-20261005/`: 615 restored original files, 252 content objects, 276 remotely verified transport files. Restore base and closeout into separate brand-new directories. Each packet's README/reconstruct.py verifies encoded chunks, objects and original file hashes; reconstruction executes no archived launcher.

On a fresh machine:

```sh
git clone https://github.com/jtobkin/supraos-workflow-plan.git supraos-plan
git clone --filter=blob:none https://github.com/jtobkin/suprafx-platform.git supraos-product
git -C supraos-product fetch origin
```

Fetch the named exact source/evidence commit and compare its SHA. Create a new owned worktree; do not substitute current main or reset another session's checkout. Install supported Node 22 dependencies from the repository lockfile, Python 3, pinned Gitleaks 8.28 and a working Linux Playwright/Chromium environment. Obtain normal host/account access separately. Read the private closeout README, restore evidence and consult its lane handoffs and source inventory before selecting the next owned task.

Old wrappers bind dated paths, inventories and consumed one-use claims. A new run requires fresh source/host admission and unique owned scratch; do not blindly replay archived commands, copy credentials, or retry an uncertain side effect. The shared old product checkout contains unrelated staged work and must not be reset/cleaned. Only the merging owner removes its own merged, clean, idle worktree with ordinary `git worktree remove`; never force or prune another lane.

## Updating and handing off this plan

1. Read this revision, the canonical record and product repository instructions before starting. Inspect existing code and receipts; distinguish missing code from missing proof/access.
2. Update `workflow-plan.json`: current evidence, task stages, actual blocker, named owner, next proof, exact candidate and timestamps. Retain historical baseline records and all task acceptance criteria.
3. Run `python3 scripts/render_plan.py`, then `python3 scripts/render_plan.py --check`. The check verifies scope, policy IDs, an acyclic graph and exact generated bytes. It does not verify product behavior.
4. Publish the record and generated files in one reviewed commit. Secret-scan plaintext before uploading evidence; encoding is not sanitization. Reuse the existing hash-manifest packaging and independent reconstruction checks.
5. Verify remote bytes and anonymous browser rendering for the three entry documents, all 33 checklist rows and the dependency graph. Record the publication/browser receipt separately; avoid a self-referential commit-hash rewrite loop.

Checkpoint report: **usable capability advanced; dependency closed; exact blocker and category; accountable owner; proof needed; next action; source/test/review/merge/deploy/activation/live state; elapsed delivery time**. Unknown timestamps remain unknown. Publish on meaningful dependency closure, blocker change, pause or handoff—not after every tool call.

The generator catches missing rules and stale generated views when run. `AGENTS.md` instructs future agents to run it; no runtime enforcement in SupraOS Build or mandatory GitHub branch protection has been installed by this documentation change.
