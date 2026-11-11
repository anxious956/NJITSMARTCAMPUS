# HighlanderSpot — smart parking for NJIT

Our entry for the **2026 Verizon Smart Campus Innovation Challenge**. "HighlanderSpot" is a working name.

This page explains the whole project in plain language. Read it once and you can explain the idea to a judge.

**Round 1 is a two-minute video, due November 12, 2026 at 11:59 p.m.**

## The problem

NJIT is a commuter campus. There are more parking permits than parking spaces, and nobody can tell which deck has room until they have already driven into it. So people circle, burn fuel, and walk into class late. Meanwhile Public Safety has no live picture of which cars are on campus.

## Our idea

Campus should already know where the open spots are and tell you before you choose a ramp.

1. **Cameras watch the lots.** Software looks at the video and marks every space as open or taken.
2. **A camera at the gate reads your licence plate** and checks it against the plate you registered with NJIT when you bought your permit.
3. **The system assigns you a lot.** Your phone and a sign at the gate say, for example, "Level 3 — 42 open."
4. **Campus stays aware.** A car with no permit is treated as a visitor and sent to visitor parking. Parking Services sees it; Public Safety is alerted only in cases a written policy allows.

## How it works, step by step

```
Camera  ──▶  Verizon 5G  ──▶  Edge AI  ──▶  Parking service  ──▶  Your phone + gate sign
(sees cars)  (carries video)  (understands   (matches permit,     (tells you where
                              the video)     picks a lot)         to park)
```

- The **camera** only captures video.
- **5G** carries that video wirelessly, so nobody has to dig up the lots to lay cable.
- The **edge AI** is a computer close to campus that turns video into simple facts — "space C-14 is open," "a car with this permit just arrived." The video is thrown away right there.
- The **parking service** decides which lot has room for you.
- The **app and sign** show the answer in the few seconds it takes you to reach the gate.

## What we would install

| Hardware | Job |
| --- | --- |
| **Plate-reading cameras** at each entry and exit | Read the plate as a car comes in |
| **Overview cameras** in decks and on light poles | Let the AI see which spaces are open; one camera covers dozens of spaces |
| **Edge AI computer** (for example an NVIDIA Jetson) in each deck | Runs the AI on site so video stays local |
| **5G router** | Connects everything to Verizon's network without cables in the ground |
| **Entry sign** | Shows open counts at the gate |
| **Sensors** in a few spaces (optional) | Cover spots the cameras cannot see |

The **software** — the AI models, the database and the app — would most likely run on **AWS**. That fits well, because Verizon's edge computing is offered together with AWS. The exact architecture is **still to be decided**; the current draft and the open choices are in [docs/03-architecture-data-security.md](docs/03-architecture-data-security.md).

## Words you will hear

| Term | What it means here |
| --- | --- |
| **5G Ultra Wideband** | Verizon's fastest wireless network. Fast enough to carry many camera feeds at once. |
| **Edge computing** | Doing the computing near where the data is made (on or next to campus) instead of in a faraway data centre. It gives faster answers and keeps video local. |
| **Private 5G** | A 5G network only campus devices can join. The cameras are never on the public internet. |
| **IoT** | "Internet of things" — small connected devices such as cameras, signs and sensors. |
| **Plate reader (ALPR / LPR)** | A camera plus software that reads the letters on a licence plate. |
| **Token** | A scrambled code that stands in for your plate. The database stores the code, never the readable plate. |
| **Retention** | How long data is kept before it is deleted. |
| **AWS** | Amazon Web Services — rented cloud computers and databases. Where our software would run. |
| **Pillar** | One of Verizon's three focus areas. Every project must fit one; ours is **AI-Driven Automation & Efficiency**. |

## Who benefits

| Who | What they get |
| --- | --- |
| Students, faculty, staff | Minutes back every day and a known spot before arriving |
| Parking Services | Real numbers on how full each lot is; no more walking rows checking hangtags |
| Public Safety | A live picture of vehicles on campus |
| NJIT and Newark | Fewer cars idling in decks means less pollution |
| Verizon | A product it could sell to every commuter campus, hospital and stadium |

## How Verizon is used

