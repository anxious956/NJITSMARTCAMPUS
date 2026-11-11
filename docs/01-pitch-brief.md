# Pitch brief

This fills in the six-point outline. Sections 1–6 map to what the judges ask for.

## 1. Topic

Real-time parking guidance and vehicle awareness for NJIT: detect open spaces in every lot, read plates at the gate, and assign each arriving car to a lot with room. One system, two beneficiaries — drivers and Public Safety.

## 2. Challenge statement

> NJIT is a commuter campus in downtown Newark with more permit holders than parking spaces. Drivers have no way to know which deck has room until they are inside it, so they circle — burning time, fuel and patience, and arriving late to class. At the same time, Public Safety has no live picture of which vehicles are on campus or whether they belong there.

Supporting data to put on screen:

| Claim | Source | Status |
| --- | --- | --- |
| US drivers spend an average of 17 hours a year looking for parking, costing $345 per driver in time, fuel and emissions | INRIX, 2017 | Confirmed, but the study is from 2017 — say "an INRIX study found" |
| About 79% of NJIT students commute | Student newspaper, citing U.S. News | **Verify** — date of the figure is unknown |
| 3,698 student permits issued against 2,968 spaces | NJIT Vector (student newspaper) | **Verify** — this report is old; ask Parking Services for current numbers |
| The Science & Technology Park garage has 981 spaces | NJIT Campus Planning page | Confirmed on NJIT's site |
| How long NJIT students actually spend finding a spot | Our own survey | **To do** — a 3-question poll of 30+ classmates today gives a real, local number |

The own-survey number is the strongest one to have: the rubric's top score for content asks for "data, research, or real-world validation."

### How parking works at NJIT today

From NJIT's Parking Services pages and what we know as students:

- **Students pay by term** for a parking permit and display a hang tag. There is no pay-by-phone parking in NJIT lots; the street meters around campus are the city's.
- **Guests need a host.** Faculty and staff book free visitor parking through an online system that does not take same-day requests. Guest parking is in Lot 7 (17 visitor spaces), the parking deck at 154 Summit Street, and the Science & Technology Parking Garage at 46 Wilsey Street.
- **At the garage gate, a guest has to ask a Public Safety officer for help** over a two-way speaker.
- **Overnight parking** (1–5 a.m., Monday to Friday) is limited to permit holders who live on campus and to certain levels — for example, no overnight parking on levels 1–3 of the Science & Technology garage. Guests of resident students get a one-night permit through Public Safety, and exceptions go through a form with a response expected within 72 hours.

Each of these is a manual check today — a hang tag, an officer at a speaker, a patrol at night — and each is something a plate-aware system can do automatically.

## 3. Solution

1. **See the spaces.** Cameras that cover the lots run a vision model that marks each space open or taken. No sensor has to be drilled into every space.
2. **Know the car.** A plate-reading camera at each entry reads the plate and matches it against NJIT's own permit list.
3. **Assign the lot.** The system picks the lot and level with room that suits the permit, and tells the driver on the app and on a sign at the gate before they commit to a full deck.
4. **Recognize guests.** An approved guest pass carries the guest's plate, so the gate recognizes the car without an officer having to answer the speaker, and the host gets a notification.
5. **Apply the overnight rules.** Cars allowed to stay overnight are sent to a level where that is permitted; a car left where it should not be is flagged.
6. **Keep campus aware.** A vehicle with no permit or pass, or in a lot it is not allowed in, raises a flag for Parking Services. Public Safety gets alerts under a written policy (see the regulations doc).
7. **Predict.** After a few weeks of data the app can say "The Summit Street parking deck usually fills by 9:40 on Tuesdays."

## 4. Value proposition

> Octopark turns the cameras and network NJIT already needs into a live map of every parking space, so a driver goes straight to an open spot instead of circling — and campus gets safer, cleaner and cheaper to run.

| Who | What they get |
| --- | --- |
| Students, faculty, staff | Minutes back every day; a known spot before they arrive |
| Parking Services | Enforcement without walking the lots; real occupancy data for planning; hang tags can go away |
| Public Safety | Officers no longer answer the gate speaker for every approved guest; live awareness of vehicles on campus; overnight rules checked automatically |
| NJIT | Fewer cars idling in decks (emissions), and data to decide whether a new deck is really needed |
| Verizon | A repeatable campus product: 5G + edge AI + IoT sold to every commuter university, hospital and stadium |

## 5. Verizon pillar

Pick one as the headline — projects must align with one of the three pillars.

- **Headline: AI-Driven Automation & Efficiency.** Vision AI at the network edge replaces manual lot checks and hangtag enforcement.
- Supporting: *Cost & Sustainability Transformation* — wireless backhaul means no trenching fiber to every lot, and less circling means less fuel burned.
- Supporting: *Next-Gen Products & Services* — the student app is the customer experience.

