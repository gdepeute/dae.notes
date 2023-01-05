---
id: 1ace5a9c-8da5-4362-abe5-881756feabd2
title: Current
desc: ''
updated: 1665786403290
created: 1604337051940
---

### Current Hot Items

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
