---
id: 0106f943-7059-46c0-a316-14297eb1be12
title: Projects2021
desc: ''
updated: 1603759110852
created: 1603759106172
---

# PDC Projects 2020-2021

## Initial Approval

### Improved Infrastructure Service Monitoring

- Implement and close existing monitoring and alerting gaps in the existing infrastructure
- Met recently to review current status and gaps
- Initial project breakdown:
  - Improved DAS monitoring
  - Improved Application analytics
    - [Mateo] Ensure all systems/services are being monitored
      - [Mateo] Most exist in Tomcat server(s)
      - [Mateo] Include all services within compatibility tab in DA dashboard
    - [Mateo] Possibly Motomo or New Relic?
      - [Mateo] Identify broken features (as they break) as well as determine which parts of the application are being used the most/least. Least-used should be considered for removal/redesign
    - [Mateo] Ensure all alerts are sent to Site 24x7 for PDC awareness
  - Monitor ArcGIS token validation
  - Monitoring notification generation and delivery
  - Verify/Enforce Log rotation for all components
  - Monitor number of connections to RDS and DocumentDB
  - Log access to all instances running each DAE instance
- Estimate: 1 man month
- Cost: \$25.6k
- Target Start: ASAP

### Services Dashboard - Phase 1

- Services Dashboard based on dae_test tool
- Initial project breakdown:
  - Deploy existing dashboard Slack alerts for EMOPS/RAPIDS
  - Solicit feedback and required changes from PDC leadership
  - Create text or web based UI (for visual observation)
  - Implement additional feedback from PDC leadership
- Estimate: 1 man month
- Cost: \$25.6k
- Target Start: ASAP

### DAS Stabilization

- Project focused on making the "existing" DAS service more robust and scalable
- Initial project breakdown:
  - Streamline data ingestion to process on new data
  - Migrate to GIS database so that queries/matches are database operations
  - Integrate with new Organization Service
- Estimate: 1.5 man month
- Cost: \$38.4k
- Target Start: ASAP (Johnny availability)

## Still Need Further Discussion

### Centralized Logging Analysis Service

- Take ALL logs from ALL services, and push into a centralized logging service (e.g. Loggly) to facilitate more proactive detection and response to issues
- Initial project breakdown:
  - Determine centralized logging service to use and cost
  - Push logs from all services in the infrastructure into central logging system
  - Create set of alerts based on common "themes"/"patterns" that occur when system is in trouble or failing
- Estimate: 2 man months
- Cost: \$51.2k
- Target Start: After _Improved Infrastructure Service Monitoring_

### Infrastructure Modernization - Phase 1 (“Fortify existing environment/design”)

- Initial project breakdown:
  - Create new maven repo
    - [Mateo] Please provide details as well as cost/benefit analysis?
  - Build system for AMI creations
    - [Mateo] Need to ensure we will have CI (Continuous Integration for builds)
    - [Mateo] Ensure AMIs are created and employed for all EC2s possible - Golden Image of each EC2 Instance Family.
    - [Mateo] Benefits
      - [Mateo] For incremental additions
      - [Mateo] Less CFN scripting
      - [Mateo] Faster machine creation
  - Implement stripe mechanism with ALB, including rollback support
    - [Mateo] MM to share PPT with Tenefit (MD)
    - [Mateo] Must improve switching mechanism to eliminate downtime and reduce complexity (e.g., host file IP changes)
    - [Mateo] Explore “generic” DA base/foundation for upgrades and new deployments
      - [Mateo] All deployments i.e., EMOPS/RAPIDS/Etc., would use the same “base”
  - [Mateo] Improve resource management
    - [Mateo] Resources per deployments; S3 bucket per DA version versus per DA instance
  - Migrate away from NGINX to ALB
    - [Mateo] Please provide details as well as cost/benefit analysis?
    - [Mateo] As non-cloud systems will still use NGINX, this may unnecessarily increase complexity
  - CloudFormation script changes to support tiers
    - [Mateo] Captured above in “AMI” & “Stripe Mechanism”
  - Parameterization of builds
    - [Mateo] Better would be Continuous Build/Deployment (CI/CD) using Jenkins Automation or Ansible.
- Cost: \$96k
- Target Start: After _Improved Infrastructure Service Monitoring_

### Infrastructure Modernization - Phase 2 (“New design(s)/Technique(s) - Future-Proofing”)

- Evolving CloudFormation and Configuration Tools to be parameterizable and easily leveraged by all tiers
  - [Mateo] Captured in Phase 1 - is this a future enhancement?
