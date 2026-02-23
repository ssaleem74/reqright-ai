# ReqRight AI — Test Cases (Phases 1–3)

---

## Phase 1: LLM Settings Panel

### TC-1.1: Settings button visibility
1. Open reqright.html
2. **Expected:** 🤖 LLM button visible in header bar, between ⚡ AI and theme toggle
3. No green dot indicator (no key configured yet)

### TC-1.2: Settings modal opens
1. Click 🤖 LLM button
2. **Expected:** Modal opens with Provider, Model, API Key fields
3. Status banner shows: "⚪ No API key configured"
4. Test Connection button is disabled/greyed out

### TC-1.3: Provider toggle
1. Open LLM settings
2. Click "OpenAI" provider
3. **Expected:** Model dropdown changes to GPT-4o / GPT-4o Mini / GPT-4.1
4. Click "Anthropic Claude" provider
5. **Expected:** Model dropdown changes to Sonnet 4.5 / Haiku 4.5 / Opus 4.5

### TC-1.4: API key paste & persistence
1. Paste a valid Anthropic API key into the key field
2. **Expected:** Status changes to "🔵 API key set — click Test Connection to verify"
3. Test Connection button becomes active
4. Close modal, reopen it
5. **Expected:** API key is still there (persisted in localStorage)

### TC-1.5: Connection test — success
1. Enter valid Anthropic API key with credits
2. Select Claude Sonnet 4.5 as model
3. Click 🔌 Test Connection
4. **Expected:** Shows "🟢 Connected — LLM features enabled."

### TC-1.6: Connection test — invalid key
1. Enter "sk-ant-api03-fake-key-12345" as API key
2. Click Test Connection
3. **Expected:** Shows "🔴 Connection failed:" with error message

### TC-1.7: Connection test — no credits
1. Enter valid key with $0 balance
2. Click Test Connection
3. **Expected:** Shows error about insufficient credits

### TC-1.8: Clear key
1. With a key configured, click 🗑 Clear Key
2. **Expected:** Key field empties, status returns to "⚪ No API key configured"
3. Green dot on header button disappears

### TC-1.9: Show/hide key toggle
1. Enter an API key
2. Click 👁 eye button
3. **Expected:** Key becomes visible (type=text)
4. Click again
5. **Expected:** Key becomes hidden (type=password)

### TC-1.10: Escape closes modal
1. Open LLM settings
2. Press Escape
3. **Expected:** Modal closes

### TC-1.11: Green dot indicator
1. Configure a valid API key
2. Close the settings modal
3. **Expected:** 🤖 LLM button has small green dot in top-right corner
4. Clear the key
5. **Expected:** Green dot disappears

---

## Phase 2: LLM Smart Rewrite (Single Requirement)

### TC-2.1: LLM Rewrite button visibility
1. Load example project, select a requirement with violations
2. **Expected:** Purple AI panel shows TWO buttons: "⚡ Auto-Fix" and "✨ LLM Rewrite"
3. Remove API key from settings
4. **Expected:** Only "⚡ Auto-Fix" button visible (no ✨ LLM Rewrite)

### TC-2.2: LLM Rewrite — basic flow
1. Select a requirement with score < 80%
2. Click ✨ LLM Rewrite
3. **Expected:** Button changes to "✨ Thinking..."
4. After 2–5 seconds, review panel appears with:
   - Original text (red, struck through)
   - Suggested rewrite (green)
   - Changes summary
   - Score comparison (before → after)
   - Confidence badge
   - Accept / Discard buttons

### TC-2.3: Accept rewrite
1. Complete TC-2.2
2. Click ✓ Accept Rewrite
3. **Expected:**
   - Requirement text updates to the suggested version
   - Toast shows score change (e.g., "LLM: 52% → 91%")
   - Review panel disappears
   - Quality score in sidebar updates
   - Quality panel on right updates

### TC-2.4: Discard rewrite
1. Complete TC-2.2
2. Click ✕ Discard
3. **Expected:** Review panel disappears, original text unchanged

