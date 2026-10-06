# SupraOS Workflow Evidence Index

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-06T10:11:19Z**. Canonical record SHA-256: `1497df9c741256d0d1e8d325806b27355221123ff0de0aaaf4ff1c72b146b3d2`.

**Execution state:** RUNNING 2026-10-06 (midday state at ~10:00Z); lanes running. Production code is main `e89acee6d2` (live). W7 drain/rerun milestone: #6239 merged and live, so live test A is CLOSED — the drained plan ended `failed` 09:09:21Z, 34 s after #6239 went live (owner not notified: known gap, fixed by #6255, open). B and C PASS 2026-10-05. The full W7 task is still NOT accepted (effects parity, safe cancellation, real L1 anchoring, F2 recovery, runtime role remain). Also merged today: #6233 (exhausted agents skip/escalate + held-task alert), #6230 (end-to-end harness S1–S13, box-ci step NOT enabled), earlier #6226 #6227 #6229. 14 production packets applied and verified today (schema first; most code PRs still open). Runtime role installed but its switch was rolled back (~09:19Z → ~09:52Z) after Settings → General returned 503; fix #6270 in review; no re-switch until it is live. Reviews passed for W2, W3–W6, X2/X3, X4/X5, canvas approvals, project server and relay client PRs (all open). PR states re-read from GitHub at 2026-10-06T10:11Z: #6239 MERGED 08:54:46Z, #6233 MERGED 09:26:41Z, #6230 MERGED 09:37:10Z (main `e89acee6d2` = live); #6246 #6247 #6249 #6252 #6253 #6254 #6255 #6256 #6257 #6258 #6259 #6261 #6263 #6270 OPEN. `https://supraos.ai/api/version` read anonymously at 2026-10-06T10:11Z reports `e89acee6d2` (stamped 10:07:17Z). Packet applies, the runtime-role switch/rollback and review verdicts are as reported in the private handoff (~07:12Z–10:00Z 2026-10-06) and were NOT re-read on production for this record..

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** **W7 DRAIN/RERUN: 3 of 3 PASS LIVE (A closed 09:09:21Z); full W7 NOT accepted.** Production code is main `e89acee6d2`. **Live test A CLOSED live:** the drained plan `ee4c97bc` (project `bacf0dc8`) became `failed` at 09:09:21Z 2026-10-06, 34 s after #6239 went live (08:54:46Z merge; live 09:08:47Z); the project became `failed` too. The owner was NOT notified — that plan was finished by the v1 finaliser before #6255 (known gap; #6255 makes a drained project say so and tells the owner; its packet `20261006030000` is applied, code PR OPEN). The next live drain after #6255 should notify. Production packets applied 2026-10-06, each APPLIED AND VERIFIED: `20261006020000` (#6239, 07:12:36Z), then 20261006030000 (#6255), 20261006040000 (#6252), 20261006050000 (#6247), 20261006060000 (#6249), 20261006070000 (#6254), 20261006110000, 111000, 112000, 114000, 115000, 115500 (#6259), 20261006120000 (#6258, runtime role), 20261006141000 (#6263). These are schema-first installs: except #6239, their code PRs are still OPEN; the #6259 switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. **Runtime role (R3B): installed, switch ROLLED BACK.** Packet `20261006120000` (#6258, OPEN) applied and verified; orphan owner schemas fixed by the owner (1 re-linked, 4 empty ones renamed as archived, 0 left); the owner set the role's login and a login through the connection pooler passed. The switch at ~09:19Z broke public-table callers (Settings → General returned 503) and was ROLLED BACK at ~09:52Z (pages verified 200). The role keeps its login but is unused. Fix [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (public-table callers use the admin connection) is in review (needs a type fix, an import guard and pre-switch privilege checks). Do NOT re-switch until #6270 is live and the privilege check passes. **Reviews PASS (open, merge when green):** W2 [#6253](https://github.com/jtobkin/suprafx-platform/pull/6253); W3–W6 [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) (includes a security fix: another account could revoke an owner's grant); X2/X3 [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261); X4/X5 [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254); canvas approvals [#6263](https://github.com/jtobkin/suprafx-platform/pull/6263); project server B1/C2 server/M1 [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) (switch off); relay client C1/C2 client [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256); also [#6246](https://github.com/jtobkin/suprafx-platform/pull/6246) House Rules apply to computer agents, [#6247](https://github.com/jtobkin/suprafx-platform/pull/6247) un-archive hole + one grant card under load, [#6252](https://github.com/jtobkin/suprafx-platform/pull/6252) owner's last decision finishes the project / Stop on a critical task drains it. Open, review status not recorded here: [#6249](https://github.com/jtobkin/suprafx-platform/pull/6249) interrupted Re-execute no longer wedges a project; [#6255](https://github.com/jtobkin/suprafx-platform/pull/6255) drained project says so and the owner is told; [#6258](https://github.com/jtobkin/suprafx-platform/pull/6258) runtime role packet; [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (in review). **New lanes running:** W7 effects parity; safe cancellation + 0-task voice planning; X1 context entries. **Follow-ups (not blockers):** #6246 floors task cost at $0.08, so an "ask above X" rule under $0.08 asks on every task; #6247 archived-project toggle returns 400; #6252 a review "reject" on a critical task now drains the plan (undisclosed); #6253 a crash between email claim and send leaves no history line; #6257 spawn retry does not return the child id; #6259 before switch-on: transport deletes blocked by observations (desktop re-sign-in 500), old poll hands out bound commands unchecked; #6254 script expectations need a writable role and two corrected lines. **Next:** merge the reviewed PRs when green; land #6270 then re-try the runtime-role switch; prove the next live drain notifies the owner; W7 effects parity, safe cancellation, X1. PR states re-read from GitHub at 2026-10-06T10:11Z: #6239 MERGED 08:54:46Z, #6233 MERGED 09:26:41Z, #6230 MERGED 09:37:10Z (main `e89acee6d2` = live); #6246 #6247 #6249 #6252 #6253 #6254 #6255 #6256 #6257 #6258 #6259 #6261 #6263 #6270 OPEN. `https://supraos.ai/api/version` read anonymously at 2026-10-06T10:11Z reports `e89acee6d2` (stamped 10:07:17Z). Packet applies, the runtime-role switch/rollback and review verdicts are as reported in the private handoff (~07:12Z–10:00Z 2026-10-06) and were NOT re-read on production for this record.

