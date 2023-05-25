---
id: 2fkjhg14th0apa5hxe64e3j
title: Notes
desc: ""
updated: 1685047275557
created: 1673230030238
---

# Bob/Johnny Discussion 5/25/23

- 140k payroll with benefits
- May 31 payroll is 85k with May deferred payroll for ALL
- Bob says he's unable to hand out stock until "someone outside the company" sets the price, at which point he would offer common options to employees with vest
  - Claims there would be acceleration on change of control
  - Bob's owns all his shares, so not restricted
  - Believe Bob is owning and not vesting his stock
- Deferred comp is "top of the list" according to Bob
- Ryan is NOT on the balance sheet, no formal agreement in place
  - We are not paying him anything at the moment, and don't plan to until we get out of this mess
- Only thing on the balance sheet is Bob's loans and deferred comp
  - Does this include Arnaldo after he leaves?

# EStaff 5/22/23

- Marsh/Wyman - lot of Q&A back and forth
- Arnaldo hand off is consuming most of time
- Spam attack yesterday consumed a couple hours to knock it down

  - Will take a few more hours today to unwind our changes

- Last hope is John Hessessey on Wednesday
  - Hyper local?
- Marsh doing markup on the SOW, expected to get it last Friday
- Crisis24 was meant to respond on Friday, but didn't
- MapFre decided to push all deals into Q3
- Trying to bring Shell growth of $35k into this quarter
- ADP Total Source recommended us to Run, and they are not responding to us
  - Sorting out timelines internally
  - Manual check for this payroll
  - Benefits run out at the end of the month (May 31)
  - Natalie reached out to old broker, from years ago which and talking to her today at 3pm
- Meeting with Ray on Friday
  - UI visualization project - as Michelle says, no revenue
  - Johnny working on potential projects, will send to Bob/myself when done
  - IAEA phase 2 completed
- Johnny met with Kaushik last week
  - Presented to them a proposal for Extreeme Temperature events
- Aranldo worked on the Meta 3rd party questionaire
  - Incorporated my feedback
- Shell process started on 3/21, initially responded on 4/1
  - Name change, new TAX ID, PayPlant
  - PayPlant info forward to Shell on Friday
- Trying to get AllScripts PO by 6/30 on special 1-time deal
  - Proposed $150k for perpetual (could run $120k thru PayPlant)
- Will bill PDC services last day of May, will get paid on 6/15ish
- Bob's got 2 other investors at 50% at best
  - JohnH will potentially recommend some other VCs and/or Google

# EStaff 4/24/23

- API prototype, working on basic documentation so we can enable Crisis24 as soon as $ come in
- Experimented with streaming hazards using SSE, works, could add to API in future release
- OliverWyman check in tomorrow, they've hit API 2200 times since 4/13
- USVP meeting with Steve/Matt
- Created map service for Joseph Spain at MB Cars
- Created map services for Jeff Dean/Databricks
- USVP feedback into doc for Bob
- Pinged Ray/Cassie regarding Crisis24 request for structured location information

  - Taken under advisement, might not be trivial but straightforward?

- Questions
  - Rory update?
  - Payroll?
  - Any update on Aravo?
  - Pipeline < $50k new business, Shell at $35k, maybe another $100k other

# EStaff 4/17/23

- API prototype, nearing completion for Crisis24 use case, but designed for flexibility
- Call with Rory/Scale last Wednesday
- Crisis24 SOW/support

  - Had meeting with Chad last week regarding pricing
  - Zach question regarding reverse geocoding for Country/Region/State
  - Told him we don't include that in our dataset, but sent him python sample code using ArcGIS reverse geocoder.
  - Asked him that if it was a drop dead not having that, to let us know

- Discovered a couple of Enterprise configuration issues
  - Worked with Cassie/Steve to resolve
- Aravo pinged about "other customers" and accessing the old API
  - Who are these customers? Thought CocaCola was the only customer?
- Questions

  - Current payroll situation
  - India payment
  - USVP next steps - where is Cabo Matt?
  - Any contact from Shell?
  - Any update re: IQgeo?
  - Any update OliverW?
  - CSL/Behring starting to poke at API

