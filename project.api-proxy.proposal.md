---
id: 36nxbqmzjocobox7q1tg6f3
title: Proposal
desc: ""
updated: 1680304403851
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

As the existing endpoints are simple HTTP proxies (mappings) to the set of URL's used by the application, my proposal is to implement the same scheme for the new endpoints. Part of the beauty of fronting this external DaaS API with the API gateway is that is isolates and hides the actual implementation. If as time goes along, we determine some customers are loading these endpoints (and thus backend map servers) too much, we can then choose to implement additional caching, OR to host the data on our own map server behid the scenes, which would be invisible to the prospect/customer, and would not require them to change any code.

Proposed new endpoints:

- /historical_hazards - fetches the historical (expired) hazards based on the search terms provided (more on this later)
- /services/<map-service-name>/... - support for the map services and layers desired by prospects

As noted, I also propose a new set of ROLES in the system to support these endpoints:

- HAZARDS_API - ROLE that provides access to the existing endpoints hosted at `https://api.disasteraware.com`
- HISTORICAL_HAZARDS_API - ROLE that provides access to the `/historical_hazards` endpoints
- LAYERS_API - ROLE that provides access to the `/services` endpoints
  - As I suspect that we'd ultimately like to group sets of map servers/layers into separate SKU's, this supports more granular ROLES, for example:
    - LAYERS_WEATHER_API - access to weather layers
    - LAYERS_HISTORICAL_API - access to historical layers
    - ...

Fortunately the AWS API gateway supports the notion of `custom authorizers` to implement validation of tokens and existence of the required ROLE(s) in order to allow the request. Part of the prototyping I've done this week was to build this `custom authorizer` which is a very small handful of lines of code implemented as a serverless AWS lambda component. This allows trival implementation/validation of the ROLE(s) proposed above, or any new set of ROLE(s) we choose to implement in the future.

The prototyping effort I undertook this week included adding the `/historical_hazards` endpoint, as well as a couple map services (which each support multiple layers) behind the `/services` endpoint. I was able to implement these, then run DisasterAWARE Enterprise pointing the application at the new endpoints to verify the implementation of the endpoints.

I'm at the point now where all key questions have been answered, and am ready to begin an implementation, assuming the team agrees to move forward.

With respect to the `/historical_hazards` endpoint, if you have used the Hazards search in DisasterAWARE Enterprise, you've likely noticed that if your search terms aren't relatively tight, then the search returns too many results to be returned to the user. I'm not proposing changing this as all, and perhaps lowering the maximum number of restuls that can be returned in any search (e.g. 1000).

Additionally, I'm proposing leveraging the existing search term syntax for the query parameter of the URL as it's known to work. It's a bit `old school` in my opinion, and we can certainly choose to improve on it later, but to create a new search term syntax would require more code to be written to map the new syntax to the existing syntax for no real benefit IMHO.

In terms of the map services/layers, we need to finalize on the initial set, in this case for Palantir/Crisis24. As Ray noted in an email, their team is reviewing all the map services and layers to see if there are further restrictions or layers we need to eliminate.

We should also start proposing/creating the map service/layer groupings that we might price differently.

As the DisasterAWARE Enterprise application is driven by a (large) configuration file, which defines all the map services and layers, my plan would be to write a small tool which takes the current configuration and build the API gateway dynamically. As the configuration of map services and layers changes relatively frequently, it's likely important that if a map service URL or layer specification `changes` that it automatically ripple into the API as well.

Then the documentation needs to be created for the `/historical_hazards` and `/services/<map-server>/...` endpoints. Luckily we have some existing documentation Johnny wrote a few years ago we can start with. It would be great to have some help getting the documentation created/updated.

In terms of timeline, I would expect to have an implementation running that meets the Palantir/Crisis24 requirements in roughly a week (maybe two), which would not include documentation.

Assuming there is agreement on the plan, then it seems like it's time to nail down Palantir/Crisis24 in terms of $ and for them to commit to getting us a PO.

Mike
