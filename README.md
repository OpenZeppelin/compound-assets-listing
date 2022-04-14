# Compound Asset Listing - Overview

As part of OpenZeppelin's security partnership with Compound, we reviewed past asset listing proposals and went through past community discussions around the topic. We also explored solutions on other protocols to create defined processes for asset listings that address Compound's security risks. 

The output of this effort is presented below with a comprehensive checklist for checking security risks and a step-by-step process for an asset listing proposal to follow.

## Quick Usage Guide

1. Read the [Process](Process.md) Guide to learn how an Asset Listing should be handled securely from start to end.
2. Use the [Checklist](Checklist.md) as a required information list to share with the community as the first step in the Asset Listing Process.
3. Review the [Risks](Risks.md) to better understand the motivations behind our Checklist, Process and the potential integration issues that could arise.

## Background

Our goal was to establish an initial process that the community should follow for securely listing assets. We intend for the community to review this work and propose improvements. We left our suggestions for future improvements at the end of this document.

We initially wanted to list all the main exploration results and summarize the Compound protocol's known risks. We created a [Risks](Risks.md) document that explore all possible risks that users should consider when using Compound, with a focus on risks related to the interaction with external assets. This document is meant to be a list of things that anyone evaluating a new asset listing must remember and consider. For each risk category, we give a little explanation or reference to explain how the risk is studied and possibly mitigated by the current design.

After the analysis of risks, we identified all of an asset's specific risks that need to be considered in a listing. For this reason we built a [Checklist](Checklist.md) of questions and information requests to be performed during the asset listing process. This list tries to address all the concerns around each specific asset and the related integration. Whoever is going to propose an asset listing must first review this checklist and provide the information requested for a community check on different potential integration issues.

Finally, we drafted a [Process](Process.md) to follow that includes reviewing the [Risks](Risks.md), going through the [Checklist](Checklist.md), and other intermediate steps.

With this, our intention is to establish a structured process for secure asset listing, which is adaptable to community feedback and improvements over time.

## Future improvements

- [ ] An automation that integrates with the forum and forces applicants to fill in a checklist's required fields to avoid bypassing important information.
- [ ] In the future, we hope that many of the checklist items can be auto-completed in a trustless way to reduce the friction of submitting a proposal to the forum by some on-chain tooling and/or scanners to retrieve information automatically.
- [ ] The checklist will be modified with new items as the community deems necessary. It can be through the same or similar mechanisms as GitHub's Pull Request.
- [ ] The tooling part can be improved. Scenario simulations would benefit from a standardization and enforcement of running them during listing process. A standard test scenario template would be an initial step.
- [ ] Create a scoring framework. For reference, look at [AAVE scoring mechanism](https://docs.aave.com/risk/asset-risk/methodology).
- [ ] In the process, we mentioned two WIPs (Work-In-Progress) items:
    - Auditing new listings.
    - Running asset specific market risk analysis.
    We left them as they are because is up to the community to include them in the process as it requires actions from external parties. It would be good to explore the possibility to include audits and market risk analysis over specific asset listing.
