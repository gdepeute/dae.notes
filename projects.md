---
id: lx1llxfx48r3hw1vambrxbe
title: Projects
desc: ""
updated: 1682010779137
created: 1666285014870
---

# Roadmap Proposal - All - 4/20/2023

## Projects

- Improved Data Architecture (2-3 man months)
  - goals: new streaming/pipelined based architecture
  - yields: performance improvments, simplifies new feature creation, ultimate cost savings
- Infrastructure moderinzation (2 man months)
  - goals: retire legacy monolithic services, re-implement within the new data architecture and streaming services
  - yeilds: cost savings, reduce complexity, brings more services into common framework/design
- DAE 7.5 (2 man months)
  - goals: improved onboarding flow for customers, dramatically simplifies initial setup/configuration
  - yields: better customer onboarding experience
- DAE 7.6 (2-3 man months)
  - goals: WMS feature improvements, layer monitoring improvements, ...
  - yields: more robust and stable end user experience
- IAEA Phase 2 - Custom Reports (2 man months)
  - goals: custom reports for IAEA, leveraged/customized for customers like Mercedes Benz and others, adds Air Quality to Wildfire Repors
  - yields: much improved and more informational wildfire reports
- IAEA Phase 3 - Custom Reports (2 man months)
  - goals: adds floods, volcanic eruptions, ...
  - yields: additional custom reports which can be upsold to customers
- DASv4 for DA (1 man month)
  - goals: migrate last holdout to new notifications system
  - yields: cost savings, unified notifications across all installations
- Organizations Improvement (1-2 man months)
  - goals: improve organizations component to make it easier to manage/add/change users, ultimately end user admin facing
  - yields: reduces current support burden, paves the way for large customer installations to be self-service
- Private Instance improvements (2 man months)
  - goals: streamline and optimize private instance deployment flow, dramatically reduce time, brings deployment time down to hours from days
  - yields: dramtic speedup to on-boarding, will enable more customized trials when we can bring up/down the private instances quickly
- API improvements (2 man months)
  - goals: add historical hazards data, and layers data to the DaaS API
  - yields: more data to sell, thus more ARR
- Asset Summary Reports (3 man months)
  - goals: extend existing asset centric notification system to provide report summaries of all assets impacted by a hazard
  - yields: for customers with large number of assets, provides a better summarized view
- Travel Tracker integration (1-2 man months)
  - goals: bring dynamic assets (travelling employees) into asset centric notification system, initially built for Citrix
  - yields: another integration of dynamic asset data to the completed integrations
- Asset Management Solution (3-6 man months)
  - goals: end user asset manangement solutions, allows ease of use creation of asset groups, relationships, notification preferences, reporting...
  - yields: allows customer to self-service/manage their assets
- Web Hook Notification Support (1 man month)
  - goals: allows integration of notifications (hazard specific and/or asset/hazard specific) into other systems which support webhooks.
  - yields: as many systems support incoming data via webhooks, this opens up many more integrations
- Streaming Hazards API (1 man month)
  - goals: add streaming endpoint for active hazards to API as alternative to polling
  - yields: more efficient way to receive data, assures no data is missed/lost, and delivers data in real time
- Data Improvements (3-6 man months)
  - goals: continual improvments and addition of data to the existing hazards/incidents, addition of impact data, hazard evolution, better description/geometries leveraging ML models
  - yields: constantly improving data products
- Layer Improvements (3-6 man months)
  - goals: continual addition of high impact, useful layers to the system based on customer needs/requirements, create custom customer layers
  - yields: constantly improving data products
- Moogsoft Integration (1-2 man months)
  - goals: leverage work for Shell to produce a generic integration for Moogsoft customers
  - yields: another completed integration in the ITSM/ITOM space
- ServiceNow Integration (1-2 man months)
  - goals: leverage experience with KBR to produce a generic integration for ServiceNow customers
  - yields: another completed integration in the ITSM/ITOM space
