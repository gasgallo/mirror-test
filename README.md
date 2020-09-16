# MR playground

Playground for MRs.

Worflow adopted: https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

## Process
- create a new branch
- work on the new branch
- create a MR
- review a MR
- merge a MR

### Create a new branch
Always create a new branch from `develop` for features, bug fixes or releases. The only exception is when working on a hotfix, in that case, the new branch must be created from `master`.

### Work on the new branch
Do what you have to do with the code/files and make sure to commit them to the new branch.

### Create a MR
A MR can be created at anytime after the new branch has been created, but there are mainly 2 scenarios:
- MR created before code is ready
- MR created after code is ready

#### MR created before code is ready
Append to the title `WIP` or `Draft`, so that it's clear that the work is not finished yet. And then same as [Both scenarios](https://gitlab.com/-/ide/project/rgall/mr-playground/tree/docs/readme/-/README.md/#both-scenarios).

#### MR created after code is ready
Same as [Both scenarios](https://gitlab.com/-/ide/project/rgall/mr-playground/tree/docs/readme/-/README.md/#both-scenarios).

#### Both scenarios

##### Title
The title is very important because it will become the commit message when the MR will be merged. Thus follow a convention in common with the whole team/company:
- Feature: add support for xxxx
- Chore: update dependencies
- Doc: improve documentation
- Bug: fix issue xxxx
- Hotfix: fix xxxxx

##### MR templates
It's good practice to use templates for each MR type so that reviewee and reviewer have a standard checklist to go through when creating or reviewing a MR.

Example: https://gitlab.com/sertiscorp/mle/misc/gitlab-description-templates

##### MR description
If using a template, then fill the template.

If not using a template, then describe the issue/feature/etc, what have been changed and why, how the code has been tested and any other useful information for the reviewer.

##### Target branch
Make sure the target branch is always `develop` or `master` in case of a `hotfix`.

##### Optional features
Gitlab provides 2 features that can be enabled when merging a MR:
- delete source branch
- squash commits

I personally suggest to enable both, so that the project graph [here](https://gitlab.com/rgall/mr-playground/-/network/master) is kept more tidy and readable on the long term.

##### Assignee
You must assign someone to review your MR before merging, otherwise it doesn't make any sense to create a MR at all. Assign yourself is forbidden!

Usually, it's better to assign someone that has at least a bit of knowledge about the project, but it's not necessary having an in-depth understanding of the whole repo, especially becasue each MR should be small enough in content that almost anyone should be able to do the review.

##### Labels and milestone
It's also possible to set some labels and milestones to make it easier to organize MRs. Some examples are:
- labels, e.g. chore, feature, doc, bug, hotfix
- milestone, e.g. new_face_detector, new_release, etc

### Review a MR
If you're assigned to review a MR, you're responsible for the content of the MR itself as much as the reviewee, thus make sure that the code is actually working and all the checks in the MR template checklist are checked before giving your approval.

#### How to review
Use the `changes` tab of the MR to go through the changes introduced by the new code and check for any bug/mistake/inconsistency. When you find something, use the inline comment functionality to report the issue and create a review (use the `suggest code` mode when possible). If the comment is generic, then you can leave it on the `overview` tab of the MR.

Things to check before approving a MR:
- code design is good and consistent with code styles
- tests pass and coverage is high enough (e.g. 80%)
- readability is good and there are enough comments
- documentation is updated
- security and privacy are taken into consideration
- if a CI/CD pipeline is present, then it must run successfully

#### How to approve
Simply comment in the `overview` tab of the MR and let the reviewee know that everything looks good.

```
@mate LGTM, feel free to merge!
/approve
```

### Merge a MR
Once the MR has been approved, you should feel confident about merging your new feature/fix into `develop`.

#### One last check
Make sure that `develop` isn't ahead of your branch by any commits because, in that case, merging could cause conflicts and we don't want that to happen.

Check in the project graph (or check near the `Merge` button) if someone else merged new code to `develop` after you created your branch from it. If that's the case, then use the command line to merge the latest `develop` into your branch:

```bash
cd my_awesome_project
git fetch
git checkout develop
git pull
git checkout my_new_branch
git merge develop
```

If the merge process doesn't complete because of some conflicts, that's good! We just avoided fixing conflicts on `develop`. Fix the conflict on your branch and commit them. Now your branch is up-to-date with the latest `develop` and it's ready the be merged.

#### Finally
You can merge the new branch to the target branch simply by clicking on the gree `Merge` button in the `overview` tab of the MR.

After merging, make sure `develop` branch is not broken and the pipeline succeeds.



