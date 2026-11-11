# What the system stores, and what that means for campus security

A common question about this project: *"If the app does not store plates, it cannot send them to anyone — so is it just a parking guidance app and no help to campus security?"*

Short answer: **it does store plate data, in coded form and for a short time.** That is enough to help campus security in real time. What it gives up is long-term history.

## What is stored

| Data | Stored? | Kept for |
| --- | --- | --- |
| Camera video | No — analyzed at the camera site, then discarded | Seconds |
| The readable plate ("K47-LMP") | No — discarded at the camera site | Seconds |
| A coded version of the plate (the **token**), with the time and lot | Yes | Permit holders: until the car leaves. Cars with no permit: up to 30 days |
| A photo of the plate | Only when a car is flagged for a person to review | Until reviewed, 30 days at most |
| Open / taken status of each space | Yes — it contains nothing personal | Indefinitely |

When the demo says **"not stored"**, it means the readable plate and the video. The token is stored.

### Why a token is still useful

NJIT holds the key that turns a plate into its token. So NJIT can always take a known plate, turn it into its token, and search for it. A token hides the plate from anyone who steals or leaks the database; it does not hide it from NJIT.

## What campus security gets

- **A live picture:** which cars are on campus right now, and which of them have no permit or guest pass.
- **Instant alerts:** a car with no permit or pass at the gate, or a car parked overnight on a level where that is not allowed.
- **A 30-day lookback on unknown vehicles** — the ones security cares most about.

## What campus security does not get

- **History on permit holders after they leave.** If a break-in at 2 p.m. is discovered at 6 p.m., the cars that already left are gone from the records.
- **Long-term history.** There is no answer to "was this car here three months ago?"
- **Sharing with the statewide police plate system.** That happens only if Public Safety runs the readers, and that brings a three-year retention rule — see [06-new-jersey-law.md](06-new-jersey-law.md).

So this is **a parking system with real-time security benefits, not an investigation tool.**

## Retention is a dial

How long records are kept is a choice the team makes, not something fixed by the technology.

| Option | Privacy message | Security value |
| --- | --- | --- |
| **Delete permit-holder records when the car leaves** (current design) | Strongest: "your data is deleted when you drive out" | Live awareness and alerts; lookback only on unknown vehicles |
| **Keep every record for a fixed short window, for example 72 hours** | Weaker: "deleted within three days" | Adds a short lookback on every vehicle — enough to cover an incident found later the same day |
| **Keep for months or years** | Weak — this is what people mean by surveillance | Full investigation tool, but it stops being a parking system |

**Our recommendation for the Round 1 video:** keep "deleted on exit." It is the cleanest answer to the surveillance objection. Describe the security benefit as live awareness and alerts.

If the team later wants security to be an equal half of the pitch, switch to the fixed window. The labels in the demo ("Deleted on exit") and the retention tables in the other docs would then need to change to match.

## One feature to leave out for now: a police watch list

It is tempting to say "Public Safety can load a list of wanted plates and get an alert." A police watch list is law-enforcement information, and loading it into a parking system probably brings that feature under the state's police plate-reader rules. Leave it out of the pitch, or say it would need legal review.
