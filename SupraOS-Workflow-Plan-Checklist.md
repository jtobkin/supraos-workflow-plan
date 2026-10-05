# SupraOS Release Plan Checklist

[Handoff](Ship-Verified-SupraOS-Agent-Workflows.md) · [Checklist](SupraOS-Workflow-Plan-Checklist.md) · [Dependency plan](Delivery-Path-Release-Plan.md) · [Evidence index](Evidence-Index.md) · [Canonical record](workflow-plan.json) · [Repository instructions](AGENTS.md)

Delivery strategy revision: **2026-10-05T01:20:34.889212+00:00**. Canonical record SHA-256: `b1e6aff578d06151e88e474c47256921cbd135141a8fda547c8ad546f8337dba`.

**Execution state:** Eight-hour execution active from 2026-10-05T01:01:15Z through 2026-10-05T09:01:15Z after documentation publication and independent anonymous-browser verification. Three lanes own failure drain, release prerequisites, and independent verification; root owns integration. W7 remains unmerged and undeployed..

**Scope:** all 33 tasks, 16 behavior families and 12 supported surfaces remain required. W7 is an intermediate milestone. iMessage is deferred; WhatsApp is excluded.

**Current delivery checkpoint:** 2026-10-05 active run: failure-drain regressions reproduced and focused source tests passing in an unqualified working successor. Independent source review continues. A source-identified multi-request rerun race is being repaired (executed concurrency reproduction pending) as part of the drain boundary; root owns its browser request binding. Fresh independently reviewed read-only production catalog observations confirm the selected W7 functions/tables/migrations and runtime role absent, and required existing relations present; this is metadata evidence, not installation or live capability. Runtime binding integration reuses the saved62b77 implementation on a separate prerequisite branch. Current qualified baseline remains ad2; no W7 merge/deployment/activation.

**Current candidate record:** `ad2ee680464217fd1b00883bf7ea9fc917ed3140`, tree `d646dcd04525189171ee67fc83098667cac6d290`. Security: PASS 51 steps; build: PASS 7 steps; macOS Native Land: Not run. Merged: False; deployed: False; activated: False; verified live: False. Scope: Qualified partial W7 checkpoint; full scope open. Observed: 2026-10-04T23:50:26Z. Update this canonical candidate record after changes; never infer status from historical receipts.

**Dated recovery baseline:** strict E3 was RED with 6,540 blockers at the prior closeout. These observations are not permission to skip fresh release checks.

Private portable evidence: `04795ddf0c18af8d40960ea29993fbf93535f5de` (2,291 restored files / 957 objects / 1,036 remotely verified transport files). Archive predates final CI; retain its original state. Baseline public handoff: `84f9f20b9fdfd33762b7e881da40980ed57349d4`. Historical documents are preserved under [history](history/20261005-before-delivery-rewrite/); historical statuses are not current authority.

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

## Current full-scope checklist — all 33 tracked items

