# Rules and regulations

This is student research for a competition pitch, not legal advice. Before any real deployment, NJIT's Office of General Counsel has to review it.

## The short answer

**Is it school rules or New Jersey rules?** Both, plus federal — three layers:

1. **Federal** law covers student records, motor-vehicle records and which camera brands a federally funded university may buy.
2. **New Jersey** has one detailed, binding rulebook for plate readers — but it applies to *police*. There is no New Jersey statute written specifically for a parking office reading plates in its own lot.
3. **NJIT** policy fills the gap: the university has to write and publish its own rules for what the cameras collect and who sees it.

**The decision that matters most is who operates the plate readers.**

| | Operated by NJIT Parking Services | Operated by NJIT Public Safety (police) |
| --- | --- | --- |
| Governing rule | NJIT policy, FERPA, general privacy law | NJ Attorney General Directive 2022-12 |
| Allowed purpose | Parking management | Law-enforcement purposes only |
| Retention | Whatever NJIT policy sets — we propose hours to days | Three years, fixed |
| Data sharing | Stays at NJIT | Must be made available to the statewide police plate-data system |
| Oversight | NJIT | Annual audit, trained and designated users, state coordinator |

**Our design choice: Parking Services operates it as a parking system.** That keeps retention short and the data on campus. Public Safety receives specific alerts under a written agreement instead of owning the database. This is the single most important privacy decision in the project and worth one line in the video.

## New Jersey

### Attorney General Directive 2022-12 (plate readers)

Issued October 21, 2022, replacing the 2010 rules. Read directly from the directive:

- **Who it binds:** "all law enforcement and prosecuting agencies operating under the authority of the laws of the State of New Jersey." NJIT Public Safety is a sworn police department, so it would be bound if it ran the readers — **confirm with NJIT**.
- **Purpose:** a plate reader and its data "shall only be used for official and legitimate law enforcement purposes."
- **What may be scanned:** only plates "exposed to public view," which includes a place the public has access to such as a parking lot.
- **Retention:** records and plate data "shall be retained for three years," then purged unless tied to an active investigation. The 2022 update cut this from five years.
- **Statewide sharing:** every police plate reader must make its data available to a statewide interface within 45 days of deployment.
- **Storage:** stored securely, access limited to authorized users, and the data "shall be the property of the agency and not any ALPR vendor."
- **Access logs:** an automated record of every access — who, when, and the justification.
- **Audit and training:** an annual audit by January 31; users must be trained and designated before they get access.
- **Private operators:** "Private entities may provide ALPR data to New Jersey agencies but cannot receive law enforcement-owned ALPR data." Commercially obtained plate data must not be mixed with police data.
- **Public records:** stored police plate data is treated as a criminal investigatory record and is not released without a subpoena or court order.

Even though we plan to stay outside this directive, we copy its good ideas: access logs, designated trained users, annual audit, NJIT owns the data and not the vendor.

### Pending bill A5637

Introduced October 15, 2026; not law. It would require police to delete plate data within 90 days and require a warrant for some searches. It shows which way New Jersey is heading — shorter retention — and supports our choice of very short retention.

### New Jersey Data Privacy Act

In effect since January 2025. It gives residents rights over their personal data and requires notice, data minimization and a risk assessment for sensitive processing. Whether it covers a public university is **unclear**: legal summaries disagree, and state agencies are generally exempt. We treat its principles as the standard to meet either way. **Ask General Counsel.**

### Other New Jersey rules

- **Breach notification (N.J.S.A. 56:8-161 and following).** Businesses and public entities must notify residents when personal information is breached. A plate number by itself is, as far as we can tell, not in the statute's definition of personal information — but a plate linked to a name and student record should be protected as if it were. **Verify the definition.**
- **Open Public Records Act.** NJIT is a public institution, so its records can be requested. Parking data held by Parking Services is not automatically exempt the way police plate data is. Short retention is the best protection: data that has been deleted cannot be requested or leaked. **Ask General Counsel which exemptions apply.**
- **Audio recording.** New Jersey's wiretap law restricts recording conversations. The cameras record video only — no microphones.

## Federal

