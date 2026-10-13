---
title: 'What happens after submitting a recipe PR'
lastUpdated: 2026-10-13T00:00:00Z
description: "How aerynOS builds, publishes, and promotes a recipe after its pull request is merged"
sidebar:
  order: 11
license: "CC-BY-SA-4.0"
copyright: "Copyright © 2025 aerynOS Developers"
---

# What happens after submitting a recipe PR

Opening a pull request is the start of the review and build process. The following steps explain what happens after a recipe PR is accepted and how to follow its progress.

## 1. The pull request is reviewed and merged

Maintainers review the recipe, its metadata, and the pull request checks. If changes are needed, respond to the review before the pull request is merged. Once the pull request is merged into the recipes repository, the build infrastructure can process the recipe.

## 2. The recipe is built

The build system discovers the merged recipe and adds it to the build queue. A recipe may wait for its build dependencies before the build starts. The build produces the package and its build records; a failed build remains visible in the build dashboard so that the failure can be investigated.

You can follow the build at [dash.aerynos.dev](https://dash.aerynos.dev/). Use the dashboard to find the recipe, check whether it is queued or running, and open the build log when a build fails.

## 3. The package is published to the volatile repository

After a successful build, the package is published to the **volatile** repository. This repository is where newly built packages are made available first, while they are being tested. The [basic packaging workflow](/packaging/workflow/basic-workflow/) explains how packagers can configure a local repository and test packages from the volatile stream.

Publication can take a little time when the build queue contains dependency chains. If the package is not visible yet, check the dashboard for pending or blocked builds before reporting a problem.

## 4. The package moves to the stable repository

After the package has been tested in the volatile repository, the maintainers synchronise the tested state to the **stable** repository. This promotion is a repository maintenance step; contributors do not need to open another pull request for it.

The package therefore follows this path:

```text
merged recipe PR
      ↓
build queue and dependency builds
      ↓
volatile repository
      ↓
stable repository
```

For the background on the repository streams, see the [aerynOS repository model](/aerynos/philosophy/).