| ID / work | Evidence state | Remaining work |
| --- | --- | --- |
| **P0 — Scope reconciliation and dependency plan** | Plan and scope reconciled; maintenance continues | Keep current evidence, dependencies and handoff aligned. |
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
| **R1 — Reconcile main, CI and exact release stack** | ad2ee680 partial successor pushed in draft6190, scoped52/types14/review PASS; required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; prior1c0 CI RED preserved; earlier privacy slices shipped | Qualify one complete successor after missing receiver integration. |
| **R2 — Installed schema, profile and release packet** | Installed profile read and source migration packets prepared | Reconcile current target ledger, source/schema/graph and guarded install packet. Fresh2026-10-05 selected read-only census independently verified:36 MC functions,8 MC tables,15 migration entries absent. Separate additive snapshot proves11 referenced preexisting relations present including vms_execution_runs. Ordered guarded installation remains pending. |
| **R3 — Writer/effect drain and faithful restore rehearsal** | Private stop/install/unknown recovery and dated restore proofs | Obtain supported all-writer fence, accepted-work accounting and current-target recovery. Code gap confirmed:existing operator still refuses because accepted-work/all-writer/backup evidence producers are not mounted. Fresh metadata observes privileged/managed sessions without exclusion authority. A concrete administrator/ticket clarification was requested; no grant assumed. |
| **I1 — Compose and independently qualify final source** | ad2ee680 integrates reviewed guard/manual/Telegram repairs on1c0;52 scoped tests/types14/review PASS; exact successor required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; unchanged UI has scoped Linux privacy proof; full final source open | Finish integration, freeze one successor and pass its final gates. |
| **D1 — Gated merge and deploy verified code** | UI6179/6181 merged/deployed/public-browser verified | Guarded W7 and wider-stack schema/runtime release after prerequisites. |
| **D2 — Activate qualified workflows after compatible rollout** | Global/workflow activation not claimed | Activate only compatible qualified schema/runtime with tested recovery. |
| **P1 — Provider and real computer readiness** | Provider readiness incomplete; Stripe configuration external | Finish normal provider/account/real-computer setup and approved live inputs. |
| **V1 — Stable deployed all-path and 16 behavior acceptance** | All16 integrated/live acceptance behaviors remain open | Independently verify stable deployed journeys across all12 surfaces. |
| **U1 — Owner confirmation and final handoff** | Portable handoff maintained; final owner confirmation pending | Provide specific owner tests only after independent applicable verification. |
| **W6 — Atomic usage limits for scoped capability grants** | Atomic grant reservations source in held draft6129 | Prove installed concurrent use, revocation and original receipt recovery. |
| **W7 — Original-operation workflow effects** | Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open | Finish remaining destinations, active cancellation and real L1; qualify combined source, release, activate and verify live. Active run: finish SQL-authoritative failure drain and actual automated/manual/recovery callers; qualify birth provenance versus legacy holds; close the source-identified rerun partial-write race; executed concurrency reproduction is pending with an atomic, original-action-bound operation and mounted browser caller. Working source tests are not native/release evidence. |
| **X2 — Confirm System Workflow durable terminal and pause receipts** | System Workflow pause and Memory Promotion partial fixes deployed | Qualify real admitted-owner pause/checkpoint/terminal recovery journeys. |
| **X3 — Refuse zero-row completion in scheduled and direct workflows** | Missing original terminal-row refusal has scoped native evidence | Verify scheduled and direct deployed paths retain truthful outcomes. |
| **X4 — Retain uncertain scheduled workflow attempts before another tick** | Scheduled original-attempt source preserved in held drafts | Install guarded occurrence schema and prove next-tick no-replay recovery. |
| **X5 — Qualify original scheduled approval continuation** | Bounded original approval continuation source qualified | Close remaining effectful graphs and real approval/uncertain-outcome acceptance. |
| **C2 — Bind project Git commands to exact workspace** | Project dispatch6118 and eligible-recipient6141 source qualified | Qualify mounted Realtime/relay, exact workspace commands and schema-first rollout. |
| **R3B — Stage runtime role before candidate schema extension** | Dormant minimal role source with scoped native ACL proof | Installed target ACL/pooler authority and guarded role rollout remain open. Fresh census:runtime role absent; selected B0 prerequisites/body hashes compatible, but7/11 source pins drifted and prior runtime identity helper/caller hooks are absent at ad2. Reconcile saved62b77 implementation with current provisioning/bridge behavior before exact-source qualification; do not install the old packet unchanged. |
| **C2S — Install and verify project schema before server rollout** | Seven ordered project-schema packets rehearsed privately | Perform guarded installed-target schema rollout with live service-role verification. |

## Detailed task contracts and preserved evidence

Historical baseline implementation/evidence is retained verbatim in `workflow-plan.json` under each task’s `baselineRecord`. It may predate the current saved-work summary. Original dependency IDs are retained below; dispatch dependencies above are the revised execution sequence. An empty original dependency list does not waive release prerequisites.

### P0 — Scope reconciliation and dependency plan

**Saved work:** Plan and scope reconciled; maintenance continues

**Remaining:** Keep current evidence, dependencies and handoff aligned.

**Acceptance:** Maintain this plan as evidence arrives; scope is not reduced to the current three lanes.

**Source:** docs/agent-run/{BASELINE-BEHAVIORS,EXECUTION-PATH-ACCEPTANCE}.md; original final handoff

**Prior owner role:** Root. Root must assign a currently available named owner before dispatch. **Original dependencies:** None recorded.

