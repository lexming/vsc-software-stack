# VSC Software Stack

Central repository of easyconfigs and easyblocks used in the software installations on VSC clusters.

## Vrije Universiteit Brussel (site-vub) branch

### Policy

* Unreviewed branch with software installed in VUB clusters

* Push easyconfigs of software that has not yet been contributed upstream

## Repository structure

The organization of this repo is structured in standard git branches, each one
providing a different degree of reliability:

* [`vsc`](https://github.com/vscentrum/vsc-software-stack/tree/vsc): main branch
  with software installations validated and tested by multiple VSC sites
* [`site-kul`](https://github.com/vscentrum/vsc-software-stack/tree/site-kul):
  software installations specific to clusters managed by KU Leuven
* [`site-ua`](https://github.com/vscentrum/vsc-software-stack/tree/site-ua):
  software installations specific to clusters managed by UAntwerp
* [`site-ugent`](https://github.com/vscentrum/vsc-software-stack/tree/site-ugent):
  software installations specific to clusters managed by UGent
* [`site-vub`](https://github.com/vscentrum/vsc-software-stack/tree/site-vub):
  software installations specific to clusters managed by VUB
* [`wip`](https://github.com/vscentrum/vsc-software-stack/tree/wip): software
  installations on any site that are work-in-progress

## Bootstrap

Users of this repo are encouraged to work with git worktrees. This approach
allows to have all easyconfigs available in the VSC Software Stack across all
its branches under a single folder in your local system.

1. Create a new folder for this repo
   ```bash
   $ mkdir vsc-software-stack
   ```
2. Clone the bare repository (we keep it in a hidden folder as it won't be used
   directly)
   ```bash
   $ git clone --bare git@github.com:vscentrum/vsc-software-stack.git vsc-software-stack/.bare
   ```
3. Point git to the bare repo already from the root folder
   ```bash
   $ echo "gitdir: ./.bare" > vsc-software-stack/.git
   ```
4. Add worktrees for each branch in their own folder
   ```bash
   $ cd vsc-software-stack
   $ git worktree add vsc
   $ git worktree add wip
   ```

## Commits with worktrees

Pushing/pulling changes in worktrees is no different than in a regular repo. As
soon as you change directory into a worktree folder, you can work as if you
were on a regular repo. There will be an active branch, you can create/checkout
other branches and commit to any branch as usual.

### Unreviewed branches

Branches such as `wip` or the `site-*` branches do not require PRs and reviews
to push changes.

1. Enter the target worktree/branch
   ```bash
   $ cd vsc-software-stack/wip
   ```
2. Fetch updates in this branch from remote repository
   ```bash
   $ git fetch origin
   $ git pull origin wip
   ```
3. Add and commit the files affected by this change
   ```bash
   $ git add 000_example/example.eb
   $ git commit -m "adding WIP easyconfig example.eb"
   ```
4. Push new commit to remote branch in vsc-software-stack repo
   ```bash
   $ git push origin wip
   ```

### Reviewed branches

The `vsc` branch requires a PR and a positive review (+ working test report) to
merge changes into it. PRs should be open from a fork of the vsc-software-stack
repo.

In the following we assume the following names for the remote repos:
* `origin`: vsc-software-stack repo in vscentrum
* `personal`: your fork of vsc-software-stack

1. Enter the target worktree/branch
   ```bash
   $ cd vsc-software-stack/vsc
   ```
2. Fetch updates in this branch from remote repository
   ```bash
   $ git fetch origin
   $ git pull origin vsc
   $ git push personal vsc
   ```
3. Create a new local branch to work on the changes
   ```bash
   $ git checkout -b 000_example
   ```
4. Add new easyconfigs from another worktree
   ```bash
   $ cp ../wip/000_example/example.eb e/example/example.eb
   ```
5. Add and commit the files affected by this change
   ```bash
   $ git add e/example/example.eb
   $ git commit -m "adding easyconfig example.eb"
   ```
6. Push local branch to your fork of the vsc-software-stack repo
   ```bash
   $ git push personal 000_example
   ```
7. Create a new PR in GitHub from the branch `000_example` in your fork of the
   vsc-software-stack to the `vsc` branch in the main vscentrum repo.

## Links

* EasyBuild documentation: https://docs.easybuild.io
* EasyBuild tutorial: https://easybuild.io/tutorial
* VSC Slack: https://vscentrum.slack.com
  * Recommended to use the `#software` channel.
  * Requires invitation, ask Kenneth (HPC-UGent) or Sam (VUB-HPC), or anyone already in the VSC Slack.
