# Architecture, data and security

**Status: draft.** This is a proposed design to get us through Round 1. The final architecture is still to be decided by the team — the open choices are listed under [Decisions still open](#decisions-still-open). For the video we only need the big picture, the hardware list and the Verizon story.

## The system at a glance

```
   PARKING LOTS AND DECKS                VERIZON NETWORK                 NJIT / CLOUD
 ┌──────────────────────────┐        ┌────────────────────┐        ┌────────────────────────┐
 │ Gate camera (plates)     │        │                    │        │ Parking service        │
 │ Overview cameras (spaces)│─video─▶│  5G / private 5G   │        │  · lot + level chooser │
 │ Entry sign               │◀─count─│        │           │        │  · permit matching     │
 └──────────────────────────┘        │        ▼           │─events▶│  · predictions         │
                                     │  Edge AI (5G Edge) │        │ Database (no raw       │
                                     │  · space open/taken│        │  plates, no video)     │
                                     │  · plate → token   │        └───────────┬────────────┘
                                     │  · blur faces      │                    │
                                     │  video stops here  │          ┌─────────┴──────────┐
                                     └────────────────────┘          ▼                    ▼
                                                              Student app        Parking / Public
                                                              (live map)         Safety dashboard
```

The key property: **video never leaves the edge.** Only small events travel on — "space C-14 is now open," "token 9f3a entered deck 2."

## Hardware

What would physically be installed. Brands are examples of the kind of device, not final choices.

| Hardware | What it does | Where | Example |
| --- | --- | --- | --- |
| **Plate-reading camera** | Reads the plate of each car entering or leaving; infrared so it works at night and in rain | One per entry and exit lane | Axis or Hanwha license-plate camera |
| **Overview cameras** | Watch rows of spaces so the AI can mark each open or taken; one camera covers roughly 20–50 spaces | Ceilings in decks, light poles in surface lots | Axis or Hanwha outdoor network camera, or cameras NJIT already has |
| **Camera companion** | Verizon's add-on device that turns a standard network camera into an AI camera for 5G Video Insights | Next to existing cameras | Verizon 5G Video Insights camera companion |
| **Edge AI computer** | Runs the vision models on site so video never has to leave | One small box per deck, in a locked cabinet | NVIDIA Jetson Orin |
| **5G router** | Connects the cameras and edge box to Verizon's network; no cable trenching | One per camera cluster | Cradlepoint or similar Verizon-certified 5G router |
| **Network switch with power-over-ethernet** | Powers the cameras and links them to the edge box over one cable each | With the edge box | Any managed PoE switch |
| **Entry sign** | Shows open counts per lot and level at the gate | Each entrance | Outdoor LED message sign |
| **In-ground or surface sensors** *(optional)* | Detect a car in spaces the cameras cannot see | Blind spots, accessible spaces | Low-power cellular (LTE-M or NB-IoT) parking sensor |
| **Drivers' own phones** | Run the app | — | — |

Two rules for buying cameras: they must come from a maker allowed under the federal supply-chain ban (no Hikvision or Dahua — see the regulations doc), and they must let us turn off audio.

For a **one-deck pilot** that is about: 2–4 plate cameras, 20–40 overview cameras, 1 edge computer, 1–2 routers, 1 switch, 1 sign.

## Software

We expect to build on **AWS**, which fits the Verizon story well: Verizon's 5G Edge is offered together with AWS (the product is called AWS Wavelength), so the same AWS tools run inside Verizon's network.

| Layer | What it does | Likely tool |
| --- | --- | --- |
| Space detection | Finds cars in the overview video and decides which spaces are open | Verizon 5G Video Insights' parking-occupancy app — or our own open-source object-detection model (YOLO family) trained on photos of NJIT lots |
| Plate reading | Finds the plate and reads the characters | An open-source plate-recognition model, or the camera's built-in reader |
| Running models at the edge | Deploys and updates the models on the edge box | AWS IoT Greengrass on the Jetson — or AWS Wavelength if the AI runs in Verizon's network |
| Device messaging | Carries the small events from edge to cloud securely | AWS IoT Core |
| Parking logic | Matches permits, picks the lot, sends alerts | AWS Lambda behind Amazon API Gateway |
| Database | Stores space status and plate tokens | Amazon DynamoDB — its expiry feature deletes records automatically, which enforces our retention rules |
| Sign-in | NJIT single sign-on for students and staff | Amazon Cognito linked to NJIT login |
| Keys and encryption | Holds the encryption and tokenizing keys | AWS Key Management Service |
| Audit logs | Records every access to the data | AWS CloudTrail and CloudWatch |
| Model training | Trains and improves the vision models | Amazon SageMaker, or a university GPU |
| App | Live map, "where do I park," predictions | A web app first (works on any phone), hosted on AWS Amplify |

## Decisions still open

| Decision | Options | What it depends on |
| --- | --- | --- |
| Space detection: buy or build | Verizon 5G Video Insights · our own model · both | Price, accuracy inside the decks, and whether it can report single spaces or only counts |
| Where the AI runs | On-site edge box · Verizon 5G Edge with AWS Wavelength · both | Verizon coverage in the decks; what the mentors recommend; cost |
| How spaces are detected | Cameras only · cameras plus sensors in blind spots · counting cars in and out per level | How well cameras can see inside the decks |
| Public 5G or private 5G | Verizon's public network with a private connection · a campus private network | Cost and NJIT IT's preference |
| Plate reading | Camera's built-in reader · our own model | Accuracy on New Jersey plates and temporary tags |
| App | Web app · inside the existing NJIT mobile app · standalone app | Whether NJIT will let us plug into its app |
| Who operates it | Parking Services (our proposal) · Public Safety | Legal review — see the regulations doc |

## What happens when a car arrives

1. The gate camera sees a car. The edge reads the plate and immediately turns it into a token (a keyed code).
2. The token is checked against the tokens of NJIT-registered permits.
3. The parking service picks the lot and level with room that the permit allows.
4. The entry sign and the driver's app show it: "Welcome — Level 3 has 42 open."
5. Overview cameras confirm when the car takes a space; the count updates for everyone.
6. An approved guest — a host-arranged visit or a one-night guest permit — is on the list too, so the guest is recognized and sent to a level where they may park. The host is notified.
7. No permit and no pass → no space is assigned and the gate officer is alerted, as happens over the speaker today.
8. Overnight (1–5 a.m. on weekdays), cars with overnight permission are sent to the levels where it is allowed; a car on the wrong level is flagged for Parking Services.

The whole loop has to finish while the car is still rolling up to the gate. That is why the computing sits at the edge and not in a distant data center.

## How Verizon is used

| Verizon capability | What it does for us | Why it matters |
| --- | --- | --- |
| **5G Video Insights** (ThingSpace) | Makes any standard network camera AI-enabled. Ready-made apps include **parking occupancy**, vehicle count, vehicle detection and object blurring | The "which spaces are open" half of our system is something Verizon already sells; video is analyzed on site with end-to-end encryption and no biometric data |
| **5G Ultra Wideband** | Carries many camera video streams wirelessly from lots to the edge | No trenching fiber across asphalt to every pole — the biggest construction cost avoided |
| **5G Edge (multi-access edge computing)** | Runs the vision AI inside Verizon's network close to campus, or on a box on campus | Answer in the time it takes a car to reach the gate; video is processed and discarded locally |
| **Private 5G network** | A campus-only network for cameras and signs | Camera traffic never touches the public internet; NJIT controls who is on it |
| **Network slicing** | A reserved lane on the network for the parking system | Stays fast on a game day or at commencement when everyone's phone is busy |
| **IoT connectivity and the ThingSpace platform** | Connects and manages low-power devices: entry signs, gate sensors, optional in-ground sensors for spots cameras cannot see | One place to monitor, update and switch off every device |
| **Fixed wireless access** | Back-up connection for the deck's equipment | Keeps the system up if the wired link fails |

What Verizon has and what we add:

- **Verizon has:** 5G Video Insights with a parking-occupancy app, on-site processing and privacy blurring. Its page says it works with any ONVIF-compliant network camera through a "camera companion" device, so cameras NJIT already owns could be reused.
- **Verizon's page does not mention:** reading license plates, matching a car to a permit, or assigning a space.
- **We add:** the plate-to-permit match, guest passes, overnight rules, the assignment of a level and space, and the student app.

So the honest line for the pitch is: "Verizon can already see which spaces are open. We turn that into telling each driver where to go."

**Ask the mentors:** which of these is realistic for a one-deck pilot at NJIT, and what coverage exists inside the decks.

## What data we collect

| Data | Personal? | Where it lives | Kept for |
| --- | --- | --- | --- |
| Camera video | Yes while it exists | Edge only, in memory | Seconds — processed, then discarded |
| Space status (open / taken) | No | Database | Indefinitely — this is the planning data |
| Plate token + time + lot | Yes (linked to a permit) | Database | Until the car leaves; unmatched reads 30 days at most |
| Permit registration (name, ID, plate) | Yes | NJIT's existing parking system | Per NJIT policy — we do not copy it |
| Plate image | Yes | Edge, only when flagged for review | Until a person reviews it; 30 days at most |
| Access logs | Staff only | Database | One year or more, for audits |

Where the plate data comes from: **drivers register their own plates with NJIT** when they buy a permit, as they already do. We do not buy plate data and do not query the Motor Vehicle Commission.

## How the data is secured

**At the edge**
- The plate is tokenized with a keyed hash before it leaves the site. The key lives in a hardware-protected store, and a stolen database is a list of meaningless codes.
- Faces and anything outside the parking area are blurred or cropped before analysis.
- Cameras come from makers that comply with the federal supply-chain ban (see the regulations doc), with default passwords removed and firmware signed.

**In transit**
- Private 5G or a private network path: devices are not reachable from the public internet.
- Each device proves its identity with a certificate and SIM; everything is encrypted with TLS 1.3.

**At rest**
- Database encrypted (AES-256), keys in a managed key store, rotated on a schedule.
- The table that links tokens to people stays in NJIT's parking system, separate from the event data.

**Access**
- Sign-in through NJIT single sign-on with two-factor.
- Roles: a student sees only their own car and lot counts; Parking Services sees violations; Public Safety sees only the alerts the written agreement allows; nobody browses plate history.
- Every lookup is logged with who, when and why, and reviewed in a yearly audit.

**Deletion**
- Automatic deletion jobs enforce the retention table above; deletion is logged too.

**If something goes wrong**
- An incident plan covering detection, containment and notification under New Jersey's breach law.
- The system fails safe: if the network or AI is down, gates open on the existing permit process and the app shows "counts unavailable" — nobody is locked out.

## What we would build first

A one-deck pilot needs only: two gate cameras, a few overview cameras on one level, one edge box, the event database, and a simple web app. A student team can build the software; the demo in `demo/` shows what the result looks like.
