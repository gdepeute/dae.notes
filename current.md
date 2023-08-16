---
id: 1ace5a9c-8da5-4362-abe5-881756feabd2
title: Current
desc: ""
updated: 1692218492431
created: 1604337051940
---

# Current 8/16

- Mobile push issue fixed - didn't affect all
- 7.9.2 client issue - code snippet removed somehow, put back in, fixed
- Monitor issues with /swagger endpoint
- Nick needs Slack permissions
- Check technical.operations@disasteraware.com for alert emails
- Nick only has one Asana ticket left
- Izzy
  - IAEA phase 3
  - fixed?
  -

# Current Tracking Items - 8/7/23

- Kyle started
  - Email access granted, Slack access granted
- Gary Frost / PLF
  - Sent email clarifying his desires for map services
- Everbridge / Thursday
- Claire / PHC
  - Rescheduling to next Monday (hopefully)
- Rosanna / Craft.co
  - Trialed 3 years ago, back looking at data
  - Sent sample hazards and detailed email on 8/7/23

# Older Tracking Items

- Crisis24 POC
- Topo1 POC
  - Wait until we decide on proposal pricing
  - Wait until meeting with Johnny/PDC regarding comparison to ???
- Lightning Strike Density Layer Issues
  - reported by Telus (Todd Maki)
- Send PDC details regarding Convexin call on 6/26/23
  - ???
- DaaS agreements and attribution clause?
  - This needs to be in our DaaS agreements
- PHC Health
  - trying to schedule
- Processing leads
  - Trials
  - PDC
  - Need automatic nuture campaign for new leads, not manual process
- BMC proposal for perpetual license
- OliverWyman/Marsh
  - POC single seat API calls

# Debug Test Kafka reachability issue

- Asset Tracker POC - MDove - r5a.xlarge

  - i-0749078f86cb89006 - us-west-2a
  - Public IP 52.88.80.144
  - Private IP 10.2.3.52
  - VPC-ID
    - vpc-0d5413ef049203af3 (magellan-dae)
      - IP 10.2.0.0/16
      - DHCP - dopt-71d93c14
      - Main route table - rtb-0523063c7a7bf67a5
        - 10.2.0.0/16 - local
        - Subnet Association - subnet-0b38c9a509b8dc7fd (magellan-dae-subnet2)
          - IP 10.2.2.0/24
      - ACL - acl-07c147fe5510b1cda
  - IAM Role
    - dae-cloudwatch-agent-role
  - Subnet ID
    - subnet-0e2be2d253189fc64 (public subnet [sub1-az])
  - Route Table

    - rtb-0b07fc3060a8e5614
      - 172.16.6.0/28 - pcx-0c9e8546995f888865d
      - 172.16.6.16/28 - same
      - 172.16.6.32/28 - same
      - 10.2.0.0/16 - local
      - 0.0.0.0/0 - igw-0c451ac9f1cda152a

  - Peering Connections
    - pcx-0c9e8546995f888865d <-> vpc-0d5413ef049203af3 (magellan-dae)
    - Requester: 10.2.0.0/16 - Accepter: 172.16.0.0/16
  - Security Group

    - sg-0a4eeadc280f51586 (asset-tracker-sg)
    - has rules for lg.mdove.com, lh.mdove.com, arnaldo@remote, tenefit@hq

  - Kaazing Techops End

    - VPC-ID

      - vpc-0e18922cdde6a8f85 (STAGE/STAGE/NetworkingStack/Vpc)
      - Requester: 10.2.0.0/16 - Accepter: 172.16.0.0
      - IP: 172.16.0.0/16
      - Main Route Table: rtb-033c062f5552aad870
      - ACL - acl-0d2fa724441196bb3

    - Subnets
      - subnet-0d1d05f00ae531387 (DatabaseSubnet1) - us-west-2a - 172.16.6.0/28
      - subnet-0b7ba3bfc55a679ea (DatabaseSubnet2) - us-west-2b - 172.16.6.16/28
      - subnet-0395d3a2818ddd44c4 (DatabaseSubnet3) - us-west-2c - 172.16.6.32/28

# Current Hot Items - review soon

- NewCo

  - Change copyrights? Update copyright dates?

- John @ AZ - ZScaler Proxy Issue
  - Need to whitelist disasteraware.com and pdc.org in Zscaler
  - Asking him to login again (today) in order to capture in Tomcat to see if it's triggering CORS issue
- Russell @ Daimler - Slow Layer Loading
  - Awaiting Sheila to address sharing to accounts issue
  - Have discovered a token expiration/null token issue that might be involved - could explain the large number of 403 errors seen in #dae-users-errors
  - RA potentially invovled, but behavior doesn't fully explain it, however we might perform an RA "turned off" experiment to gather data
- Shell - email delivery issue from Pinpoint
  - Neita has contacted IT, and they have reproduced and seen the quaratine happening
  - Awaiting an update
- 7.4 - integrate Mandrill back in (configurable)
  - Johnny a couple weeks away
  - No 7.4 feature driving an upgrade as far as I know
