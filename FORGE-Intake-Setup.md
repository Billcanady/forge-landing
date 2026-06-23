# The FORGE Intake — Setup & Deploy

**What it is:** a real 5-question diagnostic (Bill's voice, talk-or-type, ~15 min) that produces a
branded PDF the respondent keeps, captures everything to HubSpot so it comes back to you, and routes
to your iClosed scheduler. Insights are smart standard copy — no AI keys, consistent every time.

**Files**
- App: `Landing Page/forge-intake.html`
- Deploy copies: `Landing Page/deploy/index.html` (landing page) + `Landing Page/deploy/intake/index.html` (the intake)

## How the pieces connect
- The landing page's **"Start My Intake"** buttons point to **`/intake`**.
- So the intake ships inside the **same `forge-landing` repo**, in an `intake/` folder. Once deployed,
  it lives at **`forge.the8020institute.com/intake`**.

## Deploy (same flow you used before)
In the `Billcanady/forge-landing` repo:
1. **Replace** `index.html` with the new `deploy/index.html` (updated landing page).
2. **Add a folder** `intake/` and upload `deploy/intake/index.html` into it (keep the name `index.html`).
   - GitHub web: Add file → Upload files → drag the file, and in the filename box type `intake/index.html`
     so it lands in a folder. Commit.
3. Vercel auto-redeploys. The intake is then live at `forge.the8020institute.com/intake`.

## One HubSpot step to turn on delivery
The intake captures to HubSpot (portal `82724048` is already set). It just needs a form to submit to:
1. In HubSpot, **clone** the "CEO Mandate – Intake Signup" form → rename **"FORGE – Intake"**.
2. Open it → **Share / Embed** → copy the **form GUID**.
3. In `intake/index.html`, find the `CONFIG` block near the bottom and paste it into `HUBSPOT_FORM_ID`.
   Re-upload that file. Done — submissions now create/update the contact and land the full transcript
   in the contact's **Message** property (so the whole intake comes back to you in the CRM).
   - Until the GUID is set, the intake runs in **demo mode** (everything works; data logs to the
     browser console instead of HubSpot).

## Make it email them + notify you (HubSpot workflow)
Create a simple HubSpot workflow: **enrollment trigger = form submission "FORGE – Intake."** Then:
- **Internal email / task to you** — so you see every new intake and can reach out.
- **Email to the contact** — thank them, include the booking link (`app.iclosed.io/e/The8020institute/forge`),
  and (optionally) their answers via the Message property.
- The respondent also **downloads the branded PDF on the results screen** immediately — that's the
  primary "cool document." (Emailing the exact generated PDF as an attachment needs a small backend;
  that's a phase-2 add if you want it.)

## What you get vs. what they get
- **You:** the full transcript (their words + the read on each of the 5 dimensions + an overall band)
  on the HubSpot contact, plus a notification.
- **Them:** an on-brand PDF — their answers, an insight on each, an overall read, and next steps —
  downloadable on the spot, plus a booking button and the promise that you'll reach out.

## Phase 2 (when you're ready)
- **FORGE onboarding** flow for people who join (separate build; may reuse this engine).
- Optional: email the generated PDF as an attachment (needs a serverless function + email service).
