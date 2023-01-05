---
id: af1f07ac-2b12-4b77-9c03-d622647de936
title: Notifications
desc: ''
updated: 1603759078484
created: 1603759071601
---

# Notification Support

- Assertion is, one of the first things a company buys in the GSOC team is a mass notification system
  - They need a solution to get notifications/messages out to employees, customers, ...
  - Appears this is typically a standalone platform, meaning, when I have a reason to send a notification, I go to the mass notifications system, enter the message, then select who it should go to
  - Appears that typically geo-positioning information is not used in many cases as there is no mechanism to easily get geolocations from the individuals
    - Mass notification systems have API support to upload geolocation data, and could use it if they have it.

## What does this mean for us?

- Add improved notification support to DAE.
- Any user that is using DisasterAWARE app on their phone could opt in to sharing their geolocation on a regular basis (typically when there is a large change in location - 100ft or more)
- DAE could use that data as mapped to hazards to alert those users that might be in harms way/directly impacted

## Notifications requirements

- SMS/MMS messages worldwide
- Push notifications on phone (via APNS/GCNS using AWS SNS or equivalent)
- Robo dial support for voice messages
- Email support
- Other channels (social?)
- Other contacts (friends and family)
- Potentially notify on multiple devices (prioritized ordering)
- Acknowledgement support
  - SMS/MMS via user reply
- Support two-way communication
  - Delivery and optional reply via mechanism which makes sense, via original delivery method or via app or ...

## Miscellaneous Information

- Dialogic boards
- OC4J?
- Regulatory issues around text messages in other countries?
- SIP trunks for robocall voice automation
- Polling logic/flows