- DAE token re-auth issues
  - Need to expand re-auth to -2 mins from expiration vs. 1 mins as we occasionally see re-auth attempted a sec before expiration
  - Thomas has discovered a case where if DAE is asleep for 30+ minutes, thus missing 2 re-auths, then the first re-auth waking from sleep will FAIL which should kick you back to login screen but DOESN'T. Side effect might be that subsequent requests are sent with NULL TOKEN, and could reasonable explain what users like Russell @ Daimler are seeing (intemittent layers showing up/not showing up)
  - Incident of this appears to have shown up due to TAOS layers being enabled by default in the configuration (maybe Positions and Segments in Tropical Cyclones as well) which have short refresh times
- Interos - Adam - hitting too many hazard id's
  - Sent email, he's investigating...
- Ray - Hazard Connector NON-Usage
- RA bottleneck/performance?
- Responses from https://layer-monitor.disasteraware.com slow - 1-2 seconds
- PowerOutage.com has an API and historical data

---

## John @ AZ - ZScaler Proxy Issue

- Some endpoints pass thru without implicating the proxy
  - POST to jwt/v1/auth/login OK
  - GET to enterprise/configuration OK
  - GET to layer-monitor.disasteraware.com/api/user/deployment/services OK (but takes over 1 sec)
  - GET to enterprise/config/theme.json OK
  - GET to organizations/api/organization NOT OK - triggers 307
    - Could this mean the organizations endpoint configured differently?
- Once proxy engages, nothing gets passed thru correctly - could be our endpoint won't handle proxied (cross-site) request

- Requests:

  - enterprise/configuration OK
    - Headers:
      - Accept: _/_
      - Accept-Encoding: gzip, deflate, br
      - Accept-Language: en-GB,en-US-q=0.9,q=0.8
      - Authorization: Bearer <token>
      - Connection: keep-alive
      - Cookie: <cookie>
      - Host: enterprise.disasteraware.com
      - Referer: https://enterprise.disasteraware.com/enterprise/?bypassCDN
      - Sec-Fetch-Dest: empty
      - Sec-Fetch-Mode: cors
      - Sec-Fetch-Site: same-origin
      - User-Agent: Mozilla...
  - organizations/api/organization

    - Headers:

      - Accept: _/_
      - Accept-Encoding: gzip, deflate, br
      - Accept-Language: en-GB,en-US-q=0.9,q=0.8
      - authorization: Bearer <token> [NOTE: lower case]
      - Connection: keep-alive
      - Cookie: <cookie>
      - Host: enterprise.disasteraware.com
      - Referer: https://enterprise.disasteraware.com/enterprise/?bypassCDN
      - Sec-Fetch-Dest: empty
      - Sec-Fetch-Mode: cors
      - Sec-Fetch-Site: same-origin
      - User-Agent: Mozilla...

    - Headers on 307 redirect:
      - Accept: _/_
      - Accept-Encoding: gzip, deflate, br
      - Accept-Language: en-GB,en-US-q=0.9,q=0.8
      - Host: ~~enterprise.disasteraware.com~~ gateway.zscalertwo.net
      - [NEW] Origin: https://enterprise.disasteraware.com
      - Referer: https://enterprise.disasteraware.com/enterprise/?bypassCDN
      - authorization: Bearer <token> [NOTE: lower case]
      - Connection: keep-alive
      - Cookie: <cookie>
      - Sec-Fetch-Dest: empty
      - Sec-Fetch-Mode: cors
      - Sec-Fetch-Site: ~~same-origin~~ cross-site
      - User-Agent: Mozilla...

## Russel @ Daimler - Slow Layer Loading

- Was on the call, saw it myself. Assets and other layers not loading
- At one point when Russell click on the assets, nothing showed up, but also generated no requests - hit in (browser) cache?
- At one point he turned on his assets and they showed up, a couple mins later, turned them back on and nothing. Hard to believe it would have been pushed out of the cache that quickly but as I recall cache replacement in RA wasn't that smart - need to reconfirm.
- Other actions generated requests, but no data returned
- Ran experiment with ?bypassCDN and performance improved dramatically
- Ran speedtest, his machines seeing ~100Mbit up and down
- Looking at RA dashboard sees spike in backend HTTP requests, but backend connections were below 100
- When Jesse started doing experiments, he was able to push the backend requests to 300, but now back down at 50.
- If RA is turned off in the middle of a DAE session, will it recover? Thinking we will want to turn RA off for a week and see what the response is.

---

### Upcoming projects for the team

- [Zach] - IAEA
- [Johnny] - Organization API / message/data / Rave
- [Thomas] - User enhancements/bookmarks
- [Corentin] - Rave/user enhancements/bookmarks

### Remaining fixes to Asset Tracking POC

- dae-hazards
  - Try/except around all calls, believe this is done now
  - Convert prior/new to dictionaries?
- dae-test
  - Massive re-factoring needed
- dae-geomatch
  - Anti-meridian fixes not fully robust?
- dae-am
  - Build display lists with dictionaries, should speed up performance, lots of walking lists

### Miscellaneous

- Blocked on variety of tickets around MQTT, AMQP, fuzzer, ...
  - 2129, 2126, 2124, 2120, 2141, 2160

### Frequent DAE issues - resolved?

- Login issues (trial expired, no one knows)
- No hazards (Shell)
- User layers gone (Shell)
- Can't read property of "application" undefined
- Area briefs broken since 7/19 - Johnny suggests test, how?
- Trial disabled, still receiving alerts
- Email notification changes, have to restart DAS
- Performance issues, support always trying to `?bypassCDN` which is insane

### Project questions

- Cordova vs Capacitor?
