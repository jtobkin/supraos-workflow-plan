# SupraOS Release Plan Checklist

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-05T07:45:00Z**. Canonical record SHA-256: `8234647662e76f825a7c82f8ead0ac13897f37426a033a88ef93516b828a3891`.

**Execution state:** ACTIVE 2026-10-05 ~07:45Z. The W7 failure-drain/rerun candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` is INSTALLED, MERGED, DEPLOYED and ACTIVE on production, but it is NOT verified live and the milestone is NOT complete: live acceptance found two defects on production. Of 3 behaviours, 1 passed, 1 is blocked by the live defects and 1 cannot be driven from any control. Owner instruction during the run: "automerge and automigrate as needed". Sequencing resolved: the concurrent Agent Run session chose W7 first (its PR #6168 was blocked elsewhere); it resolves the 26-file overlap afterwards and asked for no further merges until it says "merges open". Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. Verified live: NO. Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. Open product note (finding X6, owner decision): the refusal wording gives owners of the 36 pre-install projects no path forward. Evidence: private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `df83c7d3fb`; the install log and the acceptance screenshot are not yet committed there. History, kept as it happened: the first cut `3214f4849e` got RED required CI at ~05:00Z and was replaced by `ac48190955`, which had required CI GREEN at 05:36Z and an independent trailing audit PASS 5/5. This is a partial-W7 milestone that is itself not yet verified live; full W7 scope and the other tasks remain open.

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** Candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (tree `49bf08e3354a115783635eebfa4801dfa953bb6c`, PR [#6196](https://github.com/jtobkin/suprafx-platform/pull/6196)) is **installed, merged, deployed and active on production, but NOT verified live — live acceptance found two defects; 1 of 3 behaviours passed, 1 is blocked by the defects, 1 is not drivable. The milestone is not complete**. Owner instruction during the run: "automerge and automigrate as needed". Sequencing resolved: the concurrent Agent Run session chose W7 first (its PR #6168 was blocked elsewhere); it resolves the 26-file overlap afterwards and asked for no further merges until it says "merges open". **Backup.** Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. **Install.** Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. **Merge.** Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. **Deploy.** Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. **Activation.** Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. **Live acceptance (as of ~07:45Z).** Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). **Live defect 1.** (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. **Live defect 2.** (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. **Behaviour A.** Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. **Test gap.** The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. **Decision.** Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. **In progress.** Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Open product note (finding X6, owner decision): the refusal wording gives owners of the 36 pre-install projects no path forward. Evidence: private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `df83c7d3fb`; the install log and the acceptance screenshot are not yet committed there. Qualification before the merge, kept as recorded: box-ci on `ac48190955` observed 05:36Z — security-gates SUCCESS (51 steps; macOS Native Land not run), production-build SUCCESS (7 steps); independent trailing audit PASS on all 5 checks (fix diff; native 26/26; ordered 24/24 packets applied and verified as non-superuser; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). History: the previous head `3214f4849e` got RED required CI at ~05:00Z from three candidate defects, all fixed in `867a5f2114`. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. Order from here: root-cause and fix live defects 1 and 2 on the hotfix branch, proven on the real server path against a real database with production-shaped data → release the hotfix → repeat live acceptance (the stuck project finishes; behaviour B) → owner decision on PR #6198, which is what makes behaviour A drivable on Mission Control plans → owner decision on finding X6 → restore-verify the pre-install backup → commit the install log and acceptance evidence to the evidence branch → PR #6197 when merges are open → remaining W7 scope

**Current candidate record:** `ac4819095585eed003eb0c510b0a8c8608d5e73f`, tree `49bf08e3354a115783635eebfa4801dfa953bb6c`. Security: box-ci/security-gates SUCCESS on ac48190955 (51 steps; macOS Native Land not run). Previous head 3214f4849e: FAILURE (whole unit tree 2 failed / 55,609 passed / 374 skipped across 4,508 files; scoped changed-file TypeScript check 5 errors); build: box-ci/production-build SUCCESS on ac48190955 (7 steps). Previous head 3214f4849e: ERROR (not built because security gates failed); macOS Native Land: Not run (not part of box-ci). Merged: True; deployed: True; activated: True; verified live: False. Scope: Composed W7 failure-drain/rerun candidate (partial W7; full scope open). Frozen candidate ac48190955 = 3214f4849e + fix commit 867a5f2114 + clean merge of origin/main 7a10b7a3fc; required CI GREEN and independent trailing audit PASS 5/5 at that commit. Squash-merged 2026-10-05 06:11:22Z as main 55a12f0da9b09052d0bfa186f747654a60f3a931 (PR #6196); production schema installed 06:03–06:10Z (24/24 packets applied and verified); deployed 06:24:35Z; active by construction (no feature flag). `verified live: False` here means NOT verified live and the milestone NOT complete. Live acceptance on production (2026-10-05): behaviour C passed (re-execute on a pre-release plan refused, nothing created); behaviour B is blocked by two live defects (a post-release project's final task cannot settle — "terminal plan chain is not bound to settled plan"; and re-execute is refused for every project because L1-anchor effects end `held_unknown` while rerun requires every effect `delivered`); behaviour A is not drivable from any production control (Mission Control plans have an empty critical path). The pre-release suites passed but were insufficient. Not part of this candidate: the hotfix branch `claude/w7-final-task-settle-fix-20261005` (PR not yet open), PR #6198 (Mission Control critical path, owner decision) and follow-up PR #6197 (held). Observed: 2026-10-05T07:45:00Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.


## Status 2026-10-05 ~07:45Z — W7 is live on production but NOT verified: two live defects found, hotfix in preparation (read this first)

The section below this one describes the earlier pause at ~02:04Z and is kept as dated history. Since then the candidate was installed, merged and deployed on production, and live acceptance then found two defects. **The W7 milestone is not complete.**

**Live acceptance result: 1 of 3 behaviours passed, 1 blocked by live defects, 1 not drivable.**

- **Behaviour C — PASS.** Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts).
- **Live defect 1 — a new project cannot finish.** (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts.
- **Live defect 2 — Re-execute is unavailable for all projects.** (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet.
- **Behaviour A — not drivable.** Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only.
- **Test gap, stated plainly.** The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them.
- **Decision taken.** Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow.

**Current blocker — two live defects.** Fix them on the hotfix branch, prove the fix on the real server path against a real database with production-shaped data, release it, then repeat live acceptance: the stuck project must finish and behaviour B must pass.

**Work in progress.**

- Hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2: root cause in progress; PR not yet open; the branch was not on the remote when checked at 07:44Z.
- PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path": OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`). Owner decision — it changes behaviour: a third failure on the main chain fails the project instead of skipping. It is what would make behaviour A drivable on Mission Control plans.
- Follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197): OPEN, held (branch `claude/w7-followups-20261005`, head `1de6f98ed2`; independently reviewed PASS at `6c8b03781b`).
- A production-shape end-to-end harness lane.
- A read-only audit of every other guarded control.
- A planner-screen bug lane: a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan.

