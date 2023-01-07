---
id: f0xq3qatoif6ebdys0sebwm
title: '745'
desc: ''
updated: 1672963605243
created: 1670874842835
---

# **DAE 7.4.5 release**

- Current Release: 7.3.12

### **Changes:**

- **CHANGE**: Build number 433 -> 435
- **CHANGE**: Bitbucket Branch release/7.3.12 -> release/7.4.5
- **REMOVE**: DAS 3.8.3
- **ADD**: Hazard-Event-Producer 1.1.0
- **ADD**: Organization-Event-Release 1.0.0
- **CHANGE**: H&P 2.16.8 -> 2.17.5
- **CHANGE**: Auth 2.5.2 -> 2.5.4
- **CHANGE**: Bookmark 3.2.0 -> 3.2.2
- **CHANGE**: Org/Sub-Org 1.6.1 -> 1.7.2
- **CHANGE**: Profile 3.0.1 -> 3.0.3
- **CHANGE**: JSON Web Token 1.3.5 -> 1.3.6
- **CHANGE**: User Management App 1.9.0 -> 1.9.4
- **CHANGE**: SNS Consumer 4.3.4 -> 4.3.7
- **CHANGE**: SNS Producer 4.2.1 -> 4.2.2
- **CHANGE**: Country 1.2.0 -> 1.2.2
- **ADD**: Geohelper 1.0.1

### Deployment Flow

Separate repos. From the deployment perspective there are two repos that are involved (per deployment that is):

- The base deployment specific repo:
  - https://us-west-2.console.aws.amazon.com/codesuite/codecommit/repositories/dae-testenterprise/browse?region=us-west-2
- And the shared AMI build repo:
  - https://us-west-2.console.aws.amazon.com/codesuite/codecommit/repositories/dae-amibuild/browse?region=us-west-2
- Which come to play under a deployment specific pipeline:
  - https://us-west-2.console.aws.amazon.com/codesuite/codepipeline/pipelines/dae-testenterprise/view?region=us-west-2
- Which in turn uses a deployment specific build job:
  - https://us-west-2.console.aws.amazon.com/codesuite/codebuild/812992951157/projects/dae-testenterprise/history?region=us-west-2
