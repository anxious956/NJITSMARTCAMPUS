# Two-minute commercial

**Hard limit: 2:00.** This script is timed to **1:55**, leaving five seconds of margin. The spoken part is about 200 words — roughly 1:25 at a calm pace — and the rest is pictures and music. If the first read-through runs long, cut the lines marked *(optional)*; do not speed up the voice.

**The format:** a filmed opening where a driver checks NJIT's own parking page and it shows something impossible, then a **freeze frame** where a teammate walks in and gives the pitch with the live demo running behind them, then the frame **unfreezes** and the same driver parks with Octopark.

The competition requires a **challenge statement** and a **value proposition**. Both appear as on-screen titles so a judge cannot miss them.

## What the pitch emphasizes

In this order, and in roughly these proportions:

1. **The driver** — about half the time. "Your phone tells you your level and space before you pick a ramp." This is the hook judges remember, and it scores on Impact because every commuter benefits.
2. **Verizon and AWS** — about a quarter. The project must fit a Verizon pillar (AI-Driven Automation & Efficiency), and the judges include Verizon. Show 5G, 5G Edge and the AWS backend doing the work.
3. **Privacy** — one confident line. It answers "isn't this surveillance?" before anyone asks. Leading with security or plate tracking invites that question instead.
4. **Public Safety** — one beat (`V`). A bonus, not the headline.

**Blame the method, not NJIT.** The judges work at NJIT. The opening shows that *counting at the gate drifts*, not that NJIT is incompetent. The research behind it is in [07-existing-njit-parking-page.md](07-existing-njit-parking-page.md).

## Script

| Time | Picture | Spoken | On screen |
| --- | --- | --- | --- |
| 0:00–0:10 | **Filmed.** From the passenger seat: up a deck ramp, every space full. Dashboard clock 8:24. | *(Engine and turn signal, no voice.)* | `8:24` |
| 0:10–0:18 | **Filmed, parked.** The driver opens NJIT's parking page on their phone. Cut to the screen recording of the page; zoom in and circle **Available 255** and **Total 155**. Back to the driver's face. | Driver: "...what?" | Circle on `255` and `155` |
| 0:18 | **Freeze frame** with a record-scratch sound. The presenter walks into frame in front of the frozen shot. | — | — |
| 0:18–0:35 | **Presenter**, frozen frame behind or beside. | Presenter: "That's NJIT's real parking page. It counts cars at the gate, so one missed car makes every number after it wrong. And with more permits than spaces, nobody knows where the open spot is until they're already inside." | **THE CHALLENGE** — More permits than spaces. No way to know where the open spot is. *(add your survey number)* |
| 0:35–0:42 | **Presenter, demo behind.** The demo comes up already running. | Presenter: "What if campus actually knew where your spot was? This is Octopark." | **Octopark** |
| 0:42–1:05 | **Presenter, demo behind.** Press `Space` — a car rolls up, the plate is read, the phone and the gate sign show the level and space. Presenter gestures to it. | Presenter: "Cameras look at every space, not just the gate. An AI computer in each deck marks every space open or taken. At the gate, a plate reader matches your car to your NJIT permit — and before you pick a ramp, your phone tells you your level and your space." | **Hardware:** overview cameras · plate reader · edge AI computer · 5G router · entry sign |
| 1:05–1:25 | **Presenter, demo behind.** The "How it works" strip at the bottom of the demo lights up left to right. | Presenter: "It runs on Verizon and AWS. 5G carries the video with no cables to dig. Verizon's 5G Edge runs AWS right inside the network, so the decision is made before you reach the gate. And the backend — permits, the live map, the app — runs on AWS." | **AI-Driven Automation & Efficiency** — Verizon 5G · 5G Edge · Backend on AWS |
| 1:25–1:38 | **Presenter, demo behind.** Press `V` — a car with no permit or pass arrives and the gate officer is alerted on the right-hand panel. | Presenter: "Privacy is built in. Video never leaves the deck, plates become codes, and they're deleted when you drive out. A car with no permit? The gate officer knows right away." | Parking only · No faces · Deleted on exit |
| 1:38–1:50 | **Filmed — the frame unfreezes.** The same driver opens Octopark, drives straight to the space, parks, walks into class relaxed. Clock: 8:14. | Voiceover: "Students get minutes back. NJIT gets parking numbers it can trust. Verizon gets a product for every campus." | **THE VALUE** — Straight to an open spot. Numbers campus can trust. |
| 1:50–1:55 | Logo and team names. | Presenter or voiceover: "Octopark. Stop circling." | Team name · NJIT · 2026 Verizon Smart Campus Challenge |

