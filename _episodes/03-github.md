---
title: "Using GitHub with EIC Software"
teaching: 10
exercises: 5
questions:
- "How do we use GitHub within the EIC community?"
objectives:
- "Several repositories contain the key geometry, simulation, reconstruction, and analysis software."
- "Working with repositories requires membership of the EIC organization on GitHub."
- "Issue reports and pull requests are ways to collaborate virtually on collaboration software tools."
keypoints:
- "We use several tools on GitHub to ensure we keep the overview of who does what work."
---
## Where are repositories located?
The main repositories are located on two locations:
- the GitHub service contains most user-facing repositories: https://github.com/eic.
- the eicweb GitLab server contains mainly continuous integration infrastructure: https://eicweb.phy.anl.gov/EIC.

We will use GitHub as the main code repository tool. The top of the github.com/eic page has several 'pinned' repositories that are most important. You can also see where most activity is happening based on the ordering of the repositories in the list.

You can 'watch' repositories to be notified of activity. This is helpful if you wish to remain up-to-date on the activity. You can 'star' repositories as another way to find them easily.

> Exercise 1:
> - Verify that are a member of the EIC organization on GitHub: Do you see the members-only page with the grid of software meetings? If not, send you GitHub user name to the [conveners](mailto:eic-software-l-request@lists.bnl.gov).
> - Check which teams you are in: Enter the search terms "members:me" into the search box in the Teams tab to see only the teams you are a member of. If you are not in ePIC Devs, request to be added at https://github.com/orgs/eic/teams/epic-devs.
> - Choose one repository to subscribe to, at some level of activity.
{: .challenge}

## What is the proper way to work with these repositories?
Duplication of work is avoided when everyone knows what is going on.

1. A typical workflow starts from the creation of an **issue** with a feature request or a bug report. This happens in the browser on the github repository site. When creating the issue, feel free to tag people you want to notify.
1. Create a branch that includes the issue number in the name. This can be done from the browser or command line as `git checkout -b issue123`
1. Edit and work on your branch. When you are ready, you can commit your changes to the branch.
1. If you are ready to merge your branch into the main repository, you can generate a **pull request** from the browser. You can assign a reviewer at this stage and add informationin the Write box that explains the changes made. If your work is not yet completed, you can utilize the Draft PR.
1. Once you've generated a pull request, continuous integration tests are run to ensure compatibility. The reviewer will approve the changes, merging your code into the main branch.
1. After the pull request is approved and the code is merged, you can delete your branch using the browser or via the command line.

A good example of the above workflow is shown in detail [here](https://eic.github.io/tutorial-jana2/05-contributing/index.html)for the EICrecon repository.

> Exercise 2:
> - Think of one issue that is related to the analysis or detector you are mainly working on.
> - Think of a good title that summarizes what the issue is.
> - Open an issue in the relevant repository and fill out the provided template.
> - Tag one person (who is not the instructor) whose input you would like on this issue.
> - Advanced users: Create a branch from the issue using the 'Development' section in the right side bar of the issue.
{: .challenge}

## How can you use eic-shell with the repositories that you are working on?

## What are the checks that are run on pull requests?

{% include links.md %}
