# CTFd

## Functional Requirements

| Student Perspective | ✅⚠️❌ |
| ------------------- | ------ |
| Challenge Overview  |   ✅ - display of challenges with files,description, tags, flags , start/end times - configs -> time -> start time/end time/ freeze time   |
| User Interface      |   ✅ - page editor accessed from admin panel - to add and customize new pages  |
| Authentication      |   ✅ - possible via plugin.for example : OAuth/ github OAuth app    |
| System Status       |   ⚠️ - could be possible by integrating with monitoring platforms like grafana  |
| Privacy             |   ✅ - could be set by admin on whether the user can be hidden   |

| Teacher / Admin Perspective | ✅⚠️❌ |
| --------------------------- | ------ |
| Flag Management             |    ⚠️ - The article of application target says about per user flags    |
| Deployment & Lifecycle      |    ✅ - deployment of challenges on one click possible through terraform but modifications like start/end time needs to be explored  |
| Administration Interface    |    ⚠️    |
| Score Export                |    ✅ - possible through csv export |
| PII Visibility              |    ✅ - admin access to the managemnt of user info  |

## Technical Requirements

| Platform Stability          | ✅⚠️❌ |
| --------------------------- | ------ |
| No fast-moving dependencies |    ✅   |
| Plugin/API Extensibility    |    ✅ - yes. For example : terraform    |

| Authentication Requirements                                  | ✅⚠️❌ |
| ------------------------------------------------------------ | ------ |
| User + Password (local)                                      |    ✅ - users must set the properties  |
| OIDC (e.g. GitLab, ZIM)                                      |    ⚠️ - could be possible with OAuth plugin facility, or through OAuth app as mentioned in SSO in doc    |
| (Opt) Multiple authentication sources combined               |        |
| -> merging rules for authentication through multiple sources |        |

| Challenges                                          | ✅⚠️❌ |
| --------------------------------------------------- | ------ |
| Single Container per user                           |   ⚠️ - Application Target under custom challenges tells about users to deploy per account instance   |
| Single Container per challenge                      |   ⚠️    |
| (Possible to add) Script that checks status         |        |
| Personalized Flags                                  |   ⚠️ - per user flag in target challenges     |
| Support file uploads                                |   ✅   |
| -> (opt) generator script for unique files per user |        |
| (opt) tls-proxy                                     |   ✅   |
| (opt) support for "solved" challenges               |   ⚠️   |

| Declarative Descriptions                           | ✅⚠️❌ |
| -------------------------------------------------- | ------ |
| Challenges described in e.g. YAML                  |    ✅ - ctfcli challenge specification is provisioned in challenge.yaml   |
| Challenges containable in single Git repository    |    ⚠️  |
| Start/Stop Time                                    |    ⚠️  |
| availability after challenge completion            |        |
| -> no further flags accepted/ points awarded       |        |
| challenge scoring configurable per challenge       |   ⚠️ - could be provisioned through multi challenges plugin  |
| -> (opt) dynamic scoring based on number of solves |   ✅ - dynamic value challenges type  |

## Administration Tools

| Administration Tools                                 | ✅⚠️❌ |
| ---------------------------------------------------- | ------ |
| Challenge Update while running                       |   ✅  - can be possible through ctfcli + terraform and integration into github CI/CD   |
| Challenge Restart while running                      |   ✅ - can be possible through targeted approach. eg: tagret modules in terraform to only update changes in it  |
| Compare actual vs desired state                      |        |
| List actions required (start/stop/restart challenge) |        |
| Support cronjob execution                            |        |