How Verizon's network is used is in [03-architecture-data-security.md](03-architecture-data-security.md#how-verizon-is-used).

## 6. Feasibility, budget and rollout

Every piece exists today. Verizon already sells **5G Video Insights**, which turns ordinary cameras into AI cameras and includes a "parking occupancy" app. Plate readers are in use at other universities' decks (VCU, NC A&T and TCNJ run plate-based virtual permits), and open-space detection from camera video is a well-studied vision problem. What is new is combining them at the network edge on 5G and using the result to *assign* drivers, not just bill them.

**The backend runs on AWS.** Permit matching, the live map, the database and the app run on standard AWS services (IoT Core, Lambda, DynamoDB, Cognito, Amplify). Verizon's 5G Edge works with AWS Wavelength, so the same AWS code can run inside Verizon's network next to campus — that is how the answer reaches the gate in time. A student team can build the pilot with these services; the full list is in [03-architecture-data-security.md](03-architecture-data-security.md#software).

**Pilot — one deck, one semester.**

| Item | Quantity for a one-deck pilot | Rough unit cost (our estimate — replace with vendor quotes) |
| --- | --- | --- |
| Plate-reading cameras at entry and exit lanes | 2–4 | $1,500–$5,000 |
| Overview cameras for space detection (one covers roughly 20–50 spaces) | 20–40 | $300–$1,000 |
| Edge compute (on-site box or Verizon 5G Edge) | 1–2 | $500–$2,000 per box, or monthly service |
| 5G routers / connectivity | per camera cluster | monthly service |
| Entry sign showing open counts | 1 | $2,000–$5,000 |
| App and dashboard | student-built for the pilot | — |

These ranges are our own planning assumptions, not quotes. The comparison worth making in the pitch: in-ground sensors need one device per space, cameras need one per few dozen spaces.

**Rollout:** Pilot one deck → all decks and surface lots → predictions and reservations → offer to other Newark campuses (Rutgers–Newark and Essex County College are next door).

**Risks and answers:**

| Risk | Answer |
| --- | --- |
| "This is surveillance" | Parking-only purpose, plates tokenized at the edge, short retention, public policy and signs — see the regulations doc |
| Plate misreads (dirt, snow, temporary tags) | App check-in as fallback; a misread never causes an automatic ticket without a human check |
| Cameras cannot see every space | Count cars in and out per level as a second signal |
| Cost | Start with one deck; reuse existing camera mounts and power |

## How we score on the rubric

| Criterion | What "High" means on the scoring guide | Our answer |
| --- | --- | --- |
| Impact | Clearly defined, significant problem with multiple beneficiaries | Every commuter, Parking Services, Public Safety, the environment |
| Feasibility | Real-world, cost-effective, can be rapidly prototyped and tested | One-deck pilot with off-the-shelf parts; proven at other universities |
| Creativity | Highly innovative and unique | Assigning a lot at the gate from live vision data; privacy designed in from day one |
| Content | Backed by data, research or real-world validation | INRIX study, NJIT numbers, our survey, the legal research |
| Presentation | Well-structured, clear, engaging, strong visuals, confident delivery | Commercial-style video with the animated demo |

## Open questions for the Verizon mentors and NJIT

1. Does NJIT already have plate readers or cameras in the decks that a pilot could reuse?
2. Who would operate the system — Parking Services or Public Safety? The legal rules differ sharply (see the regulations doc).
3. Is there Verizon 5G Ultra Wideband coverage inside the decks, or would the pilot need small cells or a private network?
4. Current permit and space counts, and peak occupancy by hour.

## Sources

- [NJIT Smart Campus competition page](https://computing.njit.edu/node/601)
- [INRIX: Searching for parking costs Americans $73 billion a year](https://inrix.com/press-releases/parking-pain-us/)
- [NJIT Vector: 3,698 student permits issued, 2,968 parking spaces available](https://njitvector.com/?p=5193)
- [NJIT Campus Planning: Science & Technology Park parking facility](https://www.njit.edu/campusplanning/node/9)
- [NJIT Parking: Visitor parking](https://www.njit.edu/parking/node/5)
- [NJIT Parking: Overnight parking](https://www.njit.edu/parking/node/6)
- [Verizon ThingSpace: 5G Video Insights](https://thingspace.verizon.com/solutions/platforms/5g-video-insights.html)
- [VCU: License plate recognition](https://parking.vcu.edu/parking/lpr/)
- [NC A&T: LPR virtual permits](https://ncat.edu/campus-life/campus-enterprises/parking-and-transportation/parking-permits/lpr-virtual-permits.php)
