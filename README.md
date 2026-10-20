# Koumara

Koumara is the mail app I'm building to replace Apple Mail on my Mac, iPad and iPhone. It sorts mail into lanes that match how I actually work, keeps my VIPs answered quickly, and does all of its AI work on my own hardware.

The name is the Greek word for the strawberry tree (*Arbutus unedo*), which shows up in the myths around Hermes, the messenger. The tree carries flowers, green fruit and ripe fruit on the same branch at once. That's the visual idea behind the app: one inbox holding mail at different stages of ripeness.

## Where things stand

Design is done enough to start building, and there's a clickable iPhone prototype to walk through. There's no app code yet. The next step is the Mac version of the prototype, then a SwiftUI build with sample mail.

## What's in here

| Path | What it is |
| --- | --- |
| [`design/brief.html`](design/brief.html) | The design brief: the lane model, visual direction, an interactive Mac window, how sorting works, VIP replies, accessibility commitments, and the decisions so far. |
| [`design/flows.html`](design/flows.html) | Storyboards for the five main flows (first run, VIP reply, fixing a misfiled message, newsletter reading, purchases) on iPhone and Mac, plus iPad differences and edge states. |
| [`design/screens.html`](design/screens.html) | Detailed screens: newsletters as a magazine Edition on all three devices, every lane in light and dark, large text, and the specs I'll build from. |
| [`design/prototype.html`](design/prototype.html) | A clickable iPhone prototype: onboarding, every lane, the Edition, purchases, search, compose and settings, all linked and working with sample mail. |

The pages are plain HTML with no build step. Open them in a browser. They load fonts from Google Fonts, so they look best online, but they work offline with fallback fonts.

## The lanes

I sort mail into five lanes instead of keeping one inbox:

- **VIP**: people I've picked. Every message arrives with a reply already drafted.
- **Action**: mail that asks me to do something, grouped by due date.
- **Reading**: newsletters, bound into a magazine-style Edition twice a day.
- **Purchases**: receipts and shipping mail, folded into one entry per order.
- **Screener**: first-time senders, who wait until I let them in.

## Decisions so far

- **Accounts:** I'm starting with Gmail and iCloud. Gmail syncs through the Gmail API with Google sign-in. iCloud syncs over IMAP with an app-specific password, because Apple doesn't offer sign-in to third-party mail apps.
- **Scope:** Koumara replaces Apple Mail, so it's a full client: writing, drafts, signatures, attachments, search, and the option to be the default mail app.
- **AI:** I'm splitting the AI work by what each job needs:
  - **Headers first.** The cheapest checks don't need a model at all. `List-Unsubscribe` marks a newsletter, and a sender match marks a VIP.
  - **Apple's on-device model** (the Foundation Models framework) sorts whatever the headers can't settle, on every device.
  - **oMLX on my Mac** writes VIP drafts and long summaries and builds search embeddings, through its OpenAI-compatible API.
- **VIP replies:** Every VIP reply is drafted automatically, and Koumara never sends anything on its own. If a VIP has been waiting too long, I get a reminder with the draft attached.
- **No illustrations:** The app has no illustrations. Delight comes from type, motion, haptics, and the lane colors and glyphs.

## Still open

- Who counts as a VIP. My default is a hand-picked list plus suggestions based on how fast I reply.
- The minimum devices and OS versions, since Apple's on-device model needs Apple Intelligence hardware.
- How iPhone reaches the Mac running oMLX when I'm away from home. A private tunnel like Tailscale would work; without one, drafts fall back to the on-device model.