- **FERPA (20 U.S.C. § 1232g; 34 CFR Part 99).** A record that links a plate to an identifiable student and is kept by the university is likely an education record. It cannot be disclosed outside NJIT without consent or a listed exception. Records created by a campus law-enforcement unit for a law-enforcement purpose are treated differently (34 CFR 99.8) — another reason to keep the parking system and the police system separate.
- **Driver's Privacy Protection Act (18 U.S.C. § 2721).** Restricts getting an owner's identity from motor-vehicle records. Our system **never looks a plate up at the Motor Vehicle Commission.** It only matches against plates that drivers registered with NJIT themselves. An unknown plate stays an unknown plate.
- **Camera supply-chain ban (Section 889 of the 2019 defense act; 2 CFR 200.216).** Recipients of federal grants may not buy or use video-surveillance equipment from Hikvision, Dahua, Hytera, Huawei or ZTE. NJIT receives federal research funding, so every camera in the system has to be from a compliant maker. Several of the cheapest cameras on the market are on the banned list — this affects the budget.
- **Fourth Amendment.** A plate in public view has no privacy protection on its own, but courts have grown wary of long-term location tracking built from many data points (*Carpenter v. United States*, 2018). Short retention keeps us far from that line.
- **Americans with Disabilities Act.** Accessible spaces must stay available. The system can show open accessible spaces and flag misuse — a benefit to feature.

## What NJIT would need to write

1. **A published parking-camera policy:** purpose, what is collected, retention, who has access, how to complain.
2. **Signs** at every entrance: "License plates are read for parking management."
3. **Notice and agreement at permit registration** — the driver registers the plate and is told how it is used.
4. **A written agreement between Parking Services and Public Safety** on exactly which alerts are passed on and when.
5. **Vendor contract terms:** NJIT owns the data; the vendor may not sell or reuse it; deletion on contract end.
6. **An option for people who object** — for example keeping a hang tag and being let in by the gate officer, as happens today.

## Our privacy rules in plain words

These are the commitments to state in the pitch.

| Rule | Detail |
| --- | --- |
| Parking only | Not used for immigration, protest monitoring, or tracking any individual's movements |
| No faces | Space cameras see cars, not people; any faces in frame are blurred at the edge before anything is stored |
| No state lookups | Plates are matched only against NJIT's own permit list |
| Plates are tokenized | The raw plate is replaced by a keyed code at the camera site; the database never holds readable plates |
| Short retention | Permit-holder reads deleted when the car leaves; unmatched reads after 30 days at most; occupancy counts kept because they contain no personal data |
| Humans decide | No automatic ticket or police dispatch from a camera read alone |
| Everything is logged | Every lookup records who, when and why; audited yearly |

## To confirm with NJIT

- Whether Public Safety is bound by the directive in the way we assume, and whether it already runs plate readers.
- Whether the New Jersey Data Privacy Act and the Open Public Records Act apply, and how.
- NJIT's existing camera and data-retention policies.

## Sources

- [NJ Attorney General Directive 2022-12 (PDF)](https://www.nj.gov/oag/dcj/agguide/directives/ag-Directive-2022-12_Updated-Directive-Regulating-Use-of-Automated-License-Plate-Recognition-(ALPR)-Technology.pdf)
- [NJ Assembly Bill A5637, as introduced](https://pub.njleg.gov/bills/2026/A6000/5637_I1.HTM)
- [Orrick: New Jersey Data Privacy Act — what companies should know](https://www.orrick.com/en/Insights/2024/03/New-Jersey-Data-Privacy-Act-What-Companies-Should-Know-About-the-States-New-Consumer-Privacy-Law)
- [Ogletree: New Jersey Data Protection Act becomes effective in January 2025](https://ogletree.com/insights-resources/blog-posts/new-jersey-joins-data-privacy-party-new-jersey-data-protection-act-becomes-effective-in-january-2025/)
- [2 CFR 200.216 (Cornell Legal Information Institute)](https://www.law.cornell.edu/cfr/text/2/200.216)
- [Boston University: Section 889 compliance](https://www.bu.edu/research/?p=45547)
