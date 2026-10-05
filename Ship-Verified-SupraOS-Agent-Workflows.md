# Ship Verified SupraOS Agent Workflows

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


## Goals and current result

Current result: see the pause checkpoint above for this run. The following table preserves earlier accumulated implementation and evidence; it does not mean those components were newly shipped during this paused run.

The run repaired and integrated original agent memory, estimator, notification, projectless finalization and safe idle-cancellation behavior; strengthened real private SQL/REST qualification; and composed a reviewed partial successor. Full production release remains blocked by code and installed-release prerequisites.

| Work | Implemented / integrated | Tested / independently reviewed | Merged / deployed / verified live |
| --- | --- | --- | --- |
| Original retrospective memory | Receiver, immediate settlement and cron recovery integrated; narrow original-bound readback repairs mapped-schema access without broad SELECT | Direct SQL and actual parent→memory REST pass. Exact `1c0` import-closure run **af423ff2** passes ten private cases, four lost-ACK faults and original public/mapped destination/refusal checks; independent audit and cleanup pass | Unmerged / undeployed / no authenticated live claim |
| Estimation recovery | Original settlement, parent, sample and plan-closer receivers integrated | Actual ten-case REST run **eed6aa56** passes four lost-ACK faults, original persisted parent checks and no duplicate writes; independently audited and cleaned | Unmerged / undeployed / no authenticated live claim |
| Notification recovery | Original owner destination binding, one-use dispatch and saved-result recovery integrated with immediate/cron callers | Direct SQL **191343ac** passes 16 cases; actual REST: PASS **c593b19b**, 12 private cases, two committed RPC ACK faults, concurrent admission and zero duplicate sends; independent audit/cleanup pass. Configuration and Telegram are stubbed. | Unmerged / undeployed / provider and authenticated live proof open |
| Signed manual notification | Commit `a97bc98bd1cc40e3b3ba079b67d22ea1d2c112be` adds original notification intent after parent finalization and invokes the existing receiver | 26 manual-action unit/receiver tests with mocked dependencies, 13 changed-file type checks and independent source review pass; 15-case actual manual-SQL→parent→notification proof **baeb5066** independently passes, including three manual cases and three total committed-ACK faults; cleanup independently confirmed. It does not import the manual TypeScript helper and stubs provider/configuration | Unmerged / undeployed / full manual terminal-event/retro parity remains open |
| New task admission guard | Commit `cb727d09f964d461942b06aca4bbee0047a2d719` refuses terminal/exhausted-critical new claims under existing locks | Native **c566a19c** passes 22 phases/49 outputs, both lock orders, exact definition/role/rollback checks and original-result admission after failure; independently audited | Unmerged / unapplied / failure drain is still separate |
| Projectless finalization and idle cancellation | Saved repairs carry exact original plan/run/version and fail closed on active or uncertain work | Projectless 18 native cases; cancellation route/native and six synthetic mounted Linux interactions pass independently | Unmerged / undeployed / active cancellation and real L1 remain open |
| Combined partial candidate | Pushed **ad2ee680464217fd1b00883bf7ea9fc917ed3140**, tree **d646dcd04525189171ee67fc83098667cac6d290**, in draft [PR6190](https://github.com/jtobkin/suprafx-platform/pull/6190). This preserves the 828 parent and adds only the independently reviewed catalog repair. | The unchanged product source passed 52 focused tests and 14 changed-file type checks. The catalog-only successor passed all 34 unchanged catalog tests, exact inventory, pinned G11 and independent committed review. Required CI on exact `ad2` now PASSES: security gates (51 steps) and production build (7 steps). macOS Native Land was not run. Earlier `828` failure is preserved: 55,188 tests passed, 374 skipped and one catalog assertion reported six diagnostics. Strict E3 recovery readiness remains RED with 6,540 blockers. | No W7 production merge, deployment or activation during this focus |

The earlier frozen `1c0e12c00717ff94572f64f821ab0663aeb54d28` in draft PR6189 remains preserved. Its required CI was **RED**: 55,181 tests passed, 374 skipped and one old direct-call Telegram assertion failed; the build was blocked. The separate repair integrates the missing manual notification and tests the real resolver/guarded transport using fake HTTP and saved-route RPC. It preserves owner precedence, active shared binding, revocation, destination-change refusal and no resend. It does not establish Telegram provider acceptance.

Exact-`1c0` Linux Chromium privacy checks at 390/1440 pass, with screenshots independently inspected. Those tests use synthetic authentication/EventSource. The Mac Chromium startup SIGTRAP is preserved; no authenticated production browser result is inferred. Later composition keeps those UI files unchanged, but final required/live gates still belong to the exact final release.


## Already shipped versus pending

Earlier dashboard/workspace privacy fixes and a narrow background-producer privacy slice remain part of the preserved project history. A fresh ordinary-TLS read of `/api/version` at 23:23 UTC returned production revision `5bd8d1f9ccd6d52cc6bf0c44ca83252d93a64f96`; this public version observation is not authenticated behavior verification. This focus produced integrated code and stronger evidence, **not a new W7 production release**. The 2026-10-05 01:01–02:04 UTC run saved three source lanes and scoped evidence only; no new production capability was deployed. The revision above remains the last observed version, not a fresh observation at publication.

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

## Parallel lanes and work limits

| Lane | Accountable work | May run now / after resume | Ownership boundary |
| --- | --- | --- | --- |
| Root | Scope, candidate, integration decisions, documentation and release coordination | Verify exact baseline and assign owners; resolve blockers | Does not silently replace another lane's source |
| Implementation | Failure drain, real automated/manual callers, recovery and truthful parent receipts | First implementation priority; one shared-file owner | Orchestrator, transition helpers and additive authority SQL owned together |
| Prerequisites | Writer/accepted-work controls, schema/roles, restoration, normal QA/provider access | In parallel from the first round | Own release packets and access records; coordinate shared source changes |
| Independent verification | Red regression, cheap preflight, source review, SQL/REST and applicable browser checks | Prepare alongside implementation; qualify immutable source afterward | No concurrent edits to implementation files; preserve failed evidence |

Start with root plus these three lanes where capacity permits. More agents get bounded independent subtasks only when they remove a dependency; they do not create extra feature streams. Grok can trace code/design tests or audit when its connector permits; read-only output is not an implementation. If a requested model is unavailable, disclose and record the fallback or capacity blocker.

Rounds below show dependency eligibility, not unlimited concurrency or duration estimates. Reconcile file ownership, CPU/memory/native host limits and access before dispatch. Keep one high-impact code slice in progress; finish failure drain before opening the next effect. BROADER is a preserved backlog umbrella, not permission to start all its tasks at once.


## Preserved failure-drain design analysis

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


## Code locations and fresh-computer recovery

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

## Definition of finished

SupraOS should execute with correct private context, exact owner/member authority and original operation identity across personal chat, Telegram, mounted/legacy voice, headless execution, delegation, System Workflows, generic workflows/Routines, background Build, workspace/cron/organization tasks, scheduled research, Rooms, and shared/company/visiting audiences. iMessage remains deferred; WhatsApp remains excluded.

The 16 behavior families cover appropriate suggestions/silence; owner-voice drafts; visible permissioned browser/shopping work; approved calls; bounded initiative; Telegram takeover/handback; loose ends and suppression; mail review/edit/send/snooze/ignore; two-owner consent/revocation; unique inbound mailboxes returning to the original conversation; exact approved purchases/payment/receipts; evidence-backed history/completion; current preferences and bounded memory; honest failure/unavailability/uncertainty; quiet hours/batching/cadence/urgency; and context-appropriate tone/length.

All agreed behavior must be integrated, independently reviewed, pass required gates on the exact final source, be merged/deployed with compatible schema/runtime, activated where required, and independently verified live with tested recovery. Unknown outcomes cannot be retried as fresh actions or reported as completed. Only then provide owner confirmation tests and a truthful operating/recovery handoff. A completed W7 slice is progress; it does not redefine the project as finished.

## Updating and handing off this plan

1. Read this revision, the canonical record and product repository instructions before starting. Inspect existing code and receipts; distinguish missing code from missing proof/access.
2. Update `workflow-plan.json`: current evidence, task stages, actual blocker, named owner, next proof, exact candidate and timestamps. Retain historical baseline records and all task acceptance criteria.
3. Run `python3 scripts/render_plan.py`, then `python3 scripts/render_plan.py --check`. The check verifies scope, policy IDs, an acyclic graph and exact generated bytes. It does not verify product behavior.
4. Publish the record and generated files in one reviewed commit. Secret-scan plaintext before uploading evidence; encoding is not sanitization. Reuse the existing hash-manifest packaging and independent reconstruction checks.
5. Verify remote bytes and anonymous browser rendering for the three entry documents, all 33 checklist rows and the dependency graph. Record the publication/browser receipt separately; avoid a self-referential commit-hash rewrite loop.

Checkpoint report: **usable capability advanced; dependency closed; exact blocker and category; accountable owner; proof needed; next action; source/test/review/merge/deploy/activation/live state; elapsed delivery time**. Unknown timestamps remain unknown. Publish on meaningful dependency closure, blocker change, pause or handoff—not after every tool call.

The generator catches missing rules and stale generated views when run. `AGENTS.md` instructs future agents to run it; no runtime enforcement in SupraOS Build or mandatory GitHub branch protection has been installed by this documentation change.
