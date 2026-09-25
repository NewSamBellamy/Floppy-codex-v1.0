# Floppy

A cinematic, local interaction prototype for Floppy: an editable, scrollable disk collection and a guided Phase 1 journey from Idea through Readiness.

Serve this directory over HTTP (ES modules require a server): `py -m http.server 8766 --bind 127.0.0.1 --directory outputs` from the workspace root. Open http://127.0.0.1:8766/index.html.

Projects, uploaded art, notes, decisions and chapter progress use local browser storage. They are device/browser-specific. Save failures and conflicting changes from other tabs are displayed. The Google key stays in the current tab and is never persisted.

The collection uses project names directly on each label with no “Project 1” naming. Continue opens the project workspace directly. Names, descriptions, case color and artwork are editable. Scroll with touch, mouse, or arrow buttons. Settings holds the Google key in memory for this tab only.

The project workspace separates lifecycle phase from chapter. Phase 1 has 13 ordered chapters (Idea, Problem, Audience, Alternatives, Evidence, Assumptions, First Product, Product, Features, Identity, Design, Idea Brief, Readiness). Each chapter can be unresolved, drafted, or resolved by the user; resolving unlocks the next chapter, and reopening a decision locks downstream chapters again for review. A user can explicitly continue with uncertainty. Prototype becomes available only after the human Readiness decision; later lifecycle phases remain visible and locked in this iteration.

The Idea chapter uses one writing surface with optional context attachments. Other chapters can prepare a Gemini-generated Work Brief from the idea, earlier decisions, and captured context. For Problem, users can attach returned research and ask Gemini for a separate proposed synthesis; they review and accept it explicitly. Context and source material are not treated as verified facts. The Idea Brief and Readiness screens summarize captured project work, but are advisory local-preview demonstrations rather than AI-generated or validated assessments. Uploaded files are locally limited to 1 MB; only files explicitly analyzed are sent to Google's Gemini API.

Project details let you edit the project name, description, and disk color. The Project Art editor accepts an uploaded image or a prompt-driven Gemini candidate, with optional confirmed project context and reference images; adjust the crop and choose **Use image** to save it. Uploads and generated art remain candidates until explicitly approved. The Gemini key is held only in the current tab's memory. Live Gemini connectivity and generation require a valid key and have not been end-to-end tested with a real account.

This is not the complete PRD implementation. Prototype, MVP, Production, and Post are navigation placeholders, not fully designed workflows. GitHub, account authentication, cloud persistence, external-tool integrations, AI evidence analysis, and deployment verification are not connected. Engineering requirements remain unconfirmed; local human decisions must not be mistaken for machine verification.

