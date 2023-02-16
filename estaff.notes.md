---
id: 2fkjhg14th0apa5hxe64e3j
title: Notes
desc: ""
updated: 1676575031174
created: 1673230030238
---

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