- Updates

  - Bob says we got the $60k from PayPlan
  - Bob asked about invoicing PDC, says we can invoice, says it would be 15 days I suspect
  - Bob suggests Steve/USVP is in, but Matt its unclear
  - Matt's concern "will we scale"
    - Asked "Why did Interos drop out?"
    - Asked "Why did Citrix drop out?"
  - Current Q2 outlook < $100k FFS

- Sales Update from Keith
  - Hearing lots of budget issues?
  - 7,8 prospects "love" the poroduct, but have no budget
  - Good momemntun in the insurance game
  - "Struggle", "grind"...
  - Campiagn to go after 5-7 prospects/week
  - Had not thought about airlines
  - $60k current Q2
    git pus

# EStaff 4/10/23

- API prototyping
  - Answered majority of questions
  - Worked thru a set of lambda issues last week
- Crisis24 SOW
- Call with Crisis24/Palantir on Friday
  - Answered questions about data
  - Learned a bit about the Topo1 project
- OliverWyman support
  - Created API specific account for them, and re-enabled for this POC work
- API reports improvements
  - New lambda custom authorizer will dramatically improve the reliability of these reports
  - Current API gateway logs missing critical information (due to truncation of 1024 bytes) to tie all the transactions together
- Spending more time in Elastic to evolve our ability to detect and alert on issues

- Updates:

  - Bob, next payroll front, still fighting with PayPlan on second installment
  - Must put the payroll in tomorrow as we are in the penalty box with ADP
  - Call with PayPlan guys this morning, gave them access to accounts and Meta portal
  - USVP wants to meet to discuss how we can scale up quickly
    - Meeting at USVP on Thursday at noon
  - Bob reading "The Wisdom of the Bull Frog" - recommending
  - Move occuring on Friday from current location over to TechMart

- Arnaldo
  - Meta 7.4.5 plan on 4/20
  - Enterprise 7.4.5 on 4/27

# EStaff 4/3/23

- API prototyping

  - Historical Hazards
  - Layers
  - Prototyping complete
  - Email sent seeking approval to set up
  - Can implement in 1-2 weeks
  - Should get $ from Crisis24/Palantir
  - YES, can webhook publish to their endpoint very easily

- Push to invoice Ray for the $90k which supposedly could get paid quickly

- Q&A
  - USVP and new partner approval
  - Factoring company and delays
  - Bob still on 4/30 as drop dead date for $
  - Scale Ventures - Bob contact starting discussions with
  - Where did we end up on the quarter?
    - ONE new logo, Databricks came in on Friday
    - Q1 end at 18k + 22k (Databricks and ???) + 250k MSA with PDC

# EStaff 3/27/23

- Mostly resolved the retry failures between the hazard producer and API gateway
  - Was due to API gateway timing out the long connection AND
  - That Camel wasn't setup/configured properly for reusing connections and checking status of connections before using
- Crisis24/Palantir
  - Been supporting their efforts and trying to get to the bottom of their requests
  - Fundamentally it's access to the historical hazards which we can add to the existing API gateway with new role
  - And a set of layers which we need to proxy (investigating MapProxy and others), fronted by NGINX behind the API gateway with yet another new role type. Have ask Michelle to think about granularity of roles (groups of layers?) so we can be determine how to implement
- Cleaned up some oganizations
  - OW/Marsh
  - MapFre
  - Sitecore
  - USGLC
- Improvements to GIS tools done last week in service to CSL Behring

  - Improved geocoding
  - Native support for symbol icons (saves a manual step)
  - Will be transitioning map service creation over to Jesse

- Q&A
  - Other VC's we were having discussions with
  - Runway left before $ needed, and plan
  - Space/bldg?
  - Lead generation efforts / any quantification?

# EStaff 3/20/23

- Root cause investigation on HTTP POST SSL failures to API gateway
- Support of Vik from Crisis24 getting access to data
  - Jesse hack/whack is not helping
  - Have active hazards coming in now
  - They WANT:
    - Historical hazards - need to decide how we want to handle and when
    - Population density
    - Forecasts
    - Airports and airport density info
    - US embassies
    - Hospitals
    - Ports
