# Ship Verified System Workflow Outcomes

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-05T05:05:23Z**. Canonical record SHA-256: `86fbfafbd895f64e66e341e35dd899956021072c1dbc8f4605319de36262ba48`.

**Execution state:** RESUMED 2026-10-05 ~05:00Z after an owner pause at ~04:47Z. Required CI on the frozen candidate `3214f4849e` is RED (box-ci/security-gates FAILURE; box-ci/production-build ERROR, not built because gates failed), so that candidate is NOT releasable. The root session is preparing a new commit (three defect fixes plus a merge of origin/main). At the pause: PR #6196 head `3214f4849e3bb0517b60ee17821826918ee11147`; production ledger 691 rows with 0 of 24 W7 packets installed; no merge. Standing order unchanged: do not install schema or merge until both box-ci statuses are success on the current head; then apply and verify the 24 packets on production → merge via `scripts/ci/box-ci/merge-if-green.sh 6196` → deploy → independent live acceptance. No W7 merge, deployment, activation or authenticated live acceptance has occurred.

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** Candidate `3214f4849e3bb0517b60ee17821826918ee11147` on branch `claude/w7-drain-rerun-compose-20261005` (PR [#6196](https://github.com/jtobkin/suprafx-platform/pull/6196)) is **not releasable**. Owner paused the run at 2026-10-05 ~04:47Z; at the pause the PR head was that commit, the production ledger held 691 rows with 0 of 24 W7 packets installed, and nothing was merged. **Trailing audit at `3214f4849e`: PASS, but scoped** — on cc-box (PostgreSQL 17.11, Node 22): native contract 26/26 with the committed fixture (populated-rollback refusal, empty rollback + reapply); ordered 24/24 packet install + VERIFY as non-superuser `postgres` via `scripts/apply-migration.mjs`; browser 46/46 archived cases + 2/2 new F1 lane checks (Playwright, Chrome 152); unit 896 pass / 0 fail / 7 skipped (scoped set; live-PostgREST skips); relay x1-bridge 28/28. Evidence: private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `b662bfbc49`, `docs/agent-run/evidence/w7-resume-20261005/live/verify/trailing-3214f4849e/RESULTS.md`. **Required CI (run resumed ~05:00Z): RED** — box-ci/security-gates FAILURE, box-ci/production-build ERROR (not built because gates failed); log `cc-box:/opt/box-ci/logs/2026-10-05/3214f4849e-gates-muurr0r1.log`. Whole unit tree: 2 failed / 55,609 passed / 374 skipped (4,508 files). Three defects, all in the candidate, none caught by the scoped audit: (a) `tests/unit/queried-tables-exist.test.ts`: `lib/vms/workflows/mc-failure-drain.ts:31` queries `vms_mc_plan_birth_guards`, which is not in the checked-in schema snapshot and has no pending-install baseline entry; (b) `tests/unit/model-adapter-verified-agent-policy.test.ts`: a merge resolution in `lib/harness/enforce.ts` starts a second, unneeded `vms_agents` scope read when the verified-scope path is on (expected 1 read, got 2); (c) scoped changed-file TypeScript check: `tests/unit/owner-db-runtime-binding.test.ts` lines 27–34 cast partial objects to `NodeJS.ProcessEnv` (5 errors). Honest reading: the trailing-audit PASS was a scoped run; the full-tree gate is the authority and it is red. The root session is preparing a new commit: the fixes plus a merge of origin/main, which moved `877f3d082e` → `7a10b7a3fc` with 3 commits (#6193, #6109, #6195). Agent Run PR #6168 is still OPEN (not merged). Stage truth: implemented yes; integrated yes (candidate being re-cut); tested = scoped PASS, full-tree RED; reviewed = trailing audit PASS at the old sha only; merged no; deployed no; activated no; live no. Standing order unchanged: do not install schema or merge until both box-ci statuses are success on the current head; then apply and verify the 24 packets on production → merge via `scripts/ci/box-ci/merge-if-green.sh 6196` → deploy → independent live acceptance

**Current candidate record:** `3214f4849e3bb0517b60ee17821826918ee11147`, tree `(see git)`. Security: box-ci/security-gates FAILURE on 3214f4849e (whole unit tree: 2 failed / 55,609 passed / 374 skipped across 4,508 files; scoped changed-file TypeScript check 5 errors); build: box-ci/production-build ERROR on 3214f4849e (not built because security gates failed); macOS Native Land: Not run (not part of box-ci). Merged: False; deployed: False; activated: False; verified live: False. Scope: Composed W7 failure-drain/rerun candidate (partial W7; full scope open). Required CI RED: NOT releasable as cut. A replacement commit (three defect fixes + merge of origin/main) is being prepared; this record must be updated to the new head and its own CI result when it lands. Scoped trailing audit PASS at this sha does not override the full-tree gate. Observed: 2026-10-05T05:05:23Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.


## Status 2026-10-05 ~05:00Z — candidate `3214f4849e` is NOT releasable (read this first)

The section below this one describes the earlier pause at ~02:04Z and is kept as dated history. Since then the three saved lanes were composed into one candidate, the owner paused again, and required CI came back red.

- **Owner pause, 2026-10-05 ~04:47Z.** At the pause: PR [#6196](https://github.com/jtobkin/suprafx-platform/pull/6196), branch `claude/w7-drain-rerun-compose-20261005`, head `3214f4849e3bb0517b60ee17821826918ee11147`; production ledger 691 rows, 0 of 24 W7 packets installed; no merge.
- **Trailing audit at `3214f4849e`: PASS (scoped).** On cc-box (PostgreSQL 17.11, Node 22): native contract 26/26 with the committed fixture (populated-rollback refusal, empty rollback + reapply); ordered 24/24 packet install + VERIFY as non-superuser `postgres` via `scripts/apply-migration.mjs`; browser 46/46 archived cases + 2/2 new F1 lane checks (Playwright, Chrome 152); unit 896 pass / 0 fail / 7 skipped (scoped set; live-PostgREST skips); relay x1-bridge 28/28. Evidence: private branch `docs/w7-resume-evidence-20261005` @ `b662bfbc49`, `docs/agent-run/evidence/w7-resume-20261005/live/verify/trailing-3214f4849e/RESULTS.md`.
- **Required CI on `3214f4849e`: RED (run resumed ~05:00Z).** box-ci/security-gates FAILURE; box-ci/production-build ERROR (not built because gates failed). Log: `cc-box:/opt/box-ci/logs/2026-10-05/3214f4849e-gates-muurr0r1.log`. Whole unit tree: 2 failed / 55,609 passed / 374 skipped (4,508 files).

Three defects, all in the candidate, none caught by the scoped audit:

1. `tests/unit/queried-tables-exist.test.ts` — `lib/vms/workflows/mc-failure-drain.ts:31` queries `vms_mc_plan_birth_guards`, which is not in the checked-in schema snapshot and has no pending-install baseline entry.
2. `tests/unit/model-adapter-verified-agent-policy.test.ts` — a merge resolution in `lib/harness/enforce.ts` starts a second, unneeded `vms_agents` scope read when the verified-scope path is on (expected 1 read, got 2).
3. Scoped changed-file TypeScript check — `tests/unit/owner-db-runtime-binding.test.ts` lines 27–34 cast partial objects to `NodeJS.ProcessEnv` (5 errors).

**Honest reading:** the trailing-audit PASS was a scoped run; the full-tree gate is the authority and it is red. Candidate `3214f4849e` is therefore not releasable. The root session is preparing a new commit: the fixes plus a merge of origin/main, which moved `877f3d082e` → `7a10b7a3fc` with 3 commits (#6193, #6109, #6195). Agent Run PR #6168 is still OPEN (not merged).

**Standing order (unchanged):** do not install schema or merge until both box-ci statuses are success on the current head; then apply and verify the 24 packets on production → merge via `scripts/ci/box-ci/merge-if-green.sh 6196` → deploy → independent live acceptance.

| Stage | State now |
| --- | --- |
| Implemented | Yes |
| Integrated | Yes (candidate, being re-cut) |
| Tested | Scoped PASS; full-tree RED |
| Independently reviewed | Trailing audit PASS at the old sha only |
| Merged | No |
| Deployed | No |
| Activated | No |
| Verified live | No |

## Current pause handoff — start here on a new computer

**Read order:** this pause checkpoint → [full checklist](SupraOS-Workflow-Plan-Checklist.md) → [dependency plan](Delivery-Path-Release-Plan.md) → private evidence README → product `AGENTS.md`, `CONTEXT.md`, build protocol and architecture. Public `workflow-plan.json` is the current status authority. Older documents, worktree paths and test counts are dated evidence, not instructions to repeat completed work.

### What this session is trying to deliver

Deliver SupraOS workflows and project execution that use the right owner's context and permissions, preserve original operation identity across retries and recovery, and report truthful results across all supported entry points. The immediate useful milestone is **failure drain with safe rerun recovery**: when a critical task fails, unstarted work can stop safely, active or uncertain work stays accounted for, terminal effects wait for truthful closure, and retrying a lost rerun response recovers the original operation rather than creating another run. This is a partial W7 milestone. All 33 task contracts, 16 behavior families and 12 supported surfaces still define full completion.

### Exact saved source and ownership

All three branches below live in **private `jtobkin/suprafx-platform`**, share the `ad2ee680464217fd1b00883bf7ea9fc917ed3140` baseline and were pushed and read back at pause. No branch was merged, deployed or activated. They must be reconciled into one coherent candidate; do not deploy one independently or assume a passing baseline gate covers a successor.

| Lane / previous owner | GitHub branch | Exact saved commit | State |
| --- | --- | --- | --- |
| Server/SQL failure drain — `/root/catalog_blocker` | `fix/w7-critical-failure-drain-20261005` | `48751b50252cb66555d0b427a47930d1bc68adb9` | Two committed changes; final tree `f4b577e5665be167e594662155afa9c99e4d6214`; final native contract unrun |
| Client integration — `/root` | `fix/w7-rerun-request-binding-20261005` | `2dc7e3809278e071b9183cdbe53062d88e297b7d` | Seven committed files; tree `72234a6a142f559ef37fe67124fece2a5508cf58`; scoped mounted browser evidence |
| Runtime prerequisite — `/root/native_closeout` | `codex/w7-runtime-binding-refresh-20261005` | `82b010441ad1a82e66368585f7ddd68d5cfc9103` | Eleven committed files; actual helper/bridge private native proof; target role installation pending |

`/root/closeout_audit` independently checked evidence and mounted browser behavior. Agent names describe previous ownership only: assign fresh available owners before resuming. Local lane folders remain under `/Users/joshuatobkin/qa-lanes/` with the same names as their purpose; all are unmerged and retained. The shared `/Users/joshuatobkin/suprafx-platform` checkout contains unrelated staged work; do not reset, clean, or use it as an integration scratch directory.

### What changed in the paused run

1. **Server/SQL failure drain:** strict all-terminal closure; SQL-positive initial task birth provenance; safe drain of positively unstarted siblings; preservation of original active-result/manual replay; closing-claim parent authorship; atomic action-bound rerun and once-only initialization; run-bound execution admission; deferred receipt-bound run replacement; forward/VERIFY/guarded rollback packets. Unknown original admissions remain immutable and legacy/no-provenance tasks stay held. Active cancellation is still incomplete.
2. **Actual callers:** project execution, workspace execution/manual actions, coordinator recovery and initialization use the revised drain/rerun boundary. The server, new SQL and client request contract must be qualified together. Pre-save department-share and assignment-log effects during initialization can remain uncertain on interruption; durable unknown blocks retry/provider admission. This is an explicit remaining boundary, not an all-effects atomicity claim.
3. **Mounted rerun recovery:** persist a wallet/project-scoped action before POST; reuse its original plan/run/version after reload or lost acknowledgment; refuse dispatch if persistence is unavailable/corrupt; prevent duplicate click/automatic execution; retain unknown responses; clear only the matching authoritative response; execute only a ready current original run. Wallet/project navigation clears stale local UI state. Recovery remains accessible when timeline data is missing, and mobile controls no longer overlap.
4. **Runtime binding:** restored and integrated the saved owner-runtime identity design into the real owner database helper and coordination bridge. Configuration changes across awaited BEGIN/identity/role setup and pre-COMMIT are refused. This source does not install the runtime database role or prove hosted pooler compatibility.
5. **Release feasibility:** independently reviewed read-only target censuses distinguish missing installed W7 schema/role from existing dependencies. A concrete role reconciliation plan reuses saved B0 SQL and names the missing caller bindings and ACL/policy proof. Release operator evidence producers still need integration.

### Evidence: what passed and what did not

| Capability | Evidence retained | Boundary still open |
| --- | --- | --- |
| Failure drain and atomic rerun source | 92 caller tests / seven files and 58-file scoped types before final small hardening; independent four-file 66-test run on final `48751b50`; final pinned G11 over both commits PASS | Complete final SQL/source review, source-bound native bundle, all 26 ordered native cases, later-trigger coinstallation, rollback/reapply and actual combined execution have NOT run |
| Catalog / schema preflight | 34 catalog tests before the final three hazard entries; add-only catalog command's built-in reconciliation PASS; final catalog 2,656 writers / 5,181 hazards; earlier schema/migration checks PASS | Last standalone scanner RED preserved; final standalone rerun not started at pause. Strict E3 remains unresolved: last printed readiness RED 6,568 before three additions. This is not a current clean E3 result |
| Mounted rerun client | 12 helper tests; earlier 46-test/four-file regression and 19-file types; independent real Linux Chromium at 390/1440: prior 32-case base, eight affected navigation/storage repairs, final six recovery/layout cases PASS with screenshots inspected | Test sets cover different source revisions; do not add them into one exact-candidate pass count. Final UI type/regression gate after the last CSS/button patch and combined release/browser/live gates remain open |
| Runtime identity helper and bridge | 47 focused tests, 28 bridge tests, 23-file types; independent source review; exact `82b01044` actual helper/bridge private PostgreSQL v2: all 19 cases PASS, including configuration drift and withheld committed acknowledgment | Private schema/admission fixtures and cached pinned dependencies; not hosted role/ACL/pooler, production, exact lockfile installation or final combined gate proof |
| Read-only installed target | Two separately reviewed repeatable-read snapshots: selected W7 36 functions / eight tables / 15 migration entries absent; runtime role absent; 11 dependency relations present; selected 12 B0 tables and five function bodies compatible | Selected metadata only; not complete schema/ACL/default privileges, a shared snapshot, backup/restore, writer exclusion or live acceptance |

Preserve failures: mounted-browser v3 stale wallet modal RED; mobile overlap screenshots; runtime native v1 HBA setup rejection before product assertions; initial source/fixture/catalog REDs; native caller bundle refusal for ignored generated indexes; G11 wrapper's network download failure. Repairs and later passes do not erase those records. Runtime v1's owned scratch was deliberately retained with no owned Docker resources; v2 scratch/resources were removed and independently checked. Inventory proof is terminal observations, not continuous monitoring.

Key exact review hashes and relative paths are indexed in the private evidence packet. Examples: runtime final independent terminal `e10bcc25d94b1d80bf86addb69b8fe843a20a219b82cba6fbfc07ec9ad172d39`; UI final recovery/layout review `e6b6c8ffec9da521aeb0ecc183cb3623c0bdaeebdbac6104a3832885754ca456`; independent pause inventory `cc3edb2c387a97b13dd39dd0cad817a8b52335f2ca3b54fdbfb2e56b7972b9d7`. These are SHA-256 receipt hashes, not Git commits.

### Where the new code and evidence live

- Drain and finalization: `lib/vms/workflows/plan-orchestrator.ts`, `execution-plan.ts`, `mc-manual-transition.ts`, `mc-owner-manual-action.ts`, plus the actual project/workspace/coordinator route callers. Inspect `git diff ad2ee680...48751b50` for the full committed file list before assigning ownership.
- New authority SQL: `supabase/migrations/20261005230000_mc_critical_failure_drain{,_VERIFY,_ROLLBACK}.sql` and `20261005231000_mc_run_rerun_atomic{,_VERIFY,_ROLLBACK}.sql`. Forward, verifier and rollback files coexist: never install a glob as migration order.
- Native drain fixture: `tests/fixtures/mc-critical-failure-drain/`, including `build-native-callers.mjs` and 26-case ordered contract/oracle. Draft actual-caller bundle `native-callers-next.cjs`, SHA-256 `b63dfe4f3c8c4d1f9967b1a55d88c4c0c2f96807a49dce3c64bef1115b2938fa`, still needs a manifest bound to exact committed source blobs and independent review before dispatch.
- Client: `app/vms/mission-control/[projectId]/page.tsx`, `project.css`; `lib/vms/workflows/mc-rerun-request.ts`, `timeline-types.ts`, `timeline-assembler.ts`; `tests/unit/mc-rerun-request.test.ts`; `docs/agent-run/mc-rerun-request-recovery.md`.
- Runtime: `lib/db-as-owner.ts`, `lib/owner-db-runtime-binding.ts`, `lib/supraos-build/coordination-mcp-x1-bridge.ts`, relay coordination route and the committed bridge implementation/tests. `git show --stat 82b01044` gives the exact eleven-file map.
- Current local evidence: `/Users/joshuatobkin/qa-evidence/workflow-execution-20261005-0101/` has `run.json`, `progress.json`, `root/`, `release/`, `verification/`; `/Users/joshuatobkin/qa-evidence/workflow-plan-rewrite-20261005/implementation/failure-drain/` has source/fixture logs and `user-pause-handoff.md`. Local paths identify provenance, not a requirement to have this Mac.
- Private runtime closeout: `release/runtime-binding/native-terminal-summary-final.json`; `release/runtime-role-reconciliation-plan.md`; independent draft wrapper review `release/drain-rerun-wrapper-draft-independent-review.json`.
- Draft native runner: `verification/drain-rerun-native-v1/`. It is UNFROZEN, unbundled and unexecuted; placeholder refusal must remain. Existing budgets: 16 GiB memory/50 GiB storage floor, 2,400-second outer bound, owned scratch and one-use admission. Reuse and finish it rather than starting a new harness.

### First five tasks after an explicit resume

1. **Root: verify and join the saved source without rebuilding it.** Fetch all three exact branches, compare commits, read this packet and current repository instructions. Assign exclusive files to three lanes. Decide the smallest failure-drain/rerun release manifest while retaining full W7/project scope. Freeze the combined source only when its coherent caller/SQL/UI contract is ready.
2. **Implementation lane: close the narrow remaining drain qualification preparation.** Explicitly seed `triggered_by='user_initial'` in the fixture instead of depending on a schema default; independently review final terminal-snapshot/run-replacement guards; rerun affected cheap checks; bind actual caller bundle inputs to committed blobs. Preserve all expected rejections and held unknowns. Source edits require a new exact successor pin.
3. **Independent verification lane: finish and qualify the existing immutable packet.** Review the reviewer-owned runner independently; full ordered later-trigger coinstallation, 26 contract cases, both lock orders/concurrency, committed ACK loss, populated rollback refusal clone, empty rollback and reapply. Then qualify the joined client/server real caller path and mounted browser recovery. Preserve failed evidence and make only narrow demonstrated repairs.
4. **Prerequisite lane in parallel: close actual release dependencies.** Implement/mount accepted-work/all-writer/backup evidence producers in the existing operation gate, reconcile runtime role packet bindings and current target ACL/default privileges/policies, prove guarded restore and pooler behavior, obtain normal QA access. Each step needs an owner and exact acceptance proof. Do not wait for Stripe to do independent implementation/qualification; do not infer release permission from a missing reply.
5. **Root: required gates and guarded delivery.** Once code and feasibility are proven, independently review one frozen candidate, pass required checks on that exact source, use supported PR merge/installation/deployment/activation, then independently verify authenticated behavior and recovery on the deployed revision. Only then offer concrete owner tests. If an external dependency still blocks release, keep its exact request current and close eligible remaining scope without declaring the milestone or project complete.

### Blockers and plain-language access guidance

**Missing code/integration:** final drain fixture/source manifest and native package; remaining W7 effects/manual parity/active cancellation/L1; release operation gate producers; final three-branch composition. **Missing evidence:** full current-target role/ACL/pooler/restore proof; exact combined native/browser/CI; installed/live journeys. **Access/provider:** normal invite-only QA access and Stripe Link configuration remain unresolved.

The earlier administrator question was too broad. A non-superuser `postgres` account is normal on managed Supabase; do not seek or invent unrestricted superuser access. The observed privileged/managed sessions are not proof that they were actively writing. The practical need is an authorized, supported way to prevent conflicting writes during this specific rollout and restore safely if necessary. First inspect existing release controls and normal project-management/backup access, then make the smallest concrete request. The owner did not know which administrator/ticket to name, and no approval was granted by that answer. CLI/token absence in one observed process is not proof that every browser/account lacks access.

`scripts/qa/w7-operation-gate.py` still refuses around its continuous-hold and accepted-work/all-writer/backup boundaries; do not remove those refusals to ship. The preserved eight-file `62b77ad2fdaef5057409ac71d16f6e0b94171c97` runtime packet contains **B0 only**, not B1. Restore/reconcile its proven B0 SQL and bind actual current callers first; retain the separate gate-six successor and default-ACL/policy work. Its verifier does not independently census `pg_default_acl`.

### Fresh-machine recovery and safe restart

The plan repository is public and requires no sign-in. Product code and detailed evidence require normal access to private `jtobkin/suprafx-platform`; do not copy credentials into any document.

```sh
git clone https://github.com/jtobkin/supraos-workflow-plan.git supraos-plan
python3 supraos-plan/scripts/render_plan.py --check
git clone --filter=blob:none https://github.com/jtobkin/suprafx-platform.git supraos-product
git -C supraos-product fetch origin fix/w7-critical-failure-drain-20261005 fix/w7-rerun-request-binding-20261005 codex/w7-runtime-binding-refresh-20261005
git -C supraos-product show --no-patch 48751b50252cb66555d0b427a47930d1bc68adb9
git -C supraos-product show --no-patch 2dc7e3809278e071b9183cdbe53062d88e297b7d
git -C supraos-product show --no-patch 82b010441ad1a82e66368585f7ddd68d5cfc9103
git -C supraos-product worktree add -b resume/w7-drain-review ../supraos-w7-drain 48751b50252cb66555d0b427a47930d1bc68adb9
```

Choose a fresh unused branch/folder; the example does not merge the other lanes automatically. Restore evidence from the private packet instructions below into a new directory; reconstruction verifies bytes and must not execute archived launchers. Use supported Node 22, lockfile dependencies, Python 3, pinned Gitleaks 8.28 and working Linux Chromium/Playwright. macOS Chromium startup failed in this session; Linux browser evidence is available. Read current resource/release controls before native allocation. Do not run a full Mac Next build or blindly replay old one-use host claims. Older packet timestamps and local paths are historical. Nobody needs to recreate this Mac's absolute paths to read the code or plan.

### Working method and pause state

Root orchestrates; one lane owns shared implementation files, one resolves release prerequisites, and one independently reviews/tests the same delivery path. Additional agents get bounded dependencies with exclusive files; agent count is not a speed metric. Freeze one candidate, preserve failed evidence, run cheap preflight before native allocation, reuse valid evidence by its exact inputs, and keep required final gates on final source. A helper needs a named production caller, integration owner and acceptance test. Keep all 13 permanent principles below in future handoffs.

All product lanes are paused. No qualification or deployment is scheduled to restart automatically. Source folders are retained because they are unmerged. After a future merge, only the merging owner may remove its own clean idle worktree with ordinary `git worktree remove`; no force or blanket prune. Session success here is portable, truthful preservation—not release completion.


## Portable private evidence for this pause

The new immutable packet is saved in private `jtobkin/suprafx-platform` on branch `docs/workflow-pause-evidence-20261005-0101`, commit **`74fd979aa5c0237076ca3547eb5acb8366a26d73`**:

[Open the exact private recovery packet](https://github.com/jtobkin/suprafx-platform/tree/74fd979aa5c0237076ca3547eb5acb8366a26d73/docs/agent-run/evidence/workflow-pause-20261005-0101) · [README and recovery instructions](https://github.com/jtobkin/suprafx-platform/blob/74fd979aa5c0237076ca3547eb5acb8366a26d73/docs/agent-run/evidence/workflow-pause-20261005-0101/README.md).

It preserves **406 original files / 319 distinct content objects, zero omissions**, across `workflow-execution-20261005-0101` and `workflow-plan-rewrite-20261005/implementation`. Manifest SHA-256: `4c9281938bd4ad3877d80febd84594241af71a7a6cfb7e253cd488cf10d92419`. Local reconstruction and independent comparison of every frozen original passed. Pinned plaintext scans include expanded source archives; nine exact nonsecret findings were independently adjudicated, not broadly excluded. Encoding is transport, not encryption. This archive-only branch does not contain a new product release or alter previous immutable packets.

From a normally authenticated private product clone, with unused output names:

```sh
git fetch origin refs/heads/docs/workflow-pause-evidence-20261005-0101
git rev-parse FETCH_HEAD
# Confirm the result is exactly 74fd979aa5c0237076ca3547eb5acb8366a26d73.
git archive --format=tar --output=workflow-pause-evidence.tar 74fd979aa5c0237076ca3547eb5acb8366a26d73
mkdir workflow-pause-evidence
tar -xf workflow-pause-evidence.tar -C workflow-pause-evidence
python3 workflow-pause-evidence/docs/agent-run/evidence/workflow-pause-20261005-0101/reconstruct.py
# Optional extraction: substitute a NEW, non-existing absolute output directory.
python3 workflow-pause-evidence/docs/agent-run/evidence/workflow-pause-20261005-0101/reconstruct.py --output /absolute/path/to/new-empty-recovery-directory
```

Read the recovered `run.json`, `progress.json`, `root/pause-source-record.json`, each lane's pause handoff, runtime final summary and reviewer pause inventory. Reconstruction verifies hashes and does not execute archived qualification launchers. Earlier 316999/04795 evidence packets below remain historical dependencies for already completed slices; the new packet supplements rather than overwrites them. Final publication/readback and anonymous document-browser receipts are stored separately to avoid rewriting immutable evidence around its own commit hash.


## Permanent execution principles

These rules must remain in every future handoff, checklist and plan. Update their canonical entries rather than deleting them during a status refresh.

**EP01 — One delivery path and one accountable owner.** Root owns the smallest useful complete capability within the unchanged full scope. Every proposed task names the production caller, integration owner, owned files, true blockers and a binary acceptance check. Missing evidence, access or approval is not automatically missing code.

**EP02 — Finish failure drain before another effect workstream.** The immediate implementation priority is the critical-failure drain and truthful terminal-parent contract. One lane owns its shared orchestration, manual and SQL files. Finish its actual callers, recovery and receipt tests before opening another effect destination, unless that destination directly unblocks the same contract.

**EP03 — Three lanes on the same release path.** Root orchestrates; implementation owns code and caller integration; prerequisites owns release control, schema, restoration and QA access; verification independently reviews and tests. At most one writer owns a shared file set. Additional Codex or Grok work is bounded to a named dependency; read-only audits do not count as implementation or a PASS without adjudication.

**EP04 — Establish release feasibility early.** Before spending another long qualification run, identify the exact installed target, schema/roles, supported all-writer and accepted-work controls, restoration method and normal QA access. Send concrete authorized requests early with owner, exact ask and proof required. Record previous requests to avoid repeating them. Continue independent work while waiting; never interpret silence as permission.

**EP05 — Reuse a maintained qualification harness.** Reuse existing SQL/REST fixtures, pinned runtime, cleanup and ACK-loss infrastructure. Extend the proven harness for the next regression; do not start a new test platform. Run fixture type checks, parser/load, required schema-shape checks and no-host launcher checks before native allocation. Preserve permissions, timeouts, memory/resource ceilings and rejection assertions.

**EP06 — Reuse evidence only within its proven scope.** Maintain a source/import/schema/config/command manifest for each receipt. Classify each source change and rerun affected contracts; retain unchanged scoped evidence with explicit parity proof. Unit, native, synthetic-browser, authenticated-provider, coinstallation and live evidence are distinct. Full required gates must pass on the exact final candidate; prior partial gates never qualify later source.

**EP07 — Freeze a coherent candidate.** Preserve ad2 as a passed partial checkpoint. New code belongs on an isolated successor branch. During qualification admit only demonstrated release-blocker repairs: preserve the failed evidence, apply a narrow repair, independently review and verify affected behavior. Unrelated main advances do not cancel a valid run; reconcile actual conflicts/required freshness explicitly.

**EP08 — Generate documents from one record.** workflow-plan.json is the current documentation source. Update it, run python3 scripts/render_plan.py and python3 scripts/render_plan.py --check, and publish the record, generator and all generated views together. Do not hand-edit generated status or append another conflicting current checkpoint. Publish at dependency closure, blocker change, pause or handoff; keep routine logs in evidence.

**EP09 — Preserve full scope and truthful status.** Retain all 33 IDs, all 16 behavior families and all 12 surfaces. Track implemented, integrated, tested, independently reviewed, merged, deployed, activated and verified live separately with evidence. A qualified partial milestone does not close full scope. Never infer code or effort percentages from task/acceptance counts; the earlier 65% conversational estimate is not a release metric.

**EP10 — Measure delivery and diagnose wasted work.** Record candidate freeze, required-gate result, deployment and first independent live acceptance timestamps. Report elapsed candidate-to-release and deployment-to-live time; separate implementation, fixture/setup, CI, access and review waits. Track demonstrated candidate resets and setup failures. Leave unavailable metrics unknown; do not manufacture a baseline.

**EP11 — Require real-path independent acceptance.** Test permissions, failure, cancellation, worker death, recovery and uncertain outcomes through named callers. Any UI-dependent change requires independent real browser/Playwright checks. Never weaken tests, safety controls, grants or release gates. Owner tests are confirmation after independent live verification.

**EP12 — Preserve work and safe recovery.** Reuse the original run/claim/effect/operation ledger. Never replay uncertain provider effects, fabricate receipts or broaden authority to make tests pass. Do not replay archived launchers or consumed claims; qualify fresh source/host admission. Do not reset the shared dirty checkout. Only the merging owner removes its own merged, clean, idle worktree using ordinary git worktree remove; never force or blanket-prune.

**EP13 — Carry these rules into every handoff.** Every generated handoff, checklist and plan must include all EP01–EP13 rules and links to the canonical record and AGENTS.md. A documentation handoff is incomplete if the renderer check fails, required tasks/evidence disappear, remote bytes differ, or anonymous browser access/rendering is unverified. These are project working instructions; they do not install a runtime policy in SupraOS Build or override higher-priority instructions.

## Parallel lanes and work limits

| Lane | Accountable work | May run now / after resume | Ownership boundary |
| --- | --- | --- | --- |
| Root | Scope, candidate, integration decisions, documentation and release coordination | Verify exact baseline and assign owners; resolve blockers | Does not silently replace another lane's source |
| Implementation | Failure drain, real automated/manual callers, recovery and truthful parent receipts | First implementation priority; one shared-file owner | Orchestrator, transition helpers and additive authority SQL owned together |
| Prerequisites | Writer/accepted-work controls, schema/roles, restoration, normal QA/provider access | In parallel from the first round | Own release packets and access records; coordinate shared source changes |
| Independent verification | Red regression, cheap preflight, source review, SQL/REST and applicable browser checks | Prepare alongside implementation; qualify immutable source afterward | No concurrent edits to implementation files; preserve failed evidence |

Start with root plus these three lanes where capacity permits. More agents get bounded independent subtasks only when they remove a dependency; they do not create extra feature streams. Grok can trace code/design tests or audit when its connector permits; read-only output is not an implementation. If a requested model is unavailable, disclose and record the fallback or capacity blocker.

Rounds below show dependency eligibility, not unlimited concurrency or duration estimates. Reconcile file ownership, CPU/memory/native host limits and access before dispatch. Keep one high-impact code slice in progress; finish failure drain before opening the next effect. BROADER is a preserved backlog umbrella, not permission to start all its tasks at once.


## Parallel ownership and dependency graph

```mermaid
flowchart TD
  RESUME["Read-only source/ref/target inventory"]
  DRAIN["Reconcile saved drain and rerun caller contract"]
  PREREQ["Supported installed release and restoration"]
  QA["Normal QA and provider access"]
  VERIFY["Cheap preflight and regression preparation"]
  DRAINQUAL["Qualify drain through real callers"]
  EFFECTS["Complete remaining W7 effects and manual parity"]
  BROADER["Close wider preserved 33-node requirements"]
  FINALJOIN["Complete frozen release source"]
  FINALGATES["Required exact-source qualification"]
  DEPLOY["Guarded merge and compatible rollout"]
  ACTIVATE["Enable qualified behavior"]
  LIVE["Authenticated acceptance"]
  OWNER["Owner confirmation and final operating handoff"]
  RESUME --> DRAIN
  RESUME --> PREREQ
  RESUME --> QA
  RESUME --> VERIFY
  DRAIN --> DRAINQUAL
  VERIFY --> DRAINQUAL
  DRAINQUAL --> EFFECTS
  RESUME --> BROADER
  EFFECTS --> FINALJOIN
  BROADER --> FINALJOIN
  FINALJOIN --> FINALGATES
  FINALGATES --> DEPLOY
  PREREQ --> DEPLOY
  DEPLOY --> ACTIVATE
  ACTIVATE --> LIVE
  QA --> LIVE
  LIVE --> OWNER
```

| Step | Depends on | Owner | Makes true / acceptance | Task coverage / owned files | Blocker category |
| --- | --- | --- | --- | --- | --- |
| RESUME | None | Root | Read-only source/ref/target inventory: Compare exact source refs and current deployment/ledger with dated evidence; assign named owners before edits | All33; No product files | Status and dependency reconciliation |
| DRAIN | RESUME | Implementation | Reconcile saved drain and rerun caller contract: Saved48751b50 server/SQL and2dc7e380 client joined; explicit fixture seed and exact committed caller manifest independently reviewed; final shared-file owners assigned | W7,X2,X3; plan-orchestrator.ts; execution-plan.ts; mc-manual-transition.ts; mc-owner-manual-action.ts; additive SQL; related tests | Remaining integration and fixture/source binding; implementation already saved |
| PREREQ | RESUME | Prerequisites | Supported installed release and restoration: Current target, roles/schema, all writers and accepted work accounted for; guarded installation and faithful restore proven | R2,R3,R3B,C2S; Owned release packet/evidence only; coordinate any product-file edits | Missing release producer code, installed evidence and normal access/approval |
| QA | RESUME | Prerequisites | Normal QA and provider access: Normal invitation, owner/foreign-owner sessions and approved provider/computer inputs available; Stripe limitation explicit | P1,V1; Access/request records; never credentials | External access/provider |
| VERIFY | RESUME | Independent verifier | Cheap preflight and regression preparation: Reuse paused native runner and actual-caller bundle; source/blob manifests, final SQL review and cheap preflight complete without weakening budgets | W7,R1,I1; Independent fixture/audit files; read-only implementation files | Evidence |
| DRAINQUAL | DRAIN, VERIFY | Independent verifier | Qualify drain through real callers: Independent SQL/REST and applicable browser proof with original identity, active/unknown hold and no duplicate effects | W7,X2,X3; Qualification evidence; fixture patches reviewed separately | Evidence |
| EFFECTS | DRAINQUAL | Implementation | Complete remaining W7 effects and manual parity: Every remaining destination below has a real caller, authority and passing recovery contract; active cancellation and L1 qualified | W7; One owner for orchestrator/coordinator/intent files; exclusive delegated receiver files | Missing code/integration |
| BROADER | RESUME | Root assigns bounded lanes | Close wider preserved 33-node requirements: Every remaining task contract resolved in dependency order; no new off-path workstream; safe independent items use spare capacity only | B1,C1,M1,W1,B2,M2,M3,J1,W2,W3,W4,W5,X1,A1,W6,X2,X3,X4,X5,C2; Assign exact file ownership before dispatch; shared-file work serialized | Mixed code/evidence/access |
| FINALJOIN | EFFECTS, BROADER | Root and integration | Complete frozen release source: Full intended release manifest composed, independently reviewed, exact source frozen and scoped proof reconciled | I1,R1; Owned release branch and composition evidence | Integration |
| FINALGATES | FINALJOIN | Independent verifier | Required exact-source qualification: Required CI plus affected native/transport/browser contracts pass on immutable final source | R1,I1; Evidence only; demonstrated repairs loop through review | Evidence |
| DEPLOY | FINALGATES, PREREQ | Authorized release owner | Guarded merge and compatible rollout: Required checks, schema/runtime/role compatibility, writer controls, restoration and deployment identity recorded | D1,R2,R3,R3B,C2S; Supported release controls only | Release prerequisites |
| ACTIVATE | DEPLOY | Authorized release owner | Enable qualified behavior: Only compatible qualified capabilities enabled with tested rollback and recovery | D2; Approved activation controls | Rollout |
| LIVE | ACTIVATE, QA | Independent verifier | Authenticated acceptance: All16 behavior families across applicable12 surfaces plus permission/failure/cancel/recovery/uncertainty pass on stable deployed identity | V1,X1,A1; Acceptance evidence, real browser and approved inputs | Live evidence |
| OWNER | LIVE | Root and owner | Owner confirmation and final operating handoff: Specific owner tests provided after independent proof; confirmation and truthful operating/recovery docs recorded | U1,P0; Documentation and owner confirmation | Owner confirmation |

Dependency rounds: 1: RESUME; 2: DRAIN, PREREQ, QA, VERIFY, BROADER; 3: DRAINQUAL; 4: EFFECTS; 5: FINALJOIN; 6: FINALGATES; 7: DEPLOY; 8: ACTIVATE; 9: LIVE; 10: OWNER.

The longest edge-count path is not an effort estimate. Release prerequisites can dominate elapsed time despite a shorter graph path. W7 may ship as a separately qualified milestone only with an explicit release manifest and its required gates; full project completion still requires every task/behavior/surface.


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

## Preserved failure-drain design contract

**Historical pre-implementation analysis at ad2, retained for design and regression fidelity. Do not reimplement this sequence blindly: the current pause checkpoint documents its committed successor and the remaining qualification steps.**

# Failure drain: re-grounded implementation boundary

Source: `ad2ee680464217fd1b00883bf7ea9fc917ed3140`, tree `d646dcd04525189171ee67fc83098667cac6d290`; clean read-only checkout. Binding hashes are in [source bindings](review/failure-drain-source-binding.json); the four pure-transition observations are in [regression output](review/failure-drain-pure-reproduction.json). These newly published read-only receipts postdate the private closeout archive and are not native acceptance. This supersedes provisional details in the earlier frozen next-task analysis; no product changes, database connections, provider calls or publication were performed.

Proposed implementation owner: `/root/catalog_blocker`, subject to explicit root assignment and current lane availability. `/root` retains integration/release ownership. Root AGENTS, CONTEXT critical/build rules, AI_BUILD_PROTOCOL closing gates, atlas reuse/workflow sections, DOC_MAINTENANCE and the AWS scheduled-work runbook were inspected. Any UI behavior change needs independent browser verification; new scheduling should reuse the existing coordinator.

## Reproduced defect and precise limit

`failure-drain-pure-reproduction.json` executes the actual `transitionMcManualTask` and `isPlanComplete` from ad2 using inert injected assignment/score dependencies. With a critical task at two prior retries and a pending, assigned, running, or blocked/outcomeUnknown sibling, each failure transition returns `plan.status=failed`, `finalized=true`, and `allTasksTerminal=false`. No new assignment occurs, but the sibling remains nonterminal. This is an executed pure-transition regression, not native SQL or end-to-end evidence.

The shared predicate at `execution-plan.ts:488` intentionally treats exhausted critical failure as complete. Claimed settlement (`plan-orchestrator.ts:2496`) and manual transition (`mc-manual-transition.ts:70`) therefore mark the plan failed. Their parent authors (`plan-orchestrator.ts:3247`, `mc-owner-manual-action.ts:110`) check terminal status rather than complete terminal task shape. The real SQL parent receiver at `20261004173518...sql:32–55` refuses that shape and holds the parent. Preserve its exact snapshot/version and all-terminal checks.

## Effective repository SQL, including additions

The earlier advice to preserve hypothetical dynamic `pg_get_functiondef` amendments needs correction: searches of the October 3–5 forward packets found no dynamic rewrite of these settlement routines. The last full definition of `settle_mc_task_v1` is **20261004150000**, after chain/task-failure/plan-chain/integration additions. `admit_mc_task_result_v1`, `list_due_mc_task_claims_v1` and the owner-manual wrapper remain defined in **20261003120000**. The finalization receiver is replaced in **20261004173518**; new-claim admission is replaced in **20261005220000**.

Later behavior is still essential: **20261005120000** introduces terminal event delivery/readback and timestamp/snapshot requirements; **20261005130000** adds `capture_mc_estimation_preimage_after_update` on plan task/assignment writes and `stamp_mc_estimation_intent_before_insert` on effect rows. The latter requires a settled claim whose final receipt version equals the current plan version and requires the terminal parent to exist before plan-estimation insertion. **20261005140000** adds notification binding/admission/result functions and the latest recovery cursor allowlist. These must be present in native rehearsals; a settlement-only fixture is insufficient.

**20261005110000 `cancel_mc_run_v1` is useful prior art, not a failure-drain substitute.** It holds the plan before project/run, refuses active/unknown claims and reserved/unknown journal costs, and writes a separate user-cancellation receipt. It requires a real run/project, changes run status to cancelled, and refuses active claims. Calling it for critical failure would introduce the wrong authority and outcome.

Repository definitions do not attest installed state. Before installation, compare a fresh read-only deployed function/trigger/ACL census to the expected source and retain drift evidence.

## Actual caller map and recovery caveats

- Project execute: `app/api/projects/[id]/execute/route.ts:247,298,319` → `claimTasksForExecution` → `settleClaimedExecutionTask`.
- Cron: `app/api/cron/mc-coordinator/route.ts:604,644,652` uses the same claim/settler. Its census at line 53 is running-only; its call to `recoverMcPlanClaims` at line 285 is additionally conditional on a running task with a claim token. Global effect recovery at line 175 does not recover task claims.
- Workspace execution: `plan-orchestrator.ts:4000 runExecutionCycle`, called by `app/api/workspace/plan/execute/route.ts:40,55`; it reads a running plan, claims assigned tasks and requires the postclaim plan still running before provider execution.
- Manual completion/failure: `app/api/workspace/plan/route.ts:187` and `.../execute/route.ts:50` call `settleOwnerManualAction`, which invokes `settle_mc_manual_task_v1`. Its replay probe comes before reading the current task. The wrapper delegates to the current `settle_mc_task_v1` after minting the claim in one transaction.
- Other paths to account for: coordinator lines 690–722 directly update terminal plan/project status; workspace plan route lines 215/250 fence edits of active/unknown attempts but `resume` writes running status; legacy `onTaskCompleted` still calls the shared predicate at lines 1259/1456. Searches found no production invocations of the legacy completion/failure exports in app/lib/core-extensions, so do not claim they are live callers without further evidence.

## Smallest safe implementation sequence

1. **Add failing contract coverage first.** Preserve the four pure regressions above and add actual automated/manual caller composition plus a captured-schema PostgreSQL case demonstrating parent refusal with a sibling. Do not change the receiver to make those fixtures pass.
2. **Keep running as the nonterminal drain state initially**, avoiding a new status/schema/UI enum. Persist an original-failure drain marker in the existing ledger, derived by SQL from the accepted original failure and bound to owner/plan/run/claim. Change terminal authorship to strict all-terminal shape. The current SQL claim guard already refuses further claims after exhausted critical failure, but explicitly fence manual new actions and scheduler assignment/retry promotion during drain. Same-action replay must remain readable.
3. **Drain only positively established unstarted siblings under the plan lock.** Add a dedicated bounded SQL operation or narrow validated settlement branch that derives exact eligible siblings from stored state; never accept arbitrary sibling rewrites in caller JSON. Preserve active claims, outputs, unknown markers and assignment history. Keep completed/skipped semantics distinct from actual failed provider work. Do not decide that token absence alone proves no dispatch for legacy rows.
4. **Use the actual closing claim as terminal authority when possible.** If the triggering failure transaction safely terminates all other work, it can author the parent. Otherwise allow original active results/reviews to settle without assigning retries or descendants; the last such accepted transaction authors the exact terminal parent/children once. SQL must independently derive terminality/status and serialize authorship. This fits existing `settled_at` and estimation-trigger contracts and avoids rebinding an old receipt to a newer snapshot.
5. **Only add asynchronous closure authority if needed.** A drain with no remaining real closing claim needs a separately designed durable closure receipt/time, consumer support and uniqueness scope, especially for projectless/null-run plans. Do not synthesize a task result or retimestamp the failure claim. Historical premature/held parents remain immutable; repairing them is explicit supersession work, not a reset to pending.
6. **Route coordinator direct finalization through the same authority**, or gate it away from claim-backed plans. Add manual `plan_terminal_event` through existing receivers using DB-minted identity and owner-manual provenance; avoid importing automated agent-learning/chain claims into human completion. Native trigger/receiver composition must prove insertion order and final version consistency.

## Unresolved authority requirements before claiming completion

The existing result admission binds the first admitted outcome/digest immutably (`20261003120000:285–289`). Recovery can admit `outcome_unknown` when no saved result exists (`plan-orchestrator.ts:3293–3297`); later successful data with another digest is then a mismatch. The generic due list excludes already settled unknowns and `review_unknown`. Therefore “accept the late original result” is valid only where its original admission still permits it. An authenticated, attempt-bound resolution protocol for already held unknowns has not been demonstrated here. It must either be implemented and proven separately or remain an explicit open hold; no automatic drain may manufacture terminality from it.

Positive proof that assigned/pending legacy work never dispatched, the cancellation representation for unstarted siblings, null-run closure uniqueness, and historical held-parent supersession require explicit contracts. They are design prerequisites, not reasons to weaken existing checks or seek blanket user permission for routine engineering.

## Required regression matrix

Native PostgreSQL: race claim/failure both lock orders, two simultaneous settlements, manual failure/claim, rollback after populated receipts, same result/action ACK loss, retry/critical-path malformed values, wrong owner/run/task/claim/version, caller-forged sibling edits, already unknown result, held head review, late matching/mismatched result, run restart and projectless state. Include estimation triggers, terminal event timestamp/readback, notification no-redispatch, and exact finalization snapshot. Assert one truthful parent, preserved claim/output/history, no new provider/assignment during drain and no terminal receipt while unknown.

Caller and browser gates: extend existing `mc-manual-transition`, `projects-execute-claim`, `plan-timeout-claim-recovery`, terminal event/stream/browser, finish-intent and notification suites. Verify the actual Mission Control/workspace draining/held state in Chromium. Check shared-file impact graph, scoped types, independent SQL/source review, catalog inventory with E3 still red, atlas notes, required CI and the separately authorized installation/release gates. A completed failure-drain slice is not all-W7 completion.


## Remaining effects after the drain

Preserve this inventory until each destination has its original identity, actual caller, integration owner and acceptance receipt: manual terminal events and retrospective parity; Hindsight original action/outcome; analyzer output and report memory/provenance; broadcast provenance; legitimate caller-saved department recipients; completion/failure umbrella broadcasts and legacy terminal fallback; safe active cancellation; real L1 execution. Existing notification/estimation/retro slices must be extended or qualified, not rebuilt. Planner assignments do not establish recipient consent. Unknown work remains held; do not manufacture terminality to deliver a notification.


## Release feasibility and external requests

| Dependency | Owner role | Exact request / proof | Work that continues meanwhile |
| --- | --- | --- | --- |
| Production writer and accepted-work control | Authorized release operator | Supported mechanism and target-bound inventory covering every writer, pending/active/unknown work and old broadcasters; faithful current-target restore evidence | Read code, prepare guarded packets and private rehearsals |
| Schema and runtime roles | Release/database operator | Fresh ledger/schema/function/ACL/pooler inventory; ordered forward/VERIFY/rollback compatibility | Compare already prepared packets; do not replay installed migrations |
| Normal authenticated QA | Existing member/account owner | Normal invite and owner/foreign-owner QA sessions; no credentials in handoff and no invite bypass | Synthetic/native negative tests and public browser checks |
| Stripe Link/provider/computer | Provider/account owner | Issued configuration status and normal approved setup/inputs | Reversible adapter tests; no unsolicited real effects |

These are outstanding categories, not claims that a new request has been sent. Inspect the prior request history before contacting anyone. Send messages only under the user's existing explicit authorization or a fresh applicable instruction. A release-feasibility finding should identify code, evidence, access or approval precisely; do not label unfinished code as an external blocker.


## Evidence reuse and qualification ladder

The complete five-child selected settlement SQL suite passes **38 ordered phases / 81 saved outputs** on exact preserved `3e27866a` source (receipt **d771f442**). Actual failed-task REST (**04bcceb4**) and coordinator-adjustment REST (**fd1edcaf**) pass with real private PostgREST `service_role` transport and committed-ACK recovery. Terminal direct SQL (**1b9e3cb8**), estimation direct SQL (**56b0a323**) and notification direct SQL are separately qualified. These are dated private schemas and synthetic identities, not production installation, JWT/signer, live cron or real L1 evidence.

Preserved failures include legitimate host-inventory refusal, malformed synthetic fixture rows, a timestamp bind-type conflict, and three `.status` assertions against an actual `Promise<void>` finalizer. Corrected fixtures inspect the durable original parent row/receipt and replay equality instead. A new real-TypeScript preflight catches all three old void-return mistakes and passes the corrected fixtures before another native allocation. Esbuild success alone was insufficient. No permissions, rejection assertions, resource floors or required gates were relaxed.

Native source, stage, one-use claim, terminal output, cleanup and independent audit are distinct receipts. Socket-only PostgreSQL and private internal Docker networks avoid production writes; no published fixture ports. Consumed or uncertain attempts are never replayed. Stopped owned scratch retained for later exact cleanup is listed in the private lifecycle handoff. No blanket Docker cleanup, worktree pruning or deletion of another agent's folder occurred.

For each receipt record: exact source commit/tree and imported-file hashes; schema/role/config/runtime fingerprints; test command/version and input identity; positive/negative/recovery scope; outcome and failed evidence; cleanup; independent reviewer; invalidating changes. Mark reuse as scoped parity, never a new execution.

Run in this order when applicable: source/caller inspection → focused regression/types/fixture checks → SQL parse/load and no-host checks → bounded native SQL/REST → independent actual caller and browser review → required exact-source CI → guarded rollout → authenticated live acceptance and tested recovery. Setup failure is not product failure; preserve and diagnose it without weakening budgets. A passing lower step does not substitute for a higher one.

The existing manifests and private packet are the starting point. Consolidation means parameterizing proven harness components during needed work; it is not a separate harness rewrite project. Keep native runs within existing resource controls and distinct owned scratch. Preserve one-use attempt semantics.


## Delivery metrics

```json
{
  "candidateFreezeToDeployment": null,
  "deploymentToIndependentLiveAcceptance": null,
  "interpretation": "Unknown until recorded; gate PASS does not imply deployment",
  "lastQualifiedCandidate": "ad2ee680464217fd1b00883bf7ea9fc917ed3140 (last with required CI PASS); 3214f4849e3bb0517b60ee17821826918ee11147 frozen 2026-10-05T04:39:50Z, required CI RED (security-gates FAILURE, production-build ERROR) \u2014 not qualified; replacement commit pending",
  "lastGateObservation": "2026-10-05 ~05:00Z: box-ci on 3214f4849e RED (security-gates FAILURE; production-build ERROR). Whole unit tree 2 failed / 55,609 passed / 374 skipped (4,508 files)",
  "implementationPausedAt": "2026-10-05T02:04:00Z (approximate minute)",
  "activeRun": {
    "startedAt": "2026-10-05T01:01:15Z",
    "plannedEndAt": "2026-10-05T09:01:15Z",
    "state": "paused_by_user",
    "baselineCandidate": "ad2ee680464217fd1b00883bf7ea9fc917ed3140",
    "documentationCommit": "77d7faaa1a98638feaf123e0dc80d6d77d625b06",
    "lanes": {
      "implementation": "catalog_blocker",
      "releasePrerequisites": "native_closeout",
      "independentVerification": "closeout_audit",
      "integrationAndRecords": "root"
    },
    "nextMilestone": "Truthful failure drain through actual callers without premature terminal effects; partial W7 only.",
    "pausedAt": "2026-10-05T02:04:00Z",
    "pauseTimestampPrecision": "Approximate minute from user pause; pre-existing tests collected afterward without new qualification",
    "actualImplementationElapsed": "Approximately 63 minutes; planned eight hours superseded by explicit pause",
    "closeout": "Documentation, evidence preservation and publication only"
  },
  "lastDependencyClosed": "Trailing audit at 3214f4849e PASS (scoped): native 26/26, ordered 24/24 packet install + VERIFY, browser 46/46 + 2/2, unit 896/0/7 skipped, relay x1-bridge 28/28. Not a release qualification: required full-tree CI is RED on the same commit",
  "candidateFrozenAt": "2026-10-05T04:39:50Z",
  "resumedAt": "2026-10-05T02:30:00Z",
  "waits": {
    "implementationLane": "~93 min",
    "verificationLane": "~61 min",
    "prerequisitesLane": "~44 min",
    "rootComposition": "~40 min (two merges of a fast-moving main, two collisions)",
    "permissionBlocks": "restored-copy rehearsal on AWS host; production apply; merge \u2014 handed to owner"
  },
  "ownerPauseAt": "2026-10-05T04:47Z (approximate)",
  "resumedAfterOwnerPauseAt": "2026-10-05T05:00Z (approximate)",
  "currentBlocker": "Required CI RED on 3214f4849e: three candidate defects (queried-tables-exist; model-adapter-verified-agent-policy; scoped TypeScript check on owner-db-runtime-binding test). Category: code defects in the candidate. Owner: root session. Proof needed: both box-ci statuses success on the new head"
}
```

Record useful delivery milestones and wait categories. Compare actual elapsed times after enough data exists; do not promise speedup percentages from agent count.


## Full scope preservation

The [33-task checklist](SupraOS-Workflow-Plan-Checklist.md) carries every acceptance contract, source pointer and original dependency. The canonical record also preserves all 20 previous release slices and 16 prior delivery steps, labeled historical. Do not execute outdated slice states without current reconciliation.

## Updating and handing off this plan

1. Read this revision, the canonical record and product repository instructions before starting. Inspect existing code and receipts; distinguish missing code from missing proof/access.
2. Update `workflow-plan.json`: current evidence, task stages, actual blocker, named owner, next proof, exact candidate and timestamps. Retain historical baseline records and all task acceptance criteria.
3. Run `python3 scripts/render_plan.py`, then `python3 scripts/render_plan.py --check`. The check verifies scope, policy IDs, an acyclic graph and exact generated bytes. It does not verify product behavior.
4. Publish the record and generated files in one reviewed commit. Secret-scan plaintext before uploading evidence; encoding is not sanitization. Reuse the existing hash-manifest packaging and independent reconstruction checks.
5. Verify remote bytes and anonymous browser rendering for the three entry documents, all 33 checklist rows and the dependency graph. Record the publication/browser receipt separately; avoid a self-referential commit-hash rewrite loop.

Checkpoint report: **usable capability advanced; dependency closed; exact blocker and category; accountable owner; proof needed; next action; source/test/review/merge/deploy/activation/live state; elapsed delivery time**. Unknown timestamps remain unknown. Publish on meaningful dependency closure, blocker change, pause or handoff—not after every tool call.

The generator catches missing rules and stale generated views when run. `AGENTS.md` instructs future agents to run it; no runtime enforcement in SupraOS Build or mandatory GitHub branch protection has been installed by this documentation change.
