# Introduction

During latest round of OpenZeppelin engagement with Compound, we reviewed past asset listing proposals and went through some important past community discussions around the topic. Further exploration has been done accross some other protocols to take inspirations by established processes to list a new asset. 

The output of this effort is presented below.

# Overview

Our goal was to establish a first version of the process that the community should follow when listing an asset in the most secure way. We aim the community to review this work and propose improvements and expansions to it. On our own, we left our suggestions for future improvements at the end of this document.

We initially wanted to list all the main exploration results and summarize Compound protocol known risks. We created a [Risks](Risks.md) document that explore all possible risks that users are faced to when using a lending protocol in general, Compound specifically, with a focus on risks related to the interaction with external assets. This document is meant to be a list of things that anyone evaluating a new asset listing must always remember and keep into consideration. Moreover, for each risk category a little explanation or reference to how the risk is studied and possibly mitigated by the current design is left.

After the analysis of risks, we identified that among all, asset's specific risks were not addressed specifically. For this reason we built a [Checklist](Checklist.md) of questions and information requests to be performed during the asset listing process. This list tries to address all the concerns around each specific asset and the related integration. Whoever is going to propose an asset listing must be reviewing this checklist and provide the information requested for a community check on different potential integration issues.

Finally we drafted a [Process](Process.md) to follow, that includes reviewing the [Risks](Risks.md), go through the [Checklist](Checklist.md) and many more intermediate steps.

With this, our intention is to establish a structured process for secure asset listing, which is adaptable to community feedback and that need to improve over time making the final experience easier and robust.

# Future improvements

- [ ] An implementation that integrates with the forum and enforces applicants to fill in checklist's required fields to avoid bypass of important information.
- [ ] In the future, we hope that many of the checklist items can be auto-completed in a trustless way to reduce the friction of submitting a proposal to the forum by some on-chain tooling and/or scanners to retrieve information automatically.
- [ ] The checklist will be modified with new items as the community deems necessary. It can be through the same or similar mechanisms as GitHub's Pull Request.
- [ ] The tooling part can be improved. Scenario simulations would benefit from a standardization and enforcement of running them during listing process. A standard test scenario template would be an initial step.
- [ ] Create a scoring framework. For reference, look at [AAVE scoring mechanism](https://docs.aave.com/risk/asset-risk/methodology).
- [ ] In the process, we mentioned two WIPs (Work-In-Progress) items:
    - Auditing new listings.
    - Running asset specific market risk analysis.
    We left them as they are because is up to the community to include them in the process as it requires actions from external parties. It would be good to explore the possibility to include audits and market risk analysis over specific asset listing.