### Notes on the opening

- **Record NJIT's parking page now.** On November 11 at about 12:30 a.m. it showed the ECC Deck with 255 available out of 155. Anyone could reset the counter at any time. Screen-record it on a phone while it is still wrong. If it is fixed by filming day, film the driver's reaction anyway and cut to the recording. The screenshot in [img/njit-parking-page-2026-11-11.jpg](img/njit-parking-page-2026-11-11.jpg) is the last-resort backup.
- **The driver is parked when they look at the phone.** Never show a driver using a phone while moving — it undercuts a safety pitch, and judges notice.
- **The numbers must be readable.** A phone screen in a car shot is tiny. Zoom in during editing and circle the two numbers, or the joke does not land.
- **Keep the reaction clean.** A face and "...what?" lands better than swearing on audio in front of NJIT faculty and Verizon.
- **Freeze frame without a green screen:** export the frozen frame as a still, put it full screen on a TV or projector, and film the presenter walking in front of it. Or do it in the edit: freeze, then cut to the presenter in front of the demo.
- **Don't claim numbers for other campuses.** We only have evidence for NJIT. "Campuses count parking this way" is fine; a statistic is not.

## Demo tasks before filming

The demo in [demo/index.html](../demo/index.html) is already finished: phone app, live space map, gate camera, the "How it works" strip and the privacy badges. **Do not add new screens or panels** — anything extra on screen competes with the presenter. Deadline: **noon on filming day**, so there is time to rehearse.

**Must do**

- [x] Set the real lot sizes at the top of the script block: Parking Deck (Summit St) **1,685**, Science & Tech Garage **922** — from NJIT's live page; the pitch brief says 981, so confirm with Parking Services. Keep Lot 7 (the visitor lot) as it is.
- [ ] Optional: story mode (`?story` on the end of the address). Each press of `→` (or a clicker) moves to the next moment in this script: Octopark, at the gate, your level and space, built on Verizon + AWS, privacy. The part being talked about comes to the front, a car arrives by itself at the gate and privacy steps, and a subtitle bar names the step. Useful when the demo plays beside the presenter at half size.
- [ ] Rehearse with `?manual` on the end of the address so cars arrive only on a key press. Time the `Space` and `V` presses against the spoken lines above.
- [ ] Record a clean 30-second, 1080p screen capture of the demo by itself, as spare footage for the editor.

**Only if all of the above is done**

- [x] One small callback to the opening, such as a line or badge reading "Counted by cameras, not gates." One line — no new panel.

## Filming the presenter with the demo behind

Two ways to do it. Pick one; the first looks more like a commercial, the second is faster.

**A. Stand in front of a big screen.** Put the demo full screen on a classroom TV or projector and film the presenter standing beside it.

- Stand to one side so the presenter does not block the gate panel on the right.
- Dim the room lights a little so the screen is not washed out, and light the presenter's face from the front with a window or a desk lamp. Check on the phone that both the face and the screen are readable before recording the real take.
- A second teammate sits at the laptop and presses `Space` and `V` on cue.
- Phone horizontal on a tripod or a stack of books, at eye level.

**B. Screen recording with a camera bubble.** Record the demo and the presenter's webcam together.

- Loom, Canva ("Record yourself"), Zoom (share screen and record) and OBS all do this for free.
- If there is time to show guests, press `G`: a guest with an approved one-night permit is recognized and the host's phone is notified. It is optional — cut it before anything else.
- Press `P` in the demo first: it clears the bottom-left corner so the camera bubble has a clean place to sit and covers nothing.
- The presenter presses `Space` and `V` themselves.

