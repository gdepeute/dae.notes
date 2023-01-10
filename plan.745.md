---
id: loepebq4pgpjtj07zhc3dcc
title: "745"
desc: ""
updated: 1673303808255
created: 1673052203319
---

# Summary from 1/9/23 Meeting with Johnny/Arnaldo

- No one is clear on our support SLA with customers and/or PDC
  - Ping'ed Natalie for details
- Unclear if the production MSK is multi-AZ and implementing all best practices
  - Ask Arnaldo to go be confident it's set up correctly in his own mind
  - No need to work thru recovery scenarios (yet) if we are running on hardware/disks in multiple different physical locations
    Next busines
- Arnaldo will be first line of contact, and will put together in the next couple weeks a playbook for Jesse and the India team as to what to watch for, what to do when a support email comes in, and when to call.
  - Arnaldo will then pull in the development team as required
- IAEA is in production now, production MSK and services
- Development owns the deployment responsibility for Test and should be Arnaldo for Production
  - From now on, IAEA production deployments will be done by Arnaldo
- Need single source of truth for BOM for release, and don't want to implement the separate spreadsheet process PDC does
- Johnny claims multiple consumer/producers on single topic has been tested and works
- Claim is scale testing (using my Neijing Taxis) has been done on TestEnterprise

# Discussion of Readiness for 7.4 Release

As I now understand it, there will be a single BigRed infrastructure which will support all production Tenefit DAE tiers in addition to all production PDC tiers. This I believe the first time where Tenefit owns and supports a key piece of infrastructure/data leveraged by all tiers. This represents a significant change in terms of responsibilities and support.

In the current world, the data generally flows from PDC as the source, down to the tiers (be it map services, databases, queues, ...). We (DAE) are primarily a "client" to these services. Thus the support process and chain is very well understood. If we (or PDC) discover an issue, tickets get raised/filed in Asana on the PDC side, and PDC has a process to stay on top of those tickets and respond to them 24x7. This will be the first instance where we will be hosting (and paying for) key infrastructure where PDC tiers would be a "client".

It's one thing if this infrastructure impacts our customers, it's a very different issue in my mind if this infrastructure impacts PDC's customers, which I view are more mission critical that our customers.

This raises several questions which I'd like to discuss when we meet.

## Questions / Plans / Actions

### Performance / Scalability

- Does it make sense to have a single MSK infrastructure for PDC and Tenefit?
- Would it not make sense to run separate MSK infrastructure at least initially until the new system is characterized?
- This represents a single point of failure for ALL running tiers, does it not? Does this make sense as the first step to deploy new infrastructure?
- How do we make sure PDC doesn't impact Tenefit and visa versa (in use cases where PDC or Tenefit is pushing data into/out of the brokers)?
- Does the same situation exist with any of the processors of MSK data (processing load from PDC or Tenefit impacting the other)?

### Support Plans

- Is there support plan?
  - What does PDC do if they detect an issue?
  - How do they contact us?
  - 24x7? We don't have 24x7 coverage.
  - Who answers the call/email?
  - Have there been any discussions regarding support with PDC?
- Is the reliability/availability of the MSK cluster mission critical?
  - If there is an issue will PDC expect 24x7 engineer/operations to resolve?
- Will (initial) front line of support be Development?
- What's the plan to convey knowledge about the system to Operations and Support for them to assume front line support?
- Does PDC have any new support they are responsible for in 7.4?

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
- Should we be pushing all MSK transactions to S3 (at least initially) to have complete transaction backup for disaster recovery?

### Logging / Monitoring

- What logging/monitoring is still to be implemented on EXISTING infrastructure (specifics)?
- What logging/monitoring is still to be implemented on NEW infrastructure (new services/containers/code - specifics)?
- Is something breaks, what is the process to debug/resolve?
- Should there be separate monitors/tools watching/observing the topic to proactively detect

### Others?

- What are you guys concerned about?
- What kinds of problems might we expect, and do we have sufficient logging/monitoring/alerting to quickly detect and resolve?
- Given issues seen during development, do you feel adequately prepared for this infrastructure to go into mission critical production in the coming weeks?
- Where did the PDC deploying 7.4 date/commitment come from? Given Tenefit is responsible for that infrastructure, don't we have a say as to readiness?
- Is there a forcing function for PDC wanting/needing to go to 7.4 in a couple weeks?
- Is there a TestRapids or TestEMOPS tier running 7.4 and using the existing Test infrastructure?
- Have we done any load/scale testing?
- What did I not ask?