- Expired Organizations
  - Meta
  - OliverWyman
  - Marsh
  - Random GMail dude
- Code refactoring
  - GIS tool mostly complete, awaiting Jesse validation, then plan to migrate map service creation over to him
- USVP update?
- Second VC update?
- Meta factoring?

- Factoring in place, can turn around in 24 hours
  - Whenever we get the Meta PO with proper language, should get $100k
- USVP
  - Met with Steve on Tuesday, was supposed to hear from him Friday, crickets
  - Bob will give him another day then will begin pushing

# EStaff 2/21/23

- Sick
- Expired accounts:
  - Facebook - 2/20
  - IQGeo (TRIAL) - 2/20
  - ControlRisks (TRIAL) - 2/17
  - Transre (TRIAL) - 2/17
- API reports refactoring
- Users report added "roles"
- Configuration report refactoring
- Arnaldo/Bills - upcoming
  - GMail could get suspended tomorrow
  - Others
- Removed LOGIN role for Apple Maps
- Worked with Jesse on his license tool

- Updates
  - AllScripts paid in full vs the reduced 10%
  - Will purchase D&O insurance
  - Catch up back pay in next payroll (not execs)
  - Full pay for everyone in next paycheck
    - Executive backpay will occur over 6 weeks
  - Give Meta PO to PayPlan

# EStaff 2/13/23

- Cleaned up database

  - Significant cleanup of users, orgs
  - Working to remove ruser16/ruser accounts
  - Licenses match all current deals
  - Tools in place to alert on violation of licenses

- Fix to registration to create new orgs as Trial

  - Still have an issue if the user waits too long to click the link after token expires.
  - Updating trial and forgot password links to 60 mins (from 10)
  - Need to investigate capturing 403 from webhook on website

- Palatir/Crisis24 meeting Friday
- IQGeo meeting Monday - Johnny rocked it
- Current status of Natalie?

- Bob stated that he did not know if this paycheck would be partial or full that we are meant to receive Wednesday. He said the call with Steve Krauz at USVP today will help determine that
- Ryan apparently won't finance the AllScripts receivables until he hears positive progress re: USVP.
- Pipeline has several delays in it, Q1 looks VERY light.

- 2/16 Update
  - AllScripts agreed to wire money by next Wednesday for 10% discount vs trying to go thru factoring process and paperwork to save an extra $15k
  - Meta license expires in 4 days but have 60 day payables which means we are floating them 2 months on expired license before getting paid
  - Going to push the Meta PO thru the factoring process which would get us 80% of the $ soon, costing us $3-5k
  - Bob going to discuss with Natalie (tomorrow) returning payroll to full and what happens with deferred

# EStaff 2/6/23

- IQGeo demo meeting later today
- Apple discussion
- Palantir discussion
- _Bad News_: AllScripts receivable not coming until mid-April, he said he never committed to beginning of February
- Natalie not with us, again...fear she is going to leave
- USVP
  - Wanted more due-dilengence names from us
  - Gave him Kaushik and Jeff Dean
  - Worried about Kaushik as he could say they get most of their stuff from NC24

# EStaff 1/30/23

- Lots of blabbering regarding the 49ers horrific loss
- Bob awaiting for closing documents from Ravix
- Bob just funded the payroll
  - "Goal" is this is the last payroll we will have reduced salaries
  - Expectation is the AllScripts receivables will cover next one and one after until USVP closes (assuming it does)
- Bob still working on stock options thoughts, awaiting to hear USVP say they want 40%
- Bob suggests sending a note to company tomorrow morning

- Pipeline

  - Victoria Secret - trial (move away from EB)
  - Woven Planet - trial Q1
  - Intuitive Surgical
  - IQGeo
  - Epic (RAVE) - Trial
  - Duty Free (RAVE) - Trial
  - Tyson - Trial
  - Craft - Trial
  - AstraZeneca - Zscaler proxy issue

- PDC Data Architecture

  - Some demos with Ray - need to get invited/involved in those