### TC-2.5: Version history tracking
1. Accept an LLM rewrite (TC-2.3)
2. Expand Version History panel for that requirement
3. **Expected:** New entry showing:
   - Field: "Statement (LLM Rewrite)"
   - Author: "LLM (claude-sonnet-4-5-20250929)"
   - Old → new text snippets

### TC-2.6: LLM Rewrite on high-scoring requirement
1. Select a requirement with score 90%+
2. **Expected:** The purple AI panel may not show (no violations)
3. If it shows with warnings, clicking ✨ LLM Rewrite should still work

### TC-2.7: Test with intentionally bad requirement
1. Create new requirement with text: "The system should handle data properly and efficiently."
2. Click ✨ LLM Rewrite
3. **Expected:** LLM rewrites to include:
   - Named entity (not just "The system")
   - "shall" instead of "should"
   - Specific measurable criteria instead of "properly" and "efficiently"
   - Tolerance values if applicable

### TC-2.8: Test with vague requirement
1. Create: "All errors must be handled in a timely manner where possible."
2. Click ✨ LLM Rewrite
3. **Expected:** LLM fixes:
   - "All" → "each" (R32)
   - "must" → "shall" (R1)
   - "timely manner" → specific time (R34)
   - "where possible" removed (R7 escape clause)

### TC-2.9: Test with passive voice
1. Create: "Data shall be processed by the system within 5 seconds."
2. Click ✨ LLM Rewrite
3. **Expected:** LLM converts to active voice: "The [System_Name] shall process each data record within 5 ± X seconds."

### TC-2.10: Undo after accept
1. Accept an LLM rewrite
2. Press Ctrl+Z
3. **Expected:** Requirement reverts to original text

### TC-2.11: Error handling — network failure
1. Disconnect from internet
2. Click ✨ LLM Rewrite
3. **Expected:** Review panel shows error: "Network error" or similar
4. ✕ Close button to dismiss

### TC-2.12: Switching requirements during LLM loading
1. Click ✨ LLM Rewrite on REQ-001
2. While it says "Thinking...", click a different requirement in sidebar
3. **Expected:** No crash. Review panel shows for original requirement when you return to it.

---

## Phase 3: Batch LLM Rewrite

### TC-3.1: Batch button visibility
1. Click ⚡ AI button in header (opens Bulk Quality Analysis modal)
2. **Expected:** Two batch buttons: "⚡ Auto-Fix All Below 80%" and "✨ LLM Fix All Below 80%"
3. Remove API key
4. **Expected:** Only "⚡ Auto-Fix All Below 80%" visible

### TC-3.2: Per-requirement LLM button in bulk modal
1. Open Bulk Quality Analysis with API key configured
2. **Expected:** Each requirement row shows TWO buttons: "⚡ Auto-Fix" and "✨ LLM"
3. Click ✨ LLM on a specific requirement
4. **Expected:** Modal closes, navigates to that requirement in Author view, LLM Rewrite triggers

### TC-3.3: Batch LLM rewrite — full flow
1. Load example project (should have several requirements < 80%)
2. Open ⚡ AI → click ✨ LLM Fix All Below 80%
3. **Expected:**
   - Button changes to "✨ Running..."
   - Progress panel appears with:
     - Progress bar filling incrementally
     - Counter: "X / Y"
     - Current requirement being processed
     - Results appearing as each completes
   - Each result shows: REQ-ID, old score → new score, +/- diff

### TC-3.4: Batch progress tracking
1. During batch run (TC-3.3), observe:
2. **Expected:**
   - "⏳ Processing REQ-XXX..." updates for each requirement
   - ✓ count increments on success
   - Progress bar advances proportionally
   - Toast appears when complete with summary

