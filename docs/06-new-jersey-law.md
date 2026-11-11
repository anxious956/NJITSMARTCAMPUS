# How the design fits New Jersey law

This is student research for a competition pitch, not legal advice. NJIT's Office of General Counsel would have to confirm it before anything is built.

For the full list of federal, state and school rules, see [02-rules-and-regulations.md](02-rules-and-regulations.md). This page answers one question: **is what we store, and who we share it with, allowed in New Jersey?**

## The short answer

**Yes, whichever retention period we choose.** New Jersey's plate-reader rules turn on *who holds and uses the data*, not on how long a parking office keeps it.

## What New Jersey law covers

**There is no law for parking offices.** We found no New Jersey statute governing plate readers run by a body that is not the police. So Parking Services can keep data for an hour, 72 hours or 30 days. Nothing requires it to keep plate data at all.

**There are strict rules for police.** Attorney General Directive 2022-12 binds every law enforcement agency in the state. That would include NJIT Public Safety, which is a sworn police department. Plate data held by police must be:

- kept for three years;
- used only for law-enforcement purposes;
- logged every time someone accesses it;
- audited every year;
- made available to the statewide police plate-data system.

## Where the two meet

| Situation | What the directive says | What it means for us |
| --- | --- | --- |
| Parking Services gives data to Public Safety | A non-police operator "may provide ALPR data to New Jersey agencies but cannot receive law enforcement-owned ALPR data" | Passing an alert to Public Safety is allowed |
| Public Safety keeps a copy | Police-held plate data falls under the directive | That copy must be kept three years, logged and audited |
| Officers can browse the parking system freely | The directive applies to any agency "using an ALPR or its data" | **Gray area.** NJIT could be treated as running a police plate reader. Passing specific alerts under a written agreement keeps the line clearer |
| Public Safety loads a watch list of wanted plates into the parking system | A watch list is law-enforcement information | **Weak point.** This probably brings the feature under the directive. Leave it out of the pitch, or say it needs legal review |

## Other New Jersey laws

| Law | How it applies | How sure we are |
| --- | --- | --- |
| **Open Public Records Act** | NJIT is a public institution, so parking records could be requested. Police plate data is exempt as a criminal investigatory record; we have not confirmed which exemption covers parking data. Short retention limits what could be released | Needs General Counsel |
| **New Jersey Data Privacy Act** | Gives residents rights over personal data. Legal summaries disagree on whether it covers a public university | Unclear — needs General Counsel |
| **Breach notification law** | A plate by itself is probably not "personal information" under the statute, but a plate linked to a student should be protected as if it were | Fairly sure; verify the definition |
| **Wiretap law** | Restricts recording conversations. Our cameras record no audio | Sure |
| **Pending bill A5637** | Would cut police retention from three years to 90 days. Introduced October 2026; **not law**. It shows the state moving toward shorter retention | Sure it is pending |

## What to say in the video

> Parking Services runs it. The data stays on campus and is kept only briefly. Public Safety gets alerts under a written agreement.

That claim is safe under everything above. Avoid saying "police can search it" or "it connects to law enforcement" — those are the statements that would change which rules apply.

## How this connects to data retention

Because the three-year rule applies only to police-held data, the retention options in [05-data-storage-and-security.md](05-data-storage-and-security.md) — delete on exit, or keep for a short fixed window — are both lawful for a system run by Parking Services.

## Sources

- [NJ Attorney General Directive 2022-12 (PDF)](https://www.nj.gov/oag/dcj/agguide/directives/ag-Directive-2022-12_Updated-Directive-Regulating-Use-of-Automated-License-Plate-Recognition-(ALPR)-Technology.pdf)
- [NJ Assembly Bill A5637, as introduced](https://pub.njleg.gov/bills/2026/A6000/5637_I1.HTM)
- [Orrick: New Jersey Data Privacy Act — what companies should know](https://www.orrick.com/en/Insights/2024/03/New-Jersey-Data-Privacy-Act-What-Companies-Should-Know-About-the-States-New-Consumer-Privacy-Law)
