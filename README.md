# AUBrokerFlow — Sales Funnel (real, deployable build)

A pixel-faithful rebuild of the Claude Design handoff (`../design_handoff_aubrokerflow_funnel/`) as a
**self-contained, zero-build web app**. No framework, no npm install, no bundler — just open or host
`index.html`. Every screen and interaction from the design is implemented and working.

## What's included
- **Landing page** — all 9 sections, verbatim copy, exact colors/type (Archivo + IBM Plex Mono, navy `#0B1E2D` / teal `#0A7F73`), hero workflow card, sticky CTA that appears after ~85% viewport scroll.
- **Qualification quiz** — the real 7 questions across a 3-step flow, single-select pills, progress bar, per-step validation, Back/Continue.
- **Branching** — qualified → Calendar; not-a-fit → polite decline screen. Rule (verbatim from spec): reject only if Q7 = "Not at the moment", **or** if leads = "1–5" **and** settlements = "0–1" **and** hours = "Less than 2 hours".
- **Calendar** — next 5 weekdays + 6 time slots, "Confirm Strategy Call" gated until a day *and* time are chosen.
- **Confirmation** — live booking summary + "before the call" prep + closing panel.

## Run / preview locally
Just open `index.html` in a browser. (Some browsers restrict `file://` for local storage; hosting avoids that.)

Optional local server (pick whatever you have installed):
```bash
python -m http.server 8080      # then open http://localhost:8080
```

## Deploy (any static host)
Upload the `aubrokerflow-funnel/` folder as-is:
- **Netlify / Vercel** — drag-and-drop the folder, or connect the repo (no build command; publish directory = this folder).
- **GitHub Pages / Cloudflare Pages / S3+CloudFront** — upload the folder; `index.html` is the entry point.

## Wire up before going live (marked with `TODO` in `index.html`)
1. **Lead capture** — `submitApplication()` currently logs the payload and stores it in `localStorage`.
   Replace the `TODO` with a POST to your CRM / webhook / email endpoint. Payload includes contact,
   all 7 answers, and the `qualified` flag.
2. **Booking** — the booking step embeds the **"30 mins Free Strategy Call"** Google
   **Appointment Schedule** (bookable): visitors pick a slot inline and it books onto the calendar,
   with Google sending the confirmation + invite. Embed uses the schedule URL with `?gv=true`
   (short link: `https://calendar.app.google/jHLrS2bEJX7szRin7`). The "I've Booked — Continue"
   button fires `submitBooking()` and moves the visitor to the confirmation screen — wire
   `submitBooking()` to your CRM the same way as the application if you want to record it.
3. **VSL / demo video** — two 16:9 placeholders (landing + confirmation) labelled `[ VSL / AI DEMO VIDEO ]`.
   Drop in the real embed when produced.
4. **Founder photo** — `assets/Bhargav.jpeg` (already included from the handoff).
5. **Logo** — currently the text/shape mark ("A" + wordmark). Swap for a real logo if one exists.

## Compliance (kept from the handoff — do not change)
- Primary CTA is always exactly **"Apply For Your 30-Day Free Pilot"**.
- No fabricated testimonials, stats, client logos, case studies, %-reduction claims, or guarantees.
- Footer disclaimer states it does not provide financial advice, make lending decisions, or replace the broker relationship.
