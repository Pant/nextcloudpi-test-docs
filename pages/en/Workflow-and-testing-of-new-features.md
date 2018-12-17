---
title: Workflow and testing of new features
keywords: maintain testing development ncp-update branches
tags: [maintain, testing, development, ncp-update, branches]
#summary: ""
sidebar: en_sidebar
sidebar_folder: 'Maintain'
language: 'en'
permalink: en_Workflow-and-testing-of-new-features.html
folder: en
---

Updates run by `ncp-update` take the latest version from the `master` branch of the repo.

These features need to be well tested in order to be merged to that branch. The typical workflow is

- Create a feature in a local separate branch
- Create a Pull Request to the `devel` branch
- Test the `devel` branch
- Merge into `master`

In order to test the `devel` or any other branch, the tester can do the following

- Start a fresh instance of the SD card image on a testing board, or QEMU
- Run `sudo ncp-update devel`
- Test

This command will bring your system to the `devel` brach. In case we decided to keep a separate branch for this feature, say `feature_1`, we could test it with

```
# ncp-update feature_1
```

After we have verified that everything works as intended we can merge into `master`
