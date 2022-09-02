---
title: "Using GitHub with EIC Software"
teaching: 20
exercises: 10
questions:
- "What is the EIC environment?"
objectives:
- "Understand what we mean with the EIC environment, or `eic-shell`."
- "Appreciate the benefits of containers as development environment."
keypoints:
- "The EIC environment `eic-shell` is a singularity/docker container with a curated selection of software components."
---

## Where are repositories located?
The main repositories are located on two locations:
- the GitHub service contains most user-facing repositories: https://github.com/eic.
- the eicweb GitLab server contains mainly continuous integration infrastructure: https://eicweb.phy.anl.gov/EIC.

We will use GitHub as the main code repository tool. The top of the github.com/eic page has several 'pinned' repositories that are most important. You can also see where most activity is happening based on the ordering of the repositories in the list.

You can 'watch' repositories to be notified of activity. This is helpful if you wish to remain up-to-date on the activity. You can 'star' repositories as another way to find them easily.

## Exercise 1:
- Verify that are a member of the EIC organization on GitHub: Do you see the members-only page with the grid of software meetings? If not, send you GitHub user name to one of the conveners.
- Check which teams you are in: Enter the search terms "members:me" into the search box to see only the teams you are a member of. If you are not in EPIC Devs, request to be added at https://github.com/orgs/eic/teams/epic-devs.
- Choose one repository to watch, at some level of activity.

## What is the proper way to work with these repositories?
Duplication of work is avoided when everyone knows what is going on.

A typical workflow starts from the filing of an issue with a feature request or a bug report. The issue generates some discussion (feel free to tag people you want to notify). Then a branch is created associated with the issue.

## Exercise 2:
- Think of one issue that is related to the analysis or detector you are mainly working on.
- Think of a good title that summarizes what the issue is.
- Open an issue in the relevant repository and fill out the provided template.
- Tag one person (who is not the instructor) who's input you would like on this issue.
- Advanced users: Create a branch from the issue using the 'Development' section in the right side bar of the issue.

## How can you use eic-shell with the repositories that you are working on?

## What are the checks that are run on pull requests?

{% include links.md %}
