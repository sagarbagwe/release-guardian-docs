# Release Guardian — Privacy notice

Effective: November 15, 2026

Release Guardian is an independent hackathon MVP developed by Sagar Bagwe. Support and privacy contact: sagarbagwe2506@gmail.com. It is not an Atlassian product or a security certification.

## What the app accesses
The app runs on Atlassian Forge and requests read:jira-work and write:jira-work. As the signed-in user, it reads the current project's versions, visible release issues, summaries, statuses/status categories, assignee presence, standard issue links, linked blocker issues, and issue-type/create metadata. Project and version identifiers, issue keys, and evidence text are processed to display a readiness report and prepare a follow-up.

## How data is used
Jira data is used only to perform the requested scan, show evidence, check for an existing labeled follow-up, and create a follow-up when explicitly approved. The app does not use an external AI service, advertising service, tracking analytics, or external data endpoint. No external egress permission is configured.

## Storage and retention
This version does not intentionally persist Jira payloads in application storage or log issue contents. Data is processed during Forge requests and in the rendered user session. Atlassian operates the underlying Forge/Jira infrastructure and may process operational logs and metadata under its own terms and policies.

An approved follow-up is a Jira issue containing its release and source evidence, identifying labels, and normal Jira authorship/audit information. It remains in the customer's Jira site under that site's permissions and retention policies. Uninstalling the app does not remove those Jira issues. The app does not create a separate external copy.

## Permissions and control
All Jira API requests use the signed-in user's permissions. The app does not grant access to otherwise hidden issues. Site administrators can uninstall the app. Authorized Jira users can edit or delete created follow-ups in Jira, subject to site permissions. Contact the site administrator for Jira data-access and retention requests.

## Support messages
If you contact the developer by email, the message and address are processed by the developer's email provider to answer the request. Do not send secrets or sensitive issue contents. Request deletion of support correspondence by emailing the contact above; mandatory legal retention, if any, may apply.

## Limitations and changes
This is a hackathon prototype, not a complete privacy or security assessment of Atlassian's services or your Jira configuration. Material changes to app data handling should be reflected in an updated notice before distribution of that change.