| Stage | Current evidence boundary |
| --- | --- |
| implemented | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| integrated | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| tested | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| independentlyReviewed | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| merged | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| deployed | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| activated | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |
| verifiedLive | Documentation-only: canonical rewrite published77d7faaa; independent fidelity and anonymous browser PASS. Product stage not applicable. New active-run revision awaits its publication verification. |

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

**Saved work:** ad2ee680 partial successor pushed in draft6190, scoped52/types14/review PASS; required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; prior1c0 CI RED preserved; earlier privacy slices shipped

**Remaining:** Qualify one complete successor after missing receiver integration.

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

**Saved work:** Installed profile read and source migration packets prepared

**Remaining:** Reconcile current target ledger, source/schema/graph and guarded install packet. Fresh2026-10-05 selected read-only census independently verified:36 MC functions,8 MC tables,15 migration entries absent. Separate additive snapshot proves11 referenced preexisting relations present including vms_execution_runs. Ordered guarded installation remains pending.

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

**Remaining:** Obtain supported all-writer fence, accepted-work accounting and current-target recovery. Code gap confirmed:existing operator still refuses because accepted-work/all-writer/backup evidence producers are not mounted. Fresh metadata observes privileged/managed sessions without exclusion authority. A concrete administrator/ticket clarification was requested; no grant assumed.

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

**Saved work:** ad2ee680 integrates reviewed guard/manual/Telegram repairs on1c0;52 scoped tests/types14/review PASS; exact successor required CI PASS on exact ad2: 51 security steps and 7 build steps; macOS Native Land not run; unchanged UI has scoped Linux privacy proof; full final source open

**Remaining:** Finish integration, freeze one successor and pass its final gates.

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

**Remaining:** Guarded W7 and wider-stack schema/runtime release after prerequisites.

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

**Saved work:** Full selected SQL suite, projectless and retro direct SQL, safe idle cancellation source qualified; failed-task and adjustment actual REST independently qualified; retrospective actual REST and terminal/estimation native proofs pass; notification direct SQL16cases passes; actual estimation/notification and exact1c0 retrospective REST independently pass; combined final qualification remains open

**Remaining:** Finish remaining destinations, active cancellation and real L1; qualify combined source, release, activate and verify live. Active run: finish SQL-authoritative failure drain and actual automated/manual/recovery callers; qualify birth provenance versus legacy holds; close the source-identified rerun partial-write race; executed concurrency reproduction is pending with an atomic, original-action-bound operation and mounted browser caller. Working source tests are not native/release evidence.

**Acceptance:** Thread server ToolContext identity, reserve before effect, preserve original run and unknown outcome, reject missing/forged identity, prove cap/no replay via actual transport. Bind actual task settlement to the original saved execution claim atomically; reject superseded results before effects and recover post-commit delivery without duplication. Prove usable original-child lookup/recovery and keep unsupported callers explicit.

**Source:** W7PR6160 frozen c3e23 required CI PASS, unmerged. Receiver successor3e278 includes c8d/ff88/fa939/2152/7bdf/critical7e1 and parse repairddc; pushed, unmerged, not covered by c3e CI. UI6179/6181 independently merged/deployed.

**Prior owner role:** release_integration: isolated claim/settlement production repair; release_verification: independent tests; root: composition/release. Root must assign a currently available named owner before dispatch. **Original dependencies:** W6.

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

**Saved work:** Dormant minimal role source with scoped native ACL proof

**Remaining:** Installed target ACL/pooler authority and guarded role rollout remain open. Fresh census:runtime role absent; selected B0 prerequisites/body hashes compatible, but7/11 source pins drifted and prior runtime identity helper/caller hooks are absent at ad2. Reconcile saved62b77 implementation with current provisioning/bridge behavior before exact-source qualification; do not install the old packet unchanged.

**Acceptance:** Exact named phase/catalog fingerprints, old/future owner clones, wrong-phase/partial schema/drift refusal, NOLOGIN and no active sessions, rollback from each phase. Still only OWNER_DB_URL scope, not REST/effects/global closure.

**Source:** scripts/qa/owner-runtime-main-role in qa-lanes/r3-owner-minimal-install-packet-20261002

**Prior owner role:** sol6_project_server; root independent review. Root must assign a currently available named owner before dispatch. **Original dependencies:** R2.

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
