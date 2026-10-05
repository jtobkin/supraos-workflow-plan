# SupraOS Release Plan Checklist

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-05T08:55:00Z**. Canonical record SHA-256: `54606c547ffc5ba3508f01eed5fe35d52d7ea7462dbb2f6821f4f8d91e46d1fc`.

**Execution state:** PAUSED. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. W7 (candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f`, PR #6196) is MERGED, DEPLOYED and ACTIVATED on production but NOT verified live (1 of 3 behaviours); the milestone is NOT complete. The active checkpoint is PRODUCTION STABILISATION. NEXT ACTION on resume: ship hotfix PR #6199 — apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production BEFORE the merge, then merge with `scripts/ci/box-ci/merge-if-green.sh 6199` once both box-ci checks are green on the current head. Production code is main `e2093866c1` (the W7 squash `55a12f0da9` from PR #6196 plus the unrelated PR #6172); `https://supraos.ai/api/version` re-read anonymously at 08:46Z reports `e2093866c1`. Main has since moved to `a2e04e9a42` (unrelated PR #6059 from another session, merged 08:37Z, not yet live at 08:46Z). Production database: the 24 W7 packets were applied and verified 06:03–06:10Z (ledger 691 → 715); the ledger read 735 at 08:34Z because the separate Agent Run session installed 16 packets of its own. That session's three "after-live" packets (`20260929010002`, `20260929080000`, `20261001000000`) are NOT installed and must not be installed until PR #6168's build is live. The pre-install backup (5.4 GB, counts match) is on the web host, NOT restore-tested; keep it until live acceptance passes. SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. One test project is stuck on production (project `43470d88`, plan `13fe1f43`, "W7 live test", status running; its final task cannot settle); it should self-heal within a minute of the hotfix going live, and the coordinator logs "terminal plan chain is not bound to settled plan" every minute until then. Mission Control admission was left OPEN on purpose. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). Live acceptance: 1 of 3 behaviours. C PASS (Re-execute on a pre-release plan refused, nothing created). B (lost-acknowledgment rerun) is blocked until PR #6199 is live. A (critical-failure drain) is not drivable from any control until PR #6198 plus an owner "mark failed" control exist. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. FIVE OWNER DECISIONS waiting: (1) Grants: every integration step in a scheduled workflow now needs a per-action grant that expires in 1–24 hours, so existing Gmail/Calendar/API workflows fail each run and file a card in Settings → Grants. Options: restore the pre-release un-gated behaviour for owner-authored scheduled workflows; make grants standing; or keep it and tell users. (2) PR #6198: Mission Control plans get a critical path — a third failure on the main chain fails the project and drains unstarted work instead of skipping the task. (3) Pre-release projects (39) cannot be re-executed: recommended "Adopt this project" signed receipt (new packet); stopgap "Duplicate as a new project" (no packet); plus plain-English refusal wording per status. (4) Owner controls: is "I'll handle it" on an unknown-outcome task = closed as skipped? Should an owner "Mark failed" be final (no automatic retry)? (5) Scheduled approval steps: turn on the three remaining switches, or keep human-approval steps unsupported in scheduled workflows for now? SEVEN-STEP EXECUTION PLAN: Step 1 — Verify state (read-only): `/api/version`; `scripts/ci/box-ci/status.sh` for #6197 #6198 #6199 #6168; whether main moved past `e2093866c1` (it has: `a2e04e9a42` at 08:46Z); the production ledger count and whether `20261005232000` is present (expect absent); the stuck plan's status; the scheduler watch queries from `scheduled-flag-on-verdict.md` (stalled occurrences, failure rate, duplicates — a duplicate slot is the ONLY reason to turn the switch off). Step 2 — Ship the hotfix PR #6199: merge origin/main in if main moved; run scoped vitest, `node scripts/check-changed-types.mjs`, `node scripts/check-private-ai-recovery-writers.mjs`, and `scripts/checks/duplicate-migration-numbers.mjs` against the merge base; run the production-shape harness on the head (expect S1–S3 pass and Re-execute "created"); wait for both box-ci statuses = success on the CURRENT head. Then, in order: apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production with `scripts/apply-migration.mjs` (expect APPLIED AND VERIFIED; on an alarm or UNKNOWN stop and reconcile by reading, do not retry) → `scripts/ci/box-ci/merge-if-green.sh 6199` → watch the deploy log on the web host for `live: <sha> health 200` → confirm the stuck plan `13fe1f43` becomes completed and the coordinator error stops. Step 3 — Live acceptance B (signed-in owner, real browser): on project `43470d88` ("W7 live test") click Re-execute → Start new run, reload the tab immediately, expect "A re-execution request needs confirmation…" and the button "Check re-execution"; click it. Pass = one row in `vms_mc_run_rerun_receipts` for that action, same run id, one new `vms_execution_runs` row, the new run completes. Screenshot. Step 4 — Merge PR #6197, then refresh `supabase/schema/public-*.txt` again for packet `20261005232000`, removing any now-stale BASELINE entry in `tests/unit/queried-tables-exist.test.ts`. Step 5 — Finish the paused lanes in parallel, each as its own PR with box-ci green, an independent review, real-database proof on the build box and, for UI, a real-browser check: (a) owner controls incl. packet `20261005233000` and fault 4 (task failure wedges a projects-route plan — it has no owner yet); (b) delete + tick isolation (rebase onto main after #6197 merges); (c) scheduled-workflow stalls, for-each, delete — reproduce on a real database first; (d) planner screen; (e) land the production-shape harness as a required pre-release check and add scenarios for every fault. Apply each packet to production before the code that needs it. Step 6 — After the owner decisions: PR #6198, then live acceptance A (critical failure with an unstarted sibling → sibling drained, plan failed, never completed); the legacy Re-execute option; grants. Step 7 — Clean up: remove the production backup and its tool folder; delete merged lane folders (only your own, `git worktree remove` without --force); then continue scope: remaining W7 effects/manual parity, active cancellation, real L1 anchoring, rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md` on #6197), coordinator sweep run-id check, the runtime role (5 unmapped owner schemas — owner decision), Stripe Link (owner external), normal QA invite. Full scope stays 33 tasks / 16 behaviours / 12 surfaces; iMessage deferred, WhatsApp excluded. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes (the review missed the live faults and the new environment switch); merged yes (`55a12f0da9`, PR #6196); deployed yes; activated yes; verified live NO — 1 of 3 behaviours (C). The W7 milestone is NOT complete. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. Owner standing instruction for this run: "automerge and automigrate as needed" (it does not bypass permissions, approvals, release gates or resource limits). Evidence: private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `b11636b366` (install log, acceptance screenshot, live-controls audit, end-to-end results, scheduler flag-on verdict). The resume prompt for the next session is in the pause handoff below (sanitised); the unsanitised prompt is in the private memory repo as `PROMPT-2026-10-05-resume-w7-stabilization.md`. History, kept as it happened: first cut `3214f4849e` got RED required CI at ~05:00Z and was replaced by `ac48190955` (required CI GREEN 05:36Z, independent trailing audit PASS 5/5); production install 06:03–06:10Z (24/24 packets applied and verified); merged 06:11:22Z → main `55a12f0da9b09052d0bfa186f747654a60f3a931`; deployed 06:24:35Z; live acceptance 06:35–07:45Z found the first two faults. This is a partial-W7 milestone that is itself not yet verified live; full W7 scope and the other tasks remain open.

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** **PRODUCTION STABILISATION (paused).** OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (tree `49bf08e3354a115783635eebfa4801dfa953bb6c`, PR [#6196](https://github.com/jtobkin/suprafx-platform/pull/6196)) is **merged, deployed and activated on production, but NOT verified live — 1 of 3 behaviours. The milestone is not complete**. **Next action.** NEXT ACTION on resume: ship hotfix PR #6199 — apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production BEFORE the merge, then merge with `scripts/ci/box-ci/merge-if-green.sh 6199` once both box-ci checks are green on the current head. **Production now.** Production code is main `e2093866c1` (the W7 squash `55a12f0da9` from PR #6196 plus the unrelated PR #6172); `https://supraos.ai/api/version` re-read anonymously at 08:46Z reports `e2093866c1`. Main has since moved to `a2e04e9a42` (unrelated PR #6059 from another session, merged 08:37Z, not yet live at 08:46Z). Production database: the 24 W7 packets were applied and verified 06:03–06:10Z (ledger 691 → 715); the ledger read 735 at 08:34Z because the separate Agent Run session installed 16 packets of its own. That session's three "after-live" packets (`20260929010002`, `20260929080000`, `20261001000000`) are NOT installed and must not be installed until PR #6168's build is live. The pre-install backup (5.4 GB, counts match) is on the web host, NOT restore-tested; keep it until live acceptance passes. One test project is stuck on production (project `43470d88`, plan `13fe1f43`, "W7 live test", status running; its final task cannot settle); it should self-heal within a minute of the hotfix going live, and the coordinator logs "terminal plan chain is not bound to settled plan" every minute until then. Mission Control admission was left OPEN on purpose. **Scheduled-workflow incident.** SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. **Eight faults.** EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). **Live acceptance.** Live acceptance: 1 of 3 behaviours. C PASS (Re-execute on a pre-release plan refused, nothing created). B (lost-acknowledgment rerun) is blocked until PR #6199 is live. A (critical-failure drain) is not drivable from any control until PR #6198 plus an owner "mark failed" control exist. **PRs and branches.** PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. **Migrations.** Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. **Owner decisions.** FIVE OWNER DECISIONS waiting: (1) Grants: every integration step in a scheduled workflow now needs a per-action grant that expires in 1–24 hours, so existing Gmail/Calendar/API workflows fail each run and file a card in Settings → Grants. Options: restore the pre-release un-gated behaviour for owner-authored scheduled workflows; make grants standing; or keep it and tell users. (2) PR #6198: Mission Control plans get a critical path — a third failure on the main chain fails the project and drains unstarted work instead of skipping the task. (3) Pre-release projects (39) cannot be re-executed: recommended "Adopt this project" signed receipt (new packet); stopgap "Duplicate as a new project" (no packet); plus plain-English refusal wording per status. (4) Owner controls: is "I'll handle it" on an unknown-outcome task = closed as skipped? Should an owner "Mark failed" be final (no automatic retry)? (5) Scheduled approval steps: turn on the three remaining switches, or keep human-approval steps unsupported in scheduled workflows for now? **Order from here.** SEVEN-STEP EXECUTION PLAN: Step 1 — Verify state (read-only): `/api/version`; `scripts/ci/box-ci/status.sh` for #6197 #6198 #6199 #6168; whether main moved past `e2093866c1` (it has: `a2e04e9a42` at 08:46Z); the production ledger count and whether `20261005232000` is present (expect absent); the stuck plan's status; the scheduler watch queries from `scheduled-flag-on-verdict.md` (stalled occurrences, failure rate, duplicates — a duplicate slot is the ONLY reason to turn the switch off). Step 2 — Ship the hotfix PR #6199: merge origin/main in if main moved; run scoped vitest, `node scripts/check-changed-types.mjs`, `node scripts/check-private-ai-recovery-writers.mjs`, and `scripts/checks/duplicate-migration-numbers.mjs` against the merge base; run the production-shape harness on the head (expect S1–S3 pass and Re-execute "created"); wait for both box-ci statuses = success on the CURRENT head. Then, in order: apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production with `scripts/apply-migration.mjs` (expect APPLIED AND VERIFIED; on an alarm or UNKNOWN stop and reconcile by reading, do not retry) → `scripts/ci/box-ci/merge-if-green.sh 6199` → watch the deploy log on the web host for `live: <sha> health 200` → confirm the stuck plan `13fe1f43` becomes completed and the coordinator error stops. Step 3 — Live acceptance B (signed-in owner, real browser): on project `43470d88` ("W7 live test") click Re-execute → Start new run, reload the tab immediately, expect "A re-execution request needs confirmation…" and the button "Check re-execution"; click it. Pass = one row in `vms_mc_run_rerun_receipts` for that action, same run id, one new `vms_execution_runs` row, the new run completes. Screenshot. Step 4 — Merge PR #6197, then refresh `supabase/schema/public-*.txt` again for packet `20261005232000`, removing any now-stale BASELINE entry in `tests/unit/queried-tables-exist.test.ts`. Step 5 — Finish the paused lanes in parallel, each as its own PR with box-ci green, an independent review, real-database proof on the build box and, for UI, a real-browser check: (a) owner controls incl. packet `20261005233000` and fault 4 (task failure wedges a projects-route plan — it has no owner yet); (b) delete + tick isolation (rebase onto main after #6197 merges); (c) scheduled-workflow stalls, for-each, delete — reproduce on a real database first; (d) planner screen; (e) land the production-shape harness as a required pre-release check and add scenarios for every fault. Apply each packet to production before the code that needs it. Step 6 — After the owner decisions: PR #6198, then live acceptance A (critical failure with an unstarted sibling → sibling drained, plan failed, never completed); the legacy Re-execute option; grants. Step 7 — Clean up: remove the production backup and its tool folder; delete merged lane folders (only your own, `git worktree remove` without --force); then continue scope: remaining W7 effects/manual parity, active cancellation, real L1 anchoring, rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md` on #6197), coordinator sweep run-id check, the runtime role (5 unmapped owner schemas — owner decision), Stripe Link (owner external), normal QA invite. Full scope stays 33 tasks / 16 behaviours / 12 surfaces; iMessage deferred, WhatsApp excluded. **Stage truth.** Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes (the review missed the live faults and the new environment switch); merged yes (`55a12f0da9`, PR #6196); deployed yes; activated yes; verified live NO — 1 of 3 behaviours (C). The W7 milestone is NOT complete. **Lesson.** Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. **Evidence.** private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `b11636b366` (install log, acceptance screenshot, live-controls audit, end-to-end results, scheduler flag-on verdict). Qualification before the merge, kept as recorded: box-ci on `ac48190955` observed 05:36Z — security-gates SUCCESS (51 steps; macOS Native Land not run), production-build SUCCESS (7 steps); independent trailing audit PASS on all 5 checks (fix diff; native 26/26; ordered 24/24 packets applied and verified as non-superuser; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run). Those suites passed and were insufficient: none drove the real server path with production-shaped data

**Current candidate record:** `ac4819095585eed003eb0c510b0a8c8608d5e73f`, tree `49bf08e3354a115783635eebfa4801dfa953bb6c`. Security: box-ci/security-gates SUCCESS on ac48190955 (51 steps; macOS Native Land not run). Previous head 3214f4849e: FAILURE (whole unit tree 2 failed / 55,609 passed / 374 skipped across 4,508 files; scoped changed-file TypeScript check 5 errors); build: box-ci/production-build SUCCESS on ac48190955 (7 steps). Previous head 3214f4849e: ERROR (not built because security gates failed); macOS Native Land: Not run (not part of box-ci). Merged: True; deployed: True; activated: True; verified live: False. Scope: Composed W7 failure-drain/rerun candidate (partial W7; full scope open). Frozen candidate ac48190955 = 3214f4849e + fix commit 867a5f2114 + clean merge of origin/main 7a10b7a3fc; required CI GREEN and independent trailing audit PASS 5/5 at that commit. Squash-merged 2026-10-05 06:11:22Z as main 55a12f0da9b09052d0bfa186f747654a60f3a931 (PR #6196); production schema installed 06:03–06:10Z (24/24 packets applied and verified); deployed 06:24:35Z; activated. `verified live: False` here means NOT verified live and the milestone NOT complete: 1 of 3 behaviours passed (C); B waits for hotfix PR #6199; A waits for PR #6198 plus an owner "mark failed" control. Eight faults are open (two fixed in the unmerged hotfix). The release also carried a once-only scheduler whose unset switch paused all 534 scheduled workflows 06:24–07:57Z; the owner turned it on; it is activated but not qualified per its cutover checklist. OWNER PAUSE at ~08:55Z: nothing from this project merged after #6196. Not part of this candidate: hotfix PR #6199 @ dfebdab30a, PR #6198 @ 19d4d01eae (owner decision), follow-up PR #6197 @ 1de6f98ed2, and five unmerged work branches. Observed: 2026-10-05T08:55:00Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.


## Status 2026-10-05 ~08:55Z — OWNER PAUSE: W7 is live but NOT verified (1 of 3); production stabilisation is next; ship hotfix #6199 first (read this first)

The section below this one describes the earlier pause at ~02:04Z and is kept as dated history. This section is the current state.

**Pause.** OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Two unrelated PRs from other sessions did reach main after it (#6172 at 07:44Z, which is live, and #6059 at 08:37Z, which was not yet live at 08:46Z).

**Where W7 stands.** Merged, deployed and activated on production, but **NOT verified live — 1 of 3 behaviours**. The milestone is not complete. The active checkpoint is **production stabilisation**.

**Next action.** NEXT ACTION on resume: ship hotfix PR #6199 — apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production BEFORE the merge, then merge with `scripts/ci/box-ci/merge-if-green.sh 6199` once both box-ci checks are green on the current head.

**Production now.** Production code is main `e2093866c1` (the W7 squash `55a12f0da9` from PR #6196 plus the unrelated PR #6172); `https://supraos.ai/api/version` re-read anonymously at 08:46Z reports `e2093866c1`. Main has since moved to `a2e04e9a42` (unrelated PR #6059 from another session, merged 08:37Z, not yet live at 08:46Z). Production database: the 24 W7 packets were applied and verified 06:03–06:10Z (ledger 691 → 715); the ledger read 735 at 08:34Z because the separate Agent Run session installed 16 packets of its own. That session's three "after-live" packets (`20260929010002`, `20260929080000`, `20261001000000`) are NOT installed and must not be installed until PR #6168's build is live. The pre-install backup (5.4 GB, counts match) is on the web host, NOT restore-tested; keep it until live acceptance passes. One test project is stuck on production (project `43470d88`, plan `13fe1f43`, "W7 live test", status running; its final task cannot settle); it should self-heal within a minute of the hotfix going live, and the coordinator logs "terminal plan chain is not bound to settled plan" every minute until then. Mission Control admission was left OPEN on purpose.

**The scheduled-workflow incident.**

- The release carried a new once-only scheduler that holds all due work while a switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is unset. It was unset on production.
- All 534 scheduled workflows were paused from 06:24Z to 07:57Z.
- The owner chose to turn the switch on. Missed work is NOT re-run.
- Since then (to 08:34Z): once-only holds — 0 duplicates in 85 runs. But 55 of 85 runs failed; 27 of them are waiting for a new per-action permission grant introduced by the same release (owner decision 1).
- The scheduler is activated by owner choice, NOT qualified per its cutover checklist. Known stalls are fault 7 below. The verdict on file says leave the switch ON; a duplicate slot is the only reason to turn it off.
- **Root cause of the miss:** the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff.

**The eight faults.**

| # | Found | Fault | State |
| --- | --- | --- | --- |
| 1 | LIVE | The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). | FIXED in PR #6199 (not merged) |
| 2 | LIVE | Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. | FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3 |
| 3 | Audit | The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. | Fix = PR #6198 (owner decision 2) |
| 4 | Audit | Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). | NOT fixed, NO lane yet |
| 5 | Audit | An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. | WIP on `claude/w7-guarded-owner-controls-20261005` |
| 6 | Audit | Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. | WIP on `claude/w7-delete-and-tick-isolation-20261005` |
| 7 | Audit | Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. | WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested) |
| 8 | LIVE | Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. | WIP on `claude/planner-zero-task-plan-20261005` (unverified) |

**Live acceptance.** Live acceptance: 1 of 3 behaviours. C PASS (Re-execute on a pre-release plan refused, nothing created). B (lost-acknowledgment rerun) is blocked until PR #6199 is live. A (critical-failure drain) is not drivable from any control until PR #6198 plus an owner "mark failed" control exist.

**PRs and branches** (all pushed; heads and states re-read from the remote at 08:46Z).

| What | PR / branch @ head | State |
| --- | --- | --- |
| Hotfix: final task settles + Re-execute unblocked | PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` | OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. |
| Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin | PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` | OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. |
| Mission Control plans get a critical path | PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` | OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). |
| Owner controls (resolve / stop / review / outputs / settings) | `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR | WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. |
| Delete project + coordinator tick isolation | `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 | WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. |
| Scheduled workflows fixes | `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR | WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. |
| Production-shape end-to-end harness (S1–S9) | `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR | Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. |
| Planner 0-task plan + panel | `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR | WIP committed by the root at pause: unverified, tests not run, no browser check. |
| Evidence (private) | `docs/w7-resume-evidence-20261005` @ `b11636b366` | Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. |
| Other session | PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` | OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. |

**Migrations.** Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger.

**Five owner decisions waiting.**

1. Grants: every integration step in a scheduled workflow now needs a per-action grant that expires in 1–24 hours, so existing Gmail/Calendar/API workflows fail each run and file a card in Settings → Grants. Options: restore the pre-release un-gated behaviour for owner-authored scheduled workflows; make grants standing; or keep it and tell users.
2. PR #6198: Mission Control plans get a critical path — a third failure on the main chain fails the project and drains unstarted work instead of skipping the task.
3. Pre-release projects (39) cannot be re-executed: recommended "Adopt this project" signed receipt (new packet); stopgap "Duplicate as a new project" (no packet); plus plain-English refusal wording per status.
4. Owner controls: is "I'll handle it" on an unknown-outcome task = closed as skipped? Should an owner "Mark failed" be final (no automatic retry)?
5. Scheduled approval steps: turn on the three remaining switches, or keep human-approval steps unsupported in scheduled workflows for now?

**Seven-step execution plan.**

1. Verify state (read-only): `/api/version`; `scripts/ci/box-ci/status.sh` for #6197 #6198 #6199 #6168; whether main moved past `e2093866c1` (it has: `a2e04e9a42` at 08:46Z); the production ledger count and whether `20261005232000` is present (expect absent); the stuck plan's status; the scheduler watch queries from `scheduled-flag-on-verdict.md` (stalled occurrences, failure rate, duplicates — a duplicate slot is the ONLY reason to turn the switch off).
2. Ship the hotfix PR #6199: merge origin/main in if main moved; run scoped vitest, `node scripts/check-changed-types.mjs`, `node scripts/check-private-ai-recovery-writers.mjs`, and `scripts/checks/duplicate-migration-numbers.mjs` against the merge base; run the production-shape harness on the head (expect S1–S3 pass and Re-execute "created"); wait for both box-ci statuses = success on the CURRENT head. Then, in order: apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production with `scripts/apply-migration.mjs` (expect APPLIED AND VERIFIED; on an alarm or UNKNOWN stop and reconcile by reading, do not retry) → `scripts/ci/box-ci/merge-if-green.sh 6199` → watch the deploy log on the web host for `live: <sha> health 200` → confirm the stuck plan `13fe1f43` becomes completed and the coordinator error stops.
3. Live acceptance B (signed-in owner, real browser): on project `43470d88` ("W7 live test") click Re-execute → Start new run, reload the tab immediately, expect "A re-execution request needs confirmation…" and the button "Check re-execution"; click it. Pass = one row in `vms_mc_run_rerun_receipts` for that action, same run id, one new `vms_execution_runs` row, the new run completes. Screenshot.
4. Merge PR #6197, then refresh `supabase/schema/public-*.txt` again for packet `20261005232000`, removing any now-stale BASELINE entry in `tests/unit/queried-tables-exist.test.ts`.
5. Finish the paused lanes in parallel, each as its own PR with box-ci green, an independent review, real-database proof on the build box and, for UI, a real-browser check: (a) owner controls incl. packet `20261005233000` and fault 4 (task failure wedges a projects-route plan — it has no owner yet); (b) delete + tick isolation (rebase onto main after #6197 merges); (c) scheduled-workflow stalls, for-each, delete — reproduce on a real database first; (d) planner screen; (e) land the production-shape harness as a required pre-release check and add scenarios for every fault. Apply each packet to production before the code that needs it.
6. After the owner decisions: PR #6198, then live acceptance A (critical failure with an unstarted sibling → sibling drained, plan failed, never completed); the legacy Re-execute option; grants.
7. Clean up: remove the production backup and its tool folder; delete merged lane folders (only your own, `git worktree remove` without --force); then continue scope: remaining W7 effects/manual parity, active cancellation, real L1 anchoring, rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md` on #6197), coordinator sweep run-id check, the runtime role (5 unmapped owner schemas — owner decision), Stripe Link (owner external), normal QA invite. Full scope stays 33 tasks / 16 behaviours / 12 surfaces; iMessage deferred, WhatsApp excluded.

**Release rules learned today (EP11).** Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow.

**Evidence.** private `jtobkin/suprafx-platform` branch `docs/w7-resume-evidence-20261005` @ `b11636b366` (install log, acceptance screenshot, live-controls audit, end-to-end results, scheduler flag-on verdict).

| Stage | State now |
| --- | --- |
| Implemented | Yes, with eight known faults; two fixed in the unmerged hotfix |
| Integrated | Candidate yes; hotfix, follow-ups and fix branches no |
| Tested | Pre-release suites passed but were insufficient; production-shape harness now exists (not yet on main) |
| Independently reviewed | Candidate yes (missed the live faults and the scheduler switch); hotfix at current head no |
| Merged | Yes, main `55a12f0da9` (PR #6196); nothing from this project since |
| Deployed | Yes; production code is main `e2093866c1` |
| Activated | Yes; scheduler switch turned on 07:57Z by owner choice |
| Verified live | NO — 1 of 3 passed (C); B waits for #6199; A waits for #6198 plus a "mark failed" control |

### Resume prompt for the next session (sanitised)

This is the prompt to paste into a new session. It is sanitised for this public repository: the settings-store location, host file paths and full project/plan identifiers are removed or shortened. The unsanitised prompt is in the private memory repo as `PROMPT-2026-10-05-resume-w7-stabilization.md`.

Resume the SupraOS Agent Workflows project (W7 milestone: Mission Control critical-failure drain with safe rerun recovery) from the saved handoff. You are on a new computer with no session context. W7 was installed, merged and deployed on 2026-10-05, and live testing then found real faults. Your job is to STABILISE production first, then finish live acceptance, then continue scope. Ground yourself in code and evidence before changing anything. Treat this as authorization to resume implementation, testing, integration, production migrations from committed files, and supported merge/deployment when all required controls pass (owner standing instruction for this run: "automerge and automigrate as needed"). Do not bypass permissions, approvals, release gates or resource limits; if a tool call is denied, hand the exact command to the owner to run and continue with other work. Run independent lanes in parallel with exclusive files. Answer the owner in plain English, under 50 words, bullets, ending with a TLDR line.

#### 0. State at pause (verified 2026-10-05 ~08:35–08:55Z; re-verify everything)

Production (https://supraos.ai, private repo jtobkin/suprafx-platform):

- Code live = main `e2093866c1` (W7 squash `55a12f0da9` from PR #6196, plus #6172). Check `curl -s https://supraos.ai/api/version`.
- Database: the 24 W7 packets were applied and verified 06:03–06:10Z (ledger 691 → 715; list in `scripts/qa/w7-packets-20261005.txt`). Ledger was 735 at 08:34Z because the Agent Run session installed 16 of its own packets. Its 3 "after-live" packets (`20260929010002`, `20260929080000`, `20261001000000`) are NOT installed and must not be installed by anyone until PR #6168's build is live.
- Backup taken before the install: on the web host (5.4 GB, counts match, NOT restore-tested; made with the tool's `--min-free-gib 60` because the host had 60.4 GB free). Keep it until live acceptance passes, then remove it and its tool folder.
- Scheduler switch: `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER=1` was created in the production settings store and applied 07:57Z (the web host's environment-refresh and restart scripts, under the deploy lock). Reason: the release replaced the scheduler with a once-only "occurrence claim" path that holds every due workflow while the switch is unset; all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on and said missed runs need NOT be re-run. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. Do not read the environment-refresh script (the permission classifier refuses; running it is fine).
- Since the switch went on (to 08:34Z): 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), but 55 failed (65%; yesterday ~2%). 27 of the failures say "Workflow API permission is waiting for your review in Settings → Grants": the release made every API / Gmail / Calendar / send-email / file / bot step need an explicit per-action grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated. OWNER DECISION NEEDED (see section 4).
- Mission Control: one test project is stuck on production — project `43470d88`, plan `13fe1f43`, "W7 live test", status running, final task task-2 cannot settle. It should self-heal within a minute of the hotfix going live. mc-coordinator logs "terminal plan chain is not bound to settled plan" every minute until then. Mission Control admission was left OPEN on purpose.

Faults found live or by audit (W7 is NOT verified live):

| # | Found | Fault | State |
| --- | --- | --- | --- |
| 1 | LIVE | The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). | FIXED in PR #6199 (not merged) |
| 2 | LIVE | Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. | FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3 |
| 3 | Audit | The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. | Fix = PR #6198 (owner decision 2) |
| 4 | Audit | Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). | NOT fixed, NO lane yet |
| 5 | Audit | An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. | WIP on `claude/w7-guarded-owner-controls-20261005` |
| 6 | Audit | Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. | WIP on `claude/w7-delete-and-tick-isolation-20261005` |
| 7 | Audit | Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. | WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested) |
| 8 | LIVE | Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. | WIP on `claude/planner-zero-task-plan-20261005` (unverified) |

Live acceptance so far: C PASS (Re-execute on a pre-release plan refused, nothing created). B (lost-acknowledgment rerun) blocked until #6199 is live. A (critical-failure drain) not drivable from any control until #6198 plus an owner "mark failed" control exist.

Open PRs and branches (all pushed; nothing merged after #6196):

| What | PR / branch @ head | State |
| --- | --- | --- |
| Hotfix: final task settles + Re-execute unblocked | PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` | OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. |
| Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin | PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` | OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. |
| Mission Control plans get a critical path | PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` | OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). |
| Owner controls (resolve / stop / review / outputs / settings) | `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR | WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. |
| Delete project + coordinator tick isolation | `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 | WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. |
| Scheduled workflows fixes | `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR | WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. |
| Production-shape end-to-end harness (S1–S9) | `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR | Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. |
| Planner 0-task plan + panel | `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR | WIP committed by the root at pause: unverified, tests not run, no browser check. |
| Evidence (private) | `docs/w7-resume-evidence-20261005` @ `b11636b366` | Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. |
| Other session | PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` | OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. |

Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger.

#### 1. Read these, in order

1. Public plan (anonymous): https://github.com/jtobkin/supraos-workflow-plan — `Ship-Verified-SupraOS-Agent-Workflows.md` ("Status" first), `SupraOS-Workflow-Plan-Checklist.md`, `Delivery-Path-Release-Plan.md`, `Evidence-Index.md`, `workflow-plan.json`, `AGENTS.md`.
2. Private evidence: branch `docs/w7-resume-evidence-20261005`, folder `docs/agent-run/evidence/w7-resume-20261005/` — `live/verify/live-controls-audit.md` (28 direct plan writers, 17 now rejected), `live/verify/prod-shape-e2e/RESULTS.md`, `live/verify/scheduled-flag-on-verdict.md` (watch queries and the turn-off condition), `live/verify/trailing-ac48190955/RESULTS.md` (how the build-box harness is run), `live/install/prod-apply-ac48190955.log`, `live/acceptance/`.
3. PR bodies of #6199, #6197, #6198.
4. Product repo rules: `AGENTS.md` → `CONTEXT.md` (Critical Rules, Build & Deploy, Build Safety) → `docs/AI_BUILD_PROTOCOL.md` → `docs/runbooks/db-migrations.md` → `supabase/migrations/README.md`; for the scheduler: `docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`. Never run a full local next build. Merge ONLY with `scripts/ci/box-ci/merge-if-green.sh <pr>`; never `--auto` / `--admin`.
5. If the owner's private memory repo is available: `HANDOFF-2026-10-05-w7-failure-drain-claude-takeover.md` and `FINDING-2026-10-05-a-cutover-flag-missed-in-deploy-safety-paused-all-workflows.md`.

#### 2. Fresh-computer setup

```
git clone https://github.com/jtobkin/supraos-workflow-plan.git supraos-plan
python3 supraos-plan/scripts/render_plan.py --check
git clone --filter=blob:none https://github.com/jtobkin/suprafx-platform.git supraos-product
cd supraos-product
git fetch origin main docs/w7-resume-evidence-20261005 claude/w7-final-task-settle-fix-20261005 claude/w7-followups-20261005 claude/w7-mc-critical-path-20261005 claude/w7-guarded-owner-controls-20261005 claude/w7-delete-and-tick-isolation-20261005 claude/scheduled-occurrence-live-fixes-20261005 claude/w7-prod-shape-e2e-20261005 claude/planner-zero-task-plan-20261005
git worktree add ../w7-hotfix origin/claude/w7-final-task-settle-fix-20261005
cd ../w7-hotfix && npm ci
```

Node 22 is the supported version. Production database reads/writes need the owner database connection setting (`scripts/apply-migration.mjs` reads it from the environment or an approved local environment file; never paste it into documents or chat). The build box is reached only from a machine that holds its key; it has a version-17 database clone of the production schema with the packets and the native contract runner; use your own scratch database, one process at a time, and clean up (this run left file-only scratch folders on the build box). The web host is reached over the owner's saved connection. Old local checkout paths are provenance, not requirements. Do not reset or clean anyone else's checkout.

#### 3. Execution plan (shortest path to a healthy production)

1. Verify state (read-only): `/api/version`; `scripts/ci/box-ci/status.sh` for #6197 #6198 #6199 #6168; whether main moved past `e2093866c1` (it has: `a2e04e9a42` at 08:46Z); the production ledger count and whether `20261005232000` is present (expect absent); the stuck plan's status; the scheduler watch queries from `scheduled-flag-on-verdict.md` (stalled occurrences, failure rate, duplicates — a duplicate slot is the ONLY reason to turn the switch off).
2. Ship the hotfix PR #6199: merge origin/main in if main moved; run scoped vitest, `node scripts/check-changed-types.mjs`, `node scripts/check-private-ai-recovery-writers.mjs`, and `scripts/checks/duplicate-migration-numbers.mjs` against the merge base; run the production-shape harness on the head (expect S1–S3 pass and Re-execute "created"); wait for both box-ci statuses = success on the CURRENT head. Then, in order: apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production with `scripts/apply-migration.mjs` (expect APPLIED AND VERIFIED; on an alarm or UNKNOWN stop and reconcile by reading, do not retry) → `scripts/ci/box-ci/merge-if-green.sh 6199` → watch the deploy log on the web host for `live: <sha> health 200` → confirm the stuck plan `13fe1f43` becomes completed and the coordinator error stops.
3. Live acceptance B (signed-in owner, real browser): on project `43470d88` ("W7 live test") click Re-execute → Start new run, reload the tab immediately, expect "A re-execution request needs confirmation…" and the button "Check re-execution"; click it. Pass = one row in `vms_mc_run_rerun_receipts` for that action, same run id, one new `vms_execution_runs` row, the new run completes. Screenshot.
4. Merge PR #6197, then refresh `supabase/schema/public-*.txt` again for packet `20261005232000`, removing any now-stale BASELINE entry in `tests/unit/queried-tables-exist.test.ts`.
5. Finish the paused lanes in parallel, each as its own PR with box-ci green, an independent review, real-database proof on the build box and, for UI, a real-browser check: (a) owner controls incl. packet `20261005233000` and fault 4 (task failure wedges a projects-route plan — it has no owner yet); (b) delete + tick isolation (rebase onto main after #6197 merges); (c) scheduled-workflow stalls, for-each, delete — reproduce on a real database first; (d) planner screen; (e) land the production-shape harness as a required pre-release check and add scenarios for every fault. Apply each packet to production before the code that needs it.
6. After the owner decisions: PR #6198, then live acceptance A (critical failure with an unstarted sibling → sibling drained, plan failed, never completed); the legacy Re-execute option; grants.
7. Clean up: remove the production backup and its tool folder; delete merged lane folders (only your own, `git worktree remove` without --force); then continue scope: remaining W7 effects/manual parity, active cancellation, real L1 anchoring, rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md` on #6197), coordinator sweep run-id check, the runtime role (5 unmapped owner schemas — owner decision), Stripe Link (owner external), normal QA invite. Full scope stays 33 tasks / 16 behaviours / 12 surfaces; iMessage deferred, WhatsApp excluded.

Release rule learned today (apply to every merge): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow.

#### 4. Owner decisions waiting (ask once, keep working on everything else)

1. Grants: every integration step in a scheduled workflow now needs a per-action grant that expires in 1–24 hours, so existing Gmail/Calendar/API workflows fail each run and file a card in Settings → Grants. Options: restore the pre-release un-gated behaviour for owner-authored scheduled workflows; make grants standing; or keep it and tell users.
2. PR #6198: Mission Control plans get a critical path — a third failure on the main chain fails the project and drains unstarted work instead of skipping the task.
3. Pre-release projects (39) cannot be re-executed: recommended "Adopt this project" signed receipt (new packet); stopgap "Duplicate as a new project" (no packet); plus plain-English refusal wording per status.
4. Owner controls: is "I'll handle it" on an unknown-outcome task = closed as skipped? Should an owner "Mark failed" be final (no automatic retry)?
5. Scheduled approval steps: turn on the three remaining switches, or keep human-approval steps unsupported in scheduled workflows for now?

#### 5. Documentation duty (EP08)

After each milestone update `workflow-plan.json` in the plan repo (executionState, activeCheckpoint, productCandidate, candidateSummary, metrics, tasks[W7] stages/remaining, pauseHandoff — replace the single status section, do not add another), serialise with `json.dumps(d, indent=1, ensure_ascii=False) + "\n"`, run `python3 scripts/render_plan.py` then `--check`, gitleaks (history and `--no-git`), commit record + generated views together, push, verify remote bytes (raw sha256 equals local) and anonymous HTTP 200. Public repo: no secrets, wallet addresses, database URLs or host addresses. Report implemented / integrated / tested / reviewed / merged / deployed / activated / verified live separately; W7 is merged, deployed and activated but NOT verified live (1 of 3 behaviours). Write memory handoffs as files in the private memory repo with a one-line index pointer.

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

**EP11 — Require real-path independent acceptance.** Test permissions, failure, cancellation, worker death, recovery and uncertain outcomes through named callers. Any UI-dependent change requires independent real browser/Playwright checks. Never weaken tests, safety controls, grants or release gates. Owner tests are confirmation after independent live verification. Lesson from the W7 release (2026-10-05): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. Both passed in full while two defects reached production. Two release rules from the same day, applied to every merge: (1) grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production — a deploy-safety review that checked only the Mission Control files missed a switch whose unset state paused all 534 scheduled workflows for 93 minutes; (2) after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200". Acceptance must also include the last step of each flow.

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
| **W7 — Original-operation workflow effects** | Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. 2026-10-05 07:45–08:55Z, production stabilisation: hotfix PR #6199 opened (`claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a`) fixing faults 1 and 2 with packet `20261005232000_mc_rerun_unsent_anchor_hold` (build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head `420a71db33`, pending at the current head). A read-only audit of every guarded control (28 direct plan writers, 17 now rejected) and a production-shape end-to-end harness (S1–S9; all scenarios fail on main, S1–S3 and the Workspace drain pass on the fix) raised the fault count to eight. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. | PAUSED by the owner at 2026-10-05 ~08:55Z; W7 is merged, deployed and activated but NOT verified live (1 of 3 behaviours) and must not be shown as complete. NEXT ACTION on resume: ship hotfix PR #6199 — apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production BEFORE the merge, then merge with `scripts/ci/box-ci/merge-if-green.sh 6199` once both box-ci checks are green on the current head. SEVEN-STEP EXECUTION PLAN: Step 1 — Verify state (read-only): `/api/version`; `scripts/ci/box-ci/status.sh` for #6197 #6198 #6199 #6168; whether main moved past `e2093866c1` (it has: `a2e04e9a42` at 08:46Z); the production ledger count and whether `20261005232000` is present (expect absent); the stuck plan's status; the scheduler watch queries from `scheduled-flag-on-verdict.md` (stalled occurrences, failure rate, duplicates — a duplicate slot is the ONLY reason to turn the switch off). Step 2 — Ship the hotfix PR #6199: merge origin/main in if main moved; run scoped vitest, `node scripts/check-changed-types.mjs`, `node scripts/check-private-ai-recovery-writers.mjs`, and `scripts/checks/duplicate-migration-numbers.mjs` against the merge base; run the production-shape harness on the head (expect S1–S3 pass and Re-execute "created"); wait for both box-ci statuses = success on the CURRENT head. Then, in order: apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production with `scripts/apply-migration.mjs` (expect APPLIED AND VERIFIED; on an alarm or UNKNOWN stop and reconcile by reading, do not retry) → `scripts/ci/box-ci/merge-if-green.sh 6199` → watch the deploy log on the web host for `live: <sha> health 200` → confirm the stuck plan `13fe1f43` becomes completed and the coordinator error stops. Step 3 — Live acceptance B (signed-in owner, real browser): on project `43470d88` ("W7 live test") click Re-execute → Start new run, reload the tab immediately, expect "A re-execution request needs confirmation…" and the button "Check re-execution"; click it. Pass = one row in `vms_mc_run_rerun_receipts` for that action, same run id, one new `vms_execution_runs` row, the new run completes. Screenshot. Step 4 — Merge PR #6197, then refresh `supabase/schema/public-*.txt` again for packet `20261005232000`, removing any now-stale BASELINE entry in `tests/unit/queried-tables-exist.test.ts`. Step 5 — Finish the paused lanes in parallel, each as its own PR with box-ci green, an independent review, real-database proof on the build box and, for UI, a real-browser check: (a) owner controls incl. packet `20261005233000` and fault 4 (task failure wedges a projects-route plan — it has no owner yet); (b) delete + tick isolation (rebase onto main after #6197 merges); (c) scheduled-workflow stalls, for-each, delete — reproduce on a real database first; (d) planner screen; (e) land the production-shape harness as a required pre-release check and add scenarios for every fault. Apply each packet to production before the code that needs it. Step 6 — After the owner decisions: PR #6198, then live acceptance A (critical failure with an unstarted sibling → sibling drained, plan failed, never completed); the legacy Re-execute option; grants. Step 7 — Clean up: remove the production backup and its tool folder; delete merged lane folders (only your own, `git worktree remove` without --force); then continue scope: remaining W7 effects/manual parity, active cancellation, real L1 anchoring, rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md` on #6197), coordinator sweep run-id check, the runtime role (5 unmapped owner schemas — owner decision), Stripe Link (owner external), normal QA invite. Full scope stays 33 tasks / 16 behaviours / 12 surfaces; iMessage deferred, WhatsApp excluded. Open faults: EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). Live acceptance: 1 of 3 behaviours. C PASS (Re-execute on a pre-release plan refused, nothing created). B (lost-acknowledgment rerun) is blocked until PR #6199 is live. A (critical-failure drain) is not drivable from any control until PR #6198 plus an owner "mark failed" control exist. FIVE OWNER DECISIONS waiting: (1) Grants: every integration step in a scheduled workflow now needs a per-action grant that expires in 1–24 hours, so existing Gmail/Calendar/API workflows fail each run and file a card in Settings → Grants. Options: restore the pre-release un-gated behaviour for owner-authored scheduled workflows; make grants standing; or keep it and tell users. (2) PR #6198: Mission Control plans get a critical path — a third failure on the main chain fails the project and drains unstarted work instead of skipping the task. (3) Pre-release projects (39) cannot be re-executed: recommended "Adopt this project" signed receipt (new packet); stopgap "Duplicate as a new project" (no packet); plus plain-English refusal wording per status. (4) Owner controls: is "I'll handle it" on an unknown-outcome task = closed as skipped? Should an owner "Mark failed" be final (no automatic retry)? (5) Scheduled approval steps: turn on the three remaining switches, or keep human-approval steps unsupported in scheduled workflows for now? Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. Then: the F2 design decision, remaining effects/manual parity, legitimate department recipients, safe active cancellation, real L1 and the rerun-init pending/unknown recovery boundary. |
| **X2 — Confirm System Workflow durable terminal and pause receipts** | System Workflow pause and Memory Promotion partial fixes deployed | Qualify real admitted-owner pause/checkpoint/terminal recovery journeys. |
| **X3 — Refuse zero-row completion in scheduled and direct workflows** | Missing original terminal-row refusal has scoped native evidence | Verify scheduled and direct deployed paths retain truthful outcomes. |
| **X4 — Retain uncertain scheduled workflow attempts before another tick** | Scheduled original-attempt source preserved in held drafts. 2026-10-05: the once-only scheduled "occurrence claim" path reached production inside the release that deployed at 06:24Z, held behind the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`. The switch was unset, so all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on at 07:57Z and said missed runs need not be re-run. Observed to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), 55 failed, 27 of them waiting for a new per-action grant introduced by the same release. Fixes for the known stalls are work in progress on `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe` (untested, no PR; its packet `20261005235000` must not be applied) | Activated on production 2026-10-05 07:57Z by owner choice as an incident repair — NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`), so this task is not accepted. Known stalls, each of which stops that ONE workflow's schedule for good: a run killed by a restart; a crash between claim and start; Run-now; a human-approval step (needs the unset sibling switches); a cancelled interval slot. Also: for-each steps fail on a repeated target; workflow delete returns 500. Grants regression from the same release: every API / Gmail / Calendar / send-email / file / bot step now needs a per-action grant (27 of 55 failures in the first 85 runs) — owner decision. Next: reproduce each stall on a real database first, fix on the scheduled-fixes branch as its own PR with box-ci green and an independent review, then run the cutover checklist and the original acceptance (real-transport lost-acknowledgment and next-tick no-repeat proof). Keep the switch ON meanwhile (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Watch queries are in the private evidence file `scheduled-flag-on-verdict.md`. |
| **X5 — Qualify original scheduled approval continuation** | Bounded original approval continuation source qualified | Close remaining effectful graphs and real approval/uncertain-outcome acceptance. 2026-10-05 production state: the once-only scheduler is on, but the three approval-related switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset, so a scheduled workflow that reaches a human-approval step stops its schedule for good. Owner decision 5: turn the three switches on, or keep human-approval steps unsupported in scheduled workflows for now. Neither is qualified. |
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

**Saved work:** Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. 2026-10-05 07:45–08:55Z, production stabilisation: hotfix PR #6199 opened (`claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a`) fixing faults 1 and 2 with packet `20261005232000_mc_rerun_unsent_anchor_hold` (build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head `420a71db33`, pending at the current head). A read-only audit of every guarded control (28 direct plan writers, 17 now rejected) and a production-shape end-to-end harness (S1–S9; all scenarios fail on main, S1–S3 and the Workspace drain pass on the fix) raised the fault count to eight. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow.

**Remaining:** PAUSED by the owner at 2026-10-05 ~08:55Z; W7 is merged, deployed and activated but NOT verified live (1 of 3 behaviours) and must not be shown as complete. NEXT ACTION on resume: ship hotfix PR #6199 — apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production BEFORE the merge, then merge with `scripts/ci/box-ci/merge-if-green.sh 6199` once both box-ci checks are green on the current head. SEVEN-STEP EXECUTION PLAN: Step 1 — Verify state (read-only): `/api/version`; `scripts/ci/box-ci/status.sh` for #6197 #6198 #6199 #6168; whether main moved past `e2093866c1` (it has: `a2e04e9a42` at 08:46Z); the production ledger count and whether `20261005232000` is present (expect absent); the stuck plan's status; the scheduler watch queries from `scheduled-flag-on-verdict.md` (stalled occurrences, failure rate, duplicates — a duplicate slot is the ONLY reason to turn the switch off). Step 2 — Ship the hotfix PR #6199: merge origin/main in if main moved; run scoped vitest, `node scripts/check-changed-types.mjs`, `node scripts/check-private-ai-recovery-writers.mjs`, and `scripts/checks/duplicate-migration-numbers.mjs` against the merge base; run the production-shape harness on the head (expect S1–S3 pass and Re-execute "created"); wait for both box-ci statuses = success on the CURRENT head. Then, in order: apply packet `20261005232000_mc_rerun_unsent_anchor_hold` to production with `scripts/apply-migration.mjs` (expect APPLIED AND VERIFIED; on an alarm or UNKNOWN stop and reconcile by reading, do not retry) → `scripts/ci/box-ci/merge-if-green.sh 6199` → watch the deploy log on the web host for `live: <sha> health 200` → confirm the stuck plan `13fe1f43` becomes completed and the coordinator error stops. Step 3 — Live acceptance B (signed-in owner, real browser): on project `43470d88` ("W7 live test") click Re-execute → Start new run, reload the tab immediately, expect "A re-execution request needs confirmation…" and the button "Check re-execution"; click it. Pass = one row in `vms_mc_run_rerun_receipts` for that action, same run id, one new `vms_execution_runs` row, the new run completes. Screenshot. Step 4 — Merge PR #6197, then refresh `supabase/schema/public-*.txt` again for packet `20261005232000`, removing any now-stale BASELINE entry in `tests/unit/queried-tables-exist.test.ts`. Step 5 — Finish the paused lanes in parallel, each as its own PR with box-ci green, an independent review, real-database proof on the build box and, for UI, a real-browser check: (a) owner controls incl. packet `20261005233000` and fault 4 (task failure wedges a projects-route plan — it has no owner yet); (b) delete + tick isolation (rebase onto main after #6197 merges); (c) scheduled-workflow stalls, for-each, delete — reproduce on a real database first; (d) planner screen; (e) land the production-shape harness as a required pre-release check and add scenarios for every fault. Apply each packet to production before the code that needs it. Step 6 — After the owner decisions: PR #6198, then live acceptance A (critical failure with an unstarted sibling → sibling drained, plan failed, never completed); the legacy Re-execute option; grants. Step 7 — Clean up: remove the production backup and its tool folder; delete merged lane folders (only your own, `git worktree remove` without --force); then continue scope: remaining W7 effects/manual parity, active cancellation, real L1 anchoring, rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md` on #6197), coordinator sweep run-id check, the runtime role (5 unmapped owner schemas — owner decision), Stripe Link (owner external), normal QA invite. Full scope stays 33 tasks / 16 behaviours / 12 surfaces; iMessage deferred, WhatsApp excluded. Open faults: EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). Live acceptance: 1 of 3 behaviours. C PASS (Re-execute on a pre-release plan refused, nothing created). B (lost-acknowledgment rerun) is blocked until PR #6199 is live. A (critical-failure drain) is not drivable from any control until PR #6198 plus an owner "mark failed" control exist. FIVE OWNER DECISIONS waiting: (1) Grants: every integration step in a scheduled workflow now needs a per-action grant that expires in 1–24 hours, so existing Gmail/Calendar/API workflows fail each run and file a card in Settings → Grants. Options: restore the pre-release un-gated behaviour for owner-authored scheduled workflows; make grants standing; or keep it and tell users. (2) PR #6198: Mission Control plans get a critical path — a third failure on the main chain fails the project and drains unstarted work instead of skipping the task. (3) Pre-release projects (39) cannot be re-executed: recommended "Adopt this project" signed receipt (new packet); stopgap "Duplicate as a new project" (no packet); plus plain-English refusal wording per status. (4) Owner controls: is "I'll handle it" on an unknown-outcome task = closed as skipped? Should an owner "Mark failed" be final (no automatic retry)? (5) Scheduled approval steps: turn on the three remaining switches, or keep human-approval steps unsupported in scheduled workflows for now? Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. Then: the F2 design decision, remaining effects/manual parity, legitimate department recipients, safe active cancellation, real L1 and the rerun-init pending/unknown recovery boundary.

**Acceptance:** Thread server ToolContext identity, reserve before effect, preserve original run and unknown outcome, reject missing/forged identity, prove cap/no replay via actual transport. Bind actual task settlement to the original saved execution claim atomically; reject superseded results before effects and recover post-commit delivery without duplication. Prove usable original-child lookup/recovery and keep unsupported callers explicit.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.; new branches/commits in pause checkpoint.

**Prior owner role:** release_integration: isolated claim/settlement production repair; release_verification: independent tests; root: composition/release. Root must assign a currently available named owner before dispatch. **Original dependencies:** W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the drain/rerun milestone in candidate ac48190955, with eight known faults. Fixes for faults 1 and 2 are implemented in hotfix PR #6199 @ dfebdab30a (not merged). Fault 3 fix = PR #6198 (owner decision). Faults 5, 6, 7, 8 are work in progress on unmerged branches; fault 4 has no lane. Remaining W7 effects still open. |
| integrated | Yes for the candidate: PR #6196 is squash-merged into main as 55a12f0da9. The hotfix, the follow-ups (PR #6197), the critical path (PR #6198), the harness and four fix branches are NOT integrated. Agent Run PR #6168 conflicts with W7 files; whoever resumes it re-merges main. |
| tested | Pre-release suites passed but were INSUFFICIENT (26 native contract cases on fixtures, 46 browser cases with the server boundary mocked; none drove the real server path with production-shaped data). Since release: a production-shape end-to-end harness (S1–S9, branch claude/w7-prod-shape-e2e-20261005 @ f146740999) fails every scenario on main and passes S1–S3 plus the Workspace drain on the hotfix. Hotfix on the build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head 420a71db33, PENDING at the current head dfebdab30a; scoped vitest at this head not run. Owner-controls packet 20261005233000: 8/8 native, TypeScript not type-checked, no unit tests. Delete/tick: 19 tests pass, browser check PASS. Scheduled fixes and planner fixes: untested. |
| independentlyReviewed | Yes at ac48190955 (trailing audit PASS 5/5) — but that review missed the live faults, and the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff, so it missed the scheduler switch. PR #6197 is independently reviewed. The hotfix PR #6199 at its current head and the four fix branches are not independently reviewed. |
| merged | Yes for the candidate: 2026-10-05 06:11:22Z via scripts/ci/box-ci/merge-if-green.sh (squash) → main 55a12f0da9b09052d0bfa186f747654a60f3a931. Nothing from this project merged after #6196: PRs #6199, #6197 and #6198 are OPEN (verified 08:46Z). |
| deployed | Yes for the candidate: production schema installed 06:03–06:10Z (24/24 packets APPLIED AND VERIFIED; ledger 691 → 715); code deployed 06:24:35Z. Production code is now main e2093866c1 (/api/version re-read 08:46Z). Packet 20261005232000 is NOT applied and the hotfix is NOT deployed. Pre-install backup sealed with matching row counts but NOT restore-tested. |
| activated | Yes: Mission Control drain/rerun is live by construction (no feature flag); admission left OPEN on purpose. The same release's once-only scheduler was held behind an unset switch, which paused all 534 scheduled workflows 06:24–07:57Z; the owner turned the switch on at 07:57Z (missed runs not re-run). Three sibling scheduler switches remain unset. |
| verifiedLive | NO — not complete. 1 of 3 behaviours. C PASS (~06:35Z; signed-in owner, real Chrome, production): re-execute on a pre-release plan refused, nothing created. B BLOCKED until hotfix PR #6199 is live. A NOT DRIVABLE until PR #6198 plus an owner "mark failed" control exist. Eight faults are open on production (see Remaining); one test project (plan 13fe1f43) is stuck running. Owner pause at ~08:55Z. |

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

**Saved work:** Scheduled original-attempt source preserved in held drafts. 2026-10-05: the once-only scheduled "occurrence claim" path reached production inside the release that deployed at 06:24Z, held behind the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`. The switch was unset, so all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on at 07:57Z and said missed runs need not be re-run. Observed to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), 55 failed, 27 of them waiting for a new per-action grant introduced by the same release. Fixes for the known stalls are work in progress on `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe` (untested, no PR; its packet `20261005235000` must not be applied)

**Remaining:** Activated on production 2026-10-05 07:57Z by owner choice as an incident repair — NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`), so this task is not accepted. Known stalls, each of which stops that ONE workflow's schedule for good: a run killed by a restart; a crash between claim and start; Run-now; a human-approval step (needs the unset sibling switches); a cancelled interval slot. Also: for-each steps fail on a repeated target; workflow delete returns 500. Grants regression from the same release: every API / Gmail / Calendar / send-email / file / bot step now needs a per-action grant (27 of 55 failures in the first 85 runs) — owner decision. Next: reproduce each stall on a real database first, fix on the scheduled-fixes branch as its own PR with box-ci green and an independent review, then run the cutover checklist and the original acceptance (real-transport lost-acknowledgment and next-tick no-repeat proof). Keep the switch ON meanwhile (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Watch queries are in the private evidence file `scheduled-flag-on-verdict.md`.

**Acceptance:** Carry exact original identity and unknown status; atomically hold/recover original schedule attempt; real transport lost-ack and next-tick no-repeat proof, installed schema and deployed checks.

**Source:** app/api/cron/workflow-triggers/route.ts:189; lib/vms/workflows/execution-engine.ts; docs/agent-run/scheduled-workflow-recovery-plan-20261001.md

**Prior owner role:** Sol SQL + Sol engine; Root native integration. Root must assign a currently available named owner before dispatch. **Original dependencies:** X3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Once-only occurrence claim path is in production code (main e2093866c1). Known stalls and for-each/delete faults are open; fixes are work in progress, untested, on claude/scheduled-occurrence-live-fixes-20261005 @ d3eb84cefe. |
| integrated | The scheduler path is integrated on main. The fixes branch is not integrated (no PR). |
| tested | Not qualified: the cutover checklist was not run before activation. Fixes are untested; nothing reproduced on a real database yet. |
| independentlyReviewed | A flag-on verdict is on file in the private evidence (leave the switch ON). The deploy-safety review missed the switch: it checked only the Mission Control files, not the whole diff. No independent review of the fixes. |
| merged | The scheduler path reached main before/with the release deployed 2026-10-05; the fixes are not merged. |
| deployed | Yes for the scheduler path (deployed 06:24Z with the switch unset, which paused all 534 scheduled workflows until 07:57Z). Fixes not deployed. |
| activated | Yes, 2026-10-05 07:57Z by owner choice (switch set in the production settings store; missed runs not re-run). An incident repair, NOT a qualified cutover. |
| verifiedLive | NO. Observation only, to 08:34Z: 0 duplicates in 85 runs (once-only holds), but 55 of 85 runs failed (27 waiting for a per-action grant) and five known stall paths are open. Acceptance proofs not run. |

### X5 — Qualify original scheduled approval continuation

**Saved work:** Bounded original approval continuation source qualified

**Remaining:** Close remaining effectful graphs and real approval/uncertain-outcome acceptance. 2026-10-05 production state: the once-only scheduler is on, but the three approval-related switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset, so a scheduled workflow that reaches a human-approval step stops its schedule for good. Owner decision 5: turn the three switches on, or keep human-approval steps unsupported in scheduled workflows for now. Neither is qualified.

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
| activated | NOT activated: the three approval switches are unset on production (2026-10-05). With the once-only scheduler on, human-approval steps in scheduled workflows stall that schedule. Owner decision pending. |
| verifiedLive | NO. Full scope pending; a known live stall exists for scheduled human-approval steps. |

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