**Process lesson (EP11).** Acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof.

**How it got here (kept as recorded).**

- **Candidate and merge.** PR [#6196](https://github.com/jtobkin/suprafx-platform/pull/6196), branch `claude/w7-drain-rerun-compose-20261005`, frozen head `ac4819095585eed003eb0c510b0a8c8608d5e73f`, tree `49bf08e3354a115783635eebfa4801dfa953bb6c`. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`.
- **Owner instruction.** Owner instruction during the run: "automerge and automigrate as needed".
- **Sequencing.** Sequencing resolved: the concurrent Agent Run session chose W7 first (its PR #6168 was blocked elsewhere); it resolves the 26-file overlap afterwards and asked for no further merges until it says "merges open".
- **Backup before install.** Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option.
- **Production install.** Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans.
- **Deployment.** Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing.
- **Activation.** Activated: yes by construction — there is no feature flag, so code + SQL deployed means live.
- **Qualification before the merge (kept as recorded).** box-ci on `ac48190955` observed 05:36Z: security-gates SUCCESS (51 steps; macOS Native Land not run), production-build SUCCESS (7 steps). Independent trailing audit PASS on all 5 checks. The first cut `3214f4849e` got RED required CI at ~05:00Z from three candidate defects, all fixed in `867a5f2114`.
- **Evidence.** Evidence: private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `df83c7d3fb`; the install log and the acceptance screenshot are not yet committed there.

**Other open items.** (1) Owner decision on finding X6: the refusal wording gives owners of pre-release projects no path forward. (2) The pre-install backup is not restore-verified. (3) The install log and acceptance evidence are not yet committed to the evidence branch.

**Order from here: fix defects 1 and 2 → prove on the real server path with production-shaped data → release the hotfix → repeat live acceptance → owner decision on PR #6198 → owner decision on X6 → restore-verify the backup → commit the missing evidence → PR #6197 when merges are open → remaining W7 scope.**

| Stage | State now |
| --- | --- |
| Implemented | Yes |
| Integrated | Yes |
| Tested | Pre-release suites passed but were insufficient |
| Independently reviewed | Yes |
| Merged | Yes, main `55a12f0da9` |
| Deployed | Yes |
| Activated | Yes |
| Verified live | NO — 1 of 3 passed (C); B blocked by live defects; A not drivable |

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

**EP11 — Require real-path independent acceptance.** Test permissions, failure, cancellation, worker death, recovery and uncertain outcomes through named callers. Any UI-dependent change requires independent real browser/Playwright checks. Never weaken tests, safety controls, grants or release gates. Owner tests are confirmation after independent live verification. Lesson from the W7 release (2026-10-05): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. Both passed in full while two defects reached production.

**EP12 — Preserve work and safe recovery.** Reuse the original run/claim/effect/operation ledger. Never replay uncertain provider effects, fabricate receipts or broaden authority to make tests pass. Do not replay archived launchers or consumed claims; qualify fresh source/host admission. Do not reset the shared dirty checkout. Only the merging owner removes its own merged, clean, idle worktree using ordinary git worktree remove; never force or blanket-prune.

**EP13 — Carry these rules into every handoff.** Every generated handoff, checklist and plan must include all EP01–EP13 rules and links to the canonical record and AGENTS.md. A documentation handoff is incomplete if the renderer check fails, required tasks/evidence disappear, remote bytes differ, or anonymous browser access/rendering is unverified. These are project working instructions; they do not install a runtime policy in SupraOS Build or override higher-priority instructions.

## Current full-scope checklist — all 33 tracked items

| ID / work | Evidence state | Remaining work |
| --- | --- | --- |
| **P0 — Scope reconciliation and dependency plan** | Canonical pause handoff, complete 33-task checklist and dependency graph updated together; private source branches preserved; publication and anonymous verification recorded in closeout receipts. | Keep current evidence, dependencies and handoff aligned. |
| **B1 — Freeze trusted internal project execution** | Trusted project execution source qualified | Join real server/client/member authority and deployed acceptance. |
| **C1 — Finish client context and history isolation** | Claude loopback isolation scoped proof; other client paths open | Qualify native Codex/Grok, configuration/hooks and real authenticated transport. |
| **M1 — Complete member dashboard and read projections** | Member projection source and mounted browser evidence retained | Join actual producer/readers and installed authenticated behavior. |
| **W1 — Bound shared DataPackage fallback waits** | Bounded shared DataPackage source qualified | Compose and verify cancellation/cache behavior through deployed callers. |
| **B2 — Remove remaining private background producer inputs** | Narrow Competitor Watch slice deployed; full producer scope open | Remove remaining private inputs and verify active worker/card recovery. |
| **M2 — Join member result and internal message readers** | Classified member readers joined in scoped native/browser fixture | Prove current publication, revocation and real shared-chat transport. |
| **M3 — Qualify owner-only Realtime transport** | Owner-topic/metadata routing implemented; socket matrix scoped | Install ACLs, drain old broadcasters and qualify JWT expiry/revocation. |
| **J1 — Join server, clients and actual native authority** | Joined server/client native and browser source evidence | Close native client and deployed transport gaps before final join. |
| **W2 — Notification recipient authority and usable authoring** | Email/recipient authority source in held draft6138 | Schema-first release plus real authorized email and uncertain-send recovery. |
| **W3 — File operation namespace and destination authority** | Storage namespace and uncertainty source in held draft6132 | Install policy/schema and verify real owner, revocation and recovery boundaries. |
| **W4 — Named OAuth and raw API authority** | Named/raw API authority source in held draft6129 | Compose exact final source and qualify installed/provider behavior. |
| **W5 — Child workflow and bot creation authority** | Child/bot creation authority source in held draft6129 | Prove real allowed creation, denied targets and original-child recovery. |
| **X1 — Qualify every supported context entry** | Entry-point context/privacy map and scoped repairs | Qualify every supported surface, including background and System Workflow runs. |
| **A1 — Finish global attention and baseline source gaps** | Attention/Room/shelf/mail foundations; global cutover remains off | Close all16 behavior gaps for cadence, suppression, consent and context. |
| **R1 — Reconcile main, CI and exact release stack** | ad2ee680 partial successor pushed in draft6190, scoped52/types14/review PASS; required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; prior1c0 CI RED preserved; earlier privacy slices shipped; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: composed `3214f4849e3bb0517b60ee17821826918ee11147` in PR #6196; duplicate-version ratchet clean; writer catalog PASS (2,657 rows); box-ci pending. | Pass box-ci security-gates and production-build on the exact frozen head; re-merge main if it moves before merge. |
| **R2 — Installed schema, profile and release packet** | Installed profile read and source migration packets prepared 2026-10-05: 24 packets classified A17/S3/T4; two version collisions renumbered; ordered 24/24 install + VERIFY proven on a prod-schema clone (not a restored data copy — that rehearsal was blocked by permissions). | Owner applies the 24 packets to production from the frozen worktree with apply-migration.mjs and confirms the ledger (+24); commit refreshed schema oracles. |
| **R3 — Writer/effect drain and faithful restore rehearsal** | Private stop/install/unknown recovery and dated restore proofs | Mount existing release gate accepted-work/all-writer/backup producers; obtain supported writer exclusion and faithful current-target restore. Managed/nonsuperuser observations do not establish active writers or a need for superuser. Owner did not understand broad administrator question; inspect normal management/backup controls before a narrow concrete request. |
| **I1 — Compose and independently qualify final source** | ad2ee680 integrates reviewed guard/manual/Telegram repairs on1c0;52 scoped tests/types14/review PASS; exact successor required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; unchanged UI has scoped Linux privacy proof; full final source open; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: frozen `3214f4849e3bb0517b60ee17821826918ee11147`; conflict resolutions reviewed by the verification lane in the trailing audit. | Trailing audit at the frozen sha; any blocker repair re-freezes. |
| **D1 — Gated merge and deploy verified code** | UI6179/6181 merged/deployed/public-browser verified | No owner-run release steps remain from the earlier note: the packets were applied on production 06:03–06:10Z (24/24 applied and verified), PR #6196 was merged 06:11:22Z via merge-if-green and deployed 06:24:35Z — all by the session under the owner's instruction "automerge and automigrate as needed"; the earlier permission blocks did not recur. The live check found two defects (see W7), so live verification is NOT complete. Remaining for this task: its own full authenticated scope, unchanged. |
| **D2 — Activate qualified workflows after compatible rollout** | Global/workflow activation not claimed | Activate only compatible qualified schema/runtime with tested recovery. |
| **P1 — Provider and real computer readiness** | Provider readiness incomplete; Stripe configuration external | Finish normal provider/account/real-computer setup and approved live inputs. |
| **V1 — Stable deployed all-path and 16 behavior acceptance** | All16 integrated/live acceptance behaviors remain open | Independently verify stable deployed journeys across all12 surfaces. |
| **U1 — Owner confirmation and final handoff** | Portable handoff maintained; final owner confirmation pending | Provide specific owner tests only after independent applicable verification. |
| **W6 — Atomic usage limits for scoped capability grants** | Atomic grant reservations source in held draft6129 | Prove installed concurrent use, revocation and original receipt recovery. |
| **W7 — Original-operation workflow effects** | Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. | First: fix the two live defects on hotfix branch `claude/w7-final-task-settle-fix-20261005` (root cause in progress; PR not yet open) — (1) the final task of a post-release Mission Control project cannot settle ("terminal plan chain is not bound to settled plan"), so the plan stays `running`; (2) re-execute is refused for every project because L1-anchor effect intents end `held_unknown` while rerun requires every effect `delivered`. Prove the fix on the real server path against a real database with production-shaped data (the production-shape end-to-end harness lane), release it, then repeat live acceptance: the stuck project must finish and behaviour B (lost-acknowledgment rerun recovers the original run, no duplicate) must pass. Behaviour A (critical-failure drain) is not drivable on production from any control until Mission Control plans carry a critical path — PR #6198, an owner decision because it changes behaviour (a third failure on the main chain fails the project instead of skipping). Until then W7 drain/rerun is NOT verified live (1 of 3 passed) and must not be shown as complete. Mission Control admission is left open by operator decision; revisit if the fix is slow. Also: finish the read-only audit of every other guarded control; fix the planner-screen bugs (a malformed planner answer produced a launchable 0-task plan; the review panel did not follow the selected plan); owner decision on finding X6 (the refusal wording gives owners of pre-release projects no path forward); restore-verify the pre-install backup; commit the install log and acceptance evidence to the evidence branch; when merges are open, get box-ci green on follow-up PR #6197 (`claude/w7-followups-20261005` @ `1de6f98ed2`) and merge it via `scripts/ci/box-ci/merge-if-green.sh`. Then: the F2 design decision, remaining effects/manual parity, legitimate department recipients, safe active cancellation, real L1 and the rerun-init pending/unknown recovery boundary. |
| **X2 — Confirm System Workflow durable terminal and pause receipts** | System Workflow pause and Memory Promotion partial fixes deployed | Qualify real admitted-owner pause/checkpoint/terminal recovery journeys. |
| **X3 — Refuse zero-row completion in scheduled and direct workflows** | Missing original terminal-row refusal has scoped native evidence | Verify scheduled and direct deployed paths retain truthful outcomes. |
| **X4 — Retain uncertain scheduled workflow attempts before another tick** | Scheduled original-attempt source preserved in held drafts | Install guarded occurrence schema and prove next-tick no-replay recovery. |
| **X5 — Qualify original scheduled approval continuation** | Bounded original approval continuation source qualified | Close remaining effectful graphs and real approval/uncertain-outcome acceptance. |
| **C2 — Bind project Git commands to exact workspace** | Project dispatch6118 and eligible-recipient6141 source qualified | Qualify mounted Realtime/relay, exact workspace commands and schema-first rollout. |
| **R3B — Stage runtime role before candidate schema extension** | Dormant minimal role source with scoped native ACL proof; runtime helper/bridge integration saved82b01044; 19 private native actual-caller cases and independent review PASS. | Reconcile B0 source packet and current caller bindings; qualify full installed ACL/default-ACL/policies and hosted transaction pooler; retain separate B1/gate-six work; guarded role rollout. Source integration is no longer missing, but production runtime role remains absent in dated census. |
| **C2S — Install and verify project schema before server rollout** | Seven ordered project-schema packets rehearsed privately | Perform guarded installed-target schema rollout with live service-role verification. |

## Detailed task contracts and preserved evidence

Historical baseline implementation/evidence is retained verbatim in `workflow-plan.json` under each task’s `baselineRecord`. It may predate the current saved-work summary. Original dependency IDs are retained below; dispatch dependencies above are the revised execution sequence. An empty original dependency list does not waive release prerequisites.

### P0 — Scope reconciliation and dependency plan

**Saved work:** Canonical pause handoff, complete 33-task checklist and dependency graph updated together; private source branches preserved; publication and anonymous verification recorded in closeout receipts.

**Remaining:** Keep current evidence, dependencies and handoff aligned.

**Acceptance:** Maintain this plan as evidence arrives; scope is not reduced to the current three lanes.

**Source:** docs/agent-run/{BASELINE-BEHAVIORS,EXECUTION-PATH-ACCEPTANCE}.md; original final handoff

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** None recorded.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| integrated | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| tested | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| independentlyReviewed | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| merged | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| deployed | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| activated | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |
| verifiedLive | Documentation-only: paused canonical revision generated from one status record; final publication/browser receipts stored separately. Product completion not applicable. |

### B1 — Freeze trusted internal project execution

**Saved work:** Trusted project execution source qualified

**Remaining:** Join real server/client/member authority and deployed acceptance.

**Acceptance:** Actual claim/output authority; current source, attempt and digest binding; replay/task-closed/rollback/personal controls. Freeze exact commit and contract. No private owner context from producer or recovery.

**Source:** lib/supraos-build/plan-coordinator.ts; execution-input and relay-response routes; migrations 010120/010140

**Prior owner role:** Sol / server. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### C1 — Finish client context and history isolation

**Saved work:** Claude loopback isolation scoped proof; other client paths open

**Remaining:** Qualify native Codex/Grok, configuration/hooks and real authenticated transport.

**Acceptance:** Qualify managed configuration, real authentication, existing resume-ID survival, Codex/Grok and deployed transport. Fix fixture types; close existing skills/config/SessionStart hook injection, not merely transcript reuse; prove Claude/Codex/Grok one-shot assignment and output identity with personal positive controls. Add server-authorized workspace context for Land/check/audit; unbound mixed-session commands must hold until producer/PUT/relay agreement and delayed/restarted cases are qualified.

**Source:** packages/supraos-relay/src/{start,pty-session,project-execution-scope}.js; electron/ipc/{embedded-relay,cli-relay-session}.ts; cli-relay-worker.ts

**Prior owner role:** Sol audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### M1 — Complete member dashboard and read projections

**Saved work:** Member projection source and mounted browser evidence retained

**Remaining:** Join actual producer/readers and installed authenticated behavior.

**Acceptance:** Audit every dashboard/client prop including digests/ideas/rules/streak, raw board callers, file paths; positive project-chat; real Chromium390/1440 and serialized HTML/RSC private sentinels. Freeze bounded checkpoint.

**Source:** lib/supraos-build/member-plan-source.ts; project/session routes; app/vms/builder/[id]; session SSR

**Prior owner role:** Sol / audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W1 — Bound shared DataPackage fallback waits

**Saved work:** Bounded shared DataPackage source qualified

**Remaining:** Compose and verify cancellation/cache behavior through deployed callers.

**Acceptance:** Per-caller cancellation without canceling shared bounded transport; pre-aborted no admission; two consumers one fetch/charge; actual HTTP header/body timeout; preserve warm cache and Routine authority.

**Source:** lib/vms/workflows/execution-engine.ts; lib/upstream/defillama/{service,client}.ts

**Prior owner role:** Sol / workflows. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### B2 — Remove remaining private background producer inputs

**Saved work:** Narrow Competitor Watch slice deployed; full producer scope open

**Remaining:** Remove remaining private inputs and verify active worker/card recovery.

**Acceptance:** Use reviewed project quality definitions and structured origin; test actual tick/recovery/template/continuation producers and changed publication. Owner-private sentinel absent in all shared prompts.

**Source:** plan-coordinator; template reviewer; task-completion-boundary; project-plan-dispatch-source; recovery/continuation callers

**Prior owner role:** Next Sol / server. Root must assign a currently available named owner before dispatch. **Original dependencies:** B1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Earlier narrow slices only |
| deployed | Earlier narrow slices only |
| activated | Full scope pending |
| verifiedLive | Scoped public checks only; full authenticated scope pending |

### M2 — Join member result and internal message readers

**Saved work:** Classified member readers joined in scoped native/browser fixture

**Remaining:** Prove current publication, revocation and real shared-chat transport.

**Acceptance:** Exact current publication/hash/task/job/input/result/accounting and completed_at binding; null summary compatibility; mutation/revocation races; actual HTTP and mounted browser positive/negative. Preserve explicit shared chat.

**Source:** member-plan-source.ts; sessions/[id]/messages; since-you-left digest; 010120/010140

**Prior owner role:** Sol / audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** B1, M1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### M3 — Qualify owner-only Realtime transport

**Saved work:** Owner-topic/metadata routing implemented; socket matrix scoped

**Remaining:** Install ACLs, drain old broadcasters and qualify JWT expiry/revocation.

**Acceptance:** Actual socket with already-minted member JWT, owner positive, revoked/joined/nonjoined Room controls; apply/rollback/reapply; old broadcaster drain explicitly gates release.

**Source:** session-broadcast.ts; use-session-realtime; use-agent-insights; 010130 migration

**Prior owner role:** Next Sol / audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** M1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### J1 — Join server, clients and actual native authority

**Saved work:** Joined server/client native and browser source evidence

**Remaining:** Close native client and deployed transport gaps before final join.

**Acceptance:** Real enqueue/pull/report/terminal/landing/internal claim/result; reclaimed refusal vs expired unreclaimed positive; no lost-ack replay; exact server response→both clients→classified result→member reader; actual SDK/CAS/native and browser.

**Source:** scripts/qa/check-project-dispatch-lineage-native.mjs; project-dispatch-native-authority.sql; actual relay mounts

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** B1, C1, M2, B2, C2.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W2 — Notification recipient authority and usable authoring

**Saved work:** Email/recipient authority source in held draft6138

**Remaining:** Schema-first release plus real authorized email and uncertain-send recovery.

**Acceptance:** Derive all to/cc/bcc/channel recipients, current owner, stored/manual/scheduled/resume routes; complete owner authoring before enforcement; reject invalid recipients before provider attempt; native + browser proof.

**Source:** PR6138 227de4f57e35cf111788f8bfca4e50a7d75342f5; qa-lanes/w2-selective-composition-20261003

**Prior owner role:** Sol server integration; Sol member native/provider; Sol workflow approval/browser. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W3 — File operation namespace and destination authority

**Saved work:** Storage namespace and uncertainty source in held draft6132

**Remaining:** Install policy/schema and verify real owner, revocation and recovery boundaries.

**Acceptance:** Bind actual bucket/owner namespace, operation and resolved destination; owned read/write positive, traversal/cross-owner negative; original resumed principal; no production storage writes for testing.

**Source:** PR6132 2b68ff4d0dbeb15032cb7b03fa1cabd4ef406350; qa-lanes/w3-storage-unknown-20261003

**Prior owner role:** Sol server composition; Sol workflow Storage/browser; Sol member native admission; root release. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0, W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W4 — Named OAuth and raw API authority

**Saved work:** Named/raw API authority source in held draft6129

**Remaining:** Compose exact final source and qualify installed/provider behavior.

**Acceptance:** Actual method/action/destination/current credentials and owner authoring; definite setup refusal vs attempted unknown; no retry after uncertain effect. Test real adapter boundaries with private local transports.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W5 — Child workflow and bot creation authority

**Saved work:** Child/bot creation authority source in held draft6129

**Remaining:** Prove real allowed creation, denied targets and original-child recovery.

**Acceptance:** Define creation/child graph/template/pipeline targets; preserve immutable owner and original graph on resume; deny before creation and prove allowed behavior with usable grant UI.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### X1 — Qualify every supported context entry

**Saved work:** Entry-point context/privacy map and scoped repairs

**Remaining:** Qualify every supported surface, including background and System Workflow runs.

**Acceptance:** Entry-by-entry current preferences, relevant bounded recall/skills/lessons, identity/audience, captured+consumed receipt, cancellation/recovery and actual entry positive/negative; no owner-equality shortcut. Include workspace execute, MC cron, org tasks and both workflow engines.

**Source:** agent-chat/stream; agent-execute; voice-router; telegram-agent-turn; delegate-tool; coordination engines; research/Room/background entry routes

**Prior owner role:** Sol workflows. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0, X2, X3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### A1 — Finish global attention and baseline source gaps

**Saved work:** Attention/Room/shelf/mail foundations; global cutover remains off

**Remaining:** Close all16 behavior gaps for cadence, suppression, consent and context.

**Acceptance:** Map all16 behaviors to actual implementation; close each source gap using existing scheduler/store. Quiet hours/cadence/urgency, suppression, consent, truthful marks and task/calendar/support context; test before live provider acceptance.

**Source:** Guide, notification delivery, Room reports, shelf/mail/cadence/state paths; baseline behavior matrix

**Prior owner role:** Sol server. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### R1 — Reconcile main, CI and exact release stack

**Saved work:** ad2ee680 partial successor pushed in draft6190, scoped52/types14/review PASS; required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; prior1c0 CI RED preserved; earlier privacy slices shipped; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: composed `3214f4849e3bb0517b60ee17821826918ee11147` in PR #6196; duplicate-version ratchet clean; writer catalog PASS (2,657 rows); box-ci pending.

**Remaining:** Pass box-ci security-gates and production-build on the exact frozen head; re-merge main if it moves before merge.

**Acceptance:** Exact-head security/build and fresh main; diagnose full-suite failure without dismissing isolated pass; preserve dependent PR order; auto-merge only unchanged guard success.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Exact ad2 security51/build7 PASS; scoped native/REST receipts retained; final complete candidate pending |
| independentlyReviewed | Partial ad2 source reviewed; final scope review pending |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### R2 — Installed schema, profile and release packet

**Saved work:** Installed profile read and source migration packets prepared 2026-10-05: 24 packets classified A17/S3/T4; two version collisions renumbered; ordered 24/24 install + VERIFY proven on a prod-schema clone (not a restored data copy — that rehearsal was blocked by permissions).

**Remaining:** Owner applies the 24 packets to production from the frozen worktree with apply-migration.mjs and confirms the ledger (+24); commit refreshed schema oracles.

**Acceptance:** Read actual installed profile/ledger and dependencies; never replay installed migrations; reconcile source/schema/graph hashes and safe forward/rollback/reapply packet before activation.

**Source:** agent-run-release-profile.py; migration ledger; shelf/grant-history; backup/operator scripts

**Prior owner role:** Sol / server. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### R3 — Writer/effect drain and faithful restore rehearsal

**Saved work:** Private stop/install/unknown recovery and dated restore proofs

**Remaining:** Mount existing release gate accepted-work/all-writer/backup producers; obtain supported writer exclusion and faithful current-target restore. Managed/nonsuperuser observations do not establish active writers or a need for superuser. Owner did not understand broad administrator question; inspect normal management/backup controls before a narrow concrete request.

**Acceptance:** Continuous REST+directPG admission closure, in-flight/unknown effect accounting and mixed-client/broadcaster drain; authorized production-copy role/grant-faithful restore/rehearsal. Never manufacture acceptance with production effects.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.

**Prior owner role:** Root / operator gate. Root must assign a currently available named owner before dispatch. **Original dependencies:** R2, R3B.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### I1 — Compose and independently qualify final source

**Saved work:** ad2ee680 integrates reviewed guard/manual/Telegram repairs on1c0;52 scoped tests/types14/review PASS; exact successor required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; unchanged UI has scoped Linux privacy proof; full final source open; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: frozen `3214f4849e3bb0517b60ee17821826918ee11147`; conflict resolutions reviewed by the verification lane in the trailing audit.

**Remaining:** Trailing audit at the frozen sha; any blocker repair re-freezes.

**Acceptance:** Freeze exact head; joined native HTTP/CAS/browser, relevant full tests, affected types, G11/catalog/security/build. Failures preserved and fixed; no skipped required coverage.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** J1, M3, W2, W3, W4, W5, X1, A1, W6, W7, X5.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Exact ad2 security51/build7 PASS; scoped native/REST receipts retained; final complete candidate pending |
| independentlyReviewed | Partial ad2 source reviewed; final scope review pending |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### D1 — Gated merge and deploy verified code

**Saved work:** UI6179/6181 merged/deployed/public-browser verified

**Remaining:** No owner-run release steps remain from the earlier note: the packets were applied on production 06:03–06:10Z (24/24 applied and verified), PR #6196 was merged 06:11:22Z via merge-if-green and deployed 06:24:35Z — all by the session under the owner's instruction "automerge and automigrate as needed"; the earlier permission blocks did not recur. The live check found two defects (see W7), so live verification is NOT complete. Remaining for this task: its own full authenticated scope, unchanged.

**Acceptance:** Guarded merge against fresh main; automatic code deployment when gates permit; stable actual deployed hash, smoke and independent browser. Disabled code deploy does not imply schema or activation.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** I1, R1, R2, C2S.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Earlier narrow slices only |
| deployed | Earlier narrow slices only |
| activated | Full scope pending |
| verifiedLive | Scoped public checks only; full authenticated scope pending |

### D2 — Activate qualified workflows after compatible rollout

**Saved work:** Global/workflow activation not claimed

**Remaining:** Activate only compatible qualified schema/runtime with tested recovery.

**Acceptance:** Verified installed schema and migration ledger; qualified source/schema/graph; maintained writer/effect hold; authorized activation/cutover with rollback/recovery evidence.

**Source:** release profile and held-window operator; installed source/schema/graph

**Prior owner role:** Root / release gate. Root must assign a currently available named owner before dispatch. **Original dependencies:** D1, R3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Not an implementation stage for this task; see acceptance |
| integrated | Not an implementation stage for this task; see acceptance |
| tested | Not an implementation stage for this task; see acceptance |
| independentlyReviewed | Not an implementation stage for this task; see acceptance |
| merged | Not an implementation stage for this task; see acceptance |
| deployed | Not an implementation stage for this task; see acceptance |
| activated | Pending; no full-scope acceptance |
| verifiedLive | Not an implementation stage for this task; see acceptance |

### P1 — Provider and real computer readiness

**Saved work:** Provider readiness incomplete; Stripe configuration external

**Remaining:** Finish normal provider/account/real-computer setup and approved live inputs.

**Acceptance:** Prepare/test all reversible adapters. Provider configuration/account/DNS/number/real worker and approved call/payment/mail inputs required for live journeys. Do not expose credentials or send unsolicited effects.

**Source:** Stripe Link; Migadu/DNS; Twilio; real browser worker and Telegram takeover

**Prior owner role:** External + Root preparation. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### V1 — Stable deployed all-path and 16 behavior acceptance

**Saved work:** All16 integrated/live acceptance behaviors remain open

**Remaining:** Independently verify stable deployed journeys across all12 surfaces.

**Acceptance:** Real Telegram same-worker takeover/handback/replay refusal, call/mail/payment receipts, owner consent, context/quiet/shelf behavior and every execution entry on stable deployed version; browser desktop/mobile; no mocked closure.

**Source:** EXECUTION-PATH-ACCEPTANCE.md; BASELINE-16-RELEASE-ACCEPTANCE.md

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** D2, P1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Not an implementation stage for this task; see acceptance |
| integrated | Not an implementation stage for this task; see acceptance |
| tested | Not an implementation stage for this task; see acceptance |
| independentlyReviewed | Not an implementation stage for this task; see acceptance |
| merged | Not an implementation stage for this task; see acceptance |
| deployed | Not an implementation stage for this task; see acceptance |
| activated | Not an implementation stage for this task; see acceptance |
| verifiedLive | Pending; no full-scope acceptance |

### U1 — Owner confirmation and final handoff

**Saved work:** Portable handoff maintained; final owner confirmation pending

**Remaining:** Provide specific owner tests only after independent applicable verification.

**Acceptance:** Only after independent success: concise specific user tests; report actual capabilities, evidence, code map, recovery instructions and any truly external unfinished scope.

**Source:** Exact deployed version, evidence packet and concrete user journeys

**Prior owner role:** Owner after independent proof. Root must assign a currently available named owner before dispatch. **Original dependencies:** V1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W6 — Atomic usage limits for scoped capability grants

**Saved work:** Atomic grant reservations source in held draft6129

**Remaining:** Prove installed concurrent use, revocation and original receipt recovery.

**Acceptance:** Concurrent one-use attempts cannot both enter provider/storage; original invocation recovery does not consume twice or replay an uncertain effect; revocation/expiry and personal compatibility controls.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W7 — Original-operation workflow effects

**Saved work:** Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof.

**Remaining:** First: fix the two live defects on hotfix branch `claude/w7-final-task-settle-fix-20261005` (root cause in progress; PR not yet open) — (1) the final task of a post-release Mission Control project cannot settle ("terminal plan chain is not bound to settled plan"), so the plan stays `running`; (2) re-execute is refused for every project because L1-anchor effect intents end `held_unknown` while rerun requires every effect `delivered`. Prove the fix on the real server path against a real database with production-shaped data (the production-shape end-to-end harness lane), release it, then repeat live acceptance: the stuck project must finish and behaviour B (lost-acknowledgment rerun recovers the original run, no duplicate) must pass. Behaviour A (critical-failure drain) is not drivable on production from any control until Mission Control plans carry a critical path — PR #6198, an owner decision because it changes behaviour (a third failure on the main chain fails the project instead of skipping). Until then W7 drain/rerun is NOT verified live (1 of 3 passed) and must not be shown as complete. Mission Control admission is left open by operator decision; revisit if the fix is slow. Also: finish the read-only audit of every other guarded control; fix the planner-screen bugs (a malformed planner answer produced a launchable 0-task plan; the review panel did not follow the selected plan); owner decision on finding X6 (the refusal wording gives owners of pre-release projects no path forward); restore-verify the pre-install backup; commit the install log and acceptance evidence to the evidence branch; when merges are open, get box-ci green on follow-up PR #6197 (`claude/w7-followups-20261005` @ `1de6f98ed2`) and merge it via `scripts/ci/box-ci/merge-if-green.sh`. Then: the F2 design decision, remaining effects/manual parity, legitimate department recipients, safe active cancellation, real L1 and the rerun-init pending/unknown recovery boundary.

**Acceptance:** Thread server ToolContext identity, reserve before effect, preserve original run and unknown outcome, reject missing/forged identity, prove cap/no replay via actual transport. Bind actual task settlement to the original saved execution claim atomically; reject superseded results before effects and recover post-commit delivery without duplication. Prove usable original-child lookup/recovery and keep unsupported callers explicit.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.; new branches/commits in pause checkpoint.

**Prior owner role:** release_integration: isolated claim/settlement production repair; release_verification: independent tests; root: composition/release. Root must assign a currently available named owner before dispatch. **Original dependencies:** W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the drain/rerun milestone: failure drain, atomic rerun, mounted rerun recovery and runtime binding are in candidate ac48190955. Remaining W7 effects still open. |
| integrated | Yes: candidate ac48190955 (PR #6196) is squash-merged into main as 55a12f0da9. The 26-file overlap with Agent Run PR #6168 is resolved afterwards by the Agent Run session. |
| tested | Pre-release suites passed but were INSUFFICIENT. At ac48190955: full-tree required CI GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps; macOS Native Land not run) plus scoped PASS (native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; unit 924 passed / 7 skipped / 0 failed on the second run). The 26 native contract cases ran on fixtures and the 46 browser cases mocked the server boundary; none exercised the real server path with production-shaped data, and two defects reached production through them. History: the previous head 3214f4849e was full-tree RED (2 failed / 55,609 passed / 374 skipped; scoped TypeScript check 5 errors). |
| independentlyReviewed | Yes at ac48190955: independent trailing audit PASS on all 5 checks, including a diff review of the fix commit. One LOW flake risk recorded (a single timeout under parallel build load; the file alone passed 12/12 three times). The follow-up branch is not reviewed. The review did not catch the two live defects found afterwards on production. |
| merged | Yes: 2026-10-05 06:11:22Z via scripts/ci/box-ci/merge-if-green.sh (squash) → main 55a12f0da9b09052d0bfa186f747654a60f3a931. |
| deployed | Yes: production schema installed 06:03–06:10Z (24/24 packets APPLIED AND VERIFIED; ledger 691 → 715); code deployed 06:24:35Z (deploy-main "live: 55a12f0da health 200"; /api/version reports 55a12f0da9). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. Pre-install backup sealed with matching row counts but NOT restore-verified. |
| activated | Yes by construction: no feature flag, so code + SQL deployed means live. mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Mission Control admission left OPEN by operator decision while the hotfix is prepared. |
| verifiedLive | NO — not complete. 1 of 3 behaviours passed, 1 is blocked by live defects, 1 is not drivable. C PASS (~06:35Z; signed-in owner, real Chrome, production): re-execute on a pre-release plan refused, nothing created. B BLOCKED: re-execute is refused for every project (L1-anchor effects end `held_unknown`; rerun requires all `delivered`; pre-release plans refused as `unproven_legacy`). A NOT DRIVABLE on production: Mission Control plans have an empty critical path, there is no owner "mark failed" control, and an owner-declared failure is re-dispatched; only Workspace-planner plans carry a critical path (17 of 40 production plans); the drain's evidence is build-box contract cases only. Additional live defect: the first post-release Mission Control project cannot finish (final-task settle rejected, "terminal plan chain is not bound to settled plan"). Live positives: the birth-proof row was written (F1) and both tasks were claimed through receipts. Open product note X6: the refusal wording gives owners of pre-release projects no path forward (owner decision). |

### X2 — Confirm System Workflow durable terminal and pause receipts

**Saved work:** System Workflow pause and Memory Promotion partial fixes deployed

**Remaining:** Qualify real admitted-owner pause/checkpoint/terminal recovery journeys.

**Acceptance:** Terminal receipt qualification plus caller handling of uncertain outcomes; required CI, installed transport, pause/resume/node acknowledgments and deployed acceptance remain open.

**Source:** lib/vms/coordination/{trigger,run-logger}.ts; tests/unit/system-workflow-terminal-durability-postgrest.test.ts

**Prior owner role:** Sol workflow / Root verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Earlier narrow slices only |
| deployed | Earlier narrow slices only |
| activated | Full scope pending |
| verifiedLive | Scoped public checks only; full authenticated scope pending |

### X3 — Refuse zero-row completion in scheduled and direct workflows

**Saved work:** Missing original terminal-row refusal has scoped native evidence

**Remaining:** Verify scheduled and direct deployed paths retain truthful outcomes.

**Acceptance:** Both scheduled engine and direct persisted execution refuse unconfirmed completion; no replay or terminal promotion after missing row.

**Source:** lib/vms/workflows/execution-engine.ts; native terminal persistence regression

**Prior owner role:** Sol workflow. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### X4 — Retain uncertain scheduled workflow attempts before another tick

**Saved work:** Scheduled original-attempt source preserved in held drafts

**Remaining:** Install guarded occurrence schema and prove next-tick no-replay recovery.

**Acceptance:** Carry exact original identity and unknown status; atomically hold/recover original schedule attempt; real transport lost-ack and next-tick no-repeat proof, installed schema and deployed checks.

**Source:** app/api/cron/workflow-triggers/route.ts:189; lib/vms/workflows/execution-engine.ts; docs/agent-run/scheduled-workflow-recovery-plan-20261001.md

**Prior owner role:** Sol SQL + Sol engine; Root native integration. Root must assign a currently available named owner before dispatch. **Original dependencies:** X3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### X5 — Qualify original scheduled approval continuation

**Saved work:** Bounded original approval continuation source qualified

**Remaining:** Close remaining effectful graphs and real approval/uncertain-outcome acceptance.

**Acceptance:** Original paused run/approved node binding, unknown-provider no replay, concurrent resume/worker death fences, owner/config changes, native and browser acceptance before activation.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** X4, W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### C2 — Bind project Git commands to exact workspace

**Saved work:** Project dispatch6118 and eligible-recipient6141 source qualified

**Remaining:** Qualify mounted Realtime/relay, exact workspace commands and schema-first rollout.

**Acceptance:** Authenticate owner+logical session+project+workspace identity for active and suspended commands; refuse delayed opposite-context commands, changed authority and missing sidecars; retain personal-only positive controls.

**Source:** relay land producer/PUT; command protocol; cloud and desktop worktree routing; PR6141 c8d5 eligible project recipient successor

**Prior owner role:** Sol6 implementation + independent verifier. Root must assign a currently available named owner before dispatch. **Original dependencies:** C1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### R3B — Stage runtime role before candidate schema extension

**Saved work:** Dormant minimal role source with scoped native ACL proof; runtime helper/bridge integration saved82b01044; 19 private native actual-caller cases and independent review PASS.

**Remaining:** Reconcile B0 source packet and current caller bindings; qualify full installed ACL/default-ACL/policies and hosted transaction pooler; retain separate B1/gate-six work; guarded role rollout. Source integration is no longer missing, but production runtime role remains absent in dated census.

**Acceptance:** Exact named phase/catalog fingerprints, old/future owner clones, wrong-phase/partial schema/drift refusal, NOLOGIN and no active sessions, rollback from each phase. Still only OWNER_DB_URL scope, not REST/effects/global closure.

**Source:** scripts/qa/owner-runtime-main-role in qa-lanes/r3-owner-minimal-install-packet-20261002; codex/w7-runtime-binding-refresh-20261005 at82b010441ad1a82e66368585f7ddd68d5cfc9103; private release/runtime-role-reconciliation-plan.md.

**Prior owner role:** sol6_project_server; root independent review. Root must assign a currently available named owner before dispatch. **Original dependencies:** R2.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Runtime identity helper/bridge source committed82b01044; full role rollout packet reconciliation pending. |
| integrated | Actual owner DB helper and coordinator bridges wired; runtime role not installed. |
| tested | 47 focused+28 bridge+23-file types; 19 private PG cases PASS. Synthetic schema/admission; hosted pooler/ACL proof open. |
| independentlyReviewed | Exact source and private native terminal independently reviewed; installed role/combined review pending. |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### C2S — Install and verify project schema before server rollout

**Saved work:** Seven ordered project-schema packets rehearsed privately

**Remaining:** Perform guarded installed-target schema rollout with live service-role verification.

**Acceptance:** Same-operation writer exclusion and faithful backup/restore; exact installed schema and service-role ACL verification; compatibility and recovery proof. No open unknown effects or unaccounted admission holders.

**Source:** Seven ordered C2 migration packets:010100,010110,010120,010140,021300,021400,021500; existing guarded release coordinator

**Prior owner role:** Root / coordinated release. Root must assign a currently available named owner before dispatch. **Original dependencies:** R2, R3, C2.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |


## Full behavior and surface acceptance

- **B01** Quiet morning suggestion or intentional silence — live acceptance open
- **B02** Owner-voice drafts: unchanged, edited, ignored; no implicit send — live acceptance open
- **B03** Visible shopping/screenshots under grants/history — live acceptance open
- **B04** Approved real call: recipient, speech and outcome — live acceptance open
- **B05** Appropriate initiative without broadened authority — live acceptance open
- **B06** Same real computer: Telegram takeover, handback, replay refusal — live acceptance open
- **B07** Loose-end shelf: add, finish, dismiss, suppress later — live acceptance open
- **B08** Mail: retrieve, review, send/edit/snooze/ignore and suppression — live acceptance open
- **B09** Two-owner friend consent and revocation/concurrency — live acceptance open
- **B10** Unique mailbox and same-conversation inbound — live acceptance open
- **B11** Exact shop/item/amount payment instrument and receipt — live acceptance open
- **B12** Truthful marks linked to checked history/context chain — live acceptance open
- **B13** Current preferences and bounded relevant older memory across surfaces — live acceptance open
- **B14** Honest site/provider/evidence/uncertain-commit stops — live acceptance open
- **B15** Quiet hours, batching, cadence, urgency, no duplicate work — live acceptance open
- **B16** Tone/length from actual task/calendar/support context — live acceptance open

Supported surfaces:

1. Personal chat full/fast/direct
2. Telegram canonical transport
3. Mounted and legacy voice
4. Headless agent-execute
5. Delegation
6. Coordination System Workflows
7. Generic Workflow executor and Routines
8. PlanGraph/background Build loops
9. Workspace plan execute, MC cron, organization tasks
10. Scheduled research and competitor scans
11. Rooms scheduled/manual/huddle
12. Shared/company/visiting audiences

## Updating and handing off this plan

1. Read this revision, the canonical record and product repository instructions before starting. Inspect existing code and receipts; distinguish missing code from missing proof/access.
2. Update `workflow-plan.json`: current evidence, task stages, actual blocker, named owner, next proof, exact candidate and timestamps. Retain historical baseline records and all task acceptance criteria.
3. Run `python3 scripts/render_plan.py`, then `python3 scripts/render_plan.py --check`. The check verifies scope, policy IDs, an acyclic graph and exact generated bytes. It does not verify product behavior.
4. Publish the record and generated files in one reviewed commit. Secret-scan plaintext before uploading evidence; encoding is not sanitization. Reuse the existing hash-manifest packaging and independent reconstruction checks.
5. Verify remote bytes and anonymous browser rendering for the three entry documents, all 33 checklist rows and the dependency graph. Record the publication/browser receipt separately; avoid a self-referential commit-hash rewrite loop.

Checkpoint report: **usable capability advanced; dependency closed; exact blocker and category; accountable owner; proof needed; next action; source/test/review/merge/deploy/activation/live state; elapsed delivery time**. Unknown timestamps remain unknown. Publish on meaningful dependency closure, blocker change, pause or handoff—not after every tool call.

The generator catches missing rules and stale generated views when run. `AGENTS.md` instructs future agents to run it; no runtime enforcement in SupraOS Build or mandatory GitHub branch protection has been installed by this documentation change.