- Initial project breakdown:
  - Implement autoscaling for services
    - [Mateo] Is this referencing auto scaling of “services” vs servers i.e., “serverless” (see next bullet)? If so, great! If not, then we already have auto scaling in place.
  - Convert components to true services, and potentially containerizing them
    - [Mateo] Or as a serverless architecture
    - [Mateo] Spring Boot Microservices Architecture using Docker/Kubernetes?
    - [Mateo] Identify what components are better deployed under a multi-tenant service
    - [Mateo] Cloudfront for HTML engine - static code that is the same across all DAs
  - Database reconciliation
    - [Mateo] Please provide details as well as cost/benefit analysis?
  - Certification management (using AWS KMS)
    - [Mateo] What does this include i.e., SSL certificates for the domains?
    - [Mateo] As non-cloud systems may not use KMS, this may unnecessarily increase complexity
  - Backup infrastructure and management
    - [Mateo] Existing infrastructure may already be sufficient
  - Documentation branding support
  - Operational Documentation
- Estimate: 25 man weeks
- Cost: \$160k
- Target Start: After _Infrastructure Modernization - Phase 1_

### Map Service Creation Tool Improvements

- Project focused on operationalizing gis_tool to be more usable
- Primary usage: import of KML, CSV files into asset map services
- Initial project breakdown:
  - Provide question based UI for ease of use (when command line parameters are not provided)
  - Improved error/warnings
  - Improve map service symbol support
  - Improve support for other input types (GEOJSON, TXT, LDAP, custom)
- Estimate: 1 man month
- Cost: \$25.6k
- Target Start: ASAP (MDove)

### Asset Tracking and Notification Architecture & Implementation - Phase 1

- Project focused on baseline architecture and implementation for Asset Tracking and Notification
- Assuming USTDA is approved and moves forward, this project would be funded from that bucket
- Initial project breakdown:
  - Implement scalable injest of location coordinates from mobile users
  - Implement data pipeline based on Kafka
  - Create horizontally scalable services to injest static and mobile assets into data pipeline
  - Create service to injest hazard data (from existing ActiveMQ streams) into data pipeline
  - Create horizontally scalable service to process geomatches of hazard updates to asset locations
  - Create new scalable notification system leveraging AWS Pinpoint service
- Estimate: 12+ man months
- Cost: Currently expected to be funded by USTDA project
- Target Start: January 2021

### Asset Tracking and Notification Improvements - Definition

- Definition phase of evolution of asset tracking and notification to support new use cases and reporting
- Initial project breakdown:
  - Define flexible asset heirarchy and relationships
  - Define additional metadata to be added to asset entities
    - Examples: value of asset, value of property, additional emergency contacts, current on-site staff, current inventory, current inbound/outbound shipping status, ...
  - Define flexible reporting module to better asses impact to asset(s) and relationship based on additionl metadata provided
  - Define flexible notification and report system, including use case specific templates
  - Define flexible notification system for asset(s) and relationships (additional contacts and additional data to be reported in notifications)
- Estimate: 2 man months
- Cost: \$51.2k
- Target Start: ASAP

### Asset Tracking and Notification Improvements - Implementation

- Implementation phase of evolution of asset tracking and notification to support new use cases and reporting
- Initial project breakdown:
  - Allow additional metadata to be added to asset entities
    - Examples: value of asset, value of property, additional emergency contacts, current on-site staff, current inventory, current inbound/outbound shipping status, ...
  - Create flexible reporting module to better asses impact to asset(s) and relationship based on additionl metadata provided
  - Support flexible notification and report system, including use case specific templates
  - Provide more flexible notification system for asset(s) and relationships (additional contacts and additional data to be reported in notifications)
- Estimate: Implementation - will be scoped based on definition phase
- Cost: Will be determined when scoped after definition phase
- Target Start: 2021

### Application GUI Improvements

- Focus on application GUI improvements
- Needs additional work from PDC/Tenefit to define complete list
- Initial project breakdown (not complete):
  - Resolve issues between mobile and desktop/web notification preferences
  - Migrate UI and menus to be more compliant to current design guidelines for iOS/Android
  - Improved/simplified navigation
  - Improved error handling and notifications
  - Wizard to simplify preference settings
  - Simplified dashboard view
  - Capacitor migration (EOL Cordova) - should this be separate project given urgency, or covered in existing BSP?
- Estimate: 6 man months
- Cost: \$153.6k
- Target Start: January 2021