Either way:

- Record sound with a phone held close or clipped to the shirt — room echo is what makes student videos sound amateur.
- Do each section as its own take, three times, and keep the best. Nobody has to get 70 seconds right in one go.
- Look at the lens, not at the screen, except when pointing at the demo.

## People on camera

| Role | Where they appear | What they do |
| --- | --- | --- |
| **The driver** (a teammate) | 0:00–0:18 and 1:38–1:50 | One line ("...what?"). Frustrated at the start, relaxed at the end. The before-and-after is the story. |
| **The presenter** (most confident speaker) | 0:18–1:38 | Walks into the freeze frame and talks to camera, then with the demo behind. Two presenters can split it: one for the problem and solution, one for Verizon, AWS and privacy. |
| **The narrator** | 1:38–1:55 | Voiceover only. Can be the presenter. |
| **Demo operator** | Off camera | Presses `Space` and `V` on cue. Open the demo with `?manual` on the end of the address so cars arrive only on a key press. |

- **Never film while actually driving.** The driver's shots are taken parked, or the passenger films out of the windshield.
- Only teammates and people who agreed appear recognizably. Blur bystanders' faces and other cars' plates in editing — showing strangers' plates would undercut the privacy message.
- A real student saying "I've been late twice this month because of parking" is worth five seconds over the challenge title at 0:20, if someone will say it on camera.

## Shot list

Everything can be filmed on a phone in about an hour.

1. **Screen recording of NJIT's parking page showing more available than total** — do this first, tonight if possible.
2. Deck ramp drive from the passenger seat, 20 seconds, horizontal. Go mid-morning when it is full.
3. Dashboard clock close-up — or film once and change the time in editing.
4. Driver, parked, opens the NJIT page and reacts. Film the face and, separately, the phone screen.
5. **Presenter walking into the freeze frame** — three takes.
6. **Presenter with the demo behind — four sections, three takes each.**
7. Driver opens Octopark, parks, walks in — one continuous take. Use the same car, clothes and spot in the deck as shot 4 so the unfreeze reads as the same moment.
8. Clean screen recording of the demo by itself, 30 seconds, as a spare to cut to.

## Production plan for the last day

| When | What | Who |
| --- | --- | --- |
| Tonight | Screen-record NJIT's parking page while it still shows the wrong numbers (shot 1) | 1 person |
| Morning | Run the 3-question survey in class group chats; confirm the upload link with the organizers | 1 person |
| Morning, by noon | Demo tasks above: real lot sizes, rehearsal with `?manual`, spare screen capture | 1 person |
| Morning | Film shots 2–4 and 7 on campus while the decks are full | 2 people |
| Midday | Film the presenter walking into the freeze frame and with the demo behind; record the voiceover in a quiet room | 2–3 people |
| Afternoon | Edit: lay the speech first, cut pictures to it, add titles, then music | 1–2 people |
| By 8 p.m. | Export, watch on a phone and a laptop, check it is under 2:00 | Everyone |
| By 10 p.m. | Upload. Do not wait for 11:59. | 1 person |

**Editing tools:** CapCut and DaVinci Resolve are free; Canva also has a video editor. Export 1080p MP4.

**Music:** use a track that is free to use — the YouTube Audio Library or the editor's built-in library. Keep it low under the voice.

**Three-question survey** (gives the on-screen number at 0:18):

1. Do you drive to NJIT?
2. On a typical day, how many minutes do you spend finding a parking space?
3. Have you been late to class because of parking this semester?

## Rules to remember

- Two minutes maximum.
- Must state the problem and the solution clearly; must include a challenge statement and a value proposition.
- Prototypes are not required and do not affect judging. The demo is a visual aid, and its on-screen label says it is a concept with simulated data — keep that label visible.
- AI tools are allowed with transparency. If an AI voice or AI images are used, add a small credit line at the end.
- Do not use the Verizon logo unless the organizers say it is fine; naming Verizon technologies in text is enough.
