---
title: "Using GitHub with EIC Software"
teaching: 10
exercises: 5
---

::::::::::::::::::::::::::::::::::::::::::: questions

- How do we use GitHub within the EIC community?

:::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::: objectives

- Several repositories contain the key geometry, simulation, reconstruction, and analysis software.
- Working with repositories requires membership of the EIC organization on GitHub.
- Issue reports and pull requests are ways to collaborate virtually on collaboration software tools.

:::::::::::::::::::::::::::::::::::::::::::

## How do I get added to @eic organization on GitHub?

In order to contribute, you need your GitHub account to be a member of the [EIC organization](https://github.com/eic) on GitHub. If it is not, follow the [getting-started instructions](https://eic.github.io/documentation/getstarted).

## Where are repositories located?

The main repositories are located on two locations:

- the GitHub service contains most user-facing repositories: <https://github.com/eic>.
- the eicweb GitLab server contains mainly continuous integration infrastructure: <https://eicweb.phy.anl.gov/EIC>.

We will use GitHub as the main code repository tool. The top of the [github.com/eic](https://github.com/eic) page has several 'pinned' repositories that are most important. You can also see where most activity is happening based on the ordering of the repositories in the list.

You can 'watch' repositories to be notified of activity. This is helpful if you wish to remain up-to-date on the activity. You can 'star' repositories as another way to find them easily.

::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise 1

- Verify that you are a member of the EIC organization on GitHub: Do you see the members-only page with the grid of software meetings? If not, see previous section.
- Check which teams you are in: Enter the search terms "members:me" into the search box in the Teams tab to see only the teams you are a member of. If you are not in ePIC Devs, request to be added at <https://github.com/orgs/eic/teams/epic-devs>.
- Choose one repository to subscribe to, at some level of activity.

::::::::::::::: solution

If you can see the members-only page you are in the organization. The Teams tab with the
`members:me` filter shows your teams; if `ePIC Devs` is missing, request to join. Use the
"Watch" / "Star" buttons on a repository to subscribe.

:::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::

## What is the proper way to work with these repositories?

Duplication of work is avoided when everyone knows what is going on.

1. A typical workflow starts from the creation of an **issue** with a feature request or a bug report. This happens in the browser on the github repository site. When creating the issue, feel free to tag people you want to notify.
1. Create a branch that includes the issue number in the name. This can be done from the browser or command line as `git checkout -b issue123`
1. Edit and work on your branch. When you are ready, you can commit your changes to the branch.
1. If you are ready to merge your branch into the main repository, you can generate a **pull request** from the browser. You can assign a reviewer at this stage and add information in the Write box that explains the changes made. If your work is not yet completed, you can utilize the Draft PR.
1. Once you've generated a pull request, continuous integration tests are run to ensure compatibility. The reviewer will approve the changes, merging your code into the main branch.
1. After the pull request is approved and the code is merged, you can delete your branch using the browser or via the command line.

A good example of the above workflow is shown in detail in the [JANA2 contributing tutorial](https://eic.github.io/tutorial-jana2/05-contributing/index.html) for the EICrecon repository.

::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise 2

- Think of one issue that is related to the analysis or detector you are mainly working on.
- Think of a good title that summarizes what the issue is.
- Open an issue in the relevant repository and fill out the provided template.
- Tag one person (who is not the instructor) whose input you would like on this issue.
- Advanced users: Create a branch from the issue using the 'Development' section in the right side bar of the issue.

::::::::::::::: solution

A good issue has a specific, searchable title and a filled-in template describing the problem and
expected behaviour. Tagging a relevant person with `@username` notifies them. The issue's
"Development" sidebar can create a linked branch you can then check out locally.

:::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::

## How can you use eic-shell with the repositories that you are working on?

`eic-shell` already contains all of the compilers and dependencies (ROOT, DD4hep, Geant4, ACTS, podio, and more) that the EIC repositories build against, so you do not have to install any of them yourself. Because your home directory and the current working directory are shared between the host and the container, the typical development loop is:

1. Clone the repository on your host system, e.g. `git clone https://github.com/eic/EICrecon`.
2. Start `eic-shell` from a directory that contains your clone, so the source tree is visible inside the container.
3. Configure and build **inside** `eic-shell` with the repository's build instructions (usually `cmake` followed by `cmake --build`). Because the build uses the container's dependencies, your result matches the standard environment used for productions and continuous integration.
4. Edit the code with your usual editor on the host, then rebuild inside `eic-shell` — no need to copy files back and forth.

The [Reconstruction framework tutorial](https://eic.github.io/tutorial-jana2/) walks through building and running EICrecon inside `eic-shell` in detail.

## What are the checks that are run on pull requests?

When you open a pull request, continuous-integration (CI) jobs run automatically, and the PR must pass them and receive at least one review from a collaborator before it can be merged. The recommended workflow and the full set of requirements for EICrecon are documented in the [EICrecon contribution guidelines](https://github.com/eic/EICrecon/blob/main/CONTRIBUTING.md). A pull request is ready to be reviewed when:

- a detailed description of the change is provided,
- all CI jobs pass (build and tests),
- `clang-format` and `clang-tidy` have been run locally (code style and static checks),
- the commit history is legible (small, self-contained commits with descriptive messages),
- the code is appropriately documented.

The reviewer then checks that the code is maintainable and scalable, that it is correct with respect to physics requirements, and that any changes in physics or computing performance (the benchmarks) are understood.

::::::::::::::::::::::::::::::::::::::::::: keypoints

- We use several tools on GitHub to ensure we keep the overview of who does what work.
- `eic-shell` provides the dependencies to build the EIC repositories; clone on the host and build inside the container.
- Every pull request must pass CI (build, tests, `clang-format`/`clang-tidy`) and receive a review before merging — see the [EICrecon contribution guidelines](https://github.com/eic/EICrecon/blob/main/CONTRIBUTING.md).

:::::::::::::::::::::::::::::::::::::::::::