### TC-3.5: Batch completion
1. Wait for batch to finish
2. **Expected:**
   - Header shows "✨ LLM Batch Rewrite Complete"
   - All results listed with score changes
   - Toast: "LLM batch: X improved, Y failed of Z"
   - ✕ Dismiss button appears
   - Click Dismiss → progress panel removed

### TC-3.6: Batch with mixed results
1. Create a project with:
   - 3 requirements scoring < 80% (should be rewritten)
   - 3 requirements scoring > 80% (should be skipped)
2. Run LLM batch
3. **Expected:** Only the 3 low-scoring requirements are processed

### TC-3.7: Batch version history
1. After successful batch run, check Version History on any improved requirement
2. **Expected:** Entry with field "Statement (LLM Batch)", author "LLM (model-name)"

### TC-3.8: Batch — no requirements below threshold
1. Load project where all requirements score ≥ 80%
2. Click ✨ LLM Fix All Below 80%
3. **Expected:** Toast: "No requirements below 80%"

### TC-3.9: Batch — API error mid-run
1. Start batch run
2. If possible, revoke API key mid-run (or use key with minimal credits)
3. **Expected:** Failed requirements show "Error: [message]" in results
4. Successful ones before the error are still saved
5. Final toast shows accurate improved/failed counts

### TC-3.10: Auto-save after batch
1. Complete a batch run
2. Close browser tab, reopen reqright.html
3. **Expected:** All batch-rewritten requirements retain their new text

---

## Cross-Cutting Tests

### TC-X.1: Auto-Fix vs LLM side by side
1. Select a low-scoring requirement
2. Note the original text
3. Click ⚡ Auto-Fix — note result and score
4. Ctrl+Z to undo
5. Click ✨ LLM Rewrite — note result and score
6. **Expected:** LLM version should be more contextually aware and typically score higher

### TC-X.2: Dark/Light theme
1. Toggle theme while LLM settings modal is open
2. **Expected:** Modal renders correctly in both themes

### TC-X.3: JSON export includes LLM history
1. After some LLM rewrites, export project as JSON
2. Open JSON file
3. **Expected:** History entries contain "LLM (claude-sonnet-4-5-20250929)" as author

### TC-X.4: JSON export excludes API key
1. Configure API key, export project
2. Search exported JSON for "sk-ant"
3. **Expected:** API key is NOT in the export file

### TC-X.5: Page reload persistence
1. Configure API key, test connection (green)
2. Refresh the page (F5)
3. Open 🤖 LLM settings
4. **Expected:** Provider, model, and API key are all preserved

### TC-X.6: Cost sanity check
1. Check your Anthropic console credits before testing
2. Run 5 individual rewrites + 1 batch of 5
3. Check credits after
4. **Expected:** Total cost should be < $0.10

---

## Test Data: Bad Requirements for Testing

Use these to create requirements and test LLM rewrite quality:

| # | Bad Requirement | Expected Violations |
|---|----------------|-------------------|
| 1 | "The system should handle data properly and efficiently." | R1 (should→shall), R3 (no entity), R7 (vague: properly, efficiently) |
| 2 | "All errors must be handled in a timely manner where possible." | R1 (must→shall), R7 (escape: where possible), R32 (all→each), R34 (timely=vague) |
| 3 | "Data shall be processed by the system within 5 seconds." | R2 (passive voice), R33 (no tolerance) |
| 4 | "The system shall always be available and reliable." | R18 (two thoughts: available AND reliable), R26 (absolute: always), R7 (vague: reliable) |
| 5 | "It shall send notifications to users." | R24 (pronoun: It), R3 (no named entity) |
| 6 | "The system shall be able to process approx 1000 requests." | R10 (superfluous: be able to), R38 (abbreviation: approx), R33 (no tolerance) |
| 7 | "The SW shall handle errors, exceptions, and edge cases as needed." | R7 (escape: as needed), R18 (multiple thoughts), R38 (abbreviation: SW) |
| 8 | "Performance should be adequate for the intended use case." | R1 (should→shall), R7 (vague: adequate), R34 (not measurable) |