**Current candidate record:** `ac4819095585eed003eb0c510b0a8c8608d5e73f`, tree `49bf08e3354a115783635eebfa4801dfa953bb6c`. Security: box-ci/security-gates SUCCESS on ac48190955 (51 steps; macOS Native Land not run). Previous head 3214f4849e: FAILURE (whole unit tree 2 failed / 55,609 passed / 374 skipped across 4,508 files; scoped changed-file TypeScript check 5 errors); build: box-ci/production-build SUCCESS on ac48190955 (7 steps). Previous head 3214f4849e: ERROR (not built because security gates failed); macOS Native Land: Not run (not part of box-ci). Merged: True; deployed: True; activated: True; verified live: yes — 3 of 3 behaviours PASS on production (A CLOSED 09:09:21Z 2026-10-06 after #6239; B and C 2026-10-05); owner notification on drain-finish is a known gap (#6255 open); full W7 task NOT accepted. Scope: Composed W7 failure-drain/rerun candidate (partial W7; full scope open). Frozen candidate ac48190955 = 3214f4849e + fix commit 867a5f2114 + clean merge of origin/main 7a10b7a3fc; required CI GREEN and independent trailing audit PASS 5/5 at that commit. Squash-merged 2026-10-05 06:11:22Z as main 55a12f0da9 (PR #6196); installed 06:03–06:10Z; deployed 06:24:35Z; activated. Stabilisation (same day, 12:59–22:23Z): 14 PRs merged via merge-if-green.sh with an independent review each; five extra packets installed (ledger 743); live = main 0d25a537b4. Follow-ups merged 2026-10-06: #6226 #6227 #6229 #6239 (finalisation after owner resolution; packet `20261006020000`) #6233 #6230; live = main `e89acee6d2`. Verified live: 3 of 3 behaviours PASS (A CLOSED 09:09:21Z 2026-10-06; B PASS 17:36Z, C PASS 06:35Z 2026-10-05); the full W7 task is NOT accepted. All four scheduler switches ON (approval siblings since 03:09:23Z 2026-10-06).. Observed: 2026-10-06T10:11:19Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.


## Status 2026-10-06 ~10:00Z — live test A CLOSED; 14 packets applied; runtime-role switch rolled back (read this first)

PR states re-read from GitHub at 2026-10-06T10:11Z: #6239 MERGED 08:54:46Z, #6233 MERGED 09:26:41Z, #6230 MERGED 09:37:10Z (main `e89acee6d2` = live); #6246 #6247 #6249 #6252 #6253 #6254 #6255 #6256 #6257 #6258 #6259 #6261 #6263 #6270 OPEN. `https://supraos.ai/api/version` read anonymously at 2026-10-06T10:11Z reports `e89acee6d2` (stamped 10:07:17Z). Packet applies, the runtime-role switch/rollback and review verdicts are as reported in the private handoff (~07:12Z–10:00Z 2026-10-06) and were NOT re-read on production for this record.

| Stage (W7 drain/rerun milestone) | State now |
| --- | --- |
| Implemented | Yes — plus finalisation after owner resolution (#6239) and exhausted-agents skip/escalate (#6233); more follow-ups open |
| Integrated | Yes — #6239 #6233 #6230 (and #6226 #6227 #6229) on main `e89acee6d2` |
| Tested | Yes per PR (box-ci green at merge); e2e harness S1–S13 merged (#6230), box-ci step NOT enabled |
| Independently reviewed | Yes for each merged PR |
| Merged / Deployed | Yes — live `e89acee6d2` |
| Activated | Yes — no feature flag; all four scheduler switches ON |
| Verified live | **3 of 3 PASS** — A closed 09:09:21Z 2026-10-06; full W7 task NOT accepted |

**Live test A CLOSED live:** the drained plan `ee4c97bc` (project `bacf0dc8`) became `failed` at 09:09:21Z 2026-10-06, 34 s after #6239 went live (08:54:46Z merge; live 09:08:47Z); the project became `failed` too. The owner was NOT notified — that plan was finished by the v1 finaliser before #6255 (known gap; #6255 makes a drained project say so and tells the owner; its packet `20261006030000` is applied, code PR OPEN). The next live drain after #6255 should notify.

**Packets.** Production packets applied 2026-10-06, each APPLIED AND VERIFIED: `20261006020000` (#6239, 07:12:36Z), then 20261006030000 (#6255), 20261006040000 (#6252), 20261006050000 (#6247), 20261006060000 (#6249), 20261006070000 (#6254), 20261006110000, 111000, 112000, 114000, 115000, 115500 (#6259), 20261006120000 (#6258, runtime role), 20261006141000 (#6263). These are schema-first installs: except #6239, their code PRs are still OPEN; the #6259 switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF.

**Runtime role (R3B): installed, switch ROLLED BACK.** Packet `20261006120000` (#6258, OPEN) applied and verified; orphan owner schemas fixed by the owner (1 re-linked, 4 empty ones renamed as archived, 0 left); the owner set the role's login and a login through the connection pooler passed. The switch at ~09:19Z broke public-table callers (Settings → General returned 503) and was ROLLED BACK at ~09:52Z (pages verified 200). The role keeps its login but is unused. Fix [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (public-table callers use the admin connection) is in review (needs a type fix, an import guard and pre-switch privilege checks). Do NOT re-switch until #6270 is live and the privilege check passes.

**Reviews PASS (open, merge when green):** W2 [#6253](https://github.com/jtobkin/suprafx-platform/pull/6253); W3–W6 [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) (includes a security fix: another account could revoke an owner's grant); X2/X3 [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261); X4/X5 [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254); canvas approvals [#6263](https://github.com/jtobkin/suprafx-platform/pull/6263); project server B1/C2 server/M1 [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) (switch off); relay client C1/C2 client [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256); also [#6246](https://github.com/jtobkin/suprafx-platform/pull/6246) House Rules apply to computer agents, [#6247](https://github.com/jtobkin/suprafx-platform/pull/6247) un-archive hole + one grant card under load, [#6252](https://github.com/jtobkin/suprafx-platform/pull/6252) owner's last decision finishes the project / Stop on a critical task drains it. Open, review status not recorded here: [#6249](https://github.com/jtobkin/suprafx-platform/pull/6249) interrupted Re-execute no longer wedges a project; [#6255](https://github.com/jtobkin/suprafx-platform/pull/6255) drained project says so and the owner is told; [#6258](https://github.com/jtobkin/suprafx-platform/pull/6258) runtime role packet; [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (in review).

**New lanes running:** W7 effects parity; safe cancellation + 0-task voice planning; X1 context entries.

**Next.** Merge the reviewed PRs when green (their packets are already live); land #6270 and re-try the runtime-role switch only after the privilege check; prove the next live drain tells the owner (#6255); continue W7 effects parity, safe cancellation and X1.

## Status 2026-10-06 ~03:25Z — live test A observed (3 of 3) with a finalisation gap; approval switches ON; runtime role NO-GO (read this first)

The run resumed at 02:17Z 2026-10-06 (owner: "resume end to end"). PR states re-read from GitHub at 2026-10-06 03:22Z (#6225 MERGED 03:21:38Z → main `4c9208fc5f`; #6226 #6227 #6229 #6230 #6233 OPEN); `https://supraos.ai/api/version` re-read anonymously at 2026-10-06 03:22:03Z reports `0d25a537b4` (#6225 not yet live at that read). Live-test, switch, rehearsal and runtime-role figures are as reported in the private handoff at 03:01–03:10Z and were NOT re-read for this record.

**Where W7 stands.** Implemented, integrated, tested, independently reviewed, merged, deployed and activated — **yes**. **Observed live — 3 of 3 behaviours**, but A was observed **with a finalisation gap**, so the milestone is **NOT accepted**.

| Stage | State now |
| --- | --- |
| Implemented | Yes — the drain/rerun milestone plus fixes for all eight faults of 2026-10-05; gap fix (packet `20261006020000` + finaliser) in progress, not merged |
| Integrated | Yes — 15 PRs on main; five follow-up PRs open (#6226 #6227 #6229 #6230 #6233) |
| Tested | Yes per PR; approval-switch rehearsal on the build box GO (13/13 + 78/78 + 7/7 contract, 29/29 packets, 7/7 two-tick drive) |
| Independently reviewed | Yes — each merged PR; the five open PRs are reviewed safe |
| Merged | Yes — last W7 merge #6221, main `0d25a537b4`; #6225 (audit fix, other session) merged 03:21Z → `4c9208fc5f` |
| Deployed | Yes — `/api/version` reports `0d25a537b4` at 03:22Z |
| Activated | Yes — no feature flag; critical path on for new projects; all four scheduler switches ON (approval siblings since 03:09:23Z) |
| Verified live | **3 of 3 OBSERVED; NOT accepted.** A PASS with gap 03:01Z 2026-10-06; B PASS 17:36Z, C PASS 06:35Z 2026-10-05 |

**Live acceptance A.** **A PASS with a finalisation gap** (2026-10-06 03:01Z, production, signed-in owner; project `bacf0dc8` "W7 drain test", born after #6198 so it carries a critical path of task-1 → task-2). Method: a temporary House Rule "always ask above $0.001" on all 35 active agents (set through the House Rules screen, removed afterwards; 0 left in the database) refused task-1 before dispatch — a pre-dispatch gate, not a real model failure. task-1 failed twice (two different agents); attempt 3 went to a shared-computer agent that BYPASSES the House Rules gate, ran ~4 minutes and ended `outcome_unknown`/blocked; the owner used Resolve → Retry (#6221, live); attempt 4 failed; retries reached 3; the `critical_failure_drain` and `critical_escalation` effects were delivered; task-2 was `skipped` with drain reason `critical_failure_unstarted`; the plan was never completed. **Gap (live):** the plan stays `running` for ever — the terminal-blocked rule (packet `20261005230000`, `mc_drain_terminal_blocked_v1`) still counts the settled unknown-outcome receipt after the owner resolved it; the coordinator skips draining plans, execute refuses, so nothing finalises; the same rule blocks Re-execute (active claim). Fix in progress: packet `20261006020000` on branch `claude/w7-owner-resolution-unblocks-20261006` plus a sanctioned finaliser; no PR yet. Evidence: private evidence lane, `live/acceptance/A-critical-drain-PASS-with-gap.md`.

**Findings.** Findings from live test A (2026-10-06): (1) shared-computer agents bypass House Rules (the pre-dispatch gate does not apply to them); (2) a skipped task renders as "planned" on the project screen — no drain wording; (3) an owner Stop on an unstarted critical task wedges the plan (retries 0 → 1, the task cannot fail again; design-lane finding).

**Scheduled approval switches (X5).** 2026-10-06 03:09:23Z: the three approval switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) were set to on in the production settings store and applied on the web host under the deploy lock (owner decision 02:25Z); both containers show all four scheduler switches on. Build-box rehearsal before the flip: GO — 13/13 + 78/78 + 7/7 contract cases, 29/29 packets, 7/7 two-tick drive (verdict file in the private evidence lane, `live/verify/scheduled-approval-switches-verdict.md`). Known limit: approvals already pending from BEFORE the flip stay held — the engine stamps the occurrence id only when the switch was on at run start — so their only exit is the workflow page "Release this run" control after 30 minutes.

**Runtime role (R3B).** 2026-10-06 ~03:00Z rehearsal verdict: **NO-GO today** (private evidence lane, `live/verify/runtime-role-verdict.md`). The role packet refuses on the production shape (an existing `vms_agent_run_shelf` table; on PostgreSQL 16+ the implicit ADMIN membership of the postgres account cannot be revoked); a code blocker in the runtime binding (`lib/owner-db-runtime-binding.ts` membership test) would make every owner-database call fail with the switch on; one `FOR SHARE` read in `lib/vms-config.ts` needs UPDATE privilege. A renumbered packet (`20261006120000`) is prepared on branch `claude/runtime-role-packet-20261006` @ `7c72542d29`, no PR. Needs first: a product PR for the binding and the read, an owner-created runtime credential, and re-mapping of the orphan owner schemas.

**Open PRs.** Open PRs (all independently reviewed safe; merges held by the Agent Run session until its audit-fix #6225 landed — #6225 MERGED 2026-10-06 03:21:38Z → main `4c9208fc5f`; merge order after it): [#6226](https://github.com/jtobkin/suprafx-platform/pull/6226) grants: approved cards clear, chosen duration survives a reload, one card per request; [#6227](https://github.com/jtobkin/suprafx-platform/pull/6227) planner works on a phone + design for re-executing after an unknown outcome; [#6229](https://github.com/jtobkin/suprafx-platform/pull/6229) archived projects cannot run, counts and lists exclude them, no 0-task projects (review PASS); [#6230](https://github.com/jtobkin/suprafx-platform/pull/6230) production-shape end-to-end harness S1–S13 (review PASS; do NOT enable the box-ci step yet); [#6233](https://github.com/jtobkin/suprafx-platform/pull/6233) a task every agent has failed no longer waits for ever; a held task alerts the owner.

**Lesson (EP11).** A live acceptance that needs a deterministic failure should use a pre-dispatch gate (a temporary House Rule) rather than real model failures; remove it afterwards and prove it is gone.

**What is left (priority order).**

1. **Close the finalisation gap** — packet `20261006020000` + a sanctioned finaliser; then re-run A on a fresh project and prove the plan ends `failed` and Re-execute is no longer blocked.
2. **Merge the five open PRs** after #6225, in review order; keep the end-to-end harness box-ci step proposed, not enabled.
3. **Fix the three findings** (shared-computer House Rules bypass; "planned" wording for a skipped task; owner Stop wedging an unstarted critical task).
4. **Scheduled approval acceptance** — drive one real human-approval step on production end-to-end; add approval scenarios to the harness.
5. **Runtime role** — product PR for the binding and the read, owner-created credential, orphan-schema re-mapping, then rehearse `20261006120000`.
6. **Remaining W7 scope** (unchanged): effects/manual parity, active cancellation, real L1 anchoring, F2 recovery, Stripe Link (owner), QA invite. Full project: 33 tasks, 16 behaviour families, 12 surfaces; iMessage deferred, WhatsApp excluded.
7. **Cleanup** — production pre-install backup and tool folder; merged lane folders (owner rule); build-box scratch.

Owner decisions answered 2026-10-06 02:25Z: turn on the three scheduled approval switches after qualification — done 03:09Z; install the runtime role after rehearsal — rehearsal said NO-GO, install not done.

## Status 2026-10-06 ~01:55Z — stabilisation COMPLETE; W7 live but NOT verified (2 of 3) — superseded by the 03:25Z section above

The sections below this one describe the earlier pauses (~08:55Z and ~02:04Z on 2026-10-05) and are kept as dated history. This section was the state at 01:55Z; the section above is current. PR states and merge commits re-read from GitHub at 2026-10-06 ~02:00Z; `https://supraos.ai/api/version` re-read anonymously at 2026-10-06 01:59:48Z reports `0d25a537b4` (= main). Ledger, switch and health figures are as reported in the private handoff at 01:55Z and were NOT re-read for this record.

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

**Current code and evidence (2026-10-06).** Product repo: private `jtobkin/suprafx-platform`, branch `main` — everything above is in it. Key code: `lib/vms/workflows/` (plan-orchestrator.ts, mc-*-effect.ts, mc-plan-finish-intents.ts, mc-rerun-request.ts, mc-owner-manual-action.ts, execution-engine.ts, workflow-telegram-notice.ts, scheduled-*.ts); `app/api/projects/**` (create, execute, rerun, duplicate, adopt, resolve, tasks/[taskId]/stop); `app/api/cron/mc-coordinator/route.ts`; `app/api/cron/workflow-triggers/route.ts`; `app/vms/mission-control/**`; `components/vms/workflow/ScheduleHoldBanner.tsx`; `lib/vms/agent-grants.ts`; `lib/db-as-owner.ts`; `supabase/migrations/2026100*`. Docs in the product repo: `docs/agent-run/RELEASE-W7-*.md`, `docs/agent-run/mc-rerun-request-recovery.md`, `docs/agent-run/mc-rerun-init-recovery-design.md` (F2), `docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`. Evidence (private): branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d` (pushed 2026-10-06 01:59Z: production install logs for the five extra packets, live test B PASS, rerun-effects proof, delete / grants / planner / legacy-rerun screenshots; earlier commit `b11636b366` has the W7 install log, live-controls audit, end-to-end results and scheduler flag-on verdict), folder `docs/agent-run/evidence/w7-resume-20261005/`. End-to-end harness: PR #6230 (OPEN, S1–S13, review PASS) from branch `claude/w7-prod-shape-e2e-20261005`. Gap-fix lane: `claude/w7-owner-resolution-unblocks-20261006` (packet `20261006020000`, no PR). Runtime-role packet: `claude/runtime-role-packet-20261006` @ `7c72542d29` (no PR). Live test A evidence, switch verdict and runtime-role verdict: private evidence lane (`live/acceptance/A-critical-drain-PASS-with-gap.md`, `live/verify/scheduled-approval-switches-verdict.md`, `live/verify/runtime-role-verdict.md`), to be committed to the private evidence branch.

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
