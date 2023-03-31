---
id: 36nxbqmzjocobox7q1tg6f3
title: Proposal
desc: ""
updated: 1680302509105
created: 1680301814578
---

## Proposal for External DaaS API Evolution

Currently the External DaaS API hosted at `https://api.disasteraware.com` supports Active Hazards and Products endpoints:

- /authorize - used to fetch authorization token providing credentials
- /hazards/active - returns the active hazards
- /hazards/<hazard-id>/alert-geography - fetches the alert-geography for the hazard
- /hazards/<hazard-id>/products - get the list of products for the hazard
- /products/<product-id> - get a specific product details for the product

The current external DaaS API is implemented using an AWS API Gateway which hosts these endpoints, and proxies them to the standard Hazards and Products endpoints that the applicaton uses. We created this external DaaS API for a couple reasons. The first was that we could get full analytics on how the DaaS endpoints are being used, and secondly was to be to better control the endpoints (provides a mechanism to limit access, or rate limit, or ...). The beauty of the existing external API is that it's been implemented in a no-code, very simple way, using a HTTP proxy which the AWS API gateway implements.

My proposal is to add the `historical hazards` and `layers` desired by prospects to this existing API via a new set of endpoints. Additionally I propose creating a new set of ROLES which would be used to control each set of end points to support the different SKU's that sales and marketing would like to support.

Proposed new endpoints:

- /historical_hazards - fetches the historical (expired) hazards based on the search terms provided (more on this later)
- /
