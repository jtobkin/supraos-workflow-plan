# SupraOS Release Plan Checklist

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-08T08:55:00Z**. Canonical record SHA-256: `80fa8386eda91ea4edd5aef301070fcb102b862bbb29c2bb70e5afec2401cf07`.

**Execution state:** RUNNING 2026-10-08 (state at ~08:50Z / 16:50 HKT). Production code is main `604b0e0964` (live). Merged since the last record (2026-10-08 00:56Z), all live: #6373 #6277 #6381 #6347 #6369 #6356 #6372 #6362 #6395 #6396 (#6373 is CI only). Packets applied since: 20261008130000 (#6401, agents-learn-preferences tables) and 20261008151500 (#6419, signal target). Open (24): #6259 #6287 #6298 #6301 #6316 #6336 #6344 #6345 #6354 #6361 #6368 #6374 #6377 #6400 #6401 #6399 #6398 #6411 #6410 #6419 #6424 #6406 #6423 #6428. PREFS (agents learn your preferences): P0–P5 built and reviewed, signals and promise tracking built, all switches off; a cloud runner rebuild is needed before the worker switch. Live proofs: #6372 seen on screen signed in; #6369 privacy fence is live but has never run on a shared audience (none exists). Owner decisions today: learned-preferences log lives in Settings → General; stop the agent-text preference job; keep the 15 old rows; revoke the July public deck link (done). Switch A on by default; all other new switches stay OFF. Telegram is still not linked. The full W7 task is still NOT accepted. PR states re-read from GitHub at 2026-10-08T08:50Z (16:50 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-08T08:50Z reports `604b0e0964` (stamped 08:48:10Z; main, #6402 from another session); every PR listed as live was verified as an ancestor of it with `git merge-base --is-ancestor`. Main head is `ec244a558f` (#6391, another session), ahead of live. Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times). Review verdicts, the turn-learner switch-on runbook and the live-proof findings are as reported in the private evidence and were NOT re-run for this record. Switch values were NOT read from the live server for this record (the runbook's read-only check at 07:20Z found all five learner switches absent)..

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** **2026-10-08 (~08:50Z): 10 more PRs merged and live, 2 more packets applied, PREFS P0–P5 built and reviewed (all switches off); full W7 NOT accepted.** Production code is main `604b0e0964`. **Merged and live since the last record:** [#6373](https://github.com/jtobkin/suprafx-platform/pull/6373) CI: native Postgres test clusters start reliably (CI only) (00:35Z); [#6277](https://github.com/jtobkin/suprafx-platform/pull/6277) Stop works while a task is running; no 0-task plan is saved (packet 151000) (01:36Z); [#6381](https://github.com/jtobkin/suprafx-platform/pull/6381) backup tool covers every owner and agent schema; does not block deploys (02:43Z); [#6347](https://github.com/jtobkin/suprafx-platform/pull/6347) desktop: pages cannot choose program or folder (web side live; desktop side ships in 0.1.59) (04:03Z); [#6369](https://github.com/jtobkin/suprafx-platform/pull/6369) privacy: owner-private memory never reaches room guests, routines or project members (04:36Z); [#6356](https://github.com/jtobkin/suprafx-platform/pull/6356) chat keeps the real error when a model attempt fails (05:17Z); [#6372](https://github.com/jtobkin/suprafx-platform/pull/6372) polish: grant durations text, House Rules cost-floor warning, card counts, alert-channel notice (05:36Z); [#6362](https://github.com/jtobkin/suprafx-platform/pull/6362) X1: read back Mission Control task context receipts (owner only) (06:11Z); [#6395](https://github.com/jtobkin/suprafx-platform/pull/6395) Mission Control project page: agent lanes show real agents (06:32Z); [#6396](https://github.com/jtobkin/suprafx-platform/pull/6396) "I could not record that": agent preference saves no longer fail when the model echoes owner quiet hours (07:03Z). **Packets applied and verified since:** `20261008130000` (#6401, ~03:20Z), `20261008151500` (#6419, ~08:18Z). **Open (24):** #6259 #6287 #6298 #6301 #6316 #6336 #6344 #6345 #6354 #6361 #6368 #6374 #6377 #6400 #6401 #6399 #6398 #6411 #6410 #6419 #6424 #6406 #6423 #6428. **PREFS:** Status 2026-10-08 ~08:50Z: P0–P5 built and independently reviewed, all OPEN: P0+P1 tables + post-reply tickets [#6401](https://github.com/jtobkin/suprafx-platform/pull/6401) (packet `20261008130000` APPLIED AND VERIFIED ~03:20Z; tables empty), P2 background scanner [#6399](https://github.com/jtobkin/suprafx-platform/pull/6399), P3 Settings → General log [#6398](https://github.com/jtobkin/suprafx-platform/pull/6398), P4 auto-save with undo + daily review card [#6411](https://github.com/jtobkin/suprafx-platform/pull/6411), P5 ask once [#6410](https://github.com/jtobkin/suprafx-platform/pull/6410). Same pipe: corrections/frustration signals [#6419](https://github.com/jtobkin/suprafx-platform/pull/6419) (reviewed; packet `20261008151500` APPLIED AND VERIFIED ~08:18Z) and promise tracking [#6424](https://github.com/jtobkin/suprafx-platform/pull/6424) (built; review not recorded), both test mode. "I could not record that" fix [#6396](https://github.com/jtobkin/suprafx-platform/pull/6396) MERGED 07:03Z and live. Stop saving preferences from agent text [#6406](https://github.com/jtobkin/suprafx-platform/pull/6406) reviewed, OPEN. **All five learner switches are off** (absent at the 07:20Z read-only check). Switch-on runbook written (enqueue → runner rebuild → worker → Settings log → auto-save → ask once; each with an off script): the cloud chat runner image predates this work and deploys do not rebuild it, so **a runner rebuild is needed before the worker switch** (it also ships earlier runner changes for the first time; prove chat still answers after). Auto-save waits for ≥30 reviewed items with ≥90 % kept. Nothing switched on. **Live proofs:** #6372 seen on screen signed in (grants "At its limit" + duration copy; Mission Control "link Telegram" notice); #6369 fence live and correctly ordered but never exercised on a shared audience (none exists); #6277 Stop, #6356 error cause, #6381 backup tool and #6362 read-back live but not exercised; #6347/#6332 desktop parts need 0.1.59. **Owner decisions today:** the learned-preferences log lives in Settings → General (not Lessons Learned); stop the job that saved preferences from agent text (#6406); keep the 15 rows it already saved; revoke the July public deck link — done. **Next:** merge the open PRs; PREFS switch-on per the runbook (runner rebuild before the worker switch); owner installs desktop 0.1.59; switches B → C; live re-tests one at a time; re-run the restore rehearsal with #6381. PR states re-read from GitHub at 2026-10-08T08:50Z (16:50 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-08T08:50Z reports `604b0e0964` (stamped 08:48:10Z; main, #6402 from another session); every PR listed as live was verified as an ancestor of it with `git merge-base --is-ancestor`. Main head is `ec244a558f` (#6391, another session), ahead of live. Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times). Review verdicts, the turn-learner switch-on runbook and the live-proof findings are as reported in the private evidence and were NOT re-run for this record. Switch values were NOT read from the live server for this record (the runbook's read-only check at 07:20Z found all five learner switches absent). Previous checkpoint follows. **New workstream (owner ruling 2026-10-08): Agents learn your preferences (async).** Agents remember the owner's preferences even when only hinted. It runs off the reply path: after the reply is sent, a cheap background model scans the turn plus the agent id. Clear requests are saved; hinted ones are saved as "learned" with undo; unsure ones are asked once. Only the owner's own words count (never guests, pasted text or other room members). Display: Settings → General gets a "What your agents learned about you" log (preference; source "You said it" / "Agent noticed"; quoted words; which agent; when; Keep / Change / Remove), linked to the existing tamper-proof preference history. NOT Lessons Learned (that page is agent mistakes shared across all agents, so wrong audience and a leak risk). Tasks, all pending: (1) fix the "I could not record that" bug (in progress); (2) design plan (in progress); (3) background queue + scanner (flag off); (4) Settings log UI; (5) ask-once confirmations; later: the same pipe for corrections / frustration detection, promised follow-ups and failed-tool flags. Nothing merged, deployed or switched on. **2026-10-08 (~00:56Z): 5 more PRs live, 2 more packets applied, restore rehearsal PASSED (public scope), desktop 0.1.59 RC ready for the owner; full W7 NOT accepted.** Production code is main `0cb2eed5ff`. **Merged and live since the last record:** [#6330](https://github.com/jtobkin/suprafx-platform/pull/6330) cards show real agents (19:38:37Z); [#6333](https://github.com/jtobkin/suprafx-platform/pull/6333) a plain goal always yields a plan (20:08:40Z); [#6249](https://github.com/jtobkin/suprafx-platform/pull/6249) interrupted Re-execute never wedges — "Discard this run" (21:01:32Z); [#6334](https://github.com/jtobkin/suprafx-platform/pull/6334) raw tool tags hidden, never executed from text (21:02:00Z); [#6332](https://github.com/jtobkin/suprafx-platform/pull/6332) Mission Control tasks self-heal; switch A on by default with it (23:51:25Z). [#6373](https://github.com/jtobkin/suprafx-platform/pull/6373) CI native-Postgres flake fix merged 2026-10-08 00:35:52Z (deploy pending). **Packets applied and verified since:** `20261008100000` (#6361, ~19:51Z), `20261008110000` (#6368, ~20:53Z). **Open (20):** #6259 #6277 #6287 #6298 #6301 #6316 #6336 #6344 #6345 #6347 #6354 (reviewed earlier) and new, reviewed and queued: #6356 #6361 #6362 #6368 #6369 #6372 #6374 #6377 #6381. **R3 restore rehearsal PASSED** for the backup tool's scope (public + migration ledger; 867/867 tables exact; production contact 20 min, site always 200, no write; deploy lock held 51 min); 339 owner/agent schemas are outside that scope — [#6381](https://github.com/jtobkin/suprafx-platform/pull/6381) widens it (open). **Desktop 0.1.59 RC** built and qualified in hidden mode (all checks PASS); relay connect and a live project turn need the owner at install; not published or installed. **Security catches:** backup-tool lock exhaustion when widened to every owner schema (caught in review of #6381, fixed before merge); live privacy leaks in rooms with guests, check-ins, routines and deck shares — no current exposure (0 share links, 1 guest), fixes [#6369](https://github.com/jtobkin/suprafx-platform/pull/6369) (main) + [#6368](https://github.com/jtobkin/suprafx-platform/pull/6368) (switch-gated) + [#6377](https://github.com/jtobkin/suprafx-platform/pull/6377), all open; deploy build-arg secrets visible in the web host's process list — rotation prep awaits the owner's yes (not verified here). **Owner rulings:** cut off removed members immediately; park stale queued jobs (233); keep old House Rules approvals; restore test with our own tool in quiet hours; remove backup-test leftovers and old restore copies from the web host (done). **Telegram still not linked**, so the drain owner alert cannot be delivered. **Next:** merge the open PRs; owner installs desktop 0.1.59; switches B → C; live re-tests one at a time; #6381 then re-run the rehearsal for owner/agent schemas; V1 and I1 release closure. PR states re-read from GitHub at 2026-10-08T00:55Z (08:55 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-08T00:55:56Z reports `0cb2eed5ff` (main, #6359 from another session); every PR listed as live was verified as an ancestor of it with `git merge-base --is-ancestor`. #6373 (CI only) merged 00:35:52Z and is main head, not yet in the live build. Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times). The restore rehearsal, release audit, desktop RC qualification and review verdicts are as reported in the private evidence and were NOT re-run for this record. Switch values were NOT read from the live server (the read is blocked for agents). Previous checkpoint follows. **2026-10-08 (2026-10-07 ~19:40Z): 8 more PRs merged and live, 4 more packets applied, switch-on plan written; full W7 NOT accepted.** Production code is main `24273f41e9`. The owner paused the project at 2026-10-07 16:10Z (nothing half-applied on production) and it resumed at 18:20Z. **Merged and live since the last record:** [#6285](https://github.com/jtobkin/suprafx-platform/pull/6285) X1 follow-ups (09:21:26Z); [#6300](https://github.com/jtobkin/suprafx-platform/pull/6300) members no longer read the owner's recalled lessons/skills (10:29:42Z); [#6311](https://github.com/jtobkin/suprafx-platform/pull/6311) Mission Control shows the true end state (10:48:13Z); [#6315](https://github.com/jtobkin/suprafx-platform/pull/6315) e2e harness S1–S13 matches main (11:25:54Z); [#6321](https://github.com/jtobkin/suprafx-platform/pull/6321) chat finish-error diagnostics (12:09:04Z); [#6258](https://github.com/jtobkin/suprafx-platform/pull/6258) runtime role packet record (14:25:02Z); [#6255](https://github.com/jtobkin/suprafx-platform/pull/6255) a drained project says so and the owner is told (14:48:22Z); [#6343](https://github.com/jtobkin/suprafx-platform/pull/6343) desktop: project Codex/Grok turns run in an isolated home (18:19:03Z; reaches users only in desktop 0.1.59). **Packets applied and verified since:** `20261007134500` (#6332, ~09:25Z), `20261007140000` (#6336, ~10:42Z), `20261007152000` (#6344, ~12:43Z), `20261007160000` (#6354, ~15:10Z); `20261008100000` (#6361) pending. **Open (19):** 17 reviewed PASS, waiting for box-ci GREEN (2 shared slots): #6249 #6259 #6277 #6287 #6298 #6301 #6316 #6330 #6332 #6333 #6334 #6336 #6344 #6345 #6347 #6354 (stacked PRs retarget to main when their base merges); newer: [#6356](https://github.com/jtobkin/suprafx-platform/pull/6356) chat keeps the real error when a model attempt fails (diagnostics only) and [#6361](https://github.com/jtobkin/suprafx-platform/pull/6361) removed members lose presence at once (stacked on #6354). **Switch-on plan (private activation runbook; nothing run yet; one switch per window, 30 min watch, owner-run):** A background-queue expiry turns on by itself when #6332 merges (pre-check returned 0 rows); B owner-only live channel `SUPRAOS_RELAY_OWNER_TOPIC_V1` after #6336; C narrow DB login (re-run the pre-switch check, owner runs the switch, KEEP only after signed-in pages return 200); D–F project switches need desktop 0.1.59 (version claimed, not built) plus the open project PRs. **Security catches by independent review this week:** grant revoke IDOR (another account could revoke an owner's grant; fixed in #6257, merged); prompt-injection tool execution in #6334 v1 (a tool written as text could run; fixed before merge); renderer argument injection in #6343 (fixed before merge); desktop trusted-exec — pages could choose which program runs and where (#6347, open); Realtime notice flooding from the member cut-off trigger (#6354, bounded before merge). **Owner rulings:** cut off removed members immediately (not after the 15-minute token expiry) — #6354/#6361; park stale queued jobs (233 parked). **Telegram not linked:** the owner has no Telegram destination and no Mission Control owner alert has ever been delivered on production, so the "owner told once" half of the drain cannot pass until the owner links Telegram (up to 4 old pending alerts may then send). **Next:** merge the 17 reviewed PRs; switch-ons A → B → C; desktop 0.1.59 RC after #6332 #6347 merge; live re-tests one at a time (Re-execute recovery, Stop while running, drain + owner alert); presence cut-off; chat finish-error root cause. PR states re-read from GitHub at 2026-10-07T19:37Z (2026-10-08 03:37 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-07T19:37:27Z reports `24273f41e9` (main; every merged PR below verified as an ancestor of it with `git merge-base --is-ancestor`). Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times); review verdicts, the activation runbook and the re-test plan are as reported in the private handoff/evidence and were NOT re-read on production for this record. Previous checkpoint follows. **2026-10-07 ~07:50Z: MC flow works live with the desktop app open; full W7 NOT accepted.** Production code is main `8e4d2d44b0`. **Live rehearsal (2026-10-07):** the owner's Mission Control flow works live once the SupraOS Build desktop app is open. Mission Control tasks run ONLY through the desktop app today (cloud runners take chat, routine and explain work only); with the app closed since 2026-10-05 and two leftover lock folders holding both slots, tasks never ran and showed "Execution failed". The locks were cleared; 233 stale queued jobs (oldest 2026-09-14) were parked as dead-letter on the owner's instruction; a 2-task project then finished in ~70 s (06:15:26Z → 06:16:32Z). Fix [#6332](https://github.com/jtobkin/suprafx-platform/pull/6332) (open): stale lock self-heals, an offline message replaces the generic failure, queue priority + expiry; packet `20261007134500` scheduled 09:25Z. **Merged and live since the last record:** 2026-10-06 #6233 #6239 #6246 #6253 #6254 #6261 #6263 #6270; 2026-10-07 #6252 (02:58Z) #6275 (03:09Z) #6256 (03:38Z) #6276 (03:41Z) #6283 (03:41Z) #6274 (03:42Z) #6257 (04:12:40Z) #6247 (04:12:59Z) #6289 (04:13Z). **Packets applied since:** `20261006151000` (#6277), `20261006115900` (#6287, after a deadlock fix), `20261006153000` (#6301) — code PRs still OPEN; `20261007134500` (#6332) scheduled 09:25Z; `20261007140000` (#6336) pending. **Merge freeze** 07:06Z → ~09:20Z for the owner's Agent VM demo (another session). PR states re-read from GitHub at 2026-10-07T07:53Z; `https://supraos.ai/api/version` read anonymously 2026-10-07T07:54Z reports `8e4d2d44b0` (main; every merged PR below verified as an ancestor of it). Packet applies, the rehearsal and review verdicts are as reported in the private handoff (2026-10-07 early → ~07:50Z) and were NOT re-read on production for this record. Previous checkpoint follows. **W7 DRAIN/RERUN: 3 of 3 PASS LIVE (A closed 09:09:21Z); full W7 NOT accepted.** Production code is main `e89acee6d2`. **Live test A CLOSED live:** the drained plan `ee4c97bc` (project `bacf0dc8`) became `failed` at 09:09:21Z 2026-10-06, 34 s after #6239 went live (08:54:46Z merge; live 09:08:47Z); the project became `failed` too. The owner was NOT notified — that plan was finished by the v1 finaliser before #6255 (known gap; #6255 makes a drained project say so and tells the owner; its packet `20261006030000` is applied, code PR OPEN). The next live drain after #6255 should notify. Production packets applied 2026-10-06, each APPLIED AND VERIFIED: `20261006020000` (#6239, 07:12:36Z), then 20261006030000 (#6255), 20261006040000 (#6252), 20261006050000 (#6247), 20261006060000 (#6249), 20261006070000 (#6254), 20261006110000, 111000, 112000, 114000, 115000, 115500 (#6259), 20261006120000 (#6258, runtime role), 20261006141000 (#6263). These are schema-first installs: except #6239, their code PRs are still OPEN; the #6259 switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. **Runtime role (R3B): installed, switch ROLLED BACK.** Packet `20261006120000` (#6258, OPEN) applied and verified; orphan owner schemas fixed by the owner (1 re-linked, 4 empty ones renamed as archived, 0 left); the owner set the role's login and a login through the connection pooler passed. The switch at ~09:19Z broke public-table callers (Settings → General returned 503) and was ROLLED BACK at ~09:52Z (pages verified 200). The role keeps its login but is unused. Fix [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (public-table callers use the admin connection) is in review (needs a type fix, an import guard and pre-switch privilege checks). Do NOT re-switch until #6270 is live and the privilege check passes. **Reviews PASS (open, merge when green):** W2 [#6253](https://github.com/jtobkin/suprafx-platform/pull/6253); W3–W6 [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) (includes a security fix: another account could revoke an owner's grant); X2/X3 [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261); X4/X5 [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254); canvas approvals [#6263](https://github.com/jtobkin/suprafx-platform/pull/6263); project server B1/C2 server/M1 [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) (switch off); relay client C1/C2 client [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256); also [#6246](https://github.com/jtobkin/suprafx-platform/pull/6246) House Rules apply to computer agents, [#6247](https://github.com/jtobkin/suprafx-platform/pull/6247) un-archive hole + one grant card under load, [#6252](https://github.com/jtobkin/suprafx-platform/pull/6252) owner's last decision finishes the project / Stop on a critical task drains it. Open, review status not recorded here: [#6249](https://github.com/jtobkin/suprafx-platform/pull/6249) interrupted Re-execute no longer wedges a project; [#6255](https://github.com/jtobkin/suprafx-platform/pull/6255) drained project says so and the owner is told; [#6258](https://github.com/jtobkin/suprafx-platform/pull/6258) runtime role packet; [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (in review). **New lanes running:** W7 effects parity; safe cancellation + 0-task voice planning; X1 context entries. **Follow-ups (not blockers):** #6246 floors task cost at $0.08, so an "ask above X" rule under $0.08 asks on every task; #6247 archived-project toggle returns 400; #6252 a review "reject" on a critical task now drains the plan (undisclosed); #6253 a crash between email claim and send leaves no history line; #6257 spawn retry does not return the child id; #6259 before switch-on: transport deletes blocked by observations (desktop re-sign-in 500), old poll hands out bound commands unchecked; #6254 script expectations need a writable role and two corrected lines. **Next:** merge the reviewed PRs when green; land #6270 then re-try the runtime-role switch; prove the next live drain notifies the owner; W7 effects parity, safe cancellation, X1. PR states re-read from GitHub at 2026-10-06T10:11Z: #6239 MERGED 08:54:46Z, #6233 MERGED 09:26:41Z, #6230 MERGED 09:37:10Z (main `e89acee6d2` = live); #6246 #6247 #6249 #6252 #6253 #6254 #6255 #6256 #6257 #6258 #6259 #6261 #6263 #6270 OPEN. `https://supraos.ai/api/version` read anonymously at 2026-10-06T10:11Z reports `e89acee6d2` (stamped 10:07:17Z). Packet applies, the runtime-role switch/rollback and review verdicts are as reported in the private handoff (~07:12Z–10:00Z 2026-10-06) and were NOT re-read on production for this record.

**Current candidate record:** `ac4819095585eed003eb0c510b0a8c8608d5e73f`, tree `49bf08e3354a115783635eebfa4801dfa953bb6c`. Security: box-ci/security-gates SUCCESS on ac48190955 (51 steps; macOS Native Land not run). Previous head 3214f4849e: FAILURE (whole unit tree 2 failed / 55,609 passed / 374 skipped across 4,508 files; scoped changed-file TypeScript check 5 errors); build: box-ci/production-build SUCCESS on ac48190955 (7 steps). Previous head 3214f4849e: ERROR (not built because security gates failed); macOS Native Land: Not run (not part of box-ci). Merged: True; deployed: True; activated: True; verified live: yes — 3 of 3 behaviours PASS on production (A CLOSED 09:09:21Z 2026-10-06 after #6239; B and C 2026-10-05); #6255 (drain owner alert) merged 2026-10-07 14:48Z but the owner has no Telegram destination, so the alert cannot be delivered; full W7 task NOT accepted; Mission Control tasks run only through the owner's desktop app. Scope: Composed W7 failure-drain/rerun candidate (partial W7; full scope open). Frozen candidate ac48190955 = 3214f4849e + fix commit 867a5f2114 + clean merge of origin/main 7a10b7a3fc; required CI GREEN and independent trailing audit PASS 5/5 at that commit. Squash-merged 2026-10-05 06:11:22Z as main 55a12f0da9 (PR #6196); installed 06:03–06:10Z; deployed 06:24:35Z; activated. Stabilisation (same day, 12:59–22:23Z): 14 PRs merged via merge-if-green.sh with an independent review each; five extra packets installed (ledger 743); live = main 0d25a537b4. Follow-ups merged 2026-10-06: #6226 #6227 #6229 #6239 (finalisation after owner resolution; packet `20261006020000`) #6233 #6230; live = main `e89acee6d2`. Verified live: 3 of 3 behaviours PASS (A CLOSED 09:09:21Z 2026-10-06; B PASS 17:36Z, C PASS 06:35Z 2026-10-05); the full W7 task is NOT accepted. All four scheduler switches ON (approval siblings since 03:09:23Z 2026-10-06). 2026-10-06/07: further follow-ups merged (#6233 #6239 #6246 #6253 #6254 #6261 #6263 #6270; #6252 (02:58Z) #6275 (03:09Z) #6256 (03:38Z) #6276 (03:41Z) #6283 (03:41Z) #6274 (03:42Z) #6257 (04:12:40Z) #6247 (04:12:59Z) #6289 (04:13Z)); live = main `8e4d2d44b0` (read 2026-10-07T07:54Z). 2026-10-07 later: #6285 #6300 #6311 #6315 #6321 #6258 #6255 #6343 merged; packets 20261007134500/140000/152000/160000 applied; live = main `24273f41e9` (read 2026-10-07T19:37Z). 2026-10-07/08: #6330 #6333 #6249 #6334 #6332 merged (live = main `0cb2eed5ff`, read 2026-10-08T00:55Z), #6373 merged (CI only); packets 20261008100000/110000 applied. 2026-10-08 later: #6373 #6277 #6381 #6347 #6369 #6356 #6372 #6362 #6395 #6396 merged (live = main `604b0e0964`, read 2026-10-08T08:50Z); packets 20261008130000/151500 applied.. Observed: 2026-10-08T08:50:00Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.


## Status 2026-10-08 ~08:50Z — 10 more PRs live; PREFS P0–P5 built and reviewed, all switches off (read this first)

PR states re-read from GitHub at 2026-10-08T08:50Z (16:50 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-08T08:50Z reports `604b0e0964` (stamped 08:48:10Z; main, #6402 from another session); every PR listed as live was verified as an ancestor of it with `git merge-base --is-ancestor`. Main head is `ec244a558f` (#6391, another session), ahead of live. Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times). Review verdicts, the turn-learner switch-on runbook and the live-proof findings are as reported in the private evidence and were NOT re-run for this record. Switch values were NOT read from the live server for this record (the runbook's read-only check at 07:20Z found all five learner switches absent).

| PR | State (GitHub, 2026-10-08T08:50Z) | What |
| --- | --- | --- |
| #6373 | MERGED 2026-10-08 00:35Z, live | CI: native Postgres test clusters start reliably (CI only) |
| #6277 | MERGED 2026-10-08 01:36Z, live | Stop works while a task is running; no 0-task plan is saved (packet 151000) |
| #6381 | MERGED 2026-10-08 02:43Z, live | backup tool covers every owner and agent schema; does not block deploys |
| #6347 | MERGED 2026-10-08 04:03Z, live | desktop: pages cannot choose program or folder (web side live; desktop side ships in 0.1.59) |
| #6369 | MERGED 2026-10-08 04:36Z, live | privacy: owner-private memory never reaches room guests, routines or project members |
| #6356 | MERGED 2026-10-08 05:17Z, live | chat keeps the real error when a model attempt fails |
| #6372 | MERGED 2026-10-08 05:36Z, live | polish: grant durations text, House Rules cost-floor warning, card counts, alert-channel notice |
| #6362 | MERGED 2026-10-08 06:11Z, live | X1: read back Mission Control task context receipts (owner only) |
| #6395 | MERGED 2026-10-08 06:32Z, live | Mission Control project page: agent lanes show real agents |
| #6396 | MERGED 2026-10-08 07:03Z, live | "I could not record that": agent preference saves no longer fail when the model echoes owner quiet hours |
| #6259 | OPEN, review PASS | project server B1/C2 server/M1, switch OFF (packets applied) |
| #6287 | OPEN, review PASS, stacked on #6259 | switch blockers (packet 115900 applied) |
| #6298 | OPEN, review PASS, stacked on #6259 | B2: owner-private inputs out of shared prompts |
| #6301 | OPEN, review PASS | review/Stop effects via effect intents (packet 153000 applied) |
| #6316 | OPEN, review PASS, stacked on #6259 | M2: members read only current-publication results |
| #6336 | OPEN, review PASS | M3 owner-only Realtime topic, switch OFF (packet 140000 applied) |
| #6344 | OPEN, review PASS, stacked on #6301 | review notes reach the agent's own memory (packet 152000 applied) |
| #6345 | OPEN, review PASS, stacked on #6316 | redaction on member results |
| #6354 | OPEN, review PASS, stacked on #6336 | removed members lose the live feed at once (packet 160000 applied) |
| #6361 | OPEN, reviewed, stacked on #6354 | removed members lose presence at once (packet 20261008100000 applied) |
| #6368 | OPEN, reviewed, stacked on #6298 | B2-2: remaining private-input producers, switch-gated (packet 20261008110000 applied) |
| #6374 | OPEN, reviewed, now on main | receipt panel ("what each agent knew") + in-app failure bell |
| #6377 | OPEN, reviewed, rebuilt onto main | approved-tools list for shared rooms; late joiners never see earlier private text |
| #6400 | OPEN, reviewed | deploy secrets via BuildKit, not build args (rotation not done) |
| #6401 | OPEN, reviewed | PREFS P0+P1: tables + post-reply tickets, switch off (packet 20261008130000 applied) |
| #6399 | OPEN, reviewed, after #6401 | PREFS P2: background scanner in test mode, switch off |
| #6398 | OPEN, reviewed, after #6401 | PREFS P3: "What your agents learned about you" in Settings → General, switch off |
| #6411 | OPEN, reviewed, stacked on #6399 | PREFS P4: auto-save with undo + daily review card, switch off |
| #6410 | OPEN, reviewed, stacked on #6398 | PREFS P5: ask once in chat, switch off |
| #6419 | OPEN, reviewed, stacked on #6399 | PREFS signals: agents notice when you correct them, test mode, switch off (packet 20261008151500 applied) |
| #6424 | OPEN, review not recorded, stacked on #6419 | PREFS promise tracking: agents keep track of what they promised you, test mode, switch off |
| #6406 | OPEN, reviewed | only the owner's own words create preferences (stop saving preferences from agent text) |
| #6423 | OPEN, review not recorded | chat dock shows a plain sentence instead of a JSON error; stuck Mission Control projects say "Waiting for you" |
| #6428 | OPEN, review not recorded | chat dock is full height again |

**Packets live (this project, all APPLIED AND VERIFIED):** 2026-10-06: 020000, 030000, 040000, 050000, 060000, 070000, 110000, 111000, 112000, 114000, 115000, 115500, 115900, 120000, 141000, 151000, 153000; 2026-10-07: 134500, 140000, 152000, 160000; 2026-10-08 series: 20261008100000 (#6361), 20261008110000 (#6368), 20261008130000 (#6401, ~03:20Z), 20261008151500 (#6419, ~08:18Z).

**PREFS — agents learn your preferences (delivery item, outside the 33 tracked tasks):** Status 2026-10-08 ~08:50Z: P0–P5 built and independently reviewed, all OPEN: P0+P1 tables + post-reply tickets [#6401](https://github.com/jtobkin/suprafx-platform/pull/6401) (packet `20261008130000` APPLIED AND VERIFIED ~03:20Z; tables empty), P2 background scanner [#6399](https://github.com/jtobkin/suprafx-platform/pull/6399), P3 Settings → General log [#6398](https://github.com/jtobkin/suprafx-platform/pull/6398), P4 auto-save with undo + daily review card [#6411](https://github.com/jtobkin/suprafx-platform/pull/6411), P5 ask once [#6410](https://github.com/jtobkin/suprafx-platform/pull/6410). Same pipe: corrections/frustration signals [#6419](https://github.com/jtobkin/suprafx-platform/pull/6419) (reviewed; packet `20261008151500` APPLIED AND VERIFIED ~08:18Z) and promise tracking [#6424](https://github.com/jtobkin/suprafx-platform/pull/6424) (built; review not recorded), both test mode. "I could not record that" fix [#6396](https://github.com/jtobkin/suprafx-platform/pull/6396) MERGED 07:03Z and live. Stop saving preferences from agent text [#6406](https://github.com/jtobkin/suprafx-platform/pull/6406) reviewed, OPEN. **All five learner switches are off** (absent at the 07:20Z read-only check). Switch-on runbook written (enqueue → runner rebuild → worker → Settings log → auto-save → ask once; each with an off script): the cloud chat runner image predates this work and deploys do not rebuild it, so **a runner rebuild is needed before the worker switch** (it also ships earlier runner changes for the first time; prove chat still answers after). Auto-save waits for ≥30 reviewed items with ≥90 % kept. Nothing switched on.

**Live proofs (read-only, plus one signed-in look):** #6372 seen on screen signed in — grants page shows "At its limit" and the duration copy; Mission Control shows the "link Telegram" notice. #6369 privacy fence: live and ordered before any context is read, but **never exercised on a shared audience** — none exists in production; nothing leaked since deploy; proving it needs a real guest or member (owner call). #6362: 4 of 5 stored receipts would read back `confirmed`; signed-in response not seen. #6277 Stop and #6356 error cause: live, not exercised. #6381: on main, not run. #6347/#6332: desktop parts need 0.1.59 (owner's Mac runs 0.1.58).

**Owner decisions today:** the learned-preferences log lives in Settings → General ("What your agents learned about you"), not Lessons Learned; stop the job that saved preferences from agent text (#6406); keep the 15 rows it already saved; revoke the July public deck link — **done** (0 shared projects now; a direct database change, no tamper-proof revoke event written).

**Switches:** A on by default; B–F and all five PREFS switches OFF. Telegram still not linked, so the drain owner alert cannot be delivered.

**Next, in order:** merge the 24 open PRs (stacked ones retarget after their base); PREFS switch-on per the runbook — enqueue, then rebuild the cloud chat runner (deploys do not rebuild it), then worker, Settings log, auto-save (after ≥30 reviewed, ≥90 % kept), ask once; owner installs desktop 0.1.59; switches B → C; live re-tests one at a time (#6249, #6277, #6255 after Telegram); re-run the restore rehearsal with #6381; V1, I1, U1 release closure. Owner decisions open: deploy-secret rotation after #6400; pooler client limit before C; link Telegram; install desktop 0.1.59; a real shared audience to prove the #6369 fence.

## Status 2026-10-08 ~00:56Z — 5 more PRs live; restore rehearsal PASSED (public scope); desktop 0.1.59 RC awaits the owner (read this first)

PR states re-read from GitHub at 2026-10-08T00:55Z (08:55 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-08T00:55:56Z reports `0cb2eed5ff` (main, #6359 from another session); every PR listed as live was verified as an ancestor of it with `git merge-base --is-ancestor`. #6373 (CI only) merged 00:35:52Z and is main head, not yet in the live build. Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times). The restore rehearsal, release audit, desktop RC qualification and review verdicts are as reported in the private evidence and were NOT re-run for this record. Switch values were NOT read from the live server (the read is blocked for agents).

| PR | State (GitHub, 2026-10-08T00:55Z) | What |
| --- | --- | --- |
| #6330 | MERGED 2026-10-07 19:38Z, live | cards show real agents (no "Agent not found") |
| #6333 | MERGED 2026-10-07 20:08Z, live | a plain goal always yields a plan |
| #6249 | MERGED 2026-10-07 21:01Z, live | interrupted Re-execute never wedges; "Discard this run" (packet 060000) |
| #6334 | MERGED 2026-10-07 21:02Z, live | raw tool tags hidden; never executed from text |
| #6332 | MERGED 2026-10-07 23:51Z, live | MC tasks self-heal; switch A on by default (packet 134500) |
| #6373 | MERGED 2026-10-08 00:35Z, deploy pending | CI: native Postgres test clusters start reliably (CI only) |
| #6343 | MERGED 2026-10-07 18:19Z, live (web) | desktop Codex/Grok isolation; ships in desktop 0.1.59 |
| #6259 | OPEN, review PASS | project server B1/C2 server/M1, switch OFF (packets applied) |
| #6277 | OPEN, review PASS | Stop while running; no 0-task plan (packet 151000 applied) |
| #6287 | OPEN, review PASS, stacked on #6259 | switch blockers (packet 115900 applied) |
| #6298 | OPEN, review PASS, stacked on #6259 | B2: owner-private inputs out of shared prompts |
| #6301 | OPEN, review PASS | review/Stop effects via effect intents (packet 153000 applied) |
| #6316 | OPEN, review PASS, stacked on #6259 | M2: members read only current-publication results |
| #6336 | OPEN, review PASS | M3 owner-only Realtime topic, switch OFF (packet 140000 applied) |
| #6344 | OPEN, review PASS, stacked on #6301 | review notes reach the agent's own memory (packet 152000 applied) |
| #6345 | OPEN, review PASS, stacked on #6316 | redaction on member results |
| #6347 | OPEN, review PASS | desktop: pages cannot choose program or folder (carried in the 0.1.59 RC) |
| #6354 | OPEN, review PASS, stacked on #6336 | removed members lose the live feed at once (packet 160000 applied) |
| #6356 | OPEN, reviewed, queued | chat keeps the real error when a model attempt fails |
| #6361 | OPEN, reviewed, stacked on #6354 | removed members lose presence at once (packet 20261008100000 applied) |
| #6362 | OPEN, reviewed, queued | X1: read back MC task context receipts (owner only) |
| #6368 | OPEN, reviewed, stacked on #6298 | B2-2: remaining private-input producers, switch-gated (packet 20261008110000 applied) |
| #6369 | OPEN, reviewed, queued | privacy: live leaks to room guests, routines, members fixed |
| #6372 | OPEN, reviewed (redone on design-system markup) | polish: grant durations text, House Rules cost-floor warning, card counts, alert-channel notice |
| #6374 | OPEN, reviewed, stacked on #6362 | receipt panel ("what each agent knew") + in-app failure bell |
| #6377 | OPEN, reviewed, stacked on #6369 | approved-tools list for shared rooms; late joiners never see earlier private text |
| #6381 | OPEN, reviewed | backup tool covers every owner/agent schema; does not block deploys (lock-exhaustion bug fixed) |

**Packets live (this project, all APPLIED AND VERIFIED):** 2026-10-06: 020000, 030000, 040000, 050000, 060000, 070000, 110000, 111000, 112000, 114000, 115000, 115500, 115900, 120000, 141000, 151000, 153000; 2026-10-07: 134500, 140000, 152000, 160000; 2026-10-08 series: 20261008100000 (#6361, ~19:51Z), 20261008110000 (#6368, ~20:53Z). Release audit: every function these packets define matches committed code by md5 (no drift); several packets are live ahead of their still-open code PRs (expected, schema first).

**Switches:** A (background-queue expiry) is on by default since #6332 went live; B–F stay OFF (not re-read from the live server). Next windows, owner-run, one at a time: B after #6336; C after the pooler client-limit check and a fresh pre-switch check; D–F after desktop 0.1.59 is installed and the project PRs merge.

**R3 restore rehearsal — PASS for the tool's scope** (2026-10-07 20:20–21:20Z, owner-approved quiet hours): read-only exported snapshot; 867/867 tables restored with exact row counts (54.1 M rows); ledger 773 equal; schema digest equal; roles/grants reproduced; packet 20261007134500 round trip PASS in the copy. Production: 20.4 min contact, site 69/69 samples HTTP 200 (0 over 2 s), 0 blocked sessions, no write; the deploy lock was held 51 min. **Not covered:** 339 owner/agent/node schemas (2,022 tables), auth/storage/vault/realtime and storage files; snapshot taken with writers running. #6381 widens the tool to every owner and agent schema (open), then re-run.

**Desktop 0.1.59 release candidate — qualified hidden, awaiting owner install:** built from main 24273f41e9 + #6347 + #6332 + version bump + hidden test mode and a sign-in leak fix. PASS: launch, invisible run, stale-lock self-heal, signed-out queue safety, IPC hardening, Codex/Grok isolation (real CLIs), sign-in leak closed, clean quit, installed app untouched. **Not proven:** relay connect and a live project turn (need the owner's admitted account). Not published, not installed. Next free version 0.1.60.

**Security catches (this round):** backup-tool lock exhaustion when widened to every owner schema (caught in review of #6381; fixed before merge); live privacy leaks — owner-private memory could reach room guests, check-ins, routines and Mission Control deck shares; **no current exposure** (0 share links, 1 guest); fixes #6369 (main), #6368 (switch-gated), #6377 — all open; deploy build-arg secrets visible in the web host's process list — rotation prep awaits the owner's yes (not verified here). Earlier this week: grant revoke IDOR (#6257), prompt-injection tool execution (#6334 v1), renderer argument injection (#6343), desktop trusted exec (#6347), Realtime notice flood (#6354), re-sign-in deadlock (#6287).

**Owner rulings:** cut off removed members immediately; park stale queued jobs (233); keep old House Rules approvals; demo freeze then resume; restore test with our own tool in quiet hours; remove backup-test leftovers and old restore copies from the web host (done; site 200).

**Telegram not linked:** the drain owner alert (#6255) is recorded but cannot be delivered until the owner links Telegram.

**Outside this project (handed over):** #6235 (CRM intake, another session) packet 20261006143000 is on main but not applied to production; live code falls back.

**New workstream (owner ruling 2026-10-08): Agents learn your preferences (async).** Agents remember the owner's preferences even when only hinted. It runs off the reply path: after the reply is sent, a cheap background model scans the turn plus the agent id. Clear requests are saved; hinted ones are saved as "learned" with undo; unsure ones are asked once. Only the owner's own words count (never guests, pasted text or other room members). Display: Settings → General gets a "What your agents learned about you" log (preference; source "You said it" / "Agent noticed"; quoted words; which agent; when; Keep / Change / Remove), linked to the existing tamper-proof preference history. NOT Lessons Learned (that page is agent mistakes shared across all agents, so wrong audience and a leak risk). Tasks, all pending: (1) fix the "I could not record that" bug (in progress); (2) design plan (in progress); (3) background queue + scanner (flag off); (4) Settings log UI; (5) ask-once confirmations; later: the same pipe for corrections / frustration detection, promised follow-ups and failed-tool flags. Nothing merged, deployed or switched on.

**Next, in order:** merge the 20 open PRs (stacked ones retarget to main after their base); owner installs desktop 0.1.59; switches B → C; live re-tests one at a time — Re-execute recovery (#6249, live), Stop while running (#6277), drain + owner alert (#6255, needs Telegram); #6381 then re-run the restore rehearsal; chat finish-error root cause (#6356); V1 16-behaviour acceptance; I1 frozen final head + Native Land + composed review; U1 owner sign-off (plain-English owner guide written). Owner decisions open: pooler client limit before C; build-arg secret rotation; e2e harness as a required check; Stripe Link, QA invite, provider accounts; link Telegram; install desktop 0.1.59.

## Status 2026-10-08 (2026-10-07 ~19:40Z) — paused 16:10Z, resumed 18:20Z; 8 more PRs live; switch-on plan written (read this first)

PR states re-read from GitHub at 2026-10-07T19:37Z (2026-10-08 03:37 HKT); `https://supraos.ai/api/version` read anonymously 2026-10-07T19:37:27Z reports `24273f41e9` (main; every merged PR below verified as an ancestor of it with `git merge-base --is-ancestor`). Packet applies are taken from the private apply logs (each ends "APPLIED AND VERIFIED"; times are log-write times); review verdicts, the activation runbook and the re-test plan are as reported in the private handoff/evidence and were NOT re-read on production for this record.

| PR | State (GitHub, 2026-10-07T19:37Z) | What |
| --- | --- | --- |
| #6285 | MERGED 2026-10-07 09:21Z | X1 follow-ups: legacy Telegram entry checks, cancel into delegation + voice workflows |
| #6300 | MERGED 2026-10-07 10:29Z | members no longer read the owner's recalled lessons and skills |
| #6311 | MERGED 2026-10-07 10:48Z | Mission Control hero/status show the true end state |
| #6315 | MERGED 2026-10-07 11:25Z | e2e harness S1–S13 matches main |
| #6321 | MERGED 2026-10-07 12:09Z | chat: record why a reply failed (diagnostics only) |
| #6258 | MERGED 2026-10-07 14:25Z | runtime role packet (applied 2026-10-06) |
| #6255 | MERGED 2026-10-07 14:48Z | drained project says so; owner told (alert recorded; no Telegram linked) |
| #6343 | MERGED 2026-10-07 18:19Z | desktop: project Codex/Grok turns run in an isolated home (needs desktop 0.1.59) |
| #6249 | OPEN, review PASS | interrupted Re-execute never wedges; Discard from any device (packet 060000 applied) |
| #6259 | OPEN, review PASS | project server B1/C2 server/M1, switch OFF (packets applied) |
| #6277 | OPEN, review PASS | Stop while running; no 0-task plan (packet 151000 applied) |
| #6287 | OPEN, review PASS, stacked on #6259 | re-sign-in deadlock fix; old poll refuses bound commands (packet 115900 applied) |
| #6298 | OPEN, review PASS, stacked on #6259 | B2: owner-private inputs out of shared prompts |
| #6301 | OPEN, review PASS | owner review/Stop effects via effect intents; six dead kinds removed (packet 153000 applied) |
| #6316 | OPEN, review PASS, stacked on #6259 | M2: members read only current-publication results |
| #6330 | OPEN, review PASS | cards show real agents (no "Agent not found") |
| #6332 | OPEN, review PASS | desktop stale-lock self-heal, offline message, MC priority, 24 h expiry (packet 134500 applied; switch A on merge) |
| #6333 | OPEN, review PASS | a plain goal always yields a plan |
| #6334 | OPEN, review PASS | raw tool tags hidden; never executed from text (v1 prompt-injection hole fixed) |
| #6336 | OPEN, review PASS | M3 owner-only Realtime topic, switch OFF (packet 140000 applied) |
| #6344 | OPEN, review PASS, stacked on #6301 | owner review notes reach the agent's own memory (packet 152000 applied) |
| #6345 | OPEN, review PASS, stacked on #6316 | redaction on member results |
| #6347 | OPEN, review PASS | desktop: pages cannot choose which program runs or where |
| #6354 | OPEN, review PASS, stacked on #6336 | removed members lose the live feed at once, switches OFF (packet 160000 applied) |
| #6356 | OPEN | chat keeps the real error when a model attempt fails (diagnostics only) |
| #6361 | OPEN, stacked on #6354 | removed members lose presence at once (packet 20261008100000 pending) |

**Packets live (this project, all APPLIED AND VERIFIED):** 2026-10-06: 020000, 030000, 040000, 050000, 060000, 070000, 110000, 111000, 112000, 114000, 115000, 115500, 115900, 120000, 141000, 151000, 153000; 2026-10-07: 134500, 140000, 152000 (#6344), 160000 (#6354). **Pending:** 20261008100000 (#6361, apply before merge).

**Switch-on plan** (private activation runbook; nothing run on production yet; one switch per window with no merges, packet applies or deploys; 30-minute watch between windows; switches are owner-run, with automatic rollback and a typed KEEP after a signed-in check):
- **A — background-queue expiry** (`SUBSCRIPTION_QUEUE_BACKGROUND_EXPIRY`, unset = on): turns on automatically when #6332 merges; read-only pre-check returned 0 rows (233 stale jobs were already parked).
- **B — owner-only live channel** (`SUPRAOS_RELAY_OWNER_TOPIC_V1`): after #6336 merges; packet 140000 applied.
- **C — narrow owner database login** (runtime role): re-run the pre-switch check (last NO-GO only for "deploy running"); owner runs the switch; KEEP only after signed-in pages return 200. Owner check of the connection-pooler client limit first.
- **D–F — project switches** (`PROJECT_REVIEWED_SOURCE_V1`, `PROJECT_WORKSPACE_COMMANDS_V1`, `PROJECT_AGENT_INPUT_RECOVERY_V1`): blocked until desktop 0.1.59 (version claimed, no build yet; needs #6332 #6347 merged, #6343 merged) is installed and the open project PRs merge.

**Security catches by independent review this week:** grant revoke IDOR (another account could revoke an owner's grant — fixed in #6257, merged 2026-10-07); prompt-injection tool execution in #6334 v1 (fixed before merge); renderer argument injection in #6343 (fixed before merge); desktop trusted-exec (#6347 — pages could choose the program and folder; open); Realtime notice flood from the member cut-off trigger (#6354 — bounded before merge). Also caught: a re-sign-in deadlock (#6287) and the 2026-10-06 runtime-role public-table breakage (rolled back live).

**Owner rulings this session:** cut off removed members immediately rather than after the 15-minute token expiry (#6354 feed, #6361 presence); park stale queued jobs (233 parked as revivable dead-letter).

**Telegram not linked:** the owner has no Telegram destination; no Mission Control owner alert has ever been delivered on production (4 pending for this owner). The drain owner-alert from #6255 is recorded but cannot be delivered until the owner links Telegram; the old pending alerts may then send.

**Live re-tests prepared, not run** (one at a time): Re-execute recovery (#6249), Stop while running (#6277), drain + owner alert (#6255; safest method after #6332: quit the desktop app so each attempt fails plainly). Each waits for its PR to be merged and live.

**Next, in order:** merge the 17 reviewed PRs (box-ci is the bottleneck); switch-ons A → B → C; desktop 0.1.59 release candidate and owner install (unlocks D–F); live re-tests; presence cut-off (#6361) and chat finish-error root cause (#6356); then R3 restore rehearsal, V1 16-behaviour acceptance, I1/R1/D1/D2/U1 release closure. Owner decisions open: pooler client limit before C; host build-arg secret rotation; make the e2e harness a required box-ci step; Stripe Link, QA invite, provider accounts.

## Status 2026-10-07 ~07:50Z — MC flow works live with the desktop app open; 17 PRs merged since the last record; merge freeze for the owner demo (read this first)

PR states re-read from GitHub at 2026-10-07T07:53Z; `https://supraos.ai/api/version` read anonymously 2026-10-07T07:54Z reports `8e4d2d44b0` (main; every merged PR below verified as an ancestor of it). Packet applies, the rehearsal and review verdicts are as reported in the private handoff (2026-10-07 early → ~07:50Z) and were NOT re-read on production for this record.

| PR | State (GitHub, 2026-10-07T07:53Z) | What |
| --- | --- | --- |
| #6233 | MERGED 2026-10-06 09:26Z | a task every agent has failed no longer waits forever; held task alerts the owner |
| #6239 | MERGED 2026-10-06 08:54Z | owner's resolution of an unknown outcome lets a drained plan finish |
| #6246 | MERGED 2026-10-06 10:22Z | House Rules apply to computer agents before work starts |
| #6253 | MERGED 2026-10-06 10:57Z | W2: notifications only reach verified destinations; uncertain sends held |
| #6261 | MERGED 2026-10-06 11:34Z | X2/X3: completed only when the row says so; System Workflow pause/recovery |
| #6263 | MERGED 2026-10-06 12:48Z | canvas-built scheduled workflows use approval continuation |
| #6254 | MERGED 2026-10-06 16:36Z | X4/X5: acceptance proof for retained attempts and approval continuation |
| #6270 | MERGED 2026-10-06 16:37Z | R3B: public-table callers use the admin connection |
| #6252 | MERGED 2026-10-07 02:58Z | W7: owner's last decision finishes the project; Stop on a critical task drains it |
| #6275 | MERGED 2026-10-07 03:09Z | W7 effects: task tools bind to the saved attempt; owner card answers reserved first |
| #6256 | MERGED 2026-10-07 03:38Z | C1/C2 client: isolated context per run, exact-workspace Git |
| #6276 | MERGED 2026-10-07 03:41Z | W7 effects: send tools — a lost reply is an unknown outcome |
| #6283 | MERGED 2026-10-07 03:41Z | AgentOrb test flake fixed |
| #6274 | MERGED 2026-10-07 03:42Z | X1: qualify every agent context entry |
| #6257 | MERGED 2026-10-07 04:12Z | W3–W6 grants (includes SECURITY fix: another account could revoke an owner's grant) |
| #6247 | MERGED 2026-10-07 04:12Z | archived projects cannot be un-archived; one grant card under load |
| #6289 | MERGED 2026-10-07 04:13Z | W7 effects: manual actions obey claim rules; retried child spawn returns the original child |
| #6249 | OPEN | interrupted Re-execute no longer wedges a project (packet applied 2026-10-06) |
| #6255 | OPEN | drained project says so; owner told (packet applied 2026-10-06) |
| #6258 | OPEN | runtime role packet (applied 2026-10-06) |
| #6259 | OPEN | B1 / C2 server / M1 (packets applied; switch OFF) |
| #6277 | OPEN | Stop works while a task runs; no 0-task plan saved (packet 151000 applied) |
| #6285 | OPEN | X1 follow-ups (stacks on #6274) |
| #6287 | OPEN | C2 project switch blockers (packet 115900 applied; stacks on #6259) |
| #6298 | OPEN | B2: no owner-private input in shared background prompts |
| #6300 | OPEN | members no longer read the owner's recalled lessons and skills |
| #6301 | OPEN | W7-4 effects: owner review and Stop go through effect intents (packet 153000 applied) |
| #6311 | OPEN | Mission Control hero/status show the true end state |
| #6315 | OPEN | e2e harness matches today's main; S1–S13 PASS |
| #6316 | OPEN | M2: members read only results bound to the current publication |
| #6321 | OPEN | chat: record why a reply failed after the AI answered (diagnostics) |
| #6330 | OPEN | Mission Control cards show the real agents (no more "Agent not found") |
| #6332 | OPEN | MC tasks self-heal: stale desktop lock, offline message, queue priority + expiry (packet 134500 scheduled 09:25Z) |
| #6333 | OPEN | a plain goal always leads to a plan |
| #6334 | OPEN | chat: a tool written as a tag never runs from text (v1 had a prompt-injection hole, caught in review) |
| #6336 | OPEN | M3: owner-only Realtime channel; switch OFF (packet 140000 pending) |

**Live rehearsal (2026-10-07, done by Claude at the owner's request).** The Mission Control flow works live once the owner's desktop app is open. Tasks run ONLY through the desktop app (its queue is not served by the cloud runners); the app had been closed since 2026-10-05 and two leftover lock folders held both slots, so tasks waited 180 s and showed a generic "Execution failed". After clearing the locks and parking 233 stale queued jobs (oldest 2026-09-14; owner said delete — parked as dead-letter, list kept privately), a 2-task demo project finished in ~70 s. Follow-ups: #6332 (self-heal, offline message, queue expiry); owner question whether Mission Control tasks should also run on cloud runners when the Mac is offline (ruling "chat goes to the cloud first").

**W7 effects parity:** #6275 #6276 #6289 merged and live; #6301 open (packet applied). **Safe cancellation:** #6277 open (packet applied). **X1:** #6274 merged; #6285 open. **B2:** #6298 open. **M2:** #6316 open (stacked on #6259). **M3:** #6336 open, switch OFF, packet pending; owner decision pending on a shorter (15-minute) member Realtime token for revocation. **C2/C2S:** #6259 and #6287 open, all their packets applied, switch `PROJECT_REVIEWED_SOURCE_V1` OFF. **R3B runtime role:** rolled back 2026-10-06; fix #6270 merged and live; re-switch waits for the owner after the Agent VM demo (pre-check passed except "deploy running").

**Security catches:** the grant-revoke hole (another account could revoke an owner's grant) fixed in #6257, merged; a prompt-injection hole in the first version of #6334 was caught by the security review before merge.

**Next.** After the freeze (~09:20Z): apply `20261007134500` at 09:25Z then merge #6332; resume merges when green; apply `20261007140000` before #6336; owner calls: runtime-role re-switch, member token length, cloud fallback for Mission Control tasks.

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

**EP11 — Require real-path independent acceptance.** Test permissions, failure, cancellation, worker death, recovery and uncertain outcomes through named callers. Any UI-dependent change requires independent real browser/Playwright checks. Never weaken tests, safety controls, grants or release gates. Owner tests are confirmation after independent live verification. Lesson from the W7 release (2026-10-05): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. Both passed in full while two defects reached production. Two release rules from the same day, applied to every merge: (1) grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production — a deploy-safety review that checked only the Mission Control files missed a switch whose unset state paused all 534 scheduled workflows for 93 minutes; (2) after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200". Acceptance must also include the last step of each flow. Two more rules from the 2026-10-05 stabilisation: (3) a catch-all error code must log the underlying cause — one code (`notice_unavailable`) hid two different root causes behind a ~9-hour Telegram alert outage; add the logging first, then fix; (4) packets that edit the same database function must be versioned above the newest packet that pins that function's body — a later pinning packet makes the VERIFY of earlier ones fail once the body changes, so renumber new packets above it and install in version order. Lesson from live test A (2026-10-06): when a live acceptance needs a deterministic failure, use a pre-dispatch gate (for example a temporary House Rule that refuses the task before dispatch) rather than waiting for real model failures — it is repeatable, cheap and leaves no provider side effects; remove the gate afterwards and prove it is gone.

**EP12 — Preserve work and safe recovery.** Reuse the original run/claim/effect/operation ledger. Never replay uncertain provider effects, fabricate receipts or broaden authority to make tests pass. Do not replay archived launchers or consumed claims; qualify fresh source/host admission. Do not reset the shared dirty checkout. Only the merging owner removes its own merged, clean, idle worktree using ordinary git worktree remove; never force or blanket-prune.

**EP13 — Carry these rules into every handoff.** Every generated handoff, checklist and plan must include all EP01–EP13 rules and links to the canonical record and AGENTS.md. A documentation handoff is incomplete if the renderer check fails, required tasks/evidence disappear, remote bytes differ, or anonymous browser access/rendering is unverified. These are project working instructions; they do not install a runtime policy in SupraOS Build or override higher-priority instructions.

## Current full-scope checklist — all 33 tracked items

| ID / work | Evidence state | Remaining work |
| --- | --- | --- |
| **P0 — Scope reconciliation and dependency plan** | Canonical pause handoff, complete 33-task checklist and dependency graph updated together; private source branches preserved; publication and anonymous verification recorded in closeout receipts. | Keep current evidence, dependencies and handoff aligned. |
| **B1 — Freeze trusted internal project execution** | Trusted project execution source qualified 2026-10-06: [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) "Projects: trusted internal execution, exact-workspace Git and member projections, rebased onto main (B1, C2 server, M1)" — independent review PASS, OPEN; its six schema packets (20261006110000/111000/112000/114000/115000/115500) APPLIED AND VERIFIED; switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. Before switch-on: observations block transport deletes (desktop re-sign-in 500) and the old poll hands out bound commands unchecked. 2026-10-07: #6259 still OPEN (re-read 07:53Z); [#6287](https://github.com/jtobkin/suprafx-platform/pull/6287) "project switch blockers: re-sign-in survives observations; old poll refuses bound commands" (stacks on #6259) reviewed, OPEN; its packet `20261006115900` APPLIED (a deadlock was fixed first). Switch `PROJECT_REVIEWED_SOURCE_V1` still OFF. | Merge #6259 then #6287 when green (switch stays off; #6287 addresses the two pre-switch follow-ups), then join real server/client/member authority and deployed acceptance. |
| **C1 — Finish client context and history isolation** | Claude loopback isolation scoped proof; other client paths open 2026-10-06: [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256) relay and desktop — isolated context per run and exact-workspace Git, rebased onto main (C1, C2 client) — independent review PASS, OPEN. 2026-10-07: #6256 MERGED 03:38:18Z and live in main `8e4d2d44b0`. 2026-10-07: [#6343](https://github.com/jtobkin/suprafx-platform/pull/6343) "project Codex/Grok turns run in an isolated home" — independent review PASS (caught a renderer argument injection, fixed before merge) — MERGED 18:19:03Z; desktop code, so it reaches users only in desktop 0.1.59 (claimed, not built). 2026-10-08: desktop 0.1.59 release candidate built (branch claude/desktop-0159-rc-20261008 @ 47a315ea90 = main 24273f41e9 + #6347 + #6332 merged in + version bump + hidden test mode and a sign-in leak fix) and qualified in hidden mode: launch, stale-lock self-heal, queue safety signed out, IPC hardening (#6347), Codex/Grok isolation (#6343, real CLIs), sign-in leak closed, clean quit — all PASS. Not proven: relay connect and a live project turn (need the owner's admitted account at install). Not published, not installed. #6347 is still OPEN on GitHub (the RC carries it merged in). Known main defect: the native land-runtime build step has failed since #6168; the RC ships the checked-in land bundle. 2026-10-08 later: [#6347](https://github.com/jtobkin/suprafx-platform/pull/6347) MERGED 04:03Z — web side live in `604b0e0964`; the desktop guards are NOT live (the owner's Mac runs 0.1.58; they ship in 0.1.59). | Owner installs desktop 0.1.59 and confirms relay connect + one project turn; then configuration/hooks and real authenticated transport. |
| **M1 — Complete member dashboard and read projections** | Member projection source and mounted browser evidence retained 2026-10-06: [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) "Projects: trusted internal execution, exact-workspace Git and member projections, rebased onto main (B1, C2 server, M1)" — independent review PASS, OPEN; its six schema packets (20261006110000/111000/112000/114000/115000/115500) APPLIED AND VERIFIED; switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. Before switch-on: observations block transport deletes (desktop re-sign-in 500) and the old poll hands out bound commands unchecked. 2026-10-07: #6259 still OPEN; M2 readers [#6316](https://github.com/jtobkin/suprafx-platform/pull/6316) stacked on it. | Merge #6259 when green (switch stays off), then join actual producer/readers and installed authenticated behavior. |
| **W1 — Bound shared DataPackage fallback waits** | Bounded shared DataPackage source qualified | Compose and verify cancellation/cache behavior through deployed callers. |
| **B2 — Remove remaining private background producer inputs** | Narrow Competitor Watch slice deployed; full producer scope open 2026-10-07: [#6298](https://github.com/jtobkin/suprafx-platform/pull/6298) "no owner-private input in shared background prompts" — OPEN, queued to merge when green. 2026-10-07: #6298 independent review PASS; still OPEN (stacked on #6259). 2026-10-08: live privacy leaks found (owner-private memory could reach room guests, check-ins, routines and Mission Control deck shares); no current exposure (0 share links, 1 guest). Fixes: [#6369](https://github.com/jtobkin/suprafx-platform/pull/6369) live leaks (on main) — reviewed, OPEN; [#6368](https://github.com/jtobkin/suprafx-platform/pull/6368) remaining private-input producers (switch-gated, stacked on #6298), packet `20261008110000` APPLIED AND VERIFIED ~20:53Z — reviewed, OPEN; [#6377](https://github.com/jtobkin/suprafx-platform/pull/6377) approved-tools list for shared rooms and late-joiner hiding (stacked on #6369) — reviewed, OPEN. 2026-10-08 later: [#6369](https://github.com/jtobkin/suprafx-platform/pull/6369) MERGED 04:36Z and live (fence ordered before computer-task detection and context building). Live-proof read-only check: the code is live, but the fence has **never run on a shared audience** in production — 0 shared rooms, the only room-posting routine is disabled, the 2 active members point at projects that no longer exist; nothing leaked since deploy. It found 1 public deck link (July) still serving project outputs; owner OK'd revoking it — done (now 0 shared projects; a direct database change, no tamper-proof revoke event). [#6377](https://github.com/jtobkin/suprafx-platform/pull/6377) rebuilt onto main, reviewed, OPEN; #6298 → #6368 OPEN (after #6259). | Merge #6377, and #6298 → #6368 (after #6259) when green; prove the #6369 fence on a real shared audience (owner call: a real guest or member); then remove any remaining private inputs and verify active worker/card recovery. |
| **M2 — Join member result and internal message readers** | Classified member readers joined in scoped native/browser fixture 2026-10-07: [#6316](https://github.com/jtobkin/suprafx-platform/pull/6316) "members read only results bound to the current publication; internal messages stay owner-only" (stacked on #6259) — reviewed, OPEN. Related: [#6300](https://github.com/jtobkin/suprafx-platform/pull/6300) members no longer read the owner's recalled lessons and skills — OPEN. 2026-10-07: #6300 MERGED 10:29:42Z and live; #6316 still OPEN (review PASS); [#6345](https://github.com/jtobkin/suprafx-platform/pull/6345) redaction on member results (stacked on #6316) — review PASS, OPEN. 2026-10-08: #6316 and #6345 still OPEN (stacked on #6259; bases re-merged by the shepherd). | Merge #6259, then #6316 and #6345 when green; then prove current publication, revocation and real shared-chat transport. |
| **M3 — Qualify owner-only Realtime transport** | Owner-topic/metadata routing implemented; socket matrix scoped 2026-10-07: [#6336](https://github.com/jtobkin/suprafx-platform/pull/6336) "owner-only Realtime channel behind a default-off drain switch" — reviewed, OPEN; switch `SUPRAOS_RELAY_OWNER_TOPIC_V1` OFF; packet `20261007140000` pending (apply before merge). Owner decision pending: shorten the member Realtime token (15 minutes) so revocation takes effect quickly. 2026-10-07: packet `20261007140000` APPLIED AND VERIFIED (~10:42Z); #6336 still OPEN (switch OFF). Owner ruling: cut off removed members immediately (not after the 15-minute token). [#6354](https://github.com/jtobkin/suprafx-platform/pull/6354) removed members lose the live feed at once (stacked on #6336; switches OFF) — review PASS (caught Realtime notice flooding from its trigger, bounded before merge), packet `20261007160000` APPLIED AND VERIFIED (~15:10Z), OPEN. [#6361](https://github.com/jtobkin/suprafx-platform/pull/6361) removed members lose presence at once (stacked on #6354) — OPEN, packet `20261008100000` pending. 2026-10-08: packet `20261008100000` (#6361) APPLIED AND VERIFIED ~19:51Z; #6336 #6354 #6361 still OPEN (bases re-merged by the shepherd); DB switch `relay_topic_epoch_db_enabled()` reads false (release audit). | Merge #6336 → #6354 → #6361 (switches stay off); switch B (`SUPRAOS_RELAY_OWNER_TOPIC_V1`) per the activation runbook; then drain old broadcasters and qualify revocation live. |
| **J1 — Join server, clients and actual native authority** | Joined server/client native and browser source evidence 2026-10-06: inputs reviewed but not merged — server #6259 and client #6256 both review PASS, OPEN; the join itself has not started. 2026-10-07: client #6256 MERGED (live); server #6259 still OPEN; the join has not started. | Merge #6259 (and #6287), then close native client and deployed transport gaps before final join. |
| **W2 — Notification recipient authority and usable authoring** | Email/recipient authority source in held draft6138 2026-10-06: [#6253](https://github.com/jtobkin/suprafx-platform/pull/6253) "notifications only reach the owner's verified destinations; uncertain sends are held" — independent review PASS, OPEN. Follow-up: a crash between email claim and send leaves no history line. Owner allowed one real test email to the owner's own address only. 2026-10-06: #6253 MERGED 10:57:48Z and live (main `8e4d2d44b0`). | One real authorized email (owner's own address) and uncertain-send recovery on production; confirm whether its schema is installed (not recorded here). |
| **W3 — File operation namespace and destination authority** | Storage namespace and uncertainty source in held draft6132 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`. | Installed/production proof of allow, deny, revocation and recovery. Install policy/schema and verify real owner, revocation and recovery boundaries. |
| **W4 — Named OAuth and raw API authority** | Named/raw API authority source in held draft6129 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`. | Installed/production proof of allow, deny, revocation and recovery. Compose exact final source and qualify installed/provider behavior. |
| **W5 — Child workflow and bot creation authority** | Child/bot creation authority source in held draft6129 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`. The spawn-retry follow-up is addressed by [#6289](https://github.com/jtobkin/suprafx-platform/pull/6289) (a retried child spawn returns the original child), MERGED 2026-10-07 04:13Z. | Installed/production proof of allow, deny, revocation and recovery. Prove real allowed creation, denied targets and original-child recovery. |
| **X1 — Qualify every supported context entry** | Entry-point context/privacy map and scoped repairs 2026-10-06: a lane for X1 context entries started (running; no PR yet). 2026-10-07: [#6274](https://github.com/jtobkin/suprafx-platform/pull/6274) "qualify every agent context entry (prefs, audience, receipts)" MERGED 03:42:08Z, live; follow-ups [#6285](https://github.com/jtobkin/suprafx-platform/pull/6285) (legacy Telegram entry checks, cancel into delegation + voice workflows, receipt read-back; stacks on #6274) — reviewed, OPEN. 2026-10-07: #6285 MERGED 09:21:26Z and live. 2026-10-08: [#6362](https://github.com/jtobkin/suprafx-platform/pull/6362) read back Mission Control task context receipts (owner only) — reviewed, OPEN; [#6374](https://github.com/jtobkin/suprafx-platform/pull/6374) receipt panel ("what each agent knew") and in-app failure bell (stacked on #6362) — reviewed, OPEN. 2026-10-08 later: [#6362](https://github.com/jtobkin/suprafx-platform/pull/6362) MERGED 06:11Z and live; read-only replay: 4 of 5 stored receipts would read `confirmed`, 1 `not_recorded`; the owner's signed-in response not yet seen. #6374 now targets main, OPEN. | Merge #6374 when green; see a signed-in receipt read-back; qualify every supported surface live, including background and System Workflow runs. |
| **A1 — Finish global attention and baseline source gaps** | Attention/Room/shelf/mail foundations; global cutover remains off 2026-10-08 release audit: the global attention batch function is not installed in production, so packet 220000 (another session) is a no-op there. | Close all16 behavior gaps for cadence, suppression, consent and context. |
| **R1 — Reconcile main, CI and exact release stack** | ad2ee680 partial successor pushed in draft6190, scoped52/types14/review PASS; required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; prior1c0 CI RED preserved; earlier privacy slices shipped; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: composed `3214f4849e3bb0517b60ee17821826918ee11147` in PR #6196; duplicate-version ratchet clean; writer catalog PASS (2,657 rows); box-ci pending. 2026-10-08 release audit (read-only, ~22:35Z 2026-10-07): R1 NOT done — main green at the live commit but many project PRs open (some stacked, some conflicting with bases at audit time, re-merged since by the shepherd), 15 packets live ahead of their code, box-ci queue ~66 jobs; 5 of the last 13 main checks red, all flakes (native Postgres initdb timeouts under load, fixed by #6373, merged). The text above (frozen 3214f48, #6160) is stale: #6196 merged 2026-10-05, #6160 is closed. Outside this project: #6235 (CRM intake, another session) packet 20261006143000 is on main but not applied to production (live code falls back; handed to that session). | Merge the remaining open project PRs via merge-if-green (packets first); retire the stale frozen-head text; reconcile outside-lane packet gaps with their owners. |
| **R2 — Installed schema, profile and release packet** | Installed profile read and source migration packets prepared 2026-10-05: 24 packets classified A17/S3/T4; two version collisions renumbered; ordered 24/24 install + VERIFY proven on a prod-schema clone (not a restored data copy — that rehearsal was blocked by permissions). | Owner applies the 24 packets to production from the frozen worktree with apply-migration.mjs and confirms the ledger (+24); commit refreshed schema oracles. |
| **R3 — Writer/effect drain and faithful restore rehearsal** | Private stop/install/unknown recovery and dated restore proofs 2026-10-08 (2026-10-07 20:20–21:20Z, owner-approved quiet hours): restore rehearsal with our backup tool PASSED for its scope (public + migration ledger): read-only exported snapshot; 50/50 key-table counts equal; 867/867 tables restored with exact counts (54.1 M rows); ledger 773 equal; schema digest equal (15/16 classes byte-exact, constraints equal after documented flattening); roles/grants reproduced; packet 20261007134500 forward/rollback/forward round trip PASS in the copy. Production contact 20.4 min; site 69/69 samples HTTP 200, 0 over 2 s; 0 sessions blocked; no production write. Side effect: the deploy lock was held 51 min. Gaps: 339 owner/agent/node schemas (2,022 tables, ~147 MB), auth/storage/vault/realtime and storage files are outside the tool's scope; packets touching realtime cannot be rehearsed on this copy; snapshot taken with writers running (cannot admit a release). [#6381](https://github.com/jtobkin/suprafx-platform/pull/6381) widens the backup tool to every owner and agent schema and stops it blocking deploys (review caught a lock-exhaustion bug — production has 10,240 lock slots — fixed before merge) — OPEN. Backup-test leftovers removed from the web host with owner OK. 2026-10-08 later: [#6381](https://github.com/jtobkin/suprafx-platform/pull/6381) MERGED 02:43Z (script on main; not yet run). Read-only catalog pre-check: 339 product schemas, no unknown schema, lock budget well above the rehearsal's — the tool's pre-flight should not refuse (inference; not run). | Re-run the rehearsal with #6381 to cover owner/agent schemas, or use the provider's restore-to-new-project for full fidelity incl. auth/realtime/vault; held-window writer drain and wiring drain census + restore into the live release gate; a written decision on storage files. |
| **I1 — Compose and independently qualify final source** | ad2ee680 integrates reviewed guard/manual/Telegram repairs on1c0;52 scoped tests/types14/review PASS; exact successor required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; unchanged UI has scoped Linux privacy proof; full final source open; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: frozen `3214f4849e3bb0517b60ee17821826918ee11147`; conflict resolutions reviewed by the verification lane in the trailing audit. 2026-10-08 release audit: not started as specified — the project ships PR by PR, so no single frozen final head exists yet. | After the last project PR merges: record main's sha; run full box-ci (both checks), macOS Native Land and the prod-shape harness S1–S13 on it; one independent review of the composed diff since ac48190955. |
| **D1 — Gated merge and deploy verified code** | UI6179/6181 merged/deployed/public-browser verified | No owner-run release steps remain from the earlier note: the packets were applied on production 06:03–06:10Z (24/24 applied and verified), PR #6196 was merged 06:11:22Z via merge-if-green and deployed 06:24:35Z — all by the session under the owner's instruction "automerge and automigrate as needed"; the earlier permission blocks did not recur. The live check found two defects (see W7), so live verification is NOT complete. Remaining for this task: its own full authenticated scope, unchanged. |
| **D2 — Activate qualified workflows after compatible rollout** | Global/workflow activation not claimed 2026-10-08: switch A (background-queue expiry) is on by default since #6332 went live (env value not re-read). Switches B–F stay OFF. | Activate only compatible qualified schema/runtime with tested recovery. |
| **P1 — Provider and real computer readiness** | Provider readiness incomplete; Stripe configuration external | Finish normal provider/account/real-computer setup and approved live inputs. |
| **V1 — Stable deployed all-path and 16 behavior acceptance** | All16 integrated/live acceptance behaviors remain open | Independently verify stable deployed journeys across all12 surfaces. |
| **U1 — Owner confirmation and final handoff** | Portable handoff maintained; final owner confirmation pending 2026-10-08: plain-English owner guide written (what is live vs waiting vs off, everyday how-to, troubleshooting, open decisions); private. | Provide specific owner tests only after independent applicable verification. |
| **W6 — Atomic usage limits for scoped capability grants** | Atomic grant reservations source in held draft6129 Related grant changes shipped 2026-10-05 (not W6 acceptance): PR #6206 (main `2e242177b3`) lets workflow grants last 1 hour / 24 hours / 1 week / 1 month / 1 year and keeps one card per workflow + action; PR #6219 (main `3f18ef481c`) stops the default-permission lookup crashing on `workflow:<id>` agents (a regression from Agent Run #6168). The owner approved their own two pending workflow grants for 1 year (18:13Z, expire 2027-10-05); other owners' cards are theirs to approve. 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-06: #6226 (approved cards clear, duration survives reload) MERGED; [#6247](https://github.com/jtobkin/suprafx-platform/pull/6247) one grant card per request under load — review PASS, OPEN, packet `20261006050000_one_pending_workflow_grant_card` APPLIED AND VERIFIED (0 duplicate pending cards beforehand). 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`. #6247 (one grant card per request under load) MERGED 04:12:59Z. | Installed/production proof of allow, deny, revocation and recovery. Prove installed concurrent use, revocation and original receipt recovery. |
| **W7 — Original-operation workflow effects** | Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. 2026-10-05 07:45–08:55Z, production stabilisation: hotfix PR #6199 opened (`claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a`) fixing faults 1 and 2 with packet `20261005232000_mc_rerun_unsent_anchor_hold` (build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head `420a71db33`, pending at the current head). A read-only audit of every guarded control (28 direct plan writers, 17 now rejected) and a production-shape end-to-end harness (S1–S9; all scenarios fail on main, S1–S3 and the Workspace drain pass on the fix) raised the fault count to eight. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. 2026-10-05 09:00Z → 22:23Z PRODUCTION STABILISATION (handed off 2026-10-06 01:55Z): all eight faults fixed and live through 14 PRs, each independently reviewed and merged with merge-if-green.sh: #6196 `55a12f0da9` (W7 release: squash of the composed failure-drain/rerun candidate `ac48190955`); #6199 `c1513db29c` (the final task of a plan settles again (finish intents now carry the task id) + packet `20261005232000`); #6197 `7b28f6a41a` (schema snapshot refresh; coordinator sweep skips drain-refused plans; manifest re-pin); #6198 `ec1e1132fe` (Mission Control plans get a critical path, so the drain can fire (owner said yes)); #6206 `2e242177b3` (workflow grants can last 1 hour / 24 hours / 1 week / 1 month / 1 year; one card per workflow + action); #6205 `aeebec0da0` (safe Delete project (refuse or archive instead of orphaning a running plan); one bad plan no longer aborts the coordinator tick); #6211 `38ef1efa84` (planner: no 0-task launch; review panel follows the selected plan; long chat scrolls); #6219 `3f18ef481c` (grants: a `workflow:<id>` agent no longer crashes the default-permission lookup (regression from Agent Run #6168)); #6213 `0622e4ea36` (test and source record for packet `20261005239000` (the packet was already live)); #6212 `2df2d3b0cc` (scheduled workflows: stalls after restart / lost reply / Run-now / cancel fixed; for-each and delete fixed; pause banner + Release; packet `20261005235000`); #6220 `9ab57850bd` (an alert for an owner without Telegram is skipped and the run completes; coded errors with logged causes); #6222 `c7e4e9b150` (a failed task retries with a different agent (the preferred agent no longer overrides the failed-agents list)); #6207 `9dcef69a69` (older projects: Duplicate and Adopt (packet `20261006000700`) + plain-English refusal wording); #6223 `e0d776651c` (alerts for owners not yet admitted (invite-required) no longer fail); #6221 `0d25a537b4` (owner controls: resolve an unknown outcome, per-task Stop is final, review / outputs / settings work or say why (packet `20261006010000`)). Five extra packets applied and verified on production: `20261005232000_mc_rerun_unsent_anchor_hold` (2026-10-05 09:00Z); `20261005239000_mc_rerun_unadmitted_effect_hold` (2026-10-05 14:41Z); `20261005235000_scheduled_occurrence_recovery` (2026-10-05 19:55Z); `20261006000700_mc_legacy_plan_adoption` (2026-10-05 21:17Z); `20261006010000_mc_unknown_task_owner_resolution` (2026-10-05 22:22Z); production ledger 743 (the Agent Run session installed its own 19). Live acceptance B PASS 17:36Z (project `43470d88`). Evidence pushed to private branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d`. Production incidents found and fixed during the run: (1) **Scheduled workflows paused 06:24–07:57Z on 2026-10-05.** The W7 release carried a once-only scheduler that holds all due work while its switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is unset; it was unset in production, so all 534 scheduled workflows stopped for 93 minutes. The deploy-safety review missed it because it checked only the Mission Control files for new switches, not the whole diff. Fixed by the owner turning the switch on at 07:57Z (missed runs not re-run); remaining scheduler stalls fixed by #6212. (2) **Telegram "Liq Warning" alerts failing from 13:15Z to ~22:08Z on 2026-10-05.** A regression from the Agent Run release (#6168): first the permission lookup crashed on workflow-style agent ids, then alerts for owners not yet admitted failed when their settings were read. A catch-all error code hid both causes. Fixed by #6219, #6220 and #6223; 0 alert failures in the 15 minutes after the last fix. 2026-10-06 02:17Z resumed. 03:01Z LIVE ACCEPTANCE A on production: **A PASS with a finalisation gap** (2026-10-06 03:01Z, production, signed-in owner; project `bacf0dc8` "W7 drain test", born after #6198 so it carries a critical path of task-1 → task-2). Method: a temporary House Rule "always ask above $0.001" on all 35 active agents (set through the House Rules screen, removed afterwards; 0 left in the database) refused task-1 before dispatch — a pre-dispatch gate, not a real model failure. task-1 failed twice (two different agents); attempt 3 went to a shared-computer agent that BYPASSES the House Rules gate, ran ~4 minutes and ended `outcome_unknown`/blocked; the owner used Resolve → Retry (#6221, live); attempt 4 failed; retries reached 3; the `critical_failure_drain` and `critical_escalation` effects were delivered; task-2 was `skipped` with drain reason `critical_failure_unstarted`; the plan was never completed. **Gap (live):** the plan stays `running` for ever — the terminal-blocked rule (packet `20261005230000`, `mc_drain_terminal_blocked_v1`) still counts the settled unknown-outcome receipt after the owner resolved it; the coordinator skips draining plans, execute refuses, so nothing finalises; the same rule blocks Re-execute (active claim). Fix in progress: packet `20261006020000` on branch `claude/w7-owner-resolution-unblocks-20261006` plus a sanctioned finaliser; no PR yet. Evidence: private evidence lane, `live/acceptance/A-critical-drain-PASS-with-gap.md`. Findings from live test A (2026-10-06): (1) shared-computer agents bypass House Rules (the pre-dispatch gate does not apply to them); (2) a skipped task renders as "planned" on the project screen — no drain wording; (3) an owner Stop on an unstarted critical task wedges the plan (retries 0 → 1, the task cannot fail again; design-lane finding). W7 verified live = 3 of 3 behaviours observed (A with the gap, B, C); NOT accepted. Open PRs (all independently reviewed safe; merges held by the Agent Run session until its audit-fix #6225 landed — #6225 MERGED 2026-10-06 03:21:38Z → main `4c9208fc5f`; merge order after it): [#6226](https://github.com/jtobkin/suprafx-platform/pull/6226) grants: approved cards clear, chosen duration survives a reload, one card per request; [#6227](https://github.com/jtobkin/suprafx-platform/pull/6227) planner works on a phone + design for re-executing after an unknown outcome; [#6229](https://github.com/jtobkin/suprafx-platform/pull/6229) archived projects cannot run, counts and lists exclude them, no 0-task projects (review PASS); [#6230](https://github.com/jtobkin/suprafx-platform/pull/6230) production-shape end-to-end harness S1–S13 (review PASS; do NOT enable the box-ci step yet); [#6233](https://github.com/jtobkin/suprafx-platform/pull/6233) a task every agent has failed no longer waits for ever; a held task alerts the owner. 2026-10-06 ~10:00Z: #6239 (owner resolution unblocks a drained plan + finaliser; packet `20261006020000` applied 07:12:36Z) MERGED 08:54:46Z, live 09:08:47Z → live test A CLOSED (plan `ee4c97bc` `failed` 09:09:21Z; owner not notified — fixed by #6255, open). #6233 (exhausted agents skip/escalate + held-task alert) MERGED 09:26:41Z; #6230 (e2e harness S1–S13) MERGED 09:37:10Z (box-ci step not enabled); #6226 #6227 #6229 merged earlier. Open with packets already applied: #6255 (030000), #6252 (040000), #6249 (060000); #6246 House Rules cover computer agents (review PASS). 2026-10-07 (~07:50Z): merged and live — #6252 (owner's last decision finishes the project; Stop on a critical task drains it), #6275 (task tools bind to the saved attempt; owner card answers reserved before any effect), #6276 (send tools: a lost reply is an unknown outcome), #6289 (manual actions obey claim rules; retried child spawn returns the original child), #6247, #6283 (test flake); #6246 merged 2026-10-06. Effects parity: #6275 #6276 #6289 merged; [#6301](https://github.com/jtobkin/suprafx-platform/pull/6301) (owner review and Stop go through effect intents; six never-delivered effect kinds stopped) OPEN with packet `20261006153000` APPLIED. Safe cancellation: [#6277](https://github.com/jtobkin/suprafx-platform/pull/6277) OPEN with packet `20261006151000` APPLIED. Open demo/MC fixes: [#6311](https://github.com/jtobkin/suprafx-platform/pull/6311) true end state, [#6330](https://github.com/jtobkin/suprafx-platform/pull/6330) real agents on cards, [#6332](https://github.com/jtobkin/suprafx-platform/pull/6332) self-heal (packet `20261007134500` scheduled 09:25Z), [#6333](https://github.com/jtobkin/suprafx-platform/pull/6333) a plain goal always yields a plan, [#6334](https://github.com/jtobkin/suprafx-platform/pull/6334) tool tags never run from text (security review caught a prompt-injection hole in v1), [#6315](https://github.com/jtobkin/suprafx-platform/pull/6315) e2e harness S1–S13 PASS on main, [#6321](https://github.com/jtobkin/suprafx-platform/pull/6321) chat diagnostics. LIVE REHEARSAL 2026-10-07: the Mission Control flow works live when the owner's desktop app is open; tasks run only through the desktop app; 233 stale queued jobs parked (owner: delete); a 2-task project finished in ~70 s. 2026-10-07 later: #6255 (drained project says so; owner told) MERGED 14:48:22Z and live — but the owner has no Telegram destination, so the alert is recorded and cannot be delivered; #6311 (true end state) #6315 (harness S1–S13) #6321 (chat diagnostics) merged and live. Packet `20261007134500` (#6332) APPLIED AND VERIFIED ~09:25Z; packet `20261007152000` (#6344, owner review notes reach the agent's own memory, stacked on #6301) APPLIED AND VERIFIED ~12:43Z. Still OPEN with review PASS: #6249 #6277 #6301 #6330 #6332 #6333 #6334 #6344; [#6356](https://github.com/jtobkin/suprafx-platform/pull/6356) chat keeps the real model error (diagnostics) OPEN. Owner paused 16:10Z, resumed 18:20Z. Live re-tests for #6249/#6277/#6255 prepared, not run. 2026-10-08: [#6330](https://github.com/jtobkin/suprafx-platform/pull/6330) cards show real agents MERGED 2026-10-07 19:38:37Z; [#6333](https://github.com/jtobkin/suprafx-platform/pull/6333) a plain goal always yields a plan MERGED 20:08:40Z; [#6249](https://github.com/jtobkin/suprafx-platform/pull/6249) interrupted Re-execute never wedges (Discard this run) MERGED 21:01:32Z; [#6334](https://github.com/jtobkin/suprafx-platform/pull/6334) raw tool tags hidden and never executed from text MERGED 21:02:00Z; [#6332](https://github.com/jtobkin/suprafx-platform/pull/6332) Mission Control tasks self-heal (stale desktop lock, offline message, queue priority, revivable 24 h expiry; switch A on with it) MERGED 23:51:25Z — all live in `0cb2eed5ff`. [#6373](https://github.com/jtobkin/suprafx-platform/pull/6373) CI: native Postgres test clusters start reliably (120/120 initdb timeouts → 0 in the lane) MERGED 2026-10-08 00:35:52Z. Still OPEN with review PASS: #6277 #6301 #6344; #6356 chat keeps the real model error (reviewed, queued). Live re-tests still not run. 2026-10-08 later: [#6277](https://github.com/jtobkin/suprafx-platform/pull/6277) Stop while running MERGED 01:36Z; [#6356](https://github.com/jtobkin/suprafx-platform/pull/6356) chat keeps the real model error MERGED 05:17Z; [#6372](https://github.com/jtobkin/suprafx-platform/pull/6372) grant durations, House Rules cost-floor warning, card counts and Telegram notice MERGED 05:36Z; [#6395](https://github.com/jtobkin/suprafx-platform/pull/6395) project-page agent lanes MERGED 06:32Z — all live in `604b0e0964`. #6372 seen on screen signed in (grants page "At its limit" + duration copy; Mission Control "link Telegram" notice). #6277 and #6356 are live but NOT exercised on production (no Stop pressed, no failing turn since). A stuck plan (running since 10-07) and a chat-dock JSON error found; fixes [#6423](https://github.com/jtobkin/suprafx-platform/pull/6423) and [#6428](https://github.com/jtobkin/suprafx-platform/pull/6428) OPEN. | The W7 drain/rerun milestone is live and its 3 behaviours PASS (A closed 2026-10-06); the full W7 task is NOT accepted. In order: (1) merge #6301 (153000) → #6344 (152000), #6423, #6428; (2) live re-tests one at a time: Re-execute recovery (#6249), Stop while running (#6277), drain + owner alert (#6255) — the owner alert needs the owner to link Telegram; (3) desktop 0.1.59 (RC qualified, awaiting owner install) carries the desktop half of #6332/#6347; (4) remaining W7 scope — effects parity (#6301 and any remaining kinds), real L1 anchoring, runtime role (R3B); see the first real failing turn's cause (#6356); Stripe Link (owner, external); QA invite. Follow-up: #6252 review "reject" on a critical task drains the plan (undisclosed). Full project: 33 tasks, 16 behaviour families, 12 surfaces; iMessage deferred, WhatsApp excluded. |
| **X2 — Confirm System Workflow durable terminal and pause receipts** | System Workflow pause and Memory Promotion partial fixes deployed 2026-10-06: [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261) "a run is only completed when its row says so; System Workflow pause and recovery proven (X2, X3)" — independent review PASS, OPEN. 2026-10-06: #6261 MERGED 11:34:52Z and live. | Qualify real admitted-owner pause/checkpoint/terminal recovery journeys on production. |
| **X3 — Refuse zero-row completion in scheduled and direct workflows** | Missing original terminal-row refusal has scoped native evidence 2026-10-06: [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261) "a run is only completed when its row says so; System Workflow pause and recovery proven (X2, X3)" — independent review PASS, OPEN. 2026-10-06: #6261 MERGED 11:34:52Z and live. | Verify scheduled and direct deployed paths retain truthful outcomes. |
| **X4 — Retain uncertain scheduled workflow attempts before another tick** | Scheduled original-attempt source preserved in held drafts. 2026-10-05: the once-only scheduled "occurrence claim" path reached production inside the release that deployed at 06:24Z, held behind the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`. The switch was unset, so all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on at 07:57Z and said missed runs need not be re-run. Observed to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), 55 failed, 27 of them waiting for a new per-action grant introduced by the same release. Fixes for the known stalls are work in progress on `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe` (untested, no PR; its packet `20261005235000` must not be applied) 2026-10-05 stabilisation: PR #6212 (main `2df2d3b0cc`, merged 19:56Z) fixed the known stalls — a run killed by a restart, a lost reply, Run-now, a cancelled slot — plus for-each on a repeated target and workflow delete, and added a pause banner with a Release control; its packet `20261005235000_scheduled_occurrence_recovery` was applied and verified on production at 19:55Z. Health in the hour before 01:55Z on 2026-10-06 (reported, not re-read here): 167 scheduled runs completed, 34 failed; 0 duplicate slots; 0 stalled occurrences; 0 Mission Control plans running. The remaining failures are owners' own model keys (30 × "No usable API key for anthropic", 2 × credit balance), not platform faults. 2026-10-06: [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254) "acceptance proof for retained attempts and approval continuation" — independent review PASS, OPEN; packet `20261006070000` APPLIED AND VERIFIED. Follow-up: its script needs a writable role for two checks and two corrected expectations. 2026-10-06: #6254 MERGED 16:36:34Z and live. | Run #6254's acceptance proof on production (#6254 merged 2026-10-06; packet 070000 applied); not recorded as run. The once-only scheduler is live and its known stalls are fixed, but this task is NOT accepted: the original acceptance proofs (real-transport lost-acknowledgment and next-tick no-repeat) have not been run, and completing the cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`) is not recorded. The three sibling approval switches were turned on 03:09Z 2026-10-06 (see X5); scheduled human-approval steps are now activated but not yet accepted live. Next: add scheduled scenarios to the end-to-end harness, run the original acceptance on production, and keep watching for duplicate slots (the only reason to turn the switch off). |
| **X5 — Qualify original scheduled approval continuation** | Bounded original approval continuation source qualified 2026-10-06 03:09:23Z: the three approval switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) were set to on in the production settings store and applied on the web host under the deploy lock (owner decision 02:25Z); both containers show all four scheduler switches on. Build-box rehearsal before the flip: GO — 13/13 + 78/78 + 7/7 contract cases, 29/29 packets, 7/7 two-tick drive (verdict file in the private evidence lane, `live/verify/scheduled-approval-switches-verdict.md`). Known limit: approvals already pending from BEFORE the flip stay held — the engine stamps the occurrence id only when the switch was on at run start — so their only exit is the workflow page "Release this run" control after 30 minutes. 2026-10-06: [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254) "acceptance proof for retained attempts and approval continuation" — independent review PASS, OPEN; packet `20261006070000` APPLIED AND VERIFIED. Follow-up: its script needs a writable role for two checks and two corrected expectations. 2026-10-06: [#6263](https://github.com/jtobkin/suprafx-platform/pull/6263) scheduled workflows built in the canvas use approval continuation — review PASS, OPEN; packet `20261006141000` APPLIED AND VERIFIED (0 live workflows had approval steps). Owner: run live scheduled-approval tests one at a time, and release pre-switch held approvals one at a time. 2026-10-06: #6254 MERGED 16:36:34Z and #6263 MERGED 12:48:43Z; both live. | #6254 and #6263 merged and live (packets 070000 and 141000 applied). Next: drive one real scheduled approval end-to-end on production, one test at a time (owner), and release pre-switch held approvals one at a time. Close remaining effectful graphs and real approval/uncertain-outcome acceptance. State at 2026-10-06 03:10Z: all four scheduler switches are ON in production (approval switches since 03:09:23Z, owner decision after a GO rehearsal). ACTIVATED, NOT accepted: the live acceptance of a human-approval step in a scheduled workflow (approve, decline, lost reply, restart between approval and continuation) has not been run on production; approvals pending from before the flip stay held until the owner presses "Release this run" after 30 minutes. Next: drive one real scheduled approval end-to-end on production and add approval scenarios to the end-to-end harness (#6230). |
| **C2 — Bind project Git commands to exact workspace** | Project dispatch6118 and eligible-recipient6141 source qualified 2026-10-06: [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) "Projects: trusted internal execution, exact-workspace Git and member projections, rebased onto main (B1, C2 server, M1)" — independent review PASS, OPEN; its six schema packets (20261006110000/111000/112000/114000/115000/115500) APPLIED AND VERIFIED; switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. Before switch-on: observations block transport deletes (desktop re-sign-in 500) and the old poll hands out bound commands unchecked. Client half in [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256) (review PASS, OPEN). 2026-10-07: #6259 still OPEN (re-read 07:53Z); [#6287](https://github.com/jtobkin/suprafx-platform/pull/6287) "project switch blockers: re-sign-in survives observations; old poll refuses bound commands" (stacks on #6259) reviewed, OPEN; its packet `20261006115900` APPLIED (a deadlock was fixed first). Switch `PROJECT_REVIEWED_SOURCE_V1` still OFF. Client half #6256 MERGED 2026-10-07 03:38Z (live). | Merge #6259 then #6287 when green (switch stays off), then qualify mounted Realtime/relay, exact workspace commands and schema-first rollout. |
| **R3B — Stage runtime role before candidate schema extension** | Dormant minimal role source with scoped native ACL proof; runtime helper/bridge integration saved82b01044; 19 private native actual-caller cases and independent review PASS. 2026-10-06 ~03:00Z rehearsal verdict: **NO-GO today** (private evidence lane, `live/verify/runtime-role-verdict.md`). The role packet refuses on the production shape (an existing `vms_agent_run_shelf` table; on PostgreSQL 16+ the implicit ADMIN membership of the postgres account cannot be revoked); a code blocker in the runtime binding (`lib/owner-db-runtime-binding.ts` membership test) would make every owner-database call fail with the switch on; one `FOR SHARE` read in `lib/vms-config.ts` needs UPDATE privilege. A renumbered packet (`20261006120000`) is prepared on branch `claude/runtime-role-packet-20261006` @ `7c72542d29`, no PR. Needs first: a product PR for the binding and the read, an owner-created runtime credential, and re-mapping of the orphan owner schemas. 2026-10-06 ~10:00Z: code blockers fixed (#6240, MERGED 08:14:30Z); packet `20261006120000` (#6258, OPEN) APPLIED AND VERIFIED; orphan owner schemas fixed by the owner (0 left); the owner set the role's login and a pooler login passed. Switch ~09:19Z broke public-table callers (Settings → General 503) → ROLLED BACK ~09:52Z (200s verified). Fix [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (public-table callers use the admin connection) in review. 2026-10-06: #6270 MERGED 16:37:23Z and live. 2026-10-07: re-switch HELD until after the owner's Agent VM demo (decision 04:20Z); pre-switch check passed except "deploy running". #6258 still OPEN. 2026-10-07: #6258 MERGED 14:25:02Z. Switch C in the private activation runbook: re-run the pre-switch check (last NO-GO only for "deploy running"), owner checks the pooler client limit, owner runs the switch, KEEP only after signed-in pages return 200. Not run yet. | Installed but NOT switched on (rolled back 2026-10-06 ~09:52Z). In order: (1) owner checks the connection-pooler client limit; (2) re-run the pre-switch privilege check (0 not-ok) with no deploy running; (3) owner runs switch C, watching Settings → General and every public-table caller (signed-in API status table), KEEP only after 200s. Earlier remaining work still applies: full installed ACL/default-ACL/policies; keep separate B1/gate-six work. |
| **C2S — Install and verify project schema before server rollout** | Seven ordered project-schema packets rehearsed privately 2026-10-06: the project schema packets for #6259 — 20261006110000, 111000, 112000, 114000, 115000, 115500 — were applied to production and each APPLIED AND VERIFIED (schema first, before the server code merges; switch `PROJECT_REVIEWED_SOURCE_V1` OFF). 2026-10-07: packet `20261006115900` (#6287) also APPLIED after a deadlock fix; switch still OFF. | Schema installed on production (incl. 115900); remaining: merge #6259 and #6287, live service-role verification with the server code, then the guarded switch-on. |

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

**Saved work:** Trusted project execution source qualified 2026-10-06: [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) "Projects: trusted internal execution, exact-workspace Git and member projections, rebased onto main (B1, C2 server, M1)" — independent review PASS, OPEN; its six schema packets (20261006110000/111000/112000/114000/115000/115500) APPLIED AND VERIFIED; switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. Before switch-on: observations block transport deletes (desktop re-sign-in 500) and the old poll hands out bound commands unchecked. 2026-10-07: #6259 still OPEN (re-read 07:53Z); [#6287](https://github.com/jtobkin/suprafx-platform/pull/6287) "project switch blockers: re-sign-in survives observations; old poll refuses bound commands" (stacks on #6259) reviewed, OPEN; its packet `20261006115900` APPLIED (a deadlock was fixed first). Switch `PROJECT_REVIEWED_SOURCE_V1` still OFF.

**Remaining:** Merge #6259 then #6287 when green (switch stays off; #6287 addresses the two pre-switch follow-ups), then join real server/client/member authority and deployed acceptance.

**Acceptance:** Actual claim/output authority; current source, attempt and digest binding; replay/task-closed/rollback/personal controls. Freeze exact commit and contract. No private owner context from producer or recovery.

**Source:** lib/supraos-build/plan-coordinator.ts; execution-input and relay-response routes; migrations 010120/010140

**Prior owner role:** Sol / server. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | PR #6259 open, not on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6259 review PASS 2026-10-06 |
| merged | No — #6259 OPEN |
| deployed | Full scope pending |
| activated | No — PROJECT_REVIEWED_SOURCE_V1 OFF |
| verifiedLive | Full scope pending |

### C1 — Finish client context and history isolation

**Saved work:** Claude loopback isolation scoped proof; other client paths open 2026-10-06: [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256) relay and desktop — isolated context per run and exact-workspace Git, rebased onto main (C1, C2 client) — independent review PASS, OPEN. 2026-10-07: #6256 MERGED 03:38:18Z and live in main `8e4d2d44b0`. 2026-10-07: [#6343](https://github.com/jtobkin/suprafx-platform/pull/6343) "project Codex/Grok turns run in an isolated home" — independent review PASS (caught a renderer argument injection, fixed before merge) — MERGED 18:19:03Z; desktop code, so it reaches users only in desktop 0.1.59 (claimed, not built). 2026-10-08: desktop 0.1.59 release candidate built (branch claude/desktop-0159-rc-20261008 @ 47a315ea90 = main 24273f41e9 + #6347 + #6332 merged in + version bump + hidden test mode and a sign-in leak fix) and qualified in hidden mode: launch, stale-lock self-heal, queue safety signed out, IPC hardening (#6347), Codex/Grok isolation (#6343, real CLIs), sign-in leak closed, clean quit — all PASS. Not proven: relay connect and a live project turn (need the owner's admitted account at install). Not published, not installed. #6347 is still OPEN on GitHub (the RC carries it merged in). Known main defect: the native land-runtime build step has failed since #6168; the RC ships the checked-in land bundle. 2026-10-08 later: [#6347](https://github.com/jtobkin/suprafx-platform/pull/6347) MERGED 04:03Z — web side live in `604b0e0964`; the desktop guards are NOT live (the owner's Mac runs 0.1.58; they ship in 0.1.59).

**Remaining:** Owner installs desktop 0.1.59 and confirms relay connect + one project turn; then configuration/hooks and real authenticated transport.

**Acceptance:** Qualify managed configuration, real authentication, existing resume-ID survival, Codex/Grok and deployed transport. Fix fixture types; close existing skills/config/SessionStart hook injection, not merely transcript reuse; prove Claude/Codex/Grok one-shot assignment and output identity with personal positive controls. Add server-authorized workspace context for Land/check/audit; unbound mixed-session commands must hold until producer/PUT/relay agreement and delayed/restarted cases are qualified.

**Source:** packages/supraos-relay/src/{start,pty-session,project-execution-scope}.js; electron/ipc/{embedded-relay,cli-relay-session}.ts; cli-relay-worker.ts

**Prior owner role:** Sol audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Yes: #6256 and #6343 on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6256 review PASS 2026-10-06; #6343 review PASS 2026-10-07 |
| merged | Yes: #6256 merged 2026-10-07 03:38:18Z; #6343 merged 2026-10-07 18:19:03Z; #6347 merged 2026-10-08 04:03:34Z |
| deployed | #6256 live; #6343 and #6347 in live web main 604b0e0964; desktop 0.1.59 RC qualified hidden, awaiting owner install |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### M1 — Complete member dashboard and read projections

**Saved work:** Member projection source and mounted browser evidence retained 2026-10-06: [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) "Projects: trusted internal execution, exact-workspace Git and member projections, rebased onto main (B1, C2 server, M1)" — independent review PASS, OPEN; its six schema packets (20261006110000/111000/112000/114000/115000/115500) APPLIED AND VERIFIED; switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. Before switch-on: observations block transport deletes (desktop re-sign-in 500) and the old poll hands out bound commands unchecked. 2026-10-07: #6259 still OPEN; M2 readers [#6316](https://github.com/jtobkin/suprafx-platform/pull/6316) stacked on it.

**Remaining:** Merge #6259 when green (switch stays off), then join actual producer/readers and installed authenticated behavior.

**Acceptance:** Audit every dashboard/client prop including digests/ideas/rules/streak, raw board callers, file paths; positive project-chat; real Chromium390/1440 and serialized HTML/RSC private sentinels. Freeze bounded checkpoint.

**Source:** lib/supraos-build/member-plan-source.ts; project/session routes; app/vms/builder/[id]; session SSR

**Prior owner role:** Sol / audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | PR #6259 open, not on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6259 review PASS 2026-10-06 |
| merged | No — #6259 OPEN |
| deployed | Full scope pending |
| activated | No — PROJECT_REVIEWED_SOURCE_V1 OFF |
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

**Saved work:** Narrow Competitor Watch slice deployed; full producer scope open 2026-10-07: [#6298](https://github.com/jtobkin/suprafx-platform/pull/6298) "no owner-private input in shared background prompts" — OPEN, queued to merge when green. 2026-10-07: #6298 independent review PASS; still OPEN (stacked on #6259). 2026-10-08: live privacy leaks found (owner-private memory could reach room guests, check-ins, routines and Mission Control deck shares); no current exposure (0 share links, 1 guest). Fixes: [#6369](https://github.com/jtobkin/suprafx-platform/pull/6369) live leaks (on main) — reviewed, OPEN; [#6368](https://github.com/jtobkin/suprafx-platform/pull/6368) remaining private-input producers (switch-gated, stacked on #6298), packet `20261008110000` APPLIED AND VERIFIED ~20:53Z — reviewed, OPEN; [#6377](https://github.com/jtobkin/suprafx-platform/pull/6377) approved-tools list for shared rooms and late-joiner hiding (stacked on #6369) — reviewed, OPEN. 2026-10-08 later: [#6369](https://github.com/jtobkin/suprafx-platform/pull/6369) MERGED 04:36Z and live (fence ordered before computer-task detection and context building). Live-proof read-only check: the code is live, but the fence has **never run on a shared audience** in production — 0 shared rooms, the only room-posting routine is disabled, the 2 active members point at projects that no longer exist; nothing leaked since deploy. It found 1 public deck link (July) still serving project outputs; owner OK'd revoking it — done (now 0 shared projects; a direct database change, no tamper-proof revoke event). [#6377](https://github.com/jtobkin/suprafx-platform/pull/6377) rebuilt onto main, reviewed, OPEN; #6298 → #6368 OPEN (after #6259).

**Remaining:** Merge #6377, and #6298 → #6368 (after #6259) when green; prove the #6369 fence on a real shared audience (owner call: a real guest or member); then remove any remaining private inputs and verify active worker/card recovery.

**Acceptance:** Use reviewed project quality definitions and structured origin; test actual tick/recovery/template/continuation producers and changed publication. Owner-private sentinel absent in all shared prompts.

**Source:** plan-coordinator; template reviewer; task-completion-boundary; project-plan-dispatch-source; recovery/continuation callers

**Prior owner role:** Next Sol / server. Root must assign a currently available named owner before dispatch. **Original dependencies:** B1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6298 review PASS 2026-10-07; #6368 #6369 #6377 reviewed 2026-10-08 |
| merged | Earlier narrow slices; #6369 merged 2026-10-08 04:36Z |
| deployed | Earlier narrow slices; #6369 live in 604b0e0964 |
| activated | Full scope pending |
| verifiedLive | #6369 live but not exercised on a shared audience (none exists); full authenticated scope pending |

### M2 — Join member result and internal message readers

**Saved work:** Classified member readers joined in scoped native/browser fixture 2026-10-07: [#6316](https://github.com/jtobkin/suprafx-platform/pull/6316) "members read only results bound to the current publication; internal messages stay owner-only" (stacked on #6259) — reviewed, OPEN. Related: [#6300](https://github.com/jtobkin/suprafx-platform/pull/6300) members no longer read the owner's recalled lessons and skills — OPEN. 2026-10-07: #6300 MERGED 10:29:42Z and live; #6316 still OPEN (review PASS); [#6345](https://github.com/jtobkin/suprafx-platform/pull/6345) redaction on member results (stacked on #6316) — review PASS, OPEN. 2026-10-08: #6316 and #6345 still OPEN (stacked on #6259; bases re-merged by the shepherd).

**Remaining:** Merge #6259, then #6316 and #6345 when green; then prove current publication, revocation and real shared-chat transport.

**Acceptance:** Exact current publication/hash/task/job/input/result/accounting and completed_at binding; null summary compatibility; mutation/revocation races; actual HTTP and mounted browser positive/negative. Preserve explicit shared chat.

**Source:** member-plan-source.ts; sessions/[id]/messages; since-you-left digest; 010120/010140

**Prior owner role:** Sol / audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** B1, M1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes in #6316 (open, stacked on #6259) |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6316 reviewed 2026-10-07 |
| merged | Partly: #6300 merged 2026-10-07 10:29:42Z; #6316 and #6345 OPEN |
| deployed | #6300 live in 24273f41e9; rest pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### M3 — Qualify owner-only Realtime transport

**Saved work:** Owner-topic/metadata routing implemented; socket matrix scoped 2026-10-07: [#6336](https://github.com/jtobkin/suprafx-platform/pull/6336) "owner-only Realtime channel behind a default-off drain switch" — reviewed, OPEN; switch `SUPRAOS_RELAY_OWNER_TOPIC_V1` OFF; packet `20261007140000` pending (apply before merge). Owner decision pending: shorten the member Realtime token (15 minutes) so revocation takes effect quickly. 2026-10-07: packet `20261007140000` APPLIED AND VERIFIED (~10:42Z); #6336 still OPEN (switch OFF). Owner ruling: cut off removed members immediately (not after the 15-minute token). [#6354](https://github.com/jtobkin/suprafx-platform/pull/6354) removed members lose the live feed at once (stacked on #6336; switches OFF) — review PASS (caught Realtime notice flooding from its trigger, bounded before merge), packet `20261007160000` APPLIED AND VERIFIED (~15:10Z), OPEN. [#6361](https://github.com/jtobkin/suprafx-platform/pull/6361) removed members lose presence at once (stacked on #6354) — OPEN, packet `20261008100000` pending. 2026-10-08: packet `20261008100000` (#6361) APPLIED AND VERIFIED ~19:51Z; #6336 #6354 #6361 still OPEN (bases re-merged by the shepherd); DB switch `relay_topic_epoch_db_enabled()` reads false (release audit).

**Remaining:** Merge #6336 → #6354 → #6361 (switches stay off); switch B (`SUPRAOS_RELAY_OWNER_TOPIC_V1`) per the activation runbook; then drain old broadcasters and qualify revocation live.

**Acceptance:** Actual socket with already-minted member JWT, owner positive, revoked/joined/nonjoined Room controls; apply/rollback/reapply; old broadcaster drain explicitly gates release.

**Source:** session-broadcast.ts; use-session-realtime; use-agent-insights; 010130 migration

**Prior owner role:** Next Sol / audience. Root must assign a currently available named owner before dispatch. **Original dependencies:** M1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes in #6336, #6354 and #6361 (open) |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6336 #6354 #6361 reviewed |
| merged | No — #6336 #6354 #6361 OPEN |
| deployed | Packets 140000, 160000 and 20261008100000 applied on production; code not merged |
| activated | No — SUPRAOS_RELAY_OWNER_TOPIC_V1 OFF |
| verifiedLive | Full scope pending |

### J1 — Join server, clients and actual native authority

**Saved work:** Joined server/client native and browser source evidence 2026-10-06: inputs reviewed but not merged — server #6259 and client #6256 both review PASS, OPEN; the join itself has not started. 2026-10-07: client #6256 MERGED (live); server #6259 still OPEN; the join has not started.

**Remaining:** Merge #6259 (and #6287), then close native client and deployed transport gaps before final join.

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

**Saved work:** Email/recipient authority source in held draft6138 2026-10-06: [#6253](https://github.com/jtobkin/suprafx-platform/pull/6253) "notifications only reach the owner's verified destinations; uncertain sends are held" — independent review PASS, OPEN. Follow-up: a crash between email claim and send leaves no history line. Owner allowed one real test email to the owner's own address only. 2026-10-06: #6253 MERGED 10:57:48Z and live (main `8e4d2d44b0`).

**Remaining:** One real authorized email (owner's own address) and uncertain-send recovery on production; confirm whether its schema is installed (not recorded here).

**Acceptance:** Derive all to/cc/bcc/channel recipients, current owner, stored/manual/scheduled/resume routes; complete owner authoring before enforcement; reject invalid recipients before provider attempt; native + browser proof.

**Source:** PR6138 227de4f57e35cf111788f8bfca4e50a7d75342f5; qa-lanes/w2-selective-composition-20261003

**Prior owner role:** Sol server integration; Sol member native/provider; Sol workflow approval/browser. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes: #6253 |
| integrated | Yes: #6253 on main |
| tested | Per PR checks; review harness |
| independentlyReviewed | Yes: #6253 review PASS 2026-10-06 |
| merged | Yes: #6253 merged 2026-10-06 10:57:48Z |
| deployed | Yes: live in 8e4d2d44b0 (read 2026-10-07T07:54Z) |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W3 — File operation namespace and destination authority

**Saved work:** Storage namespace and uncertainty source in held draft6132 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`.

**Remaining:** Installed/production proof of allow, deny, revocation and recovery. Install policy/schema and verify real owner, revocation and recovery boundaries.

**Acceptance:** Bind actual bucket/owner namespace, operation and resolved destination; owned read/write positive, traversal/cross-owner negative; original resumed principal; no production storage writes for testing.

**Source:** PR6132 2b68ff4d0dbeb15032cb7b03fa1cabd4ef406350; qa-lanes/w3-storage-unknown-20261003

**Prior owner role:** Sol server composition; Sol workflow Storage/browser; Sol member native admission; root release. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0, W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the file operations slice in #6257 (open) |
| integrated | Yes: #6257 on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6257 review PASS 2026-10-06 (incl. grant-revoke security fix) |
| merged | Yes: #6257 merged 2026-10-07 04:12:40Z |
| deployed | Yes: live in 8e4d2d44b0 (read 2026-10-07T07:54Z) |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W4 — Named OAuth and raw API authority

**Saved work:** Named/raw API authority source in held draft6129 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`.

**Remaining:** Installed/production proof of allow, deny, revocation and recovery. Compose exact final source and qualify installed/provider behavior.

**Acceptance:** Actual method/action/destination/current credentials and owner authoring; definite setup refusal vs attempted unknown; no retry after uncertain effect. Test real adapter boundaries with private local transports.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the API (named/raw) slice in #6257 (open) |
| integrated | Yes: #6257 on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6257 review PASS 2026-10-06 (incl. grant-revoke security fix) |
| merged | Yes: #6257 merged 2026-10-07 04:12:40Z |
| deployed | Yes: live in 8e4d2d44b0 (read 2026-10-07T07:54Z) |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W5 — Child workflow and bot creation authority

**Saved work:** Child/bot creation authority source in held draft6129 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`. The spawn-retry follow-up is addressed by [#6289](https://github.com/jtobkin/suprafx-platform/pull/6289) (a retried child spawn returns the original child), MERGED 2026-10-07 04:13Z.

**Remaining:** Installed/production proof of allow, deny, revocation and recovery. Prove real allowed creation, denied targets and original-child recovery.

**Acceptance:** Define creation/child graph/template/pipeline targets; preserve immutable owner and original graph on resume; deny before creation and prove allowed behavior with usable grant UI.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the child-workflow slice in #6257 (open) |
| integrated | Yes: #6257 on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6257 review PASS 2026-10-06 (incl. grant-revoke security fix) |
| merged | Yes: #6257 merged 2026-10-07 04:12:40Z |
| deployed | Yes: live in 8e4d2d44b0 (read 2026-10-07T07:54Z) |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### X1 — Qualify every supported context entry

**Saved work:** Entry-point context/privacy map and scoped repairs 2026-10-06: a lane for X1 context entries started (running; no PR yet). 2026-10-07: [#6274](https://github.com/jtobkin/suprafx-platform/pull/6274) "qualify every agent context entry (prefs, audience, receipts)" MERGED 03:42:08Z, live; follow-ups [#6285](https://github.com/jtobkin/suprafx-platform/pull/6285) (legacy Telegram entry checks, cancel into delegation + voice workflows, receipt read-back; stacks on #6274) — reviewed, OPEN. 2026-10-07: #6285 MERGED 09:21:26Z and live. 2026-10-08: [#6362](https://github.com/jtobkin/suprafx-platform/pull/6362) read back Mission Control task context receipts (owner only) — reviewed, OPEN; [#6374](https://github.com/jtobkin/suprafx-platform/pull/6374) receipt panel ("what each agent knew") and in-app failure bell (stacked on #6362) — reviewed, OPEN. 2026-10-08 later: [#6362](https://github.com/jtobkin/suprafx-platform/pull/6362) MERGED 06:11Z and live; read-only replay: 4 of 5 stored receipts would read `confirmed`, 1 `not_recorded`; the owner's signed-in response not yet seen. #6374 now targets main, OPEN.

**Remaining:** Merge #6374 when green; see a signed-in receipt read-back; qualify every supported surface live, including background and System Workflow runs.

**Acceptance:** Entry-by-entry current preferences, relevant bounded recall/skills/lessons, identity/audience, captured+consumed receipt, cancellation/recovery and actual entry positive/negative; no owner-equality shortcut. Include workspace execute, MC cron, org tasks and both workflow engines.

**Source:** agent-chat/stream; agent-execute; voice-router; telegram-agent-turn; delegate-tool; coordination engines; research/Room/background entry routes

**Prior owner role:** Sol workflows. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0, X2, X3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes: #6274 #6285 #6362 merged; #6374 open |
| integrated | #6274 #6285 #6362 on main; #6374 open |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6274 #6285 #6362 #6374 reviewed |
| merged | Yes: #6274 merged 2026-10-07 03:42:08Z; #6285 merged 09:21:26Z; #6362 merged 2026-10-08 06:11:55Z |
| deployed | #6274 #6285 #6362 live in 604b0e0964; #6374 pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### A1 — Finish global attention and baseline source gaps

**Saved work:** Attention/Room/shelf/mail foundations; global cutover remains off 2026-10-08 release audit: the global attention batch function is not installed in production, so packet 220000 (another session) is a no-op there.

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

**Saved work:** ad2ee680 partial successor pushed in draft6190, scoped52/types14/review PASS; required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; prior1c0 CI RED preserved; earlier privacy slices shipped; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: composed `3214f4849e3bb0517b60ee17821826918ee11147` in PR #6196; duplicate-version ratchet clean; writer catalog PASS (2,657 rows); box-ci pending. 2026-10-08 release audit (read-only, ~22:35Z 2026-10-07): R1 NOT done — main green at the live commit but many project PRs open (some stacked, some conflicting with bases at audit time, re-merged since by the shepherd), 15 packets live ahead of their code, box-ci queue ~66 jobs; 5 of the last 13 main checks red, all flakes (native Postgres initdb timeouts under load, fixed by #6373, merged). The text above (frozen 3214f48, #6160) is stale: #6196 merged 2026-10-05, #6160 is closed. Outside this project: #6235 (CRM intake, another session) packet 20261006143000 is on main but not applied to production (live code falls back; handed to that session).

**Remaining:** Merge the remaining open project PRs via merge-if-green (packets first); retire the stale frozen-head text; reconcile outside-lane packet gaps with their owners.

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

**Saved work:** Private stop/install/unknown recovery and dated restore proofs 2026-10-08 (2026-10-07 20:20–21:20Z, owner-approved quiet hours): restore rehearsal with our backup tool PASSED for its scope (public + migration ledger): read-only exported snapshot; 50/50 key-table counts equal; 867/867 tables restored with exact counts (54.1 M rows); ledger 773 equal; schema digest equal (15/16 classes byte-exact, constraints equal after documented flattening); roles/grants reproduced; packet 20261007134500 forward/rollback/forward round trip PASS in the copy. Production contact 20.4 min; site 69/69 samples HTTP 200, 0 over 2 s; 0 sessions blocked; no production write. Side effect: the deploy lock was held 51 min. Gaps: 339 owner/agent/node schemas (2,022 tables, ~147 MB), auth/storage/vault/realtime and storage files are outside the tool's scope; packets touching realtime cannot be rehearsed on this copy; snapshot taken with writers running (cannot admit a release). [#6381](https://github.com/jtobkin/suprafx-platform/pull/6381) widens the backup tool to every owner and agent schema and stops it blocking deploys (review caught a lock-exhaustion bug — production has 10,240 lock slots — fixed before merge) — OPEN. Backup-test leftovers removed from the web host with owner OK. 2026-10-08 later: [#6381](https://github.com/jtobkin/suprafx-platform/pull/6381) MERGED 02:43Z (script on main; not yet run). Read-only catalog pre-check: 339 product schemas, no unknown schema, lock budget well above the rehearsal's — the tool's pre-flight should not refuse (inference; not run).

**Remaining:** Re-run the rehearsal with #6381 to cover owner/agent schemas, or use the provider's restore-to-new-project for full fidelity incl. auth/realtime/vault; held-window writer drain and wiring drain census + restore into the live release gate; a written decision on storage files.

**Acceptance:** Continuous REST+directPG admission closure, in-flight/unknown effect accounting and mixed-client/broadcaster drain; authorized production-copy role/grant-faithful restore/rehearsal. Never manufacture acceptance with production effects.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.

**Prior owner role:** Root / operator gate. Root must assign a currently available named owner before dispatch. **Original dependencies:** R2, R3B.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Restore rehearsal PASS 2026-10-07 for public scope (owner/agent schemas not covered) |
| independentlyReviewed | #6381 reviewed (lock-exhaustion fix); rehearsal evidence private |
| merged | #6381 merged 2026-10-08 02:43Z; full scope pending |
| deployed | Full scope pending |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### I1 — Compose and independently qualify final source

**Saved work:** ad2ee680 integrates reviewed guard/manual/Telegram repairs on1c0;52 scoped tests/types14/review PASS; exact successor required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; unchanged UI has scoped Linux privacy proof; full final source open; paused successors48751b50/2dc7e380/82b01044 are separate and unqualified as a combined release. 2026-10-05: frozen `3214f4849e3bb0517b60ee17821826918ee11147`; conflict resolutions reviewed by the verification lane in the trailing audit. 2026-10-08 release audit: not started as specified — the project ships PR by PR, so no single frozen final head exists yet.

**Remaining:** After the last project PR merges: record main's sha; run full box-ci (both checks), macOS Native Land and the prod-shape harness S1–S13 on it; one independent review of the composed diff since ac48190955.

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

**Saved work:** Global/workflow activation not claimed 2026-10-08: switch A (background-queue expiry) is on by default since #6332 went live (env value not re-read). Switches B–F stay OFF.

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

**Saved work:** Portable handoff maintained; final owner confirmation pending 2026-10-08: plain-English owner guide written (what is live vs waiting vs off, everyday how-to, troubleshooting, open decisions); private.

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

**Saved work:** Atomic grant reservations source in held draft6129 Related grant changes shipped 2026-10-05 (not W6 acceptance): PR #6206 (main `2e242177b3`) lets workflow grants last 1 hour / 24 hours / 1 week / 1 month / 1 year and keeps one card per workflow + action; PR #6219 (main `3f18ef481c`) stops the default-permission lookup crashing on `workflow:<id>` agents (a regression from Agent Run #6168). The owner approved their own two pending workflow grants for 1 year (18:13Z, expire 2027-10-05); other owners' cards are theirs to approve. 2026-10-06: [#6257](https://github.com/jtobkin/suprafx-platform/pull/6257) "Grants: file, API, child-workflow and one-use limits proven (W3–W6)" — independent review PASS, OPEN; includes a SECURITY fix (another account could revoke an owner's grant). Follow-up: spawn retry does not return the child id. 2026-10-06: #6226 (approved cards clear, duration survives reload) MERGED; [#6247](https://github.com/jtobkin/suprafx-platform/pull/6247) one grant card per request under load — review PASS, OPEN, packet `20261006050000_one_pending_workflow_grant_card` APPLIED AND VERIFIED (0 duplicate pending cards beforehand). 2026-10-07: #6257 MERGED 04:12:40Z (includes the SECURITY fix: another account could revoke an owner's grant) and live in main `8e4d2d44b0`. #6247 (one grant card per request under load) MERGED 04:12:59Z.

**Remaining:** Installed/production proof of allow, deny, revocation and recovery. Prove installed concurrent use, revocation and original receipt recovery.

**Acceptance:** Concurrent one-use attempts cannot both enter provider/storage; original invocation recovery does not consume twice or replay an uncertain effect; revocation/expiry and personal compatibility controls.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the one-use limits slice in #6257 (open) |
| integrated | Yes: #6257 and #6247 on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6257 review PASS 2026-10-06 (incl. grant-revoke security fix) |
| merged | Yes: #6206 #6219 (2026-10-05), #6226 (2026-10-06), #6257 #6247 (2026-10-07) |
| deployed | Yes: live in 8e4d2d44b0 (read 2026-10-07T07:54Z); packet 20261006050000 applied 2026-10-06 |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### W7 — Original-operation workflow effects

**Saved work:** Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open; paused drain/server/SQL48751b50 and mounted rerun client2dc7e380 now committed/pushed; actual source callers integrated with scoped tests and browser evidence. Native drain contract remains unrun. 2026-10-05 resume: three saved lanes composed into `3214f4849e3bb0517b60ee17821826918ee11147`; native 26/26 with committed fixture; caller repairs F1/F3/F4; browser 46/46; open boundaries F2/F5 documented. 2026-10-05 ~05:00Z: trailing audit at `3214f4849e` PASS but scoped (native 26/26; ordered 24/24 install + VERIFY; browser 46/46 + 2/2 F1; unit 896 pass / 0 fail / 7 skipped; relay x1-bridge 28/28). Required box-ci on the same commit is RED (security-gates FAILURE; production-build ERROR; whole unit tree 2 failed / 55,609 passed / 374 skipped): three candidate defects. `3214f4849e` was NOT releasable and was replaced. 2026-10-05 05:36Z: new candidate `ac4819095585eed003eb0c510b0a8c8608d5e73f` (= `3214f4849e` + fix commit `867a5f2114` + clean merge of origin/main `7a10b7a3fc`) has required box-ci GREEN (security-gates SUCCESS 51 steps; production-build SUCCESS 7 steps) and an independent trailing audit PASS 5/5 (fix diff; native 26/26; ordered 24/24 applied and verified; browser 46/46 + 2/2 F1; scoped unit 924 passed / 7 skipped / 0 failed on the second run, one load-related timeout on the first, LOW flake risk). At 05:36Z it was not merged, not installed and not deployed. 2026-10-05 05:42–06:35Z: owner instruction during the run: "automerge and automigrate as needed"; sequencing with Agent Run PR #6168 resolved (W7 first). Backup before install: a sealed archive of the `public` and `supabase_migrations` schemas was taken 05:42–06:02Z (dump 5.4 GB); row counts match the source (ledger 691, plans 39). The backup is NOT restore-verified. Disclosed deviation: the backup tool's default free-space floor is 80 GiB and the host had 60.4 GiB, so it was run with the tool's own `--min-free-gib 60` option. Production install 06:03–06:10Z from the frozen worktree at `ac48190955`: 24/24 packets "APPLIED AND VERIFIED" via `scripts/apply-migration.mjs`. Read-back: ledger 691 → 715; 24/24 W7 versions present; `vms_mc_execution_admission_gate.admission_open = true`; `settle_mc_task_v1` present; `vms_mc_plan_birth_guards` present with 0 rows; 10 `vms_mc` tables; 0 active plans. Merged 06:11:22Z via `scripts/ci/box-ci/merge-if-green.sh` (squash) → main `55a12f0da9b09052d0bfa186f747654a60f3a931`. Deployed: deploy-main log "live: 55a12f0da health 200" at 06:24:35Z; `https://supraos.ai/api/version` reports `55a12f0da9` (re-read anonymously at 06:31Z for this record). Old code ran against the new SQL for 21 minutes (06:03–06:24Z); no plan was created in that window. The mc-coordinator cron returned 200 every minute after deploy; no cron newly failing. Activated: yes by construction — there is no feature flag, so code + SQL deployed means live. 2026-10-05 06:35–07:45Z live acceptance on production: Behaviour C PASS (~06:35Z, approximate; signed-in owner, real Chrome, production): Re-execute on a pre-release plan was refused and nothing was created (plan unchanged, 0 rerun receipts). LIVE DEFECT 1 (found 06:46–06:58Z): the first real Mission Control project created after the release (2 tasks, made through the normal New project screen) cannot finish. Its first task settled. Its FINAL task produced output and has a completed, approved claim receipt, but the settle function rejects the terminal transition with "terminal plan chain is not bound to settled plan" (migration `20261005230000`, the `plan_chain_log` check) on every coordinator tick, so the plan stays `running`. Positive observations on the same project: the birth-proof row was written (finding F1 holds live) and both tasks were claimed through receipts. LIVE DEFECT 2 (verified by code and production data): every claimed task writes L1-anchor effect intents whose delivery has no positive branch — they end `held_unknown` (reason `high_value_anchor_capability_unverified`) — while the rerun function refuses with `unknown` unless every effect of the current run is `delivered`. Consequence: no plan born after the release can be re-executed, and plans born before it are refused as `unproven_legacy`. Re-execute is therefore unavailable for ALL projects until fixed, and behaviour B (lost-acknowledgment rerun) cannot be accepted live yet. Behaviour A (critical-failure drain) is NOT drivable on production from any control: Mission Control's project route writes an empty critical path, so its plans never have a critical task; there is no owner "mark failed" control; and an owner-declared failure is re-dispatched automatically. Only Workspace-planner plans carry a critical path (17 of 40 production plans). The drain's evidence remains the build-box contract cases only. The pre-release suites passed but were insufficient: the 26 native contract cases and the 46 mocked browser cases did not exercise the real server path with production-shaped data, and both live defects passed through them. Operator decision: Mission Control admission is left OPEN while a hotfix is prepared — work is not lost; affected plans wait at their last task. Revisit if the fix is slow. Work in progress: (a) hotfix branch `claude/w7-final-task-settle-fix-20261005` for defects 1 and 2 — root cause in progress, PR not yet open, branch not on the remote when checked at 07:44Z; (b) PR [#6198](https://github.com/jtobkin/suprafx-platform/pull/6198) "Mission Control plans get a critical path" — OPEN (branch `claude/w7-mc-critical-path-20261005`, head `19d4d01eae`), an owner decision because it changes behaviour: a third failure on the main chain fails the project instead of skipping; (c) follow-up PR [#6197](https://github.com/jtobkin/suprafx-platform/pull/6197) — OPEN, held (head `1de6f98ed2`); (d) a production-shape end-to-end harness lane; (e) a read-only audit of every other guarded control; (f) a planner-screen bug lane — a malformed planner answer produced a launchable 0-task plan, and the review panel did not follow the selected plan. Stage truth: implemented yes; integrated yes; tested — pre-release suites passed but were insufficient; independently reviewed yes; merged yes (`55a12f0da9`); deployed yes; activated yes; verified live NO — 1 of 3 behaviours passed (C), 1 blocked by live defects (B), 1 not drivable (A). The W7 milestone is NOT complete. Process lesson (recorded under EP11): acceptance must drive the real server path against a real database with production-shaped data before release; fixture-only contract cases plus mocked-boundary browser cases are not proof. 2026-10-05 07:45–08:55Z, production stabilisation: hotfix PR #6199 opened (`claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a`) fixing faults 1 and 2 with packet `20261005232000_mc_rerun_unsent_anchor_hold` (build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match; box-ci green at the earlier head `420a71db33`, pending at the current head). A read-only audit of every guarded control (28 direct plan writers, 17 now rejected) and a production-shape end-to-end harness (S1–S9; all scenarios fail on main, S1–S3 and the Workspace drain pass on the fix) raised the fault count to eight. EIGHT FAULTS found live or by audit: (1) The final task of every agent-run plan cannot settle, so the plan stays `running`. Cause: `buildMcPlanFinishIntents` (`lib/vms/workflows/mc-plan-finish-intents.ts:61`) never sent `taskId`; `settle_mc_task_v1` requires it (`supabase/migrations/20261005230000_mc_critical_failure_drain.sql:541`). FIXED in PR #6199 (not merged). (2) Re-execute is dead for every project: L1-anchor effects always end `held_unknown`, six effect kinds have no receiver and stay pending, and `rerun_mc_plan_v1` (migration `20261005231000` ~129-133) refuses unless every effect is delivered; pre-release plans are refused `unproven_legacy`. FIXED in PR #6199 by packet `20261005232000` (not merged, packet not applied); pre-release plans still refused — owner decision 3. (3) The critical-failure drain cannot fire for Mission Control projects: `app/api/projects/route.ts:305` writes an empty critical path. Fix = PR #6198 (owner decision 2). (4) Any task failure on a projects-route plan wedges it: "invalid target task transition" (migration `20261005230000`:274-281; `plan-orchestrator.ts` ~869-883 retries the same preferred agent). NOT fixed, NO lane yet. (5) An unknown-outcome task can never be resolved (the resolve route writes directly, the guard rejects → 503); per-task Stop returns 500; cancel refuses while a task runs; review / outputs / Settings pause-complete-fail are silent no-ops. WIP on `claude/w7-guarded-owner-controls-20261005`. (6) Delete project fails or orphans a running plan; one rejected write aborts the whole coordinator tick. WIP on `claude/w7-delete-and-tick-isolation-20261005`. (7) Scheduled path: a run killed by a restart, a crash between claim and start, Run-now, a human-approval step (needs the unset switches) or a cancelled interval slot each stop that ONE workflow's schedule for good; for-each steps fail on a repeated target; workflow delete returns 500. WIP on `claude/scheduled-occurrence-live-fixes-20261005` (untested). (8) Planner screen (`/vms/mission-control/new`): a malformed planner answer produced a launchable 0-task plan and the review panel did not follow the selected plan. WIP on `claude/planner-zero-task-plan-20261005` (unverified). SCHEDULED-WORKFLOW INCIDENT: the release carried a new once-only scheduler (an "occurrence claim" path) that holds every due workflow while the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER` is unset. It was unset on production, so all 534 scheduled workflows were paused from 06:24Z to 07:57Z. The owner chose to turn the switch on (set in the production settings store and applied 07:57Z under the deploy lock) and said the missed runs need NOT be re-run. Since then, to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds, 0 duplicates), but 55 of 85 runs failed (65%; about 2% the day before). 27 of the failures are waiting for a new per-action permission grant that the same release introduced: every API / Gmail / Calendar / send-email / file / bot step now needs an explicit grant (`lib/vms/workflows/execution-engine.ts` ~3604-3617), previously un-gated — an owner decision. The three sibling switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) are unset. The scheduler is ACTIVATED by owner choice but NOT qualified per its cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`). The verdict on file says leave the switch ON (it fails safe; off pauses everything); a duplicate slot is the only reason to turn it off. Root cause of the miss: the deploy-safety review checked only the Mission Control files for new environment switches, not the whole diff. PRs and branches (all pushed; heads re-read from the remote at 08:46Z): [Hotfix: final task settles + Re-execute unblocked] PR #6199 `claude/w7-final-task-settle-fix-20261005` @ `dfebdab30a` — OPEN, not merged. Packet `20261005232000_mc_rerun_unsent_anchor_hold` is FINAL — apply to production BEFORE merge. Build box: 25/25 packets verified as non-superuser, native 27/27, rollback + reapply match. box-ci was green at the earlier head `420a71db33`; at the current head both box-ci checks were still PENDING when read at 08:46Z. Not done: scoped vitest at this head, conflict check against #6168. [Follow-ups: schema snapshot refresh, sweep fix, manifest re-pin] PR #6197 `claude/w7-followups-20261005` @ `1de6f98ed2` — OPEN. box-ci GREEN (both checks success, re-read 08:46Z), independently reviewed. Mergeable. The snapshot must be refreshed again after packet `20261005232000` is applied. [Mission Control plans get a critical path] PR #6198 `claude/w7-mc-critical-path-20261005` @ `19d4d01eae` — OPEN. box-ci GREEN (re-read 08:46Z). OWNER DECISION (changes behaviour). [Owner controls (resolve / stop / review / outputs / settings)] `claude/w7-guarded-owner-controls-20261005` @ `f7999b06ee`, no PR — WIP. Packet `20261005233000_mc_unknown_task_owner_resolution` drafted and verified on the build box (8/8 native). TypeScript written but NOT type-checked, no unit tests, UI not done. "I'll handle it" → closed as skipped is a behaviour choice needing sign-off. [Delete project + coordinator tick isolation] `claude/w7-delete-and-tick-isolation-20261005` @ `a9e41aee05`, no PR, stacked on #6197 — WIP. 19 tests pass, browser check PASS. Left: dependent vitest, changed-types, writers catalog, duplicate-migration check, merge main, open PR. [Scheduled workflows fixes] `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe`, no PR — WIP, untested, nothing reproduced on a real database. Do NOT apply its packet `20261005235000`. [Production-shape end-to-end harness (S1–S9)] `claude/w7-prod-shape-e2e-20261005` @ `f146740999`, no PR — Works. On main all scenarios fail; on the fix S1–S3 and the Workspace drain pass. [Planner 0-task plan + panel] `claude/planner-zero-task-plan-20261005` @ `689cbe8d72`, no PR — WIP committed by the root at pause: unverified, tests not run, no browser check. [Evidence (private)] `docs/w7-resume-evidence-20261005` @ `b11636b366` — Install log, acceptance screenshot, audit, end-to-end results, flag-on verdict. [Other session] PR #6168 Agent Run `codex/agent-run-release-composition-20261004` @ `9a0624083f` — OPEN, NOT merged, paused by the owner. Merge hold is LIFTED ("merges open"). It conflicts with W7 files; whoever resumes it re-merges main. Reserved migration versions: `20261005232000` (PR #6199, final), `20261005233000` (owner controls), `20261005234000` (delete/tick, unused so far), `20261005235000` (scheduled; do not apply). The Agent Run release uses nothing above `20261003021000`. Always re-check for collisions against main AND the production ledger. OWNER PAUSE at 2026-10-05 ~08:55Z (the second pause of the day; the first was ~04:47Z): all six lanes are stopped, their work is committed and pushed, nothing is running, and nothing from this project was merged after PR #6196. Release rules learned 2026-10-05 (recorded under EP11): grep the WHOLE diff for new `process.env` reads and write down what the code does when each is unset in production; after every deploy compare before/after rates of high-volume background jobs (rows per 15 minutes), not just "cron returned 200"; acceptance must drive the real server path on a real database with production-shaped data, including the last step of each flow. 2026-10-05 09:00Z → 22:23Z PRODUCTION STABILISATION (handed off 2026-10-06 01:55Z): all eight faults fixed and live through 14 PRs, each independently reviewed and merged with merge-if-green.sh: #6196 `55a12f0da9` (W7 release: squash of the composed failure-drain/rerun candidate `ac48190955`); #6199 `c1513db29c` (the final task of a plan settles again (finish intents now carry the task id) + packet `20261005232000`); #6197 `7b28f6a41a` (schema snapshot refresh; coordinator sweep skips drain-refused plans; manifest re-pin); #6198 `ec1e1132fe` (Mission Control plans get a critical path, so the drain can fire (owner said yes)); #6206 `2e242177b3` (workflow grants can last 1 hour / 24 hours / 1 week / 1 month / 1 year; one card per workflow + action); #6205 `aeebec0da0` (safe Delete project (refuse or archive instead of orphaning a running plan); one bad plan no longer aborts the coordinator tick); #6211 `38ef1efa84` (planner: no 0-task launch; review panel follows the selected plan; long chat scrolls); #6219 `3f18ef481c` (grants: a `workflow:<id>` agent no longer crashes the default-permission lookup (regression from Agent Run #6168)); #6213 `0622e4ea36` (test and source record for packet `20261005239000` (the packet was already live)); #6212 `2df2d3b0cc` (scheduled workflows: stalls after restart / lost reply / Run-now / cancel fixed; for-each and delete fixed; pause banner + Release; packet `20261005235000`); #6220 `9ab57850bd` (an alert for an owner without Telegram is skipped and the run completes; coded errors with logged causes); #6222 `c7e4e9b150` (a failed task retries with a different agent (the preferred agent no longer overrides the failed-agents list)); #6207 `9dcef69a69` (older projects: Duplicate and Adopt (packet `20261006000700`) + plain-English refusal wording); #6223 `e0d776651c` (alerts for owners not yet admitted (invite-required) no longer fail); #6221 `0d25a537b4` (owner controls: resolve an unknown outcome, per-task Stop is final, review / outputs / settings work or say why (packet `20261006010000`)). Five extra packets applied and verified on production: `20261005232000_mc_rerun_unsent_anchor_hold` (2026-10-05 09:00Z); `20261005239000_mc_rerun_unadmitted_effect_hold` (2026-10-05 14:41Z); `20261005235000_scheduled_occurrence_recovery` (2026-10-05 19:55Z); `20261006000700_mc_legacy_plan_adoption` (2026-10-05 21:17Z); `20261006010000_mc_unknown_task_owner_resolution` (2026-10-05 22:22Z); production ledger 743 (the Agent Run session installed its own 19). Live acceptance B PASS 17:36Z (project `43470d88`). Evidence pushed to private branch `docs/w7-resume-evidence-20261005` @ `9ec3ab950d`. Production incidents found and fixed during the run: (1) **Scheduled workflows paused 06:24–07:57Z on 2026-10-05.** The W7 release carried a once-only scheduler that holds all due work while its switch (`WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`) is unset; it was unset in production, so all 534 scheduled workflows stopped for 93 minutes. The deploy-safety review missed it because it checked only the Mission Control files for new switches, not the whole diff. Fixed by the owner turning the switch on at 07:57Z (missed runs not re-run); remaining scheduler stalls fixed by #6212. (2) **Telegram "Liq Warning" alerts failing from 13:15Z to ~22:08Z on 2026-10-05.** A regression from the Agent Run release (#6168): first the permission lookup crashed on workflow-style agent ids, then alerts for owners not yet admitted failed when their settings were read. A catch-all error code hid both causes. Fixed by #6219, #6220 and #6223; 0 alert failures in the 15 minutes after the last fix. 2026-10-06 02:17Z resumed. 03:01Z LIVE ACCEPTANCE A on production: **A PASS with a finalisation gap** (2026-10-06 03:01Z, production, signed-in owner; project `bacf0dc8` "W7 drain test", born after #6198 so it carries a critical path of task-1 → task-2). Method: a temporary House Rule "always ask above $0.001" on all 35 active agents (set through the House Rules screen, removed afterwards; 0 left in the database) refused task-1 before dispatch — a pre-dispatch gate, not a real model failure. task-1 failed twice (two different agents); attempt 3 went to a shared-computer agent that BYPASSES the House Rules gate, ran ~4 minutes and ended `outcome_unknown`/blocked; the owner used Resolve → Retry (#6221, live); attempt 4 failed; retries reached 3; the `critical_failure_drain` and `critical_escalation` effects were delivered; task-2 was `skipped` with drain reason `critical_failure_unstarted`; the plan was never completed. **Gap (live):** the plan stays `running` for ever — the terminal-blocked rule (packet `20261005230000`, `mc_drain_terminal_blocked_v1`) still counts the settled unknown-outcome receipt after the owner resolved it; the coordinator skips draining plans, execute refuses, so nothing finalises; the same rule blocks Re-execute (active claim). Fix in progress: packet `20261006020000` on branch `claude/w7-owner-resolution-unblocks-20261006` plus a sanctioned finaliser; no PR yet. Evidence: private evidence lane, `live/acceptance/A-critical-drain-PASS-with-gap.md`. Findings from live test A (2026-10-06): (1) shared-computer agents bypass House Rules (the pre-dispatch gate does not apply to them); (2) a skipped task renders as "planned" on the project screen — no drain wording; (3) an owner Stop on an unstarted critical task wedges the plan (retries 0 → 1, the task cannot fail again; design-lane finding). W7 verified live = 3 of 3 behaviours observed (A with the gap, B, C); NOT accepted. Open PRs (all independently reviewed safe; merges held by the Agent Run session until its audit-fix #6225 landed — #6225 MERGED 2026-10-06 03:21:38Z → main `4c9208fc5f`; merge order after it): [#6226](https://github.com/jtobkin/suprafx-platform/pull/6226) grants: approved cards clear, chosen duration survives a reload, one card per request; [#6227](https://github.com/jtobkin/suprafx-platform/pull/6227) planner works on a phone + design for re-executing after an unknown outcome; [#6229](https://github.com/jtobkin/suprafx-platform/pull/6229) archived projects cannot run, counts and lists exclude them, no 0-task projects (review PASS); [#6230](https://github.com/jtobkin/suprafx-platform/pull/6230) production-shape end-to-end harness S1–S13 (review PASS; do NOT enable the box-ci step yet); [#6233](https://github.com/jtobkin/suprafx-platform/pull/6233) a task every agent has failed no longer waits for ever; a held task alerts the owner. 2026-10-06 ~10:00Z: #6239 (owner resolution unblocks a drained plan + finaliser; packet `20261006020000` applied 07:12:36Z) MERGED 08:54:46Z, live 09:08:47Z → live test A CLOSED (plan `ee4c97bc` `failed` 09:09:21Z; owner not notified — fixed by #6255, open). #6233 (exhausted agents skip/escalate + held-task alert) MERGED 09:26:41Z; #6230 (e2e harness S1–S13) MERGED 09:37:10Z (box-ci step not enabled); #6226 #6227 #6229 merged earlier. Open with packets already applied: #6255 (030000), #6252 (040000), #6249 (060000); #6246 House Rules cover computer agents (review PASS). 2026-10-07 (~07:50Z): merged and live — #6252 (owner's last decision finishes the project; Stop on a critical task drains it), #6275 (task tools bind to the saved attempt; owner card answers reserved before any effect), #6276 (send tools: a lost reply is an unknown outcome), #6289 (manual actions obey claim rules; retried child spawn returns the original child), #6247, #6283 (test flake); #6246 merged 2026-10-06. Effects parity: #6275 #6276 #6289 merged; [#6301](https://github.com/jtobkin/suprafx-platform/pull/6301) (owner review and Stop go through effect intents; six never-delivered effect kinds stopped) OPEN with packet `20261006153000` APPLIED. Safe cancellation: [#6277](https://github.com/jtobkin/suprafx-platform/pull/6277) OPEN with packet `20261006151000` APPLIED. Open demo/MC fixes: [#6311](https://github.com/jtobkin/suprafx-platform/pull/6311) true end state, [#6330](https://github.com/jtobkin/suprafx-platform/pull/6330) real agents on cards, [#6332](https://github.com/jtobkin/suprafx-platform/pull/6332) self-heal (packet `20261007134500` scheduled 09:25Z), [#6333](https://github.com/jtobkin/suprafx-platform/pull/6333) a plain goal always yields a plan, [#6334](https://github.com/jtobkin/suprafx-platform/pull/6334) tool tags never run from text (security review caught a prompt-injection hole in v1), [#6315](https://github.com/jtobkin/suprafx-platform/pull/6315) e2e harness S1–S13 PASS on main, [#6321](https://github.com/jtobkin/suprafx-platform/pull/6321) chat diagnostics. LIVE REHEARSAL 2026-10-07: the Mission Control flow works live when the owner's desktop app is open; tasks run only through the desktop app; 233 stale queued jobs parked (owner: delete); a 2-task project finished in ~70 s. 2026-10-07 later: #6255 (drained project says so; owner told) MERGED 14:48:22Z and live — but the owner has no Telegram destination, so the alert is recorded and cannot be delivered; #6311 (true end state) #6315 (harness S1–S13) #6321 (chat diagnostics) merged and live. Packet `20261007134500` (#6332) APPLIED AND VERIFIED ~09:25Z; packet `20261007152000` (#6344, owner review notes reach the agent's own memory, stacked on #6301) APPLIED AND VERIFIED ~12:43Z. Still OPEN with review PASS: #6249 #6277 #6301 #6330 #6332 #6333 #6334 #6344; [#6356](https://github.com/jtobkin/suprafx-platform/pull/6356) chat keeps the real model error (diagnostics) OPEN. Owner paused 16:10Z, resumed 18:20Z. Live re-tests for #6249/#6277/#6255 prepared, not run. 2026-10-08: [#6330](https://github.com/jtobkin/suprafx-platform/pull/6330) cards show real agents MERGED 2026-10-07 19:38:37Z; [#6333](https://github.com/jtobkin/suprafx-platform/pull/6333) a plain goal always yields a plan MERGED 20:08:40Z; [#6249](https://github.com/jtobkin/suprafx-platform/pull/6249) interrupted Re-execute never wedges (Discard this run) MERGED 21:01:32Z; [#6334](https://github.com/jtobkin/suprafx-platform/pull/6334) raw tool tags hidden and never executed from text MERGED 21:02:00Z; [#6332](https://github.com/jtobkin/suprafx-platform/pull/6332) Mission Control tasks self-heal (stale desktop lock, offline message, queue priority, revivable 24 h expiry; switch A on with it) MERGED 23:51:25Z — all live in `0cb2eed5ff`. [#6373](https://github.com/jtobkin/suprafx-platform/pull/6373) CI: native Postgres test clusters start reliably (120/120 initdb timeouts → 0 in the lane) MERGED 2026-10-08 00:35:52Z. Still OPEN with review PASS: #6277 #6301 #6344; #6356 chat keeps the real model error (reviewed, queued). Live re-tests still not run. 2026-10-08 later: [#6277](https://github.com/jtobkin/suprafx-platform/pull/6277) Stop while running MERGED 01:36Z; [#6356](https://github.com/jtobkin/suprafx-platform/pull/6356) chat keeps the real model error MERGED 05:17Z; [#6372](https://github.com/jtobkin/suprafx-platform/pull/6372) grant durations, House Rules cost-floor warning, card counts and Telegram notice MERGED 05:36Z; [#6395](https://github.com/jtobkin/suprafx-platform/pull/6395) project-page agent lanes MERGED 06:32Z — all live in `604b0e0964`. #6372 seen on screen signed in (grants page "At its limit" + duration copy; Mission Control "link Telegram" notice). #6277 and #6356 are live but NOT exercised on production (no Stop pressed, no failing turn since). A stuck plan (running since 10-07) and a chat-dock JSON error found; fixes [#6423](https://github.com/jtobkin/suprafx-platform/pull/6423) and [#6428](https://github.com/jtobkin/suprafx-platform/pull/6428) OPEN.

**Remaining:** The W7 drain/rerun milestone is live and its 3 behaviours PASS (A closed 2026-10-06); the full W7 task is NOT accepted. In order: (1) merge #6301 (153000) → #6344 (152000), #6423, #6428; (2) live re-tests one at a time: Re-execute recovery (#6249), Stop while running (#6277), drain + owner alert (#6255) — the owner alert needs the owner to link Telegram; (3) desktop 0.1.59 (RC qualified, awaiting owner install) carries the desktop half of #6332/#6347; (4) remaining W7 scope — effects parity (#6301 and any remaining kinds), real L1 anchoring, runtime role (R3B); see the first real failing turn's cause (#6356); Stripe Link (owner, external); QA invite. Follow-up: #6252 review "reject" on a critical task drains the plan (undisclosed). Full project: 33 tasks, 16 behaviour families, 12 surfaces; iMessage deferred, WhatsApp excluded.

**Acceptance:** Thread server ToolContext identity, reserve before effect, preserve original run and unknown outcome, reject missing/forged identity, prove cap/no replay via actual transport. Bind actual task settlement to the original saved execution claim atomically; reject superseded results before effects and recover post-commit delivery without duplication. Prove usable original-child lookup/recovery and keep unsupported callers explicit.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.; new branches/commits in pause checkpoint.

**Prior owner role:** release_integration: isolated claim/settlement production repair; release_verification: independent tests; root: composition/release. Root must assign a currently available named owner before dispatch. **Original dependencies:** W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes for the drain/rerun milestone and all 2026-10-05 faults; 2026-10-06: finalisation after owner resolution (#6239) and exhausted-agents skip/escalate (#6233) merged; #6246 (2026-10-06) and #6252 #6247 #6275 #6276 #6289 (2026-10-07) merged; #6255 merged 2026-10-07; #6249 #6330 #6332 #6333 #6334 merged 2026-10-07; #6277 #6356 #6372 merged 2026-10-08; #6301 #6344 open. Effects/manual parity, active cancellation, L1 anchoring still open. |
| integrated | Yes: #6196 + 14 stabilisation PRs + 2026-10-06/07 follow-ups (#6226 #6227 #6229 #6239 #6233 #6230 #6246 #6252 #6275 #6276 #6289 #6247 #6283) on main (live = 8e4d2d44b0); 2026-10-07 later: #6255 #6311 #6315 #6321 (live = 24273f41e9). 2026-10-07/08: #6330 #6333 #6249 #6334 #6332 (live = 0cb2eed5ff); #6373 (CI) on main. 2026-10-08: #6277 #6356 #6372 #6395 #6396 (live = 604b0e0964). |
| tested | Yes per PR: required box-ci checks green at each merge (merge-if-green.sh); five extra packets APPLIED AND VERIFIED on production. Lesson kept: fixture contract cases and mocked browser tests missed three live faults; the production-shape end-to-end harness (S1–S3, S9 and the Workspace drain PASS on the hotfix) is PR #6230 (S1–S13, review PASS), proposed — not enabled — as a box-ci step. Approval-switch rehearsal on the build box: 13/13 + 78/78 + 7/7 contract, 29/29 packets, 7/7 two-tick drive (GO). 2026-10-06: e2e harness S1–S13 merged (#6230); box-ci step not enabled (owner: not yet a required gate). |
| independentlyReviewed | Yes: an independent review for each of the 15 PRs before merge (per the run record). The candidate review at ac48190955 had missed the live faults and the scheduler switch. |
| merged | Yes: #6196 (55a12f0da9) and #6199 #6197 #6198 #6206 #6205 #6211 #6219 #6213 #6212 #6220 #6222 #6207 #6223 #6221 (last: 0d25a537b4, 22:23:13Z 2026-10-05). Verified MERGED on GitHub 2026-10-06 ~02:00Z. 2026-10-06: #6226 #6227 #6229, #6239 (08:54:46Z), #6233 (09:26:41Z), #6230 (09:37:10Z → e89acee6d2). 2026-10-06: #6246 (10:22:59Z). 2026-10-07: #6252 #6275 #6276 #6283 #6247 #6289. 2026-10-07 later: #6311 (10:48Z) #6315 (11:25Z) #6321 (12:09Z) #6255 (14:48Z). 2026-10-07/08: #6330 (19:38Z) #6333 (20:08Z) #6249 (21:01Z) #6334 (21:02Z) #6332 (23:51Z) #6373 (2026-10-08 00:35Z). 2026-10-08: #6277 (01:36Z) #6356 (05:17Z) #6372 (05:36Z) #6395 (06:32Z) #6396 (07:03Z). |
| deployed | Yes: /api/version reports 604b0e0964 (read 2026-10-08T08:50Z), which contains every merged W7 PR. Packets 153000 (#6301) and 152000 (#6344) applied ahead of their open PRs. Pre-install backup deleted 2026-10-06 (owner OK); a separate restore rehearsal of a fresh logical backup PASSED 2026-10-07 for public scope (see R3). |
| activated | Yes: Mission Control drain/rerun is live by construction (no feature flag); critical path on for new projects (#6198); the once-only scheduler switch ON since 07:57Z 2026-10-05; its three approval siblings ON since 03:09:23Z 2026-10-06 (owner decision, after rehearsal). Switch A (background-queue expiry) on by default since #6332 went live (env value not re-read). |
| verifiedLive | 3 of 3 behaviours PASS on production; full W7 NOT accepted. A CLOSED 09:09:21Z 2026-10-06 (plan ee4c97bc / project bacf0dc8 → `failed`, 34 s after #6239 live; observed with gap 03:01Z; owner not notified — #6255). B PASS 17:36Z 2026-10-05. C PASS 06:35Z 2026-10-05. 2026-10-07 rehearsal: Mission Control flow works live with the owner's desktop app open (tasks run only through it; first 2-task project ~70 s after clearing stale locks and parking 233 old jobs). 2026-10-07: #6255 owner alert not provable live — no Telegram destination linked. 2026-10-08: #6372 seen on screen signed in; #6277 and #6356 live but not exercised. |

### X2 — Confirm System Workflow durable terminal and pause receipts

**Saved work:** System Workflow pause and Memory Promotion partial fixes deployed 2026-10-06: [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261) "a run is only completed when its row says so; System Workflow pause and recovery proven (X2, X3)" — independent review PASS, OPEN. 2026-10-06: #6261 MERGED 11:34:52Z and live.

**Remaining:** Qualify real admitted-owner pause/checkpoint/terminal recovery journeys on production.

**Acceptance:** Terminal receipt qualification plus caller handling of uncertain outcomes; required CI, installed transport, pause/resume/node acknowledgments and deployed acceptance remain open.

**Source:** lib/vms/coordination/{trigger,run-logger}.ts; tests/unit/system-workflow-terminal-durability-postgrest.test.ts

**Prior owner role:** Sol workflow / Root verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes in #6261 (open) |
| integrated | PR #6261 open, not on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6261 review PASS 2026-10-06 |
| merged | Yes: #6261 merged 2026-10-06 11:34:52Z |
| deployed | Yes: live in 8e4d2d44b0 |
| activated | Full scope pending |
| verifiedLive | Scoped public checks only; full authenticated scope pending |

### X3 — Refuse zero-row completion in scheduled and direct workflows

**Saved work:** Missing original terminal-row refusal has scoped native evidence 2026-10-06: [#6261](https://github.com/jtobkin/suprafx-platform/pull/6261) "a run is only completed when its row says so; System Workflow pause and recovery proven (X2, X3)" — independent review PASS, OPEN. 2026-10-06: #6261 MERGED 11:34:52Z and live.

**Remaining:** Verify scheduled and direct deployed paths retain truthful outcomes.

**Acceptance:** Both scheduled engine and direct persisted execution refuse unconfirmed completion; no replay or terminal promotion after missing row.

**Source:** lib/vms/workflows/execution-engine.ts; native terminal persistence regression

**Prior owner role:** Sol workflow. Root must assign a currently available named owner before dispatch. **Original dependencies:** P0.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes in #6261 (open) |
| integrated | PR #6261 open, not on main |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6261 review PASS 2026-10-06 |
| merged | Yes: #6261 merged 2026-10-06 11:34:52Z |
| deployed | Yes: live in 8e4d2d44b0 |
| activated | Full scope pending |
| verifiedLive | Full scope pending |

### X4 — Retain uncertain scheduled workflow attempts before another tick

**Saved work:** Scheduled original-attempt source preserved in held drafts. 2026-10-05: the once-only scheduled "occurrence claim" path reached production inside the release that deployed at 06:24Z, held behind the switch `WORKFLOW_SCHEDULED_OCCURRENCE_CUTOVER`. The switch was unset, so all 534 scheduled workflows were paused 06:24–07:57Z. The owner chose to turn it on at 07:57Z and said missed runs need not be re-run. Observed to 08:34Z: 85 scheduled runs, 0 workflows with more than one occurrence (once-only holds), 55 failed, 27 of them waiting for a new per-action grant introduced by the same release. Fixes for the known stalls are work in progress on `claude/scheduled-occurrence-live-fixes-20261005` @ `d3eb84cefe` (untested, no PR; its packet `20261005235000` must not be applied) 2026-10-05 stabilisation: PR #6212 (main `2df2d3b0cc`, merged 19:56Z) fixed the known stalls — a run killed by a restart, a lost reply, Run-now, a cancelled slot — plus for-each on a repeated target and workflow delete, and added a pause banner with a Release control; its packet `20261005235000_scheduled_occurrence_recovery` was applied and verified on production at 19:55Z. Health in the hour before 01:55Z on 2026-10-06 (reported, not re-read here): 167 scheduled runs completed, 34 failed; 0 duplicate slots; 0 stalled occurrences; 0 Mission Control plans running. The remaining failures are owners' own model keys (30 × "No usable API key for anthropic", 2 × credit balance), not platform faults. 2026-10-06: [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254) "acceptance proof for retained attempts and approval continuation" — independent review PASS, OPEN; packet `20261006070000` APPLIED AND VERIFIED. Follow-up: its script needs a writable role for two checks and two corrected expectations. 2026-10-06: #6254 MERGED 16:36:34Z and live.

**Remaining:** Run #6254's acceptance proof on production (#6254 merged 2026-10-06; packet 070000 applied); not recorded as run. The once-only scheduler is live and its known stalls are fixed, but this task is NOT accepted: the original acceptance proofs (real-transport lost-acknowledgment and next-tick no-repeat) have not been run, and completing the cutover checklist (`docs/agent-run/scheduled-workflow-cutover-checklist-20261001.md`) is not recorded. The three sibling approval switches were turned on 03:09Z 2026-10-06 (see X5); scheduled human-approval steps are now activated but not yet accepted live. Next: add scheduled scenarios to the end-to-end harness, run the original acceptance on production, and keep watching for duplicate slots (the only reason to turn the switch off).

**Acceptance:** Carry exact original identity and unknown status; atomically hold/recover original schedule attempt; real transport lost-ack and next-tick no-repeat proof, installed schema and deployed checks.

**Source:** app/api/cron/workflow-triggers/route.ts:189; lib/vms/workflows/execution-engine.ts; docs/agent-run/scheduled-workflow-recovery-plan-20261001.md

**Prior owner role:** Sol SQL + Sol engine; Root native integration. Root must assign a currently available named owner before dispatch. **Original dependencies:** X3.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes: once-only occurrence claim path, plus stall/for-each/delete fixes (#6212). |
| integrated | Yes: on main (#6212 = 2df2d3b0cc; live = 0d25a537b4). |
| tested | Required box-ci checks green at merge; packet 235000 applied and verified on production. Original acceptance proofs not run. |
| independentlyReviewed | Yes: #6254 review PASS 2026-10-06 |
| merged | Yes: #6212 (2026-10-05) and #6254 (2026-10-06 16:36:34Z) |
| deployed | Yes: live in 8e4d2d44b0 |
| activated | Yes: switch ON since 2026-10-05 07:57Z (owner choice after the 06:24–07:57Z pause of all 534 scheduled workflows). |
| verifiedLive | NO (observation only): last hour before 01:55Z 2026-10-06 — 167 completed / 34 failed (owners' own model keys), 0 duplicate slots, 0 stalled occurrences. Acceptance proofs not run. |

### X5 — Qualify original scheduled approval continuation

**Saved work:** Bounded original approval continuation source qualified 2026-10-06 03:09:23Z: the three approval switches (`WORKFLOW_SCHEDULED_TERMINAL_APPROVAL_CUTOVER`, `WORKFLOW_SCHEDULED_APPROVAL_CONTINUATION_CUTOVER`, `WORKFLOW_SCHEDULED_OWNER_STATUS_READ`) were set to on in the production settings store and applied on the web host under the deploy lock (owner decision 02:25Z); both containers show all four scheduler switches on. Build-box rehearsal before the flip: GO — 13/13 + 78/78 + 7/7 contract cases, 29/29 packets, 7/7 two-tick drive (verdict file in the private evidence lane, `live/verify/scheduled-approval-switches-verdict.md`). Known limit: approvals already pending from BEFORE the flip stay held — the engine stamps the occurrence id only when the switch was on at run start — so their only exit is the workflow page "Release this run" control after 30 minutes. 2026-10-06: [#6254](https://github.com/jtobkin/suprafx-platform/pull/6254) "acceptance proof for retained attempts and approval continuation" — independent review PASS, OPEN; packet `20261006070000` APPLIED AND VERIFIED. Follow-up: its script needs a writable role for two checks and two corrected expectations. 2026-10-06: [#6263](https://github.com/jtobkin/suprafx-platform/pull/6263) scheduled workflows built in the canvas use approval continuation — review PASS, OPEN; packet `20261006141000` APPLIED AND VERIFIED (0 live workflows had approval steps). Owner: run live scheduled-approval tests one at a time, and release pre-switch held approvals one at a time. 2026-10-06: #6254 MERGED 16:36:34Z and #6263 MERGED 12:48:43Z; both live.

**Remaining:** #6254 and #6263 merged and live (packets 070000 and 141000 applied). Next: drive one real scheduled approval end-to-end on production, one test at a time (owner), and release pre-switch held approvals one at a time. Close remaining effectful graphs and real approval/uncertain-outcome acceptance. State at 2026-10-06 03:10Z: all four scheduler switches are ON in production (approval switches since 03:09:23Z, owner decision after a GO rehearsal). ACTIVATED, NOT accepted: the live acceptance of a human-approval step in a scheduled workflow (approve, decline, lost reply, restart between approval and continuation) has not been run on production; approvals pending from before the flip stay held until the owner presses "Release this run" after 30 minutes. Next: drive one real scheduled approval end-to-end on production and add approval scenarios to the end-to-end harness (#6230).

**Acceptance:** Original paused run/approved node binding, unknown-provider no replay, concurrent resume/worker death fences, owner/config changes, native and browser acceptance before activation.

**Source:** PR6129 frozen9c3c7bd4e6c4c6ba58d2fa69424424fa84c79365; basePR6123 8415b13a51751928529a27d54b2b8490ff2bfa4f

**Prior owner role:** Root release; Sol server implementation; independent Sol verification. Root must assign a currently available named owner before dispatch. **Original dependencies:** X4, W6.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Scoped integration only; remaining caller joins are listed |
| tested | Scoped evidence only; exact acceptance still applies. Build-box rehearsal before the flip (2026-10-06): 13/13 + 78/78 + 7/7 contract cases, 29/29 packets, 7/7 two-tick drive — GO. |
| independentlyReviewed | Yes: #6254 review PASS 2026-10-06 and #6263 review PASS |
| merged | Yes: #6254 and #6263 merged 2026-10-06 |
| deployed | Yes: live in 8e4d2d44b0 |
| activated | YES since 2026-10-06 03:09:23Z: the three approval switches are on in production (owner decision 02:25Z; applied under the deploy lock; both containers show all four scheduler switches on). Known limit: approvals pending from before the flip stay held until the owner releases the run. |
| verifiedLive | NO. Activated but no production acceptance of a scheduled human-approval step yet; pre-flip pending approvals need the owner's "Release this run". |

### C2 — Bind project Git commands to exact workspace

**Saved work:** Project dispatch6118 and eligible-recipient6141 source qualified 2026-10-06: [#6259](https://github.com/jtobkin/suprafx-platform/pull/6259) "Projects: trusted internal execution, exact-workspace Git and member projections, rebased onto main (B1, C2 server, M1)" — independent review PASS, OPEN; its six schema packets (20261006110000/111000/112000/114000/115000/115500) APPLIED AND VERIFIED; switch `PROJECT_REVIEWED_SOURCE_V1` stays OFF. Before switch-on: observations block transport deletes (desktop re-sign-in 500) and the old poll hands out bound commands unchecked. Client half in [#6256](https://github.com/jtobkin/suprafx-platform/pull/6256) (review PASS, OPEN). 2026-10-07: #6259 still OPEN (re-read 07:53Z); [#6287](https://github.com/jtobkin/suprafx-platform/pull/6287) "project switch blockers: re-sign-in survives observations; old poll refuses bound commands" (stacks on #6259) reviewed, OPEN; its packet `20261006115900` APPLIED (a deadlock was fixed first). Switch `PROJECT_REVIEWED_SOURCE_V1` still OFF. Client half #6256 MERGED 2026-10-07 03:38Z (live).

**Remaining:** Merge #6259 then #6287 when green (switch stays off), then qualify mounted Realtime/relay, exact workspace commands and schema-first rollout.

**Acceptance:** Authenticate owner+logical session+project+workspace identity for active and suspended commands; refuse delayed opposite-context commands, changed authority and missing sidecars; retain personal-only positive controls.

**Source:** relay land producer/PUT; command protocol; cloud and desktop worktree routing; PR6141 c8d5 eligible project recipient successor

**Prior owner role:** Sol6 implementation + independent verifier. Root must assign a currently available named owner before dispatch. **Original dependencies:** C1.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | See saved work; full-scope completion not asserted |
| integrated | Client half #6256 on main (live 8e4d2d44b0); server #6259 and #6287 OPEN |
| tested | Scoped evidence only; exact acceptance still applies |
| independentlyReviewed | Yes: #6259 review PASS 2026-10-06 |
| merged | No — #6259 OPEN |
| deployed | Full scope pending |
| activated | No — PROJECT_REVIEWED_SOURCE_V1 OFF |
| verifiedLive | Full scope pending |

### R3B — Stage runtime role before candidate schema extension

**Saved work:** Dormant minimal role source with scoped native ACL proof; runtime helper/bridge integration saved82b01044; 19 private native actual-caller cases and independent review PASS. 2026-10-06 ~03:00Z rehearsal verdict: **NO-GO today** (private evidence lane, `live/verify/runtime-role-verdict.md`). The role packet refuses on the production shape (an existing `vms_agent_run_shelf` table; on PostgreSQL 16+ the implicit ADMIN membership of the postgres account cannot be revoked); a code blocker in the runtime binding (`lib/owner-db-runtime-binding.ts` membership test) would make every owner-database call fail with the switch on; one `FOR SHARE` read in `lib/vms-config.ts` needs UPDATE privilege. A renumbered packet (`20261006120000`) is prepared on branch `claude/runtime-role-packet-20261006` @ `7c72542d29`, no PR. Needs first: a product PR for the binding and the read, an owner-created runtime credential, and re-mapping of the orphan owner schemas. 2026-10-06 ~10:00Z: code blockers fixed (#6240, MERGED 08:14:30Z); packet `20261006120000` (#6258, OPEN) APPLIED AND VERIFIED; orphan owner schemas fixed by the owner (0 left); the owner set the role's login and a pooler login passed. Switch ~09:19Z broke public-table callers (Settings → General 503) → ROLLED BACK ~09:52Z (200s verified). Fix [#6270](https://github.com/jtobkin/suprafx-platform/pull/6270) (public-table callers use the admin connection) in review. 2026-10-06: #6270 MERGED 16:37:23Z and live. 2026-10-07: re-switch HELD until after the owner's Agent VM demo (decision 04:20Z); pre-switch check passed except "deploy running". #6258 still OPEN. 2026-10-07: #6258 MERGED 14:25:02Z. Switch C in the private activation runbook: re-run the pre-switch check (last NO-GO only for "deploy running"), owner checks the pooler client limit, owner runs the switch, KEEP only after signed-in pages return 200. Not run yet.

**Remaining:** Installed but NOT switched on (rolled back 2026-10-06 ~09:52Z). In order: (1) owner checks the connection-pooler client limit; (2) re-run the pre-switch privilege check (0 not-ok) with no deploy running; (3) owner runs switch C, watching Settings → General and every public-table caller (signed-in API status table), KEEP only after 200s. Earlier remaining work still applies: full installed ACL/default-ACL/policies; keep separate B1/gate-six work.

**Acceptance:** Exact named phase/catalog fingerprints, old/future owner clones, wrong-phase/partial schema/drift refusal, NOLOGIN and no active sessions, rollback from each phase. Still only OWNER_DB_URL scope, not REST/effects/global closure.

**Source:** scripts/qa/owner-runtime-main-role in qa-lanes/r3-owner-minimal-install-packet-20261002; codex/w7-runtime-binding-refresh-20261005 at82b010441ad1a82e66368585f7ddd68d5cfc9103; private release/runtime-role-reconciliation-plan.md.

**Prior owner role:** sol6_project_server; root independent review. Root must assign a currently available named owner before dispatch. **Original dependencies:** R2.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Yes: role packet + binding fixes (#6240) + public-table caller fix (#6270), both merged |
| integrated | #6240, #6270 and packet PR #6258 on main |
| tested | 47 focused+28 bridge+23-file types; 19 private PG cases PASS. Synthetic schema/admission; hosted pooler/ACL proof open. 2026-10-06 rehearsal on the production shape: packet REFUSES (existing shelf table; un-revocable ADMIN membership on PostgreSQL 16+) — NO-GO. 2026-10-06: installed and verified on production; pooler login passed; live switch exposed the public-table caller fault. |
| independentlyReviewed | Exact source and private native terminal independently reviewed; installed role/combined review pending. |
| merged | #6240 (2026-10-06 08:14:30Z), #6270 (2026-10-06 16:37:23Z) and #6258 (2026-10-07 14:25:02Z) merged |
| deployed | Role installed on production 2026-10-06 (packet 20261006120000 applied and verified) |
| activated | NO — rolled back 2026-10-06 ~09:52Z; switch C planned after switches A and B (owner-run) |
| verifiedLive | No — rollback verified (pages 200); role unused |

### C2S — Install and verify project schema before server rollout

**Saved work:** Seven ordered project-schema packets rehearsed privately 2026-10-06: the project schema packets for #6259 — 20261006110000, 111000, 112000, 114000, 115000, 115500 — were applied to production and each APPLIED AND VERIFIED (schema first, before the server code merges; switch `PROJECT_REVIEWED_SOURCE_V1` OFF). 2026-10-07: packet `20261006115900` (#6287) also APPLIED after a deadlock fix; switch still OFF.

**Remaining:** Schema installed on production (incl. 115900); remaining: merge #6259 and #6287, live service-role verification with the server code, then the guarded switch-on.

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
| deployed | Schema yes: six packets applied and verified 2026-10-06; server code (#6259) not merged |
| activated | No — switch OFF |
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
