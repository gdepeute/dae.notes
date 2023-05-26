---
id: pamfjr2m652j0p05ecrllpb
title: Diq
desc: ""
updated: 1685135096824
created: 1684534102990
---

Arnaldo leaving on 5/26/23

- OPS Handbook: https://sites.google.com/nten.io/devopshandbook/home?authuser=0&pli=1

- OnePassword main vault contains ALL random crap
- SteveK has access to all of our systems
- IT Wiki is referenced - ping Cassie if don't already have access

# Arnaldo Deployment Review - 5/23/23 2pm

- Reviewing DAE New Stripe Deployment Sequence (Production)
- CodeCommit Repository per component

  - All share dae-amibuild

- LDAP server - used for VPN credentials and anything behind it (anything \*.us)

  - Apache Director Studio
  - Needs VPN connected
  - 1Password/ldap.tenefit.wan
  - Jenkins and \*.us respoitories

- GMail

  - admin.google.com, my credentials mike.dove@tenefit.com already set up
  - There is an Archive Manager account with GDrive associated (456GB)
  - You might need to archive/download and then push nto Archive Manager GDrive
  - In some cases you need to login as the individual user in order to perform a TakeOut (data archive), and might need to disable 2FA
  - When user passwords are changed, they are stored in Archive Manager entry in 1Password
  - When Delete User, asks if you want to Transfer, select Archive Manager, and it will push the data there
  - If you login into Archive Manager, go to Drive, and you'll see the users which have been archived and then delete the user

- DeltaPath number I should have - can use that and SMS to that to be forwarded to my phone.

  - No idea where my Deltapath number
  - Suggests to put the DeltaPath number in for recovery/other...

- Slack - already have admin priviledges

- Resource termination of AWS resources

  - Have not cleaned things up like LoadBlancers for RA (DevPay us-west-2)
  - Clean up LB's for RA

- AWS Kaazing Main

  - Cost Center?
  - Go to Billing Dashboard under main screen
  - Elastic costing $3-4k!
  - AWS Cost Management / Reports
    - BigRed PinPoint Cost report on page 1 of Ops Handbook
    - For this month PinPoint at $2700
    - Select Dimension - Service
    - Will get breakdown to cut/paste with Natalie
  - Lambda in DevPay - list file in S3 of certificate expirations
    - DisasterAWARE Certificate Management Project in GitHub
      - Will show prior and upcoming ones
    - July upcoming for repository.kaazing.us - see ticket #591
      - Scripts look for instance in TechOps - certbot and monitor in eu-west-2

- Elastic

  - Elastic and Metric agents are running on some EC2 instances, so if one pauses Elastic, some instances might start throwing errors...

- GoDaddy

  - In 1password

- PM2 - Uploader

  - Node process manager
  - Runs on Sentinel box

- EC2
  - Some EC2 instances allow connecting with Session Manager which is easier than setting up SSH
