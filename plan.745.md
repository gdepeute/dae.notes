---
id: loepebq4pgpjtj07zhc3dcc
title: "745"
desc: ""
updated: 1673054448177
created: 1673052203319
---

# Discussion of Readiness for 7.4 Release

As I now understand it, there will be a single BigRed infrastructure which will support Tenefit DAE tiers in addition to PDC tiers. This I believe the first time where Tenefit owns and supports a key piece of infrastructure leveraged by all tiers. This represents a significant change in terms of responsibilities and support.

In the current world, the data generally flows from PDC as the source, down to the tiers (be it map services, databases, queues, ...). We (DAE) are primarily a "client" to these services. Thus the support process and chain is very well understood. If we (or PDC) discover an issue, tickets get filed in Asana on the PDC side, and PDC has a process to stay on top of those tickets and responsd to them 24x7. This will be the first instance where we will be hosting (and paying for) key infrastructure where PDC tiers would be a "client".

It's one thing if this infrastructure impacts our customers, it's a very different issue in my mind if this infrastructure impacts PDC's customers, which I view are more mission critical that our customers.

This raises several questions which I'd like to discuss when we meet.

## Questions / Plans / Actions

### Performance / Scalability

- Does it make sense to have a single MSK infrastructure for PDC and Tenefit?
- Would it not make sense to run separate MSK infrastructure at least initially until the new system is characterized?
- How do we make sure PDC doesn't impact Tenefit and visa versa (in use cases where PDC or Tenefit is pushing data into/out of the brokers)?
- Does the same situation exist with any of the processors of MSK data (processing load from PDC or Tenefit impacting the other)?

### Support Plans

- Is there a current support plan?
  - What does PDC do if they detect an issue?
  - How do they contact us?
  - 24x7? We don't have 24x7 coverage.
  - Who answers the call/email?
- Is the reliability/availability of the MSK cluster mission critical?
  - If there is an issue will PDC expect 24x7 engineer/operations to resolve?
- Will (initial) front line of support be Development?
- What's the plan to convey knowledge about the system to Operations and Support for them to asssume front line support?

### Configuration / Sizing

- What is the specification or requirements for the production cluster?
- How were the specification/requirements determined? Quantitatively using calculator?
  - Include retention requirements (to determine size and log rotation parameters)
- How are we estimating Tenefit load vs PDC load?
- How are we estimating going forward needs? How much buffer should we build in now?
- Given recent disk space issue surprise, how do we make sure this doesn't impact us again?
- What set of AZ's will this cluster be deployed in?
- Are all processors available in multi-AZ's?
- Do all (or ones where load might be variable) processors support auto-scaling?

### Logging / Monitoring

- What logging/monitoring is still to be implemented on EXISTING infrastructure (specifics)?
- What logging/monitoring is still to be implemented on NEW infrastructure (new services/containers/code - specifics)?
- Is something breaks, what is the process to debug/resolve?

### Others?

- What are you guys concerned about?
-
