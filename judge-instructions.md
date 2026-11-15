# Judge installation and test guide

## Access status
The production installation link is available in this repository's [README](README.md). Do not use the development app URL as the judge-install link. Judges install into their own Jira Cloud test site; no access to the author's Jira account is required or provided.

## Prerequisites
- Be an administrator of a Jira Cloud test site where Forge installation is permitted.
- Have access to a Jira software project with versions/releases and permission to view issues.
- To test follow-up creation, also have Create issues permission and an issue type without extra unsupported required fields.
- Allow the app's read:jira-work and write:jira-work scopes. It makes calls as the signed-in user.
- This installation-link build is an unlicensed hackathon MVP, not a paid Marketplace listing.

## Install and open
1. Open the production installation link, select the Jira site, review permissions, and install.
2. Open a Jira software project/space. In Apps or the project's More navigation, open Release Guardian. Navigation labels may differ by Jira layout.
3. Complete Atlassian's first-use authorization if requested.
4. Choose a non-archived version and click Check readiness. No external account, API key, AI service, or app configuration is required.

## Reproduce the demo on your site
Use a dedicated synthetic project. The keys and version IDs shown in the video belong to the author's demo site; your IDs will differ.

Create versions 1.0 Launch, 0.9 Stable, and 2.0 Planning.

| Issue summary | Status category | Owner | Fix version |
| --- | --- | --- | --- |
| Checkout API | Done | Any test user | 1.0 Launch |
| Payment retries | In progress | Unassigned | 1.0 Launch |
| Idempotency contract | To do | Any or none | None |
| Order audit events | Done | Any test user | 1.0 Launch |
| Stable release smoke check | Done | Any test user | 0.9 Stable |

Create a standard Blocks link so **Idempotency contract blocks Payment retries** (Payment retries is blocked by Idempotency contract). Do not add Idempotency contract to a version. Leave 2.0 Planning empty.

If the project requires assignment, relax nothing in production: use an authorized isolated test project or skip the missing-owner part. Workflow names may differ; the app uses Jira status categories.

## Expected results
- 1.0 Launch: Blocked; 2 of 3 visible issues complete; one incoming blocking relationship; one unfinished issue without an owner; three findings.
- 0.9 Stable: Ready within the visible supported scope, 1 of 1 complete.
- 2.0 Planning: Unknown, zero visible issues.
- Mark Idempotency contract Done, rescan 1.0 Launch: At risk because Payment retries is unfinished.
- Assign and complete Payment retries, rescan: Ready within scope. Jira search updates may take a short time to become visible.

## Follow-up test
1. In a finding, click Review follow-up and inspect the evidence and proposed text.
2. Click Cancel: no issue should be created.
3. Review again, select an issue type, and explicitly approve creation. This creates one follow-up, not a source-issue edit.
4. Inspect the created issue: it includes release/source evidence and identifying labels. No assignee or Fix version is explicitly set by the app; Jira defaults may apply.
5. Review the same finding again: an indexed existing labeled follow-up is reused. Deduplication is best effort, not a concurrency guarantee.

Only perform this step on synthetic data. You can delete the resulting test follow-up through Jira afterward.

## Interpreting the result
This is not a full release sign-off. Only visible issues and direct standard Blocks links are supported. Hidden issues, custom/transitive relationships, deployments and tests are outside scope. Limits: 500 release issues and 50 unique external blockers per scan. Incomplete or unknown coverage never qualifies for Ready.

## Troubleshooting
- No versions: create a non-archived project version using Jira's release/version settings.
- No app entry: verify installation is on the correct Jira site, then reopen the project and its Apps/More menu.
- Permission or authorization error: complete Atlassian consent and verify the user's Jira access. The app does not bypass permission checks.
- Create failure: verify Create issues permission and whether the project requires additional fields the MVP does not support.
- A changed issue still appears stale: wait briefly for Jira search indexing and click Scan again.
- Contact: sagarbagwe2506@gmail.com. Do not send production secrets or sensitive Jira issue contents in support email.

## Uninstall
Use Atlassian's connected-app administration to uninstall Release Guardian. Uninstalling does not delete Jira follow-up issues previously created by an explicit approval. Remove test issues separately in Jira if desired.
