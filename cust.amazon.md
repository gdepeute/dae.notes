---
id: hw9q7gtgv9yfwl3rjodqimk
title: Amazon
desc: ""
updated: 1673377141484
created: 1673373729713
---

# Amazon

## Call 1/10/23

- Amazon

  - Matt Hovs
  - Taher Beawerwala / EU in London / PM
    - Weather and man-made events focus in EU
  - Guilhem Busset / SW Dev Manager PreCOM
    - 10 SW devs on the project

- Last meeting was 12/5 with Sheila and Keith
- Kepler to injest NWS events
- NOT interested in weather events, mostly interested in NON-weather
- Injest and decision making around weather events "solved" in their mind
- No planned action until at least March - Andrew out until then on paternity leave
- Recommending them to trial and dig into the system
- Deployment no earlier that Q2/2024

### Questions from Matt / Guilhem

- Mindset comes from experience with Everbridge
- PreCOM is the internal tool they are injesting
- Large number of drivers is the focus
- Wildfires - asked question of difference of burn zone and impact area
  - Erin responded to the question
- AIM - All Hazards Impact Model - now AIM 3
- Wants to know what countries we are pulling weather data in from
  - Erin mentioned our manual hazard team
- Guilhem might be interested in Webhook for pushing events
  - Wants to know HA/DR and scalability
  - Perhaps some VPC level integration with a Amazon Private Instance
- Matt asked about the customization level able to be made (with private instance)
  - Example: 6" of snow across 4 states, and if/when winds exceed 58mph
- Taher is interesting in effect custom reports overlapped with zipcodes
  - They use zipcode as the smallest geographic unit Amazon is dealing with
