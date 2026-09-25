# Floppy handoff

Current milestone:
Milestones 1–6 complete. Internal MVP finish audit passed; ready for handoff.

Completed:
- Autonomous finish system created: `AGENTS.md`, `GOAL.md`, `PLAN.md`, `IMPLEMENT.md`, `STATUS.md`.
- Milestone 1 restored project entry, reconciled all eight failing regressions, restored the Readiness → Prototype handoff, and kept unlocked phases revisitable.
- Prior decisions and source excerpts now carry into later chapter context within a bounded prompt. Legacy drafts, malformed source records, cached investigation status, and interrupted AI requests recover safely.
- Editing the foundational Idea retains downstream answers as drafts while clearing their confirmed status. Failed Work Brief refreshes keep the last good brief.
- `node --test`: 32 passed, 0 failed. Syntax and diff checks passed.
- Isolated 1366×768 browser journey passed: created a project with context before creation, completed Idea and all 12 later chapters, opened all 13 investigations, synthesized Problem research, confirmed each chapter, entered Prototype, revisited phases, refreshed, returned from Projects, and reopened Idea. Mocked Gemini responses were used. The intentional mock 503 generated the only browser console error.
- Milestone 2 project art verified in an isolated 1366×768 Chromium journey using mocked Gemini output: upload candidate/cancel, editable prompt, optional project context, current/uploaded/project references, disconnected Settings return, generation, failed regeneration/retry, zoom/drag/reset, explicit Use image, save rollback on quota failure, reload persistence, and editor/carousel pixel comparison. Saved art remained intact before approval and across failures. The only expected browser console error was the intentionally mocked HTTP 503.
- Gemini 3.1 Flash Image request now uses the documented `generationConfig.responseFormat.image.aspectRatio` at the nearest supported 16:9 ratio. The editor and carousel use the same exact 2:1 crop geometry. Unconfirmed Problem/Audience shortcuts were removed from image-generation context; confirmed chapter context remains bounded.
- `node --test`: 32 passed, 0 failed after Milestone 2. The standalone browser journey is `milestone2.browser.cjs` (requires Playwright and an HTTP-served app).
- Milestone 3 refinement removed the unreachable legacy identity dialog and its duplicate upload/AI-art handlers, leaving project details and the Project Art editor as the active paths. Chapter evidence no longer repeats its trust/status line; full source details open on demand through “Open source details.”
- Before/after isolated Chromium screenshot audit passed at 1366×768, 1440×900, 1920×1080, 1280×720, and 390×844 for picker, Idea, Settings, art editor, Problem and evidence details. Screenshots were visually compared; only the intended duplicate evidence/source UI changed. Page dimensions matched each viewport and `scrollY` remained 0. Settings and art dialog actions remained in view; mobile art controls remained reachable inside the dialog’s scrollable content. No browser console errors.
- The Problem evidence disclosure opens, and “Open source details” reveals the detailed local source record. The viewport harness is `milestone3-visual-audit.cjs`; it supports checkpoint/current screenshot runs via `FLOPPY_URL` and `FLOPPY_AUDIT_TAG`.
- `node --test`: 32 passed, 0 failed after Milestone 3. The Milestone 2 art browser journey still passes after cleanup.
- Milestone 4 reliability audit found and fixed a root cause: context-note/link/upload handlers and new-project creation previously proceeded as if complete after `persist()` returned false. Failed additions now roll back the mutated in-memory record and keep the capture/create dialog open with a retry message; successful retry persists exactly once. Storage failures continue to show the global warning. Added `restoreProjectSnapshot` for transaction rollback.
- Isolated browser reliability journey (`milestone4-reliability-audit.cjs`) verified Idea autosave after the 500 ms debounce and exact restore after reload; context note quota failure does not enter storage or close capture; retry and source removal persist; pre-creation context is included in the project; failed creation under quota pressure rolls back and retries once; PDF, image, and link attachments persist; malformed storage is preserved without overwrite; and a stale tab cannot overwrite a newer version.
- Extended mocked project-art browser journey to delay a generation response, cancel it, and confirm that neither saved art nor the next editor candidate is replaced by the late response. Generation failure remains actionable and does not mutate confirmed art.
- `node --test`: 32 passed, 0 failed. Browser checks: `milestone4-reliability-audit.cjs` passed, and the full `milestone2.browser.cjs` art journey (including cancellation, failed regeneration, crop, approval, reload, and pixel comparison) passed. Browser profiles were isolated; no real Gemini key or user project data was read.
- Failure simulation used a temporary Playwright-only `Storage.prototype.setItem` override in isolated contexts and restored it before retry. Malformed-save and tab-conflict data were also confined to isolated contexts.
- Milestone 5 found and fixed a keyboard access issue in the project picker. The Edit image action was removed from keyboard sequence while visibility transitioned from hidden; its visual hover/focus treatment now keeps it tabbable and reveals it when the disk card has focus, without changing the interaction design.
- Keyboard audit (`milestone5-accessibility-audit.cjs`) passed for carousel arrow selection and pressed state, project-title focus on entry, chapter-rail keyboard focus, Settings/context/new-idea Escape and focus restoration, context removal by keyboard, art-editor opening from the keyboard sequence, crop arrow-key adjustment, art-dialog focus restoration, labeled visible form controls, named icon buttons, and fresh console. Actual browser viewport was 1366×768; document was 1366×768 with scrollY 0.
- Fresh screenshot audit run using Playwright Chromium at 1366×768, 1440×900, 1920×1080, 1280×720, and 390×844 across home, Idea, Settings, art, Problem, evidence details, and source details. All reported innerWidth/innerHeight exactly matched configured dimensions; document dimensions matched viewport and page scrollY was 0 for all states; no console errors. Screenshots saved under `%TEMP%` as `floppy-m3-m5-<width>x<height>-<view>.png` and visually inspected at narrow art-editor and 1280×720 Idea states.
- Core text palette measured against the dark shell background: primary 16.52:1, secondary 10.74:1, muted 7.79:1. Disabled text is 4.27:1 and applies only to inactive controls.
- Milestone 6 end-to-end run passed in a fresh isolated Chromium profile at 1366×768 using the Clydeo project: created with context, generated and approved a Working Idea, completed and confirmed all 13 chapters, opened each investigation, returned and synthesized Problem research, revisited prior decisions, exercised a mocked Work Brief 503 and interrupted generation recovery, approved prompt-generated Project Art, refreshed/reopened, and verified the art, Idea, confirmed Problem answer, research proposal, and project identity persisted.
- Settings and all Gemini calls in the journey used a disposable mock API key intercepted by Playwright. No saved/user credential was read, printed, persisted, or sent to Google. The only browser console error allowed in the journey was the deliberate mocked HTTP 503; all other console/page errors were asserted absent. Real Gemini connectivity remains unverified.
- Updated the stale README Project Details / Project Art section to reflect the active editor, explicit image approval, and tab-memory key behavior while retaining the existing product-scope explanation.
- Final verification: `node --test` 32 passed / 0 failed; syntax checks passed for app and browser harnesses; Milestone 1 integrated Clydeo journey passed; Milestone 2 art journey passed; Milestone 4 reliability journey passed three consecutive isolated runs; Milestone 5 keyboard/focus journey passed; 35 screenshot states across 1366×768, 1440×900, 1920×1080, 1280×720, and 390×844 matched actual viewport dimensions, had document height equal to viewport height, scrollY 0, and no console errors. `git diff --check` passed.