- **5G** connects the cameras without cables.
- **5G Edge** runs the AI close to campus so the answer arrives before the car reaches the gate.
- **Private 5G** keeps camera traffic off the public internet.
- **IoT tools** connect and manage the signs and sensors.

More detail: [docs/03-architecture-data-security.md](docs/03-architecture-data-security.md).

## Privacy and the law, in short

The first thing a judge will ask is "isn't this surveillance?" Our answer:

- It is for **parking only**. It is not used to track where a person goes.
- **Video never leaves the edge**, and it is not stored.
- **Plates are turned into tokens** before anything is saved.
- **Data is deleted when you drive out.**
- We only match against plates **people registered with NJIT themselves**. We never look anyone up in state motor-vehicle records.
- A person, not a camera, makes any decision about a ticket.

On the rules: New Jersey has strict rules for plate readers run by **police** — data kept three years and shared with a statewide police system. We deliberately have **Parking Services** run the system instead, so the data stays on campus and is deleted quickly. Federal student-privacy law (FERPA) also applies because a plate can be linked to a student.

Full research with sources: [docs/02-rules-and-regulations.md](docs/02-rules-and-regulations.md). It is student research, not legal advice.

## Questions a judge might ask

**Does this already exist?** Parts of it do. Some universities read plates in place of hangtags, and some garages count open spaces. Combining both on 5G with edge AI, and using it to assign you a lot at the gate, is the new part.

**What does it cost?** Cameras cover dozens of spaces each, so it is far cheaper than putting a sensor in every space. We would start with one deck for one semester. Rough numbers are in the pitch brief.

**What if the camera misreads a plate?** The app lets you check in manually, and no ticket is ever issued from a camera read alone.

**What if the network goes down?** Gates work the way they do today and the app says counts are unavailable. Nobody gets locked out.

**Did you build it?** Not yet. Round 1 is a concept pitch, and prototypes are not required and do not affect judging. The demo is a simulation that shows what it would look like.

## The video

Two minutes maximum — ours is timed to 1:55. It opens with real footage of circling a full deck, then a teammate talks to camera with the demo running behind them, then it closes on the driver walking into class on time.

Script, shot list and the plan for filming day: [docs/04-video-script.md](docs/04-video-script.md).

## Running the demo

1. Download or clone this repo and open `demo/index.html` in Chrome. No install needed.
2. Press `F11` for full screen.
3. Keys: `Space` sends a car with a permit through the gate, `V` sends a car with no permit, `P` clears a corner for a webcam bubble.

The demo uses made-up plates and numbers. Lot names and sizes are placeholders at the top of the script block in the file — edit them to match campus.

## What is in this repo

| File | What it is |
| --- | --- |
| [docs/01-pitch-brief.md](docs/01-pitch-brief.md) | The pitch: challenge statement, value proposition, pillar, how we score on the rubric, budget, risks |
| [docs/02-rules-and-regulations.md](docs/02-rules-and-regulations.md) | Federal, New Jersey and NJIT rules for plate readers and campus cameras |
| [docs/03-architecture-data-security.md](docs/03-architecture-data-security.md) | System design, how Verizon is used, what data is collected and how it is secured |
| [docs/04-video-script.md](docs/04-video-script.md) | The two-minute script, shot list and production plan |
| [demo/index.html](demo/index.html) | The animated concept demo for the video |

## Before we submit

- [ ] Find out where the video is uploaded. The competition page says "Online" but gives no link — check the registration email or ask the organisers at Ying Wu College of Computing.
- [ ] Replace the numbers marked **verify** in the pitch brief with current ones from Parking Services, or with our own survey of classmates.
- [ ] Video is 2:00 or under, and states the challenge and the value proposition.
- [ ] If an AI tool made any voice or image in the video, credit it at the end.

## Competition facts

- Teams of 3–6. Judged on impact, feasibility, creativity, content and presentation.
- Round 2 is a poster showcase on February 11, 2027. Round 3 is a presentation on March 2, 2027. Three winning teams get $3,000 each and present at Verizon headquarters on March 30, 2027.
- Details: [NJIT Smart Campus page](https://computing.njit.edu/node/601).
