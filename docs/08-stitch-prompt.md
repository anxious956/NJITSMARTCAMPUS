# Prompt for Google Stitch

Use this if you want Google Stitch (stitch.withgoogle.com) to try its own design for the demo screen. Choose **Web** mode (not App: the demo is one 1920x1080 widescreen page, and the phone is just one part of it). Paste the prompt below. With the **+** button, attach `demo/octopark-logo-full.png` so Stitch uses the real logo, and `demo/preview.png` too if you want it to keep the same layout.

Stitch only draws still screens. It cannot make the cars move, the gate lift or the pipeline light up. If you like what it makes, export it as HTML or a screenshot and bring it back so the look can be applied to `demo/index.html`, which already has all the animation.

## The prompt

```text
Design a single 1920x1080 desktop screen for "Octopark", a live parking system for NJIT (a university in Newark, NJ). It will be shown full screen behind a presenter in a 2-minute pitch video, so text must be large and readable from across a room.

Style: looks like a real shipped product, not a concept. Light theme. Flat: white panels on a warm light-grey background, thin 1px grey borders, small corner radius (8-10px), no shadows, no gradients, no glow, no glassmorphism, no neon, no dark mode. Typography like US road and parking signage: Overpass (bold headings, regular body), Overpass Mono for licence plates and codes. Brand colors from the Octopark logo: navy #0C2141 and parking-sign blue #1559A0. Other colors: black ink #14161A for text, parking-sign yellow #FFC20E for "your spot", green #157A3A for open spaces, red #D22630 for full and alerts, blue #1D5BD0 for guests. Simple line icons only, no emoji, no illustrations of people.

Layout, left to right:
1. Header bar: the attached Octopark logo (an octopus with a P) and the name "OCTOPARK", subtitle "Live parking for NJIT". A wide navy status strip in the middle with white text: "Permit recognized • go to Level 4, space C12". On the right: "280 open on campus", "87% full", "8:12 AM", and a small outlined tag "Concept demo • simulated data".
2. Left column: an iPhone showing the student app. Title "Find parking". A large yellow card: "Permit recognized at the gate / Level 4 • Space C12 / Guiding you in". A list of three lots with open counts and thin fill bars: Parking Deck • Summit St 141 (filling up), Science & Tech Garage 212 (plenty of room), Lot 16 • New St 5 (almost full). A small bar chart forecast for Lot 16 "Full by ~10:10". Tab bar: Park, Lots, My car, Alerts.
3. Centre: a large panel "Live space map — Science & Tech Garage" showing a top-down floor plan of one garage level: four rows of 16 numbered parking spaces (A1-D16) with grey cars, about 15 spaces highlighted green as open, one space yellow as the driver's assigned spot, and a dotted route from the entrance to it. Big green number "12 open on Level 4". Level selector 1-7 with 4 selected. Below it a small panel "How it works": five icons connected by lines: Cameras → Verizon 5G → Edge AI → Cloud → App + sign.
4. Right column: "Gate 1 camera • Parking Services": a security camera view of a car at a striped gate arm with its licence plate boxed in green. Under it a black LED entry sign with amber text "WELCOME L4 · C12". Then a 4-step checklist with green checkmarks: Plate read at the edge, Converted to a token, Checked against NJIT permits (Student term permit), Space assigned (Level 4 • Space C12). Then "Recent arrivals" with 3 rows. Footer row: No video stored • Plates tokenized • Deleted on exit.
```

## If the result still looks generic

Add one of these lines to the end of the prompt and generate again:

- "Make it look like the screen of a real parking guidance system made by a hardware company, not a startup landing page."
- "Use fewer rounded cards; separate sections with thin lines instead."
- "Remove any decorative shapes or background patterns."