Current known state:
- Repo: `outputs/`. The Milestone 1 checkpoint includes the intended source work that was uncommitted at its start; backup folders remain outside commit scope.
- Local browser app uses `index.html`, `style.css`, `app.js`, `identity.js`, `chapter-intelligence.mjs`, `chapter-investigation.mjs`, and `project-art.mjs`. There is no package/build manifest; tests run with `node --test`; serve over HTTP for browser modules.
- Projects and attachments use browser `localStorage` under `floppy-projects-v3` with a version 4 payload. Gemini key is held in tab memory only. Do not read or log a user's credential while auditing.
- The project carousel, 13-chapter Phase 1 rail, Working Idea, proposals, investigations, research return, confirmation, Prototype handoff, and project art passed isolated mocked browser journeys.

Known issues:
- Live Gemini connectivity, chapter generation, and image generation were not tested with a real key. Mocked request/response checks do not prove live service success. This is the remaining external sign-off item; the internal MVP does not require a real credential to use its local/manual paths.
- The source backup at `../floppy-finishing-backup-20260924/` is available if later investigation needs it. Preserve all browser project data.
- `README.md` describes portions of an older prototype and should be reconciled after the product stabilizes.

Decisions made:
- Preserve the current lifecycle and 13 Phase 1 chapters; focus on an internal MVP.
- Keep the three layers distinct: original sources, Floppy synthesis, human-confirmed state.
- Treat credentials and existing local project data as user-owned. Use a fresh isolated browser profile for journey tests. Keep downstream answers as drafts when the Idea is revised.

Needs human decision:
- None for the completed internal-MVP scope. A user-provided working Gemini key would be required for live-service sign-off; no key was requested or inspected.

Next:
- Handoff from checkpoint after Milestone 6. Keep the stable local-first direction. If live Gemini sign-off is desired later, provide a test key through Settings directly; never paste it into chat or logs.
