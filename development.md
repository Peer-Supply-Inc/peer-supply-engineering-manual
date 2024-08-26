## Development Processes
We are constantly learning and changing, so expect to change this document as we improve.


### Aim towards continuous delivery
We are a small team today, so we may not release every day or every week, but our aim is to move things to production quickly. This means breaking down work in a way that we can safely deploy new features and functionality behind flags until it is customer-ready.

We recognize this is not always possible, but we strive to do so as a primary way of developing.

### From idea to production
Our product team operates product planning in "Now", "Next" and "Later" columns in [Notion](https://www.notion.so/). Those issues in now and sometimes next will be those represented in our project management tool, JIRA.

Once it's decided we're going to execute on work either from the product planning board or from technical debt tickets we have created as an engineering team, groom them, point them, and order them in the backlog as a whole team, together with product, design, and engineers.

### Track our work
We use tools like JIRA to track our work efficiently. Instead of leaving a todo or a comment in our codebase, opt to leave a comment on the associated work. Comments rarely get updated and todos hardly ever get done when left in code. This gives us clear records of what we need to do and when. Sometimes an entirely new ticket will be necessary. If work is discovered that will increase the scope of a current ticket in progress, that ticket may need to be re-refined by our process.

### Build for each other
When building components and services in our codebase think about your teammates. Think about how the code you're writing will be _read_ by others and if the code you are writing could be rewritten to be _used_ by others. Think about your naming and is it clear and consistent. Could the issue you're creating a function for possibly come up in other areas? Keeping these in mind will allow us to build utilities that will speed us up as we continue to build for the long term. Keep in mind to [Avoid Hasty Abstractions](https://kentcdodds.com/blog/aha-programming) and strike a balance. 

#### Estimation
We use story points for our estimation instead of time since we have different skill levels on our team. We use fibonnacci numbers for pointing - 1, 2, 3, 5, 8, 13...

- If a ticket is larger than an 8, it's probably too large. We should try to break it down
- For most issues, we should land around 3 or 5, with 3 meaning it is a reasonably sized ticket, 5 meaning it's reasonably sized but with some caveats / extra considerations. 8 is a large ticket, which requires extra attention.

#### Work assignment
It is up to the team to self-assign tickets as they are working on them. This should be based on the tickets included in sprint planning, and if those are complete, prioritized based on tickets in the engineer's focus area in the backlog. Tickets should only be assigned when they are actively in progress. Ideally only one ticket should be in progress at a time. Exceptions are when a ticket is being reworked from QA and/or PR review, or when tickets are small and closely related enough to make sense to do together.

#### Statuses
Jira statuses should be updated for different states of work. If work is in progress, ready for code review, or ready for deployment it should always reflect that to make it easy for others to see and work with asynchronously

#### Branching
We use [trunk based development](https://trunkbaseddevelopment.com/) to decrease our cycle time. Engineers should branch feature branches off of the main branch and PR / merge back to main. Feature branches should use the associated Jira ticket name for ease of linking.

Merging should be done if and only if PRs have been approved and automated build and test scripts have passed.

#### PRs
*Titles*: Titles should have the ticket number from Jira.

*Descriptions*: PRs should include a description of the work completed, as well as any relevant details needed for deployment. It should contain enough relevant details for any engineer to move it through CI/CD or a manual deployment.

*Reviews*: PR reviews are a great place for us to manage the quality of our code and improve ourselves as engineers. PR reviews should always be done with empathy in mind. Shaming an engineer's work is not acceptable, even if there are issues in the code. Suggesting changes in an empathetic manner is encouraged. We should all be open to feedback. No engineer, staff, senior, or junior, is right 100% of the time.

A reviewer should be able to assess in a PR review 1. Is the feature code complete 2. Does the implemented change introduce technical debt 3. Does the implemented change make use of best practices for the language as well as good naming conventions, performance, error handling, and security. 4. Does the implemented change include tests

#### Deployments
Deployments are done using CI/CD. Currently both primary Peer Supply repos automatically deploy to production when a push is made to the main branch. Smoke testing should be conducted after a feature has been deployed.

Rollbacks: We currently use Cloud Run for our API and our front-end. If a major bug is discovered on production, the previous revision in Cloud Run should be served until a fix or rollback commit has made it through the PR review process.

#### Post-deployment production changes
Periodically activities need to be done on production manually, though this should be the exception and automated where possible. Each engineer is individually responsible for shepherding those changes (manual database change, api call to make, etc) after deployment
