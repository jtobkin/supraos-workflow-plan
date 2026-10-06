# SupraOS Release Plan Checklist

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-06T02:05:00Z**. Canonical record SHA-256: `a0d89af75a519f7880bee2cff25ec61e85668f8d151a03814ad83f39616c581c`.

**Execution state:** HANDED OFF — production stabilisation COMPLETE (2026-10-06 01:55Z); nothing from this project is running. W7 (candidate `ac48190955`, PR #6196) and all 14 stabilisation PRs are MERGED, DEPLOYED and ACTIVATED; production code is main `0d25a537b4`. W7 is NOT verified live: 2 of 3 behaviours (B lost-acknowledgment rerun PASS 17:36Z 2026-10-05; C legacy refusal PASS 06:35Z 2026-10-05); A, the critical-failure drain, has NOT been run. The milestone is NOT complete. Production ledger 743 (24 W7 packets + five extra packets from this run); the once-only scheduler switch is ON. Two production incidents were found and fixed during the run (scheduled workflows paused 06:24–07:57Z; Telegram "Liq Warning" alerts failing 13:15Z to ~22:08Z). NEXT ACTION on resume: live acceptance A (drain), then open the end-to-end harness PR. PR states and merge commits re-read from GitHub at 2026-10-06 ~02:00Z; `https://supraos.ai/api/version` re-read anonymously at 2026-10-06 01:59:48Z reports `0d25a537b4` (= main). Ledger, switch and health figures are as reported in the private handoff at 01:55Z and were NOT re-read for this record..

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** **LIVE ACCEPTANCE A (critical-failure drain) — W7 is 2 of 3 verified live; not complete.** Production stabilisation is complete: W7 (candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f`, PR [#6196](https://github.com/jtobkin/suprafx-platform/pull/6196)) plus 14 fix PRs are merged, deployed and activated; live = main `0d25a537b4`. Live acceptance on production, signed-in owner: **C PASS** (2026-10-05 06:35Z — Re-execute on a pre-release plan refused, nothing created; after #6207 it now offers Duplicate / Adopt). **B PASS** (2026-10-05 17:36Z — project `43470d88` "W7 live test": Re-execute → reload (lost reply) → "Check re-execution" → original run recovered, exactly 1 rerun receipt, no duplicate). **A NOT RUN** (critical-failure drain): needs a project created after #6198 whose critical task fails 3 times with an unstarted sibling; there is no deterministic way from the screen because per-task Stop is now final (no retry). Options: wait for a natural triple failure, or add a test-only owner action. Proof rows expected: a `critical_failure_drain` effect delivered; the sibling `skipped` with drain reason `critical_failure_unstarted`; the plan `failed`, never `completed`. **Then:** Open the PR for the production-shape end-to-end harness, branch `claude/w7-prod-shape-e2e-20261005` @ `080907ff6b` (scenarios S1–S9, `scripts/qa/w7-prod-shape-e2e/`, `run.sh`, runs on the build box; no PR yet, verified 02:00Z): merge main first, add a scenario for every fault found on 2026-10-05, and propose (do not enable) it as a required pre-release check. PR states and merge commits re-read from GitHub at 2026-10-06 ~02:00Z; `https://supraos.ai/api/version` re-read anonymously at 2026-10-06 01:59:48Z reports `0d25a537b4` (= main). Ledger, switch and health figures are as reported in the private handoff at 01:55Z and were NOT re-read for this record.

**Current candidate record:** `ac4819095585eed003eb0c510b0a8c8608d5e73f`, tree `49bf08e3354a115783635eebfa4801dfa953bb6c`. Security: box-ci/security-gates SUCCESS on ac48190955 (51 steps; macOS Native Land not run). Previous head 3214f4849e: FAILURE (whole unit tree 2 failed / 55,609 passed / 374 skipped across 4,508 files; scoped changed-file TypeScript check 5 errors); build: box-ci/production-build SUCCESS on ac48190955 (7 steps). Previous head 3214f4849e: ERROR (not built because security gates failed); macOS Native Land: Not run (not part of box-ci). Merged: True; deployed: True; activated: True; verified live: False. Scope: Composed W7 failure-drain/rerun candidate (partial W7; full scope open). Frozen candidate ac48190955 = 3214f4849e + fix commit 867a5f2114 + clean merge of origin/main 7a10b7a3fc; required CI GREEN and independent trailing audit PASS 5/5 at that commit. Squash-merged 2026-10-05 06:11:22Z as main 55a12f0da9 (PR #6196); installed 06:03–06:10Z; deployed 06:24:35Z; activated. Stabilisation (same day, 12:59–22:23Z): 14 PRs merged via merge-if-green.sh with an independent review each; five extra packets installed (ledger 743); live = main 0d25a537b4. `verified live: False` means NOT verified live and the milestone NOT complete: 2 of 3 behaviours (B PASS 17:36Z, C PASS 06:35Z; A, the critical-failure drain, not run). The once-only scheduler switch is ON (since 07:57Z 2026-10-05); its three approval siblings are unset (owner decision).. Observed: 2026-10-06T02:05:00Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.


## Status 2026-10-06 ~01:55Z — stabilisation COMPLETE; W7 live but NOT verified (2 of 3); next = live test A (read this first)

The sections below this one describe the earlier pauses (~08:55Z and ~02:04Z on 2026-10-05) and are kept as dated history. This section is the current state. PR states and merge commits re-read from GitHub at 2026-10-06 ~02:00Z; `https://supraos.ai/api/version` re-read anonymously at 2026-10-06 01:59:48Z reports `0d25a537b4` (= main). Ledger, switch and health figures are as reported in the private handoff at 01:55Z and were NOT re-read for this record.

**Where W7 stands.** Implemented, integrated, tested, independently reviewed, merged, deployed and activated — **yes**. **Verified live — NO: 2 of 3.** The milestone is **not complete**.

| Stage | State now |
| --- | --- |
| Implemented | Yes — the drain/rerun milestone plus fixes for all eight faults found on 2026-10-05 |
| Integrated | Yes — 15 PRs on main; end-to-end harness branch not yet (no PR) |
| Tested | Yes per PR — required box-ci checks green at each merge; five extra packets applied and verified on production |
| Independently reviewed | Yes — an independent review for each PR before merge |
| Merged | Yes — last merge #6221, main `0d25a537b4`, 22:23Z 2026-10-05 |
| Deployed | Yes — `/api/version` reports `0d25a537b4` |
| Activated | Yes — no feature flag; critical path on for new projects; once-only scheduler switch ON |
| Verified live | **NO — 2 of 3.** B PASS 17:36Z, C PASS 06:35Z (2026-10-05); A not run |

**Live acceptance.** Live acceptance on production, signed-in owner: **C PASS** (2026-10-05 06:35Z — Re-execute on a pre-release plan refused, nothing created; after #6207 it now offers Duplicate / Adopt). **B PASS** (2026-10-05 17:36Z — project `43470d88` "W7 live test": Re-execute → reload (lost reply) → "Check re-execution" → original run recovered, exactly 1 rerun receipt, no duplicate). **A NOT RUN** (critical-failure drain): needs a project created after #6198 whose critical task fails 3 times with an unstarted sibling; there is no deterministic way from the screen because per-task Stop is now final (no retry). Options: wait for a natural triple failure, or add a test-only owner action. Proof rows expected: a `critical_failure_drain` effect delivered; the sibling `skipped` with drain reason `critical_failure_unstarted`; the plan `failed`, never `completed`.

**Every PR merged in this run** (each independently reviewed, merged with `scripts/ci/box-ci/merge-if-green.sh`; states and commits re-read from GitHub 2026-10-06 ~02:00Z):

| PR | What it does | Merged (2026-10-05, UTC) | main commit |
| --- | --- | --- | --- |
| #6196 | W7 release: squash of the composed failure-drain/rerun candidate `ac48190955` | 06:11Z | `55a12f0da9` |
| #6199 | the final task of a plan settles again (finish intents now carry the task id) + packet `20261005232000` | 12:59Z | `c1513db29c` |
| #6197 | schema snapshot refresh; coordinator sweep skips drain-refused plans; manifest re-pin | 13:15Z | `7b28f6a41a` |
| #6198 | Mission Control plans get a critical path, so the drain can fire (owner said yes) | 13:15Z | `ec1e1132fe` |
| #6206 | workflow grants can last 1 hour / 24 hours / 1 week / 1 month / 1 year; one card per workflow + action | 17:43Z | `2e242177b3` |
| #6205 | safe Delete project (refuse or archive instead of orphaning a running plan); one bad plan no longer aborts the coordinator tick | 17:46Z | `aeebec0da0` |
| #6211 | planner: no 0-task launch; review panel follows the selected plan; long chat scrolls | 18:42Z | `38ef1efa84` |
| #6219 | grants: a `workflow:<id>` agent no longer crashes the default-permission lookup (regression from Agent Run #6168) | 19:07Z | `3f18ef481c` |
| #6213 | test and source record for packet `20261005239000` (the packet was already live) | 19:08Z | `0622e4ea36` |
| #6212 | scheduled workflows: stalls after restart / lost reply / Run-now / cancel fixed; for-each and delete fixed; pause banner + Release; packet `20261005235000` | 19:56Z | `2df2d3b0cc` |
| #6220 | an alert for an owner without Telegram is skipped and the run completes; coded errors with logged causes | 20:35Z | `9ab57850bd` |
| #6222 | a failed task retries with a different agent (the preferred agent no longer overrides the failed-agents list) | 21:06Z | `c7e4e9b150` |
| #6207 | older projects: Duplicate and Adopt (packet `20261006000700`) + plain-English refusal wording | 21:18Z | `9dcef69a69` |
| #6223 | alerts for owners not yet admitted (invite-required) no longer fail | 21:55Z | `e0d776651c` |
| #6221 | owner controls: resolve an unknown outcome, per-task Stop is final, review / outputs / settings work or say why (packet `20261006010000`) | 22:23Z | `0d25a537b4` |

**Production database.** Ledger **743**: the 24 W7 packets (06:03–06:10Z 2026-10-05) plus five extra packets from this run, all "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. The Agent Run session installed 19 of its own. One packet from another session (`20261002050000_signals_pattern_ids_like`) is not installed by anyone (fails safe).

| Packet | Installed (UTC) |
| --- | --- |
| `20261005232000_mc_rerun_unsent_anchor_hold` | 2026-10-05 09:00Z |
| `20261005239000_mc_rerun_unadmitted_effect_hold` | 2026-10-05 14:41Z |
| `20261005235000_scheduled_occurrence_recovery` | 2026-10-05 19:55Z |
| `20261006000700_mc_legacy_plan_adoption` | 2026-10-05 21:17Z |
| `20261006010000_mc_unknown_task_owner_resolution` | 2026-10-05 22:22Z |

**Scheduler.** The once-only scheduler switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is ON in the production settings store, applied on the web host under its deploy lock. Its three approval siblings are still unset, so human-approval steps in scheduled workflows stay unsupported (owner decision).

**Health.** Health in the hour before 01:55Z on 2026-10-06 (reported, not re-read here): 167 scheduled runs completed, 34 failed; 0 duplicate slots; 0 stalled occurrences; 0 Mission Control plans running. The remaining failures are owners' own model keys (30 × "No usable API key for anthropic", 2 × credit balance), not platform faults.

**Two production incidents found and fixed during the run.**

(1) **Scheduled workflows paused 06:24–07:57Z on 2026-10-05.** The W7 release carried a once-only scheduler that holds all due work while its switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is unset; it was unset in production, so all 534 scheduled workflows stopped for 93 minutes. The deploy-safety review missed it because it checked only the Mission Control files for new switches, not the whole diff. Fixed by the owner turning the switch on at 07:57Z (missed runs not re-run); remaining scheduler stalls fixed by #6212.

(2) **Telegram "Liq Warning" alerts failing from 13:15Z to ~22:08Z on 2026-10-05.** A regression from the Agent Run release (#6168): first the permission lookup crashed on workflow-style agent ids, then alerts for owners not yet admitted failed when their settings were read. A catch-all error code hid both causes. Fixed by #6219, #6220 and #6223; 0 alert failures in the 15 minutes after the last fix.

**What is left (priority order).**

1. **Live acceptance A** — the critical-failure drain (above).
2. **End-to-end harness PR.** Open the PR for the production-shape end-to-end harness, branch `claude/w7-prod-shape-e2e-20261005` @ `080907ff6b` (scenarios S1–S9, `scripts/qa/w7-prod-shape-e2e/`, `run.sh`, runs on the build box; no PR yet, verified 02:00Z): merge main first, add a scenario for every fault found on 2026-10-05, and propose (do not enable) it as a required pre-release check.
3. **Follow-ups found in review** (not blockers):
- A task that EVERY agent has failed stays `ready` forever (owners with a single agent) — needs skip or escalate.
- An archived project with an approved or paused plan can still be executed by direct link (the execute route ignores the archive flag).
- "Active projects" count includes archived projects.
- A held task re-queues forever with no owner alert (coordinator).
- Grants picker resets to 1 hour after reloading a half-saved approval; the approved card stays and the count does not change.
- Creating a project accepts empty workflow steps (no server-side 0-task guard).
- Voice-capture planning can return a 0-task plan.
- Planner chat box is squashed at 390 px wide once a plan appears.
- Re-execute after an unknown outcome is still refused (the plan finishes or stops but cannot be re-run).
- Two concurrent runs can create two grant cards.
- A Telegram kill-switch-locked owner with no chat id is now skipped (confirm intended).
4. **Owner decisions still open:**
1. The three sibling scheduler switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are still unset, so human-approval steps in scheduled workflows stay unsupported. Turn them on, or keep approval steps unsupported?
2. Should "Telegram not set up" ever fail a run? (Now: the alert is skipped and the run completes.)
3. The `supra_owner_runtime` role (5 owner schemas are not mapped).
5. **Remaining W7 scope: remaining effects and manual parity; safe active cancellation; real L1 anchoring (anchors always end `held_unknown`; the capability is unverified); F2 rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md`); the runtime role; Stripe Link (owner, external); QA invite. Full project: 33 tasks, 16 behaviour families, 12 surfaces; iMessage deferred, WhatsApp excluded.**
6. **Cleanup: remove the pre-install production backup (5.4 GB, counts matched, never restore-tested) and its tool folder from the web host; delete merged lane folders (owner rule: `git worktree remove`, no --force, clean and idle, own lanes only; keep the end-to-end harness lane until its PR merges); remove leftover file-only scratch folders from this run on the build box.**

Owner decisions answered during the run: critical path for Mission Control plans — yes (#6198); grants — longer durations up to 1 year (#6206); pre-release projects — Duplicate and Adopt (#6207); owner controls — resolve an unknown outcome, per-task Stop is final (#6221).

**Where the code and evidence are.** Product repo: private `jtobkin/suprafx-platform`, branch `main` — everything above is in it. Key code: `lib/vms/workflows/` (plan-orchestrator.ts, mc-*-effect.ts, mc-plan-finish-intents.ts, mc-rerun-request.ts, mc-owner-manual-action.ts, execution-engine.ts, workflow-telegram-notice.ts, scheduled-*.ts); `app/api/projects/**` (create, execute, rerun, duplicate, adopt, resolve, tasks/[taskId]/stop); `app/api/cron/mc-coordinator/route.ts`; `app/api/cron/workflow-triggers/route.ts`; `app/vms/mission-control/**`; `components/vms/workflow/ScheduleHoldBanner.tsx`; `lib/vms/agent-grants.ts`; `lib/db-as-owner.ts`; `supabase/migrations/2026100*`. Docs in the product repo: `docs/agent-run/RELEASE-W7-*.md`, `docs/agent-run/mc-rerun-request-recovery.md`, `docs/agent-run/mc-rerun-init-recovery-design.md` (F2), `docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`. Evidence (private): branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d` (pushed 2026-10-06 01:59Z: production install logs for the five extra packets, live test B PASS, rerun-effects proof, delete / grants / planner / legacy-rerun screenshots; earlier commit `b11636b366` has the W7 install log, live-controls audit, end-to-end results and scheduler flag-on verdict), folder `docs/agent-run/evidence/w7-resume-20261005/`. End-to-end harness: branch `claude/w7-prod-shape-e2e-20261005` @ `080907ff6b` (no PR). Public plan: this repository (`workflow-plan.json` → `python3 scripts/render_plan.py`).

**Release rules learned (EP11).** Grep the WHOLE diff for new environment reads and know each one's unset behaviour in production; compare background-job rates before and after each deploy; drive the real server path on a real database with production-shaped data, including the last step of each flow; a catch-all error code must log the underlying cause; packets editing the same function must be versioned above the newest packet that pins that function.

### Resume prompt for the next session (sanitised)

This is the prompt to paste into a new session. It is sanitised for this public repository: database connection strings, host addresses, settings-store paths and full identifiers are removed or shortened. The unsanitised prompt is `PROMPT-2026-10-06-resume-w7-after-stabilization.md` in the owner's private memory repo.

Resume the SupraOS Agent Workflows project (W7: Mission Control critical-failure drain with safe rerun recovery) on this computer. W7 is merged, installed and live, and the stabilisation fixes are all merged. Ground yourself in evidence before changing anything. Treat this as authorization for implementation, testing, production migrations from committed files, and merge/deploy through the supported path when all checks pass ("automerge and automigrate as needed"). Do not bypass permissions, approvals, release gates or resource limits; if a tool call is denied, give the owner the exact command to run and continue with other work. Use several parallel agents with exclusive files, and an independent reviewer for every PR before merge. Answer in plain English, under 50 words, bullets, ending with a TLDR line.

1. Read first: the owner's private memory repo → its index → the W7 stabilisation handoff of 2026-10-06 (state, every PR, where all code and evidence lives, what is left, traps). If memory is unreachable: this public plan (`Ship-Verified-SupraOS-Agent-Workflows.md`, this status section). Product repo: private `jtobkin/suprafx-platform` — `AGENTS.md` → `CONTEXT.md` → `docs/AI_BUILD_PROTOCOL.md` → `docs/runbooks/db-migrations.md`. Merge ONLY with `scripts/ci/box-ci/merge-if-green.sh <pr>`; never a full local production build.
2. Re-verify (read-only): `curl -s https://supraos.ai/api/version` (expect main ≥ `0d25a537b4`); `git log --oneline -5 origin/main`; production ledger count (743 at handoff) and the five extra packets (`20261005232000`, `20261005239000`, `20261005235000`, `20261006000700`, `20261006010000`) present; scheduled-workflow health — failures in the last hour by error, 0 duplicate slots (`select workflow_id, slot_key, count(*) from vms_scheduled_workflow_occurrences group by 1,2 having count(*)>1`), stalled occurrences older than 45 minutes; open PRs from branches `claude/w7-*`. Production database access needs the owner database connection setting from the approved local environment file (TLS required); never paste it anywhere.
3. Work, in parallel lanes:
   a. Update this public plan repo (record `workflow-plan.json`, serialise with `json.dumps(d, indent=1, ensure_ascii=False)+"\n"`, `python3 scripts/render_plan.py` then `--check`, secret scan, push, verify raw sha256 + anonymous 200) after each milestone. Sanitise (no addresses, database URLs, host addresses or settings-store paths).
   b. (Done 2026-10-06 01:59Z: the local-only evidence was committed to the private evidence branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d`.)
   c. Live acceptance A (drain) on production — design the least-risk way to make a critical task fail 3 times with an unstarted sibling on a project created after #6198, run it, prove the rows (drain effect delivered; sibling skipped with reason `critical_failure_unstarted`; plan failed, never completed), screenshot or text evidence.
   d. Open the PR for the end-to-end harness branch `claude/w7-prod-shape-e2e-20261005` (merge main first), add scenarios for every fault found on 2026-10-05, propose (do not enable) a box-ci step.
   e. Follow-ups, highest user impact first: a task every agent failed stays ready forever; an archived project is still executable by direct link; a held task re-queues forever with no alert; server-side 0-task guard.
4. Ask the owner once, then keep working: the three sibling scheduler switches (approval steps in scheduled workflows); the `supra_owner_runtime` role.
5. After each milestone: update the memory handoff (one-line index pointer) and this public plan. Delete merged lane folders you own (`git worktree remove`, no --force).

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

**EP11 — Require real-path independent acceptance.** Test permissions, failure, cancellation, worker death, recovery and uncertain outcomes through named callers. Any UI-dependent change requires independent real browser/Playwright checks. Never weaken tests, safety controls, grants or release gates. Owner tests are confirmation after independent live verification. Lesson from the W7 release (2026-10-05): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. Both passed in full while two defects reached production. Two release rules from the same day, applied to every merge: (1) grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production — a deploy-safety review that checked only the Mission Control files missed a switch whose unset state paused all 534 scheduled workflows for 93 minutes; (2) after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200". Acceptance must also include the last step of each flow. Two more rules from the 2026-10-05 stabilisation: (3) a catch-all error code must log the underlying cause — one code (`notice_unavailable`) hid two different root causes behind a ~9-hour Telegram alert outage; add the logging first, then fix; (4) packets that edit the same database function must be versioned above the newest packet that pins that function's body — a later pinning packet makes the VERIFY of earlier ones fail once the body changes, so renumber new packets above it and install in version order.

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
| **W6 — Atomic usage limits for scoped capability grants** | Atomic grant reservations source in held draft6129 Related grant changes shipped 2026-10-05 (not W6 acceptance): PR #6206 (main `2e242177b3`) lets workflow grants last 1 hour / 24 hours / 1 week / 1 month / 1 year and keeps one card per workflow + action; PR #6219 (main `3f18ef481c`) stops the default-permission lookup crashing on `workflow:<id>` agents (a regression from Agent Run #6168). The owner approved their own two pending workflow grants for 1 year (18:13Z, expire 2027-10-05); other owners' cards are theirs to approve. | Prove installed concurrent use, revocation and original receipt recovery. Known grant follow-ups from the 2026-10-05 review: two concurrent runs can create two grant cards; the grants picker resets to 1 hour after reloading a half-saved approval (the approved card stays and the count does not change). |
| **W7 — Original-operation workflow effects** | Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. 2026-10-05 07:45–08:55Z, production stabilisation: hotfix PR #6199 opened (`claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a`) fixing faults 1 and 2 with packet `20261005232000_mc_rerun_unsent_anchor_hold` (build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head `420a71db33`, pending at the current head). A read-only audit of every guarded control (28 direct plan writers, 17 now rejected) and a production-shape end-to-end harness (S1–S9; all scenarios fail on main, S1–S3 and the Workspace drain pass on the fix) raised the fault count to eight. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. 2026-10-05 09:00Z → 22:23Z PRODUCTION STABILISATION (handed off 2026-10-06 01:55Z): all eight faults fixed and live through 14 PRs, each independently reviewed and merged with merge-if-green.sh: #6196 `55a12f0da9` (W7 release: squash of the composed failure-drain/rerun candidate `ac48190955`); #6199 `c1513db29c` (the final task of a plan settles again (finish intents now carry the task id) + packet `20261005232000`); #6197 `7b28f6a41a` (schema snapshot refresh; coordinator sweep skips drain-refused plans; manifest re-pin); #6198 `ec1e1132fe` (Mission Control plans get a critical path, so the drain can fire (owner said yes)); #6206 `2e242177b3` (workflow grants can last 1 hour / 24 hours / 1 week / 1 month / 1 year; one card per workflow + action); #6205 `aeebec0da0` (safe Delete project (refuse or archive instead of orphaning a running plan); one bad plan no longer aborts the coordinator tick); #6211 `38ef1efa84` (planner: no 0-task launch; review panel follows the selected plan; long chat scrolls); #6219 `3f18ef481c` (grants: a `workflow:<id>` agent no longer crashes the default-permission lookup (regression from Agent Run #6168)); #6213 `0622e4ea36` (test and source record for packet `20261005239000` (the packet was already live)); #6212 `2df2d3b0cc` (scheduled workflows: stalls after restart / lost reply / Run-now / cancel fixed; for-each and delete fixed; pause banner + Release; packet `20261005235000`); #6220 `9ab57850bd` (an alert for an owner without Telegram is skipped and the run completes; coded errors with logged causes); #6222 `c7e4e9b150` (a failed task retries with a different agent (the preferred agent no longer overrides the failed-agents list)); #6207 `9dcef69a69` (older projects: Duplicate and Adopt (packet `20261006000700`) + plain-English refusal wording); #6223 `e0d776651c` (alerts for owners not yet admitted (invite-required) no longer fail); #6221 `0d25a537b4` (owner controls: resolve an unknown outcome, per-task Stop is final, review / outputs / settings work or say why (packet `20261006010000`)). Five extra packets applied and verified on production: `20261005232000_mc_rerun_unsent_anchor_hold` (2026-10-05 09:00Z); `20261005239000_mc_rerun_unadmitted_effect_hold` (2026-10-05 14:41Z); `20261005235000_scheduled_occurrence_recovery` (2026-10-05 19:55Z); `20261006000700_mc_legacy_plan_adoption` (2026-10-05 21:17Z); `20261006010000_mc_unknown_task_owner_resolution` (2026-10-05 22:22Z); production ledger 743 (the Agent Run session installed its own 19). Live acceptance B PASS 17:36Z (project `43470d88`). Evidence pushed to private branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d`. Production incidents found and fixed during the run: (1) **Scheduled workflows paused 06:24–07:57Z on 2026-10-05.** The W7 release carried a once-only scheduler that holds all due work while its switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is unset; it was unset in production, so all 534 scheduled workflows stopped for 93 minutes. The deploy-safety review missed it because it checked only the Mission Control files for new switches, not the whole diff. Fixed by the owner turning the switch on at 07:57Z (missed runs not re-run); remaining scheduler stalls fixed by #6212. (2) **Telegram "Liq Warning" alerts failing from 13:15Z to ~22:08Z on 2026-10-05.** A regression from the Agent Run release (#6168): first the permission lookup crashed on workflow-style agent ids, then alerts for owners not yet admitted failed when their settings were read. A catch-all error code hid both causes. Fixed by #6219, #6220 and #6223; 0 alert failures in the 15 minutes after the last fix. | W7 is merged, deployed and activated but NOT verified live (2 of 3) and must not be shown as complete. In priority order: (1) LIVE ACCEPTANCE A — Live acceptance on production, signed-in owner: **C PASS** (2026-10-05 06:35Z — Re-execute on a pre-release plan refused, nothing created; after #6207 it now offers Duplicate / Adopt). **B PASS** (2026-10-05 17:36Z — project `43470d88` "W7 live test": Re-execute → reload (lost reply) → "Check re-execution" → original run recovered, exactly 1 rerun receipt, no duplicate). **A NOT RUN** (critical-failure drain): needs a project created after #6198 whose critical task fails 3 times with an unstarted sibling; there is no deterministic way from the screen because per-task Stop is now final (no retry). Options: wait for a natural triple failure, or add a test-only owner action. Proof rows expected: a `critical_failure_drain` effect delivered; the sibling `skipped` with drain reason `critical_failure_unstarted`; the plan `failed`, never `completed`. (2) Open the PR for the production-shape end-to-end harness, branch `claude/w7-prod-shape-e2e-20261005` @ `080907ff6b` (scenarios S1–S9, `scripts/qa/w7-prod-shape-e2e/`, `run.sh`, runs on the build box; no PR yet, verified 02:00Z): merge main first, add a scenario for every fault found on 2026-10-05, and propose (do not enable) it as a required pre-release check. (3) Follow-ups found in review (not blockers): (1) A task that EVERY agent has failed stays `ready` forever (owners with a single agent) — needs skip or escalate. (2) An archived project with an approved or paused plan can still be executed by direct link (the execute route ignores the archive flag). (3) "Active projects" count includes archived projects. (4) A held task re-queues forever with no owner alert (coordinator). (5) Grants picker resets to 1 hour after reloading a half-saved approval; the approved card stays and the count does not change. (6) Creating a project accepts empty workflow steps (no server-side 0-task guard). (7) Voice-capture planning can return a 0-task plan. (8) Planner chat box is squashed at 390 px wide once a plan appears. (9) Re-execute after an unknown outcome is still refused (the plan finishes or stops but cannot be re-run). (10) Two concurrent runs can create two grant cards. (11) A Telegram kill-switch-locked owner with no chat id is now skipped (confirm intended). (4) Owner decisions still open: (1) The three sibling scheduler switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are still unset, so human-approval steps in scheduled workflows stay unsupported. Turn them on, or keep approval steps unsupported? (2) Should "Telegram not set up" ever fail a run? (Now: the alert is skipped and the run completes.) (3) The `supra_owner_runtime` role (5 owner schemas are not mapped). (5) Remaining W7 scope: remaining effects and manual parity; safe active cancellation; real L1 anchoring (anchors always end `held_unknown`; the capability is unverified); F2 rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md`); the runtime role; Stripe Link (owner, external); QA invite. Full project: 33 tasks, 16 behaviour families, 12 surfaces; iMessage deferred, WhatsApp excluded. (6) Cleanup: remove the pre-install production backup (5.4 GB, counts matched, never restore-tested) and its tool folder from the web host; delete merged lane folders (owner rule: `git worktree remove`, no --force, clean and idle, own lanes only; keep the end-to-end harness lane until its PR merges); remove leftover file-only scratch folders from this run on the build box. |
| **X2 — Confirm System Workflow durable terminal and pause receipts** | System Workflow pause and Memory Promotion partial fixes deployed | Qualify real admitted-owner pause/checkpoint/terminal recovery journeys. |
| **X3 — Refuse zero-row completion in scheduled and direct workflows** | Missing original terminal-row refusal has scoped native evidence | Verify scheduled and direct deployed paths retain truthful outcomes. |
| **X4 — Retain uncertain scheduled workflow attempts before another tick** | Scheduled original-attempt source preserved in held drafts. 2026-10-05: the once-only scheduled "occurrence claim" path reached production inside the release that deployed at 06:24Z, held behind the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`. The switch was unset, so all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on at 07:57Z and said missed runs need not be re-run. Observed to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), 55 failed, 27 of them waiting for a new per-action grant introduced by the same release. Fixes for the known stalls are work in progress on `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe` (untested, no PR; its packet `20261005235000` must not be applied) 2026-10-05 stabilisation: PR #6212 (main `2df2d3b0cc`, merged 19:56Z) fixed the known stalls — a run killed by a restart, a lost reply, Run-now, a cancelled slot — plus for-each on a repeated target and workflow delete, and added a pause banner with a Release control; its packet `20261005235000_scheduled_occurrence_recovery` was applied and verified on production at 19:55Z. Health in the hour before 01:55Z on 2026-10-06 (reported, not re-read here): 167 scheduled runs completed, 34 failed; 0 duplicate slots; 0 stalled occurrences; 0 Mission Control plans running. The remaining failures are owners' own model keys (30 × "No usable API key for anthropic", 2 × credit balance), not platform faults. | The once-only scheduler is live and its known stalls are fixed, but this task is NOT accepted: the original acceptance proofs (real-transport lost-acknowledgment and next-tick no-repeat) have not been run, and completing the cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`) is not recorded. Human-approval steps in scheduled workflows stay unsupported while the three sibling switches are unset (owner decision; see X5). Next: add scheduled scenarios to the end-to-end harness, run the original acceptance on production, and keep watching for duplicate slots (the only reason to turn the switch off). |
| **X5 — Qualify original scheduled approval continuation** | Bounded original approval continuation source qualified | Close remaining effectful graphs and real approval/uncertain-outcome acceptance. State at 2026-10-06: the once-only scheduler is on and its stalls are fixed (#6212), but the three approval switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are still unset, so human-approval steps in scheduled workflows remain unsupported. Owner decision still open: turn the three switches on, or keep approval steps unsupported. Neither is qualified. |
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

**Saved work:** Atomic grant reservations source in held draft6129 Related grant changes shipped 2026-10-05 (not W6 acceptance): PR #6206 (main `2e242177b3`) lets workflow grants last 1 hour / 24 hours / 1 week / 1 month / 1 year and keeps one card per workflow + action; PR #6219 (main `3f18ef481c`) stops the default-permission lookup crashing on `workflow:<id>` agents (a regression from Agent Run #6168). The owner approved their own two pending workflow grants for 1 year (18:13Z, expire 2027-10-05); other owners' cards are theirs to approve.

**Remaining:** Prove installed concurrent use, revocation and original receipt recovery. Known grant follow-ups from the 2026-10-05 review: two concurrent runs can create two grant cards; the grants picker resets to 1 hour after reloading a half-saved approval (the approved card stays and the count does not change).

**Acceptance:** Concurrent one-use attempts cannot both enter provider/storage; original invocation recovery does not consume twice or replay an uncertain effect; revocation/expiry and personal compatibility controls.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | See cited review evidence; no full-path approval inferred |
| merged | Full scope pending. Related grant-duration and lookup fixes merged 2026-10-05 (#6206, #6219); atomic usage limits not merged. |
| deployed | Full scope pending. #6206 and #6219 are live (main 0d25a537b4). |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W7 — Original-operation workflow effects

**Saved work:** Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. 2026-10-05 07:45–08:55Z, production stabilisation: hotfix PR #6199 opened (`claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a`) fixing faults 1 and 2 with packet `20261005232000_mc_rerun_unsent_anchor_hold` (build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head `420a71db33`, pending at the current head). A read-only audit of every guarded control (28 direct plan writers, 17 now rejected) and a production-shape end-to-end harness (S1–S9; all scenarios fail on main, S1–S3 and the Workspace drain pass on the fix) raised the fault count to eight. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. 2026-10-05 09:00Z → 22:23Z PRODUCTION STABILISATION (handed off 2026-10-06 01:55Z): all eight faults fixed and live through 14 PRs, each independently reviewed and merged with merge-if-green.sh: #6196 `55a12f0da9` (W7 release: squash of the composed failure-drain/rerun candidate `ac48190955`); #6199 `c1513db29c` (the final task of a plan settles again (finish intents now carry the task id) + packet `20261005232000`); #6197 `7b28f6a41a` (schema snapshot refresh; coordinator sweep skips drain-refused plans; manifest re-pin); #6198 `ec1e1132fe` (Mission Control plans get a critical path, so the drain can fire (owner said yes)); #6206 `2e242177b3` (workflow grants can last 1 hour / 24 hours / 1 week / 1 month / 1 year; one card per workflow + action); #6205 `aeebec0da0` (safe Delete project (refuse or archive instead of orphaning a running plan); one bad plan no longer aborts the coordinator tick); #6211 `38ef1efa84` (planner: no 0-task launch; review panel follows the selected plan; long chat scrolls); #6219 `3f18ef481c` (grants: a `workflow:<id>` agent no longer crashes the default-permission lookup (regression from Agent Run #6168)); #6213 `0622e4ea36` (test and source record for packet `20261005239000` (the packet was already live)); #6212 `2df2d3b0cc` (scheduled workflows: stalls after restart / lost reply / Run-now / cancel fixed; for-each and delete fixed; pause banner + Release; packet `20261005235000`); #6220 `9ab57850bd` (an alert for an owner without Telegram is skipped and the run completes; coded errors with logged causes); #6222 `c7e4e9b150` (a failed task retries with a different agent (the preferred agent no longer overrides the failed-agents list)); #6207 `9dcef69a69` (older projects: Duplicate and Adopt (packet `20261006000700`) + plain-English refusal wording); #6223 `e0d776651c` (alerts for owners not yet admitted (invite-required) no longer fail); #6221 `0d25a537b4` (owner controls: resolve an unknown outcome, per-task Stop is final, review / outputs / settings work or say why (packet `20261006010000`)). Five extra packets applied and verified on production: `20261005232000_mc_rerun_unsent_anchor_hold` (2026-10-05 09:00Z); `20261005239000_mc_rerun_unadmitted_effect_hold` (2026-10-05 14:41Z); `20261005235000_scheduled_occurrence_recovery` (2026-10-05 19:55Z); `20261006000700_mc_legacy_plan_adoption` (2026-10-05 21:17Z); `20261006010000_mc_unknown_task_owner_resolution` (2026-10-05 22:22Z); production ledger 743 (the Agent Run session installed its own 19). Live acceptance B PASS 17:36Z (project `43470d88`). Evidence pushed to private branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d`. Production incidents found and fixed during the run: (1) **Scheduled workflows paused 06:24–07:57Z on 2026-10-05.** The W7 release carried a once-only scheduler that holds all due work while its switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is unset; it was unset in production, so all 534 scheduled workflows stopped for 93 minutes. The deploy-safety review missed it because it checked only the Mission Control files for new switches, not the whole diff. Fixed by the owner turning the switch on at 07:57Z (missed runs not re-run); remaining scheduler stalls fixed by #6212. (2) **Telegram "Liq Warning" alerts failing from 13:15Z to ~22:08Z on 2026-10-05.** A regression from the Agent Run release (#6168): first the permission lookup crashed on workflow-style agent ids, then alerts for owners not yet admitted failed when their settings were read. A catch-all error code hid both causes. Fixed by #6219, #6220 and #6223; 0 alert failures in the 15 minutes after the last fix.

**Remaining:** W7 is merged, deployed and activated but NOT verified live (2 of 3) and must not be shown as complete. In priority order: (1) LIVE ACCEPTANCE A — Live acceptance on production, signed-in owner: **C PASS** (2026-10-05 06:35Z — Re-execute on a pre-release plan refused, nothing created; after #6207 it now offers Duplicate / Adopt). **B PASS** (2026-10-05 17:36Z — project `43470d88` "W7 live test": Re-execute → reload (lost reply) → "Check re-execution" → original run recovered, exactly 1 rerun receipt, no duplicate). **A NOT RUN** (critical-failure drain): needs a project created after #6198 whose critical task fails 3 times with an unstarted sibling; there is no deterministic way from the screen because per-task Stop is now final (no retry). Options: wait for a natural triple failure, or add a test-only owner action. Proof rows expected: a `critical_failure_drain` effect delivered; the sibling `skipped` with drain reason `critical_failure_unstarted`; the plan `failed`, never `completed`. (2) Open the PR for the production-shape end-to-end harness, branch `claude/w7-prod-shape-e2e-20261005` @ `080907ff6b` (scenarios S1–S9, `scripts/qa/w7-prod-shape-e2e/`, `run.sh`, runs on the build box; no PR yet, verified 02:00Z): merge main first, add a scenario for every fault found on 2026-10-05, and propose (do not enable) it as a required pre-release check. (3) Follow-ups found in review (not blockers): (1) A task that EVERY agent has failed stays `ready` forever (owners with a single agent) — needs skip or escalate. (2) An archived project with an approved or paused plan can still be executed by direct link (the execute route ignores the archive flag). (3) "Active projects" count includes archived projects. (4) A held task re-queues forever with no owner alert (coordinator). (5) Grants picker resets to 1 hour after reloading a half-saved approval; the approved card stays and the count does not change. (6) Creating a project accepts empty workflow steps (no server-side 0-task guard). (7) Voice-capture planning can return a 0-task plan. (8) Planner chat box is squashed at 390 px wide once a plan appears. (9) Re-execute after an unknown outcome is still refused (the plan finishes or stops but cannot be re-run). (10) Two concurrent runs can create two grant cards. (11) A Telegram kill-switch-locked owner with no chat id is now skipped (confirm intended). (4) Owner decisions still open: (1) The three sibling scheduler switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are still unset, so human-approval steps in scheduled workflows stay unsupported. Turn them on, or keep approval steps unsupported? (2) Should "Telegram not set up" ever fail a run? (Now: the alert is skipped and the run completes.) (3) The `supra_owner_runtime` role (5 owner schemas are not mapped). (5) Remaining W7 scope: remaining effects and manual parity; safe active cancellation; real L1 anchoring (anchors always end `held_unknown`; the capability is unverified); F2 rerun-init pending/unknown recovery (design note `docs/agent-run/mc-rerun-init-recovery-design.md`); the runtime role; Stripe Link (owner, external); QA invite. Full project: 33 tasks, 16 behaviour families, 12 surfaces; iMessage deferred, WhatsApp excluded. (6) Cleanup: remove the pre-install production backup (5.4 GB, counts matched, never restore-tested) and its tool folder from the web host; delete merged lane folders (owner rule: `git worktree remove`, no --force, clean and idle, own lanes only; keep the end-to-end harness lane until its PR merges); remove leftover file-only scratch folders from this run on the build box.

**Acceptance:** Thread server ToolContext identity, reserve before effect, preserve original run and unknown outcome, reject missing/forged identity, prove cap/no replay via actual transport. Bind actual task settlement to the original saved execution claim atomically; reject superseded results before effects and recover post-commit delivery without duplication. Prove usable original-child lookup/recovery and keep unsupported callers explicit.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.; new branches/commits in pause checkpoint.

**Prior owner role:** release_integration: isolated claim/settlement production repair; release_verification: independent tests; root: composition/release. Root must assign a currently available named owner before dispatch. **Original dependencies:** W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the drain/rerun milestone (candidate ac48190955) and for all eight faults found on 2026-10-05 (14 fix PRs, including owner controls #6221, legacy Duplicate/Adopt #6207, critical path #6198, safe delete #6205, failed-task retry #6222). Remaining W7 effects/manual parity, active cancellation, real L1 anchoring and F2 recovery are still open. |
| integrated | Yes: PR #6196 and the 14 stabilisation PRs are on main (live = 0d25a537b4). The end-to-end harness branch (080907ff6b) is not integrated (no PR). |
| tested | Yes per PR: required box-ci checks green at each merge (merge-if-green.sh); five extra packets APPLIED AND VERIFIED on production. Lesson kept: fixture contract cases and mocked browser tests missed three live faults; the production-shape end-to-end harness (S1–S3, S9 and the Workspace drain PASS on the hotfix) is not yet a required check. |
| independentlyReviewed | Yes: an independent review for each of the 15 PRs before merge (per the run record). The candidate review at ac48190955 had missed the live faults and the scheduler switch. |
| merged | Yes: #6196 (55a12f0da9) and #6199 #6197 #6198 #6206 #6205 #6211 #6219 #6213 #6212 #6220 #6222 #6207 #6223 #6221 (last: 0d25a537b4, 22:23:13Z 2026-10-05). Verified MERGED on GitHub 2026-10-06 ~02:00Z. |
| deployed | Yes: /api/version reports 0d25a537b4 (2026-10-06 01:59Z). Production ledger 743: 24 W7 packets + 5 extra packets (232000, 239000, 235000, 20261006000700, 20261006010000), all applied and verified. Pre-install backup NOT restore-tested. |
| activated | Yes: Mission Control drain/rerun is live by construction (no feature flag); critical path on for new projects (#6198); the once-only scheduler switch is ON since 07:57Z 2026-10-05. Three sibling scheduler switches unset (owner decision). |
| verifiedLive | NO — 2 of 3. C PASS 06:35Z 2026-10-05 (legacy Re-execute refused, nothing created). B PASS 17:36Z 2026-10-05 (lost-acknowledgment rerun recovered, exactly 1 receipt). A (critical-failure drain) NOT RUN. The milestone is not complete. |

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

**Saved work:** Scheduled original-attempt source preserved in held drafts. 2026-10-05: the once-only scheduled "occurrence claim" path reached production inside the release that deployed at 06:24Z, held behind the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`. The switch was unset, so all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on at 07:57Z and said missed runs need not be re-run. Observed to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), 55 failed, 27 of them waiting for a new per-action grant introduced by the same release. Fixes for the known stalls are work in progress on `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe` (untested, no PR; its packet `20261005235000` must not be applied) 2026-10-05 stabilisation: PR #6212 (main `2df2d3b0cc`, merged 19:56Z) fixed the known stalls — a run killed by a restart, a lost reply, Run-now, a cancelled slot — plus for-each on a repeated target and workflow delete, and added a pause banner with a Release control; its packet `20261005235000_scheduled_occurrence_recovery` was applied and verified on production at 19:55Z. Health in the hour before 01:55Z on 2026-10-06 (reported, not re-read here): 167 scheduled runs completed, 34 failed; 0 duplicate slots; 0 stalled occurrences; 0 Mission Control plans running. The remaining failures are owners' own model keys (30 × "No usable API key for anthropic", 2 × credit balance), not platform faults.

**Remaining:** The once-only scheduler is live and its known stalls are fixed, but this task is NOT accepted: the original acceptance proofs (real-transport lost-acknowledgment and next-tick no-repeat) have not been run, and completing the cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`) is not recorded. Human-approval steps in scheduled workflows stay unsupported while the three sibling switches are unset (owner decision; see X5). Next: add scheduled scenarios to the end-to-end harness, run the original acceptance on production, and keep watching for duplicate slots (the only reason to turn the switch off).

**Acceptance:** Carry exact original identity and unknown status; atomically hold/recover original schedule attempt; real transport lost-ack and next-tick no-repeat proof, installed schema and deployed checks.

**Source:** app/api/cron/workflow-triggers/route.ts:189; lib/vms/workflows/execution-engine.ts; docs/agent-run/scheduled-workflow-recovery-plan-20261001.md

**Prior owner role:** Sol SQL + Sol engine; Root native integration. Root must assign a currently available named owner before dispatch. **Original dependencies:** X3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes: once-only occurrence claim path, plus stall/for-each/delete fixes (#6212). |
| integrated | Yes: on main (#6212 = 2df2d3b0cc; live = 0d25a537b4). |
| tested | Required box-ci checks green at merge; packet 235000 applied and verified on production. Original acceptance proofs not run. |
| independentlyReviewed | Yes for #6212 (independent review before merge, per the run record). |
| merged | Yes: #6212 merged 2026-10-05 19:56Z. |
| deployed | Yes: live in main 0d25a537b4; packet 235000 installed 19:55Z. |
| activated | Yes: switch ON since 2026-10-05 07:57Z (owner choice after the 06:24–07:57Z pause of all 534 scheduled workflows). |
| verifiedLive | NO (observation only): last hour before 01:55Z 2026-10-06 — 167 completed / 34 failed (owners' own model keys), 0 duplicate slots, 0 stalled occurrences. Acceptance proofs not run. |

### X5 — Qualify original scheduled approval continuation

**Saved work:** Bounded original approval continuation source qualified

**Remaining:** Close remaining effectful graphs and real approval/uncertain-outcome acceptance. State at 2026-10-06: the once-only scheduler is on and its stalls are fixed (#6212), but the three approval switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are still unset, so human-approval steps in scheduled workflows remain unsupported. Owner decision still open: turn the three switches on, or keep approval steps unsupported. Neither is qualified.

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
| activated | NOT activated: the three approval switches are unset on production (re-stated 2026-10-06). Owner decision pending. |
| verifiedLive | NO. Full scope pending; scheduled human-approval steps are unsupported until the owner decides. |

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