- Investigate Integrations into Supply Chain Management Products
  - goals: investigate Oracle SCM, SAP Ariba, ...
  - yields: better combined solutions leveraging our extensive and over two decade of historical data
- Investigate Integrations into Insurance Products
  - goals: investigate LexisNexis Risk Solutions, RMS, AIR Worldwide, ...
  - yields: better combined solutions leveraging our extensive and over two decade of historical data

# Active 4/5/23

- Have myself and Jesse add additional user-agent information in the short term to disambiguate the requests

  - dae-asset-tracking-mdove - user agents: python-requests/2.28.1, python-requests/2.28.2, curl/7.85.0
  - disasteralertforkbrservicenow@kbr.com - user agents: Jakarta_Com, ServiceNow/1.0
  - ancaraballo@coca-cola.com - user agents: Apache-HttpClient/4.5.12\_(Ja
  - hazard-api-bot - user agents: Java/1.8.0_272
  - jselitham - user agents: python-requests/2.28.2, PostmanRuntime/7.31.3
  - trivikram.pathak@crisis24.com - user agents: python-requests/2.28.2, Python-urllib/3.10
  - disasterawareingestion@crisis24.com - user agents: curl/7.86.0, python-requests/2.28.1, python-requests/2.28.1_Fou
  - trivikam.pathak@crisis24.com - user agents: Python-urllib/3.10
  - maps-traffic-accounts@group.apple.com - user agents: okhttp/4.10.0
  - your_username - user agents: curl/7.84.0
  - henry.stroud@oliverwyman.com - user agents: curl/7.84.0

# Active/Completed Projects as of 3/16/23

## **Engineering**

Summary: Team led by Johnny (the man), includes Thomas (senior), Nick (junior), Izzy (junior)

- Johnny -> Hazard Data Processing / Asset Protection / Push Notifications
- Thomas -> DisasterAWARE MSA support / Asset Protection / Push Notifications
- Nick -> Pipeline of pipelines, DisasterAWARE MSA support / Migrating Aylien aka Magellan data feeds to new infrastructure
- Izzy -> IAEA Phase III / Asset Protection

### **Completed**

- DisasterAlert Mobile (nearing completion)
  - in testing now, previously paid for
- Asset Protection (nearing completion)
  - in active development, already paid for
  - to be deployed with 7.4
- IAEA Phase 2 (nearing completion)
  - development about to begin, next phase of hazards (Wildfire, Tsunami, Tornado)
  - leverage for Mercedes Benz Custom Reports for Wildfire
    - Still open as to how we address air quality request/requirement
  - 95% complete
- Infrastructure (nearing completion)
  - Building out BigRed architecture
  - Migrating more functionality in common code to provide better leverage between projects
  - Develop deployment framework and CDK's to ease transition to operations

### **Planned**

- Improved Data Architecture / Hazard Processing
  - Johnny leading the effort
  - working on Volcanos now
  - paid for from MSA agreement
  - 1 month full time, then part time after
- Infrastructure improvements
  - migrating Aylien and Magellan data to new architecture
  - additional pipeline modularization/improvements
  - 1 month
- DAE 7.5
  - includes: onboarding flow
  - ? months
- DAE 7.6
  - includes: WMS feature improvements, layer monitoring improvements, ..., bug fixes
  - ? months
- IAEA Phase 2 Customization for Mercedes Benz
  - still open as to how we address air quality request/requirement
  - 1-2 months
- IAEA Phase 3
  - planned for Floods, Volcanic Eruptions, others...
  - PDC planning/coordination to begin next week
  - PDC is dictating the schedule
- DAS v4
  - migrate DisasterAlert notifications to DAS v4
  - work started then put on hold
  - 1 month
- Organization improvement
  - add ability to change organizations of existing users in the system
  - will allow accurate tracking of licenses and seats used
  - 1 month?
- Support existing projects (ongoing)
  - Large number of projects being supported: - DisasterAWARE - Disaster Alert - Print Services - Media Services - Media Data Classifier - Organization Services - DAS v3 - DAS v4 - Asset Protection v1 - Asset Protection v2 - Disease API - Mass Notification (RAVE) - IAEA Report Generator - IAEA Admin Portal - Layer Monitoring - Layer Monitoring App - Hazard Impact Reports - Uploader - Facebook Hazard Filters - License Manager - Registration Services
  - new MSA will pay for some of this support
  - agreement still not executed, once executed we can invoice for Jan/Feb 2023

## **Operations**

Summary: Single resource (Arnaldo), supporting not only Enterprise, but supporting PDC efforts given unified on shared stack.

### **Completed**

- Testenterprise/Meta catchup deployments (done)
- Service Monitoring (ongoing)
  - approx 40% complete
- DAE 7.4 Planning/Deployment (nearing completion)
  - deployment of DAE Pro happening 3/14, additional PDC and DIQ tiers over coming weeks
- Operations debt
  - completed some AWS cleanup, Kaazing website overhaul (exploit), ...

### **Planned**

- Moving to new Office Space
  - 1-2 weeks
- DAE 7.4 remaining deployments
  - Meta by end of March
  - DAE by end of April
  - 1 week each
- Testenterprise Infrastructure - MSK (was previously deferred)
  - 1 week
- Service Monitoring (ongoing)
  - 3 months
- Improve Private Instance deployments
  - 2 months
- SFTP endpoint for Shell (assuming commitment)
  - 1 week
- Cost Allocation Tags
  - 2 weeks
- Important Operations Debt
  - 2 month
- Support/Documentation
  - 30% of cycles

---

# Active Projects as of 10/20/22

## Engineering

Summary: All Engineering Resources consumed well into Q123 on existing projects we've been or will be paid for. Team led by Johnny (the man), includes Thomas (senior), Nick (junior), Izzy (junior)

- DisasterAlert Mobile (mostly complete)
  - in testing now, previously paid for
- Asset Protection (active)
  - in active development, already paid for
  - development resources consumed into Q123
- IAEA Phase 2 (active)
  - development about to begin, next phase of hazards (Wildfire, Tsunami, Tornado)
  - development resources consumed into Q123
  - leverage for Mercedes Benz Custom Reports for Wildfire
    - Still open as to how we address air quality request/requirement
- Infrastructure (active)
  - Building out BigRed architecture
  - Migrating more functionality in common code to provide better leverage between projects
  - Develop deployment framework and CDK's to ease transition to operations
  - development part of other projects into Q123
- DAS v4
  - Migrate DisasterAlert notifications to DAS v4
  - 1 month, not started
- Support existing projects (active)
  - Current model with PDC is not working
  - They request some work, then suggest we just bill them for X hours
  - 1 full time engineer, usually interruptions
  - Large number of projects being supported: - DisasterAWARE - Disaster Alert - Print Services - Media Services - Media Data Classifier - Organization Services - DAS v3 - DAS v4 - Asset Protection v1 - Asset Protection v2 - Disease API - Mass Notification (RAVE) - IAEA Report Generator - IAEA Admin Portal - Layer Monitoring - Layer Monitoring App - Hazard Impact Reports - Uploader - Facebook Hazard Filters - License Manager - Registration Services

## Operations

Summary: Single resource (Arnaldo), supporting not only Enterprise, but supporting PDC efforts given unified on shared stack.

- Service Monitoring (proactive detection of issues)
  - 1 month
- Testenterprise/Meta catchup deployments
  - 1 week
- Testenterprise Infrastructure - MSK
  - 1 week
- DAE 7.4 Planning/Deployment
  - 2 weeks
- Improve Private Instance deployments
  - 1 month
- SFTP endpoint for Shell (assuming commitment)
  - 1 week
- Cost Allocation Tags
  - 2 weeks
- Important Operations Debt
  - 1 month
- Support/Documentation
  - 30% of cycles
- POTENTIAL INAWARE project - migrate tier from Alibaba to AWS
  - Swag guess 2-3 months
  - Cost rollup not complete yet