- Now looking at mid-market companies
- ABC process requires cancelling all leases
  - San Jose will attempt to be renegotiated post ABC
  - Johnny's Lahaina office lease is cancelled - Johnny needs it...

# EStaff 1/23/23

- Ravix playing hardball, wants to wait until Monday to "potentially" accept our offer
- Bob suggesting the withdraw the offer, and if Ray is in agreement using their license to our IP, to partner with PDC WITHOUT the Tenefit assets altogether
  - What does that mean regarding legacy products which PDC does NOT have license to

# EStaff 1/16/23

- Other bidders in ABC process:

  - OnSolve
  - AlertMedia
  - TIBCO
  - We are putting our bid in on Wednesday - we are putting 48 hour clock on our bid

- 13 terminated, Natalie still employed by Tenefit for a few more days
- Offer letters sent last night around 8:30pm
- Sign and send back to Natalie personal email

- Moving forward with USVP

  - On the phone with Steve yesterday with Bob/Michelle
  - Bob/Michelle working on the pitch for Thursday
  - Johnny performing demo

- IQgeo Meeting tomorrow - no invite

  - Castrel - Mohsen - company owns 26% of IQgeo

- Payable status

  - Tail insurance
  - Amazon we owe $11k
  - Credit card $700 left

- A/R
  - AXA $43k - 1/17
  - Quotech $12k - 1/20 (expected tomorrow)
  - Enerflex $14k - 1/23

# EStaff 1/12/23

- Russell @ Daimler

  - Adam responded to me yesterday, DID find configuration issue, since fixed, should no longer see time skew

- Live Updates
  - Negus brothers backed out at the last minute

# EStaff 1/9/23

- Russell @ Daimler

  - Clock skew issue, generating lots of analytic messages
  - Ping Adam on their side, he suggested Russell's skew was only 40 seconds
  - Had Thomas improve the analytic to only produce if > 1:45 and to include time of skew
  - Will clean up #dae-users-errors

- Patch 7.3.14-442

  - Patch completed on Sunday by Thomas, to be deployed by Arnaldo (when?)

- IQgeo call

  - We saw Matt's demo
  - Offered to produce latest data for his meeting with higher ups
  - He said he would let me know

- Shell call

  - Bit of a dud
  - No one showed up, all actions still in their court
  - Frustrating...

- Review of 7.4 and readiness happening this afternoon

- Live Updates

  - ABC process - received shareholder and board approacl
  - Assign all assets to assignee - we give list of 10 companies to sell the comapny to
  - We are putting in a bid as the management organization (assume SQN debt $4M, 200k promisory note paid back in a year)
    - Hence our offer is effectively $4.2M
    - Any other competitive offer would need to exceed the $4.2M to even be considered
  - Have money for next payroll, but not the one at the end of the month
  - Who are the other 10 companies
  - Will pay Tenefit payroll this week as scheduled the employees out of Tenefit, NewCo would pay the estaff
  - Will need new employment contracts with NewCo
  - 50% ownership NewCo, 50% Dana - new stock issued equally from NewCo/Dana
  - Ravix is the assignee we just paid $50k to in order to try and sell the company
  - PDC license may NOT go with one of the other companies
  - Moshen helping to get the deal with IQgeo completed into NewCo
  - Payroll for Tenefit will be a bridge loan to NewCo
  - "Believes" he has funding committed for NewCo, but should know before payroll date
  - Trying to get IQgeo to invest in NewCo at up to $1M
  - Potential deal with USVP, asking for customer references, and talk to Ray
  - $200-300k receivables, not enough to cover ALL payroll
  - $230k AllScripts receivable by 2/6.
  - $70k receivables coming in between 15th an 21st.
  - Asking EStaff to delay payroll by one week so we can get commitment, unclear how 1 week commitment can be made as the $ to cover it isn't there
  - Complete the PDC license AFTER the ABC is complete

  - Friday meeting with Ray - took him thru the investor deck
  - Discussed the ABC process, claims he was knodding/smiling - perhaps this is simply getting Dana out of our hair
