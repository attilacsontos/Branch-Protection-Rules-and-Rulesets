# GitHub Branch Protection Rules

## 1.	Protected branches

You can protect important branches by setting branch protection rules, which define whether collaborators can delete or force push to the branch. (Source: [**About protected branches**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches))

## 2.	Branch Protection Rules

You can enforce certain workflows or requirements before a collaborator can push changes to a branch in your repository, including merging a pull request into the branch, by creating a branch protection rule. Actors may only be added to bypass lists when the repository belongs to an organization.

By default, each branch protection rule disables force pushes to the matching branches and prevents the matching branches from being deleted. You can optionally disable these restrictions and enable additional branch protection settings.

You can create a branch protection rule in a repository for a specific branch, all branches, or any branch that matches a name pattern you specify with fnmatch syntax. 

**For each branch protection rule, you can choose to enable or disable the following settings:**

1.	Require pull request reviews before merging
2.	Require status checks before merging
3.	Require conversation resolution before merging
4.	Require signed commits
5.	Require linear history
6.	Require merge queue
7.	Require deployments to succeed before merging
8.	Lock branch
9.	Do not allow bypassing the above settings
10.	Restrict who can push to matching branches
11.	Allow force pushes
12.	Allow deletions

A YouTube video on [**How to set up a branch protection rule?**](https://www.youtube.com/watch?v=hQZ2Bm1GhTE)

You can create a branch protection rule in three simple steps:
![](http://hdoc.csirt-tooling.org/uploads/upload_86a826016b9fa4197efba19f7587f2bc.png)

### 2.1.	Require pull request reviews before merging

Repository administrators or custom roles with the "edit repository rules" permission can require that all pull requests receive a specific number of approving reviews before someone merges the pull request into a protected branch. You can require approving reviews from people with write permissions in the repository or from a designated code owner.

If you enable required reviews, collaborators can only push changes to a protected branch via a pull request that is approved by the required number of reviewers with write permissions. *(I think we need this but need to discuss how many reviewers should check the changes).*

If a person with admin permissions chooses the Request changes option in a review, then that person must approve the pull request before the pull request can be merged. If a reviewer who requests changes on a pull request isn't available, anyone with write permissions for the repository can dismiss the blocking review.

### 2.2.	Require status checks before merging

Required status checks ensure that all required CI tests are either passing or skipped before collaborators can make changes to a protected branch. Required status checks can be checks or statuses. For more information, see "[**About status checks**](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks)."

### 2.3.	Require conversation resolution before merging

Requires all comments on the pull request to be resolved before it can be merged to a protected branch. This ensures that all comments are addressed or acknowledged before merge. (*Probably this is what we want?*)

### 2.4.	Require signed commits

When you enable required commit signing on a branch, contributors and bots can only push commits that have been signed and verified to the branch. For more information, see "**[About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)**." (*I do not think we need this*)

### 2.5.	Require linear history

Enforcing a linear commit history prevents collaborators from pushing merge commits to the branch. This means that any pull requests merged into the protected branch must use a squash merge or a rebase merge. (*I do not think we need this*)

### 2.6.	Require merge queue

A merge queue helps increase velocity by automating pull request merges into a busy branch and ensuring the branch is never broken by incompatible changes.

The merge queue provides the same benefits as the Require branches to be up to date before merging branch protection, but does not require a pull request author to update their pull request branch and wait for status checks to finish before trying to merge.

Using a merge queue is particularly useful on branches that have a relatively high number of pull requests merging each day from many different users. (*I do not think we need this*)

### 2.7.	Require deployments to succeed before merging

You can require that changes are successfully deployed to specific environments before a branch can be merged. For example, you can use this rule to ensure that changes are successfully deployed to a staging environment before the changes merge to your default branch. (*I do not think we need this*)

### 2.8.	Lock branch

Locking a branch will make the branch read-only and ensures that no commits can be made to the branch. Locked branches can also not be deleted. (*it is good to know that there is a feature like this*)

### 2.9.	Do not allow bypassing the above settings

By default, the restrictions of a branch protection rule do not apply to people with admin permissions to the repository or custom roles with the "bypass branch protections" permission in a repository. You can enable this setting to apply the restrictions to admins and roles with the "bypass branch protections" permission, too.

### 2.10.	Restrict who can push to matching branches

When you enable branch restrictions, only users, teams, or apps that have been given permission can push to the protected branch. You can view and edit the users, teams, or apps with push access to a protected branch in the protected branch's settings.

When status checks are required, the people, teams, and apps that have permission to push to a protected branch will still be prevented from merging into the branch when the required checks fail. People, teams, and apps that have permission to push to a protected branch will still need to create a pull request when pull requests are required.

You can only give push access to a protected branch, or give permission to create a matching branch, to users, teams, or installed GitHub Apps with write access to a repository. People and apps with admin permissions to a repository are always able to push to a protected branch or create a matching branch.

### 2.11.	Allow force pushes

By default, GitHub blocks force pushes on all protected branches. When you enable force pushes to a protected branch, you can choose one of two groups who can force push:
1.	Allow everyone with at least write permissions to the repository to force push to the branch, including those with admin permissions.
2.	Allow only specific people or teams to force push to the branch.  
(*I do not think we need this*)

### 2.12.	Allow deletions

By default, you cannot delete a protected branch. When you enable deletion of a protected branch, anyone with at least write permissions to the repository can delete the branch.
Note: If the branch is locked, you cannot delete the branch even if you have permission to delete it. (*I do not think we need this*)

## 3.	Managing Branch Protection Rules

After enabling required status checks, all required status checks must pass before collaborators can merge changes into the protected branch. After all required status checks pass, any commits must either be pushed to another branch and then merged or pushed directly to the protected branch. (*I am not sure we want that*)
(Source: [**Managing a branch protection rule**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule))

## 4.	About Rulesets

****Rulesets help you to control how people can interact with branches and tags in a repository. A ruleset is a named list of rules that applies to a repository****. You can have up to 75 rulesets per repository.
(Source: **[About Rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets)**)

When you create a ruleset, you can allow certain users to bypass the rules in the ruleset. This can be users with a certain role, such as repository administrator, or it can be specific teams or GitHub Apps. For more information about granting bypass permissions, see "[**Creating rulesets for a repository**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository#granting-bypass-permissions-for-your-ruleset)."

### 4.1.	Branch and tag rulesets

You can create rulesets to control how people can interact with selected branches and tags in a repository. You can control things like who can push commits to a certain branch, or who can delete or rename a tag. 

For example, you could set up a ruleset for your repository's feature branch that requires signed commits and blocks force pushes for all users except repository administrators. For each ruleset you create, you specify which branches or tags in your repository the ruleset applies to.

### 4.2.	About rulesets, protected branches, and protected tags

Rulesets work alongside any branch protection rules and tag protection rules in a repository. 

**Rulesets have the following advantages over branch and tag protection rules.**

* Unlike protection rules, multiple rulesets can apply at the same time, so you can be confident that every rule targeting a branch or tag in your repository will be evaluated when someone interacts with that branch or tag. For more information, see "[**About rule layering**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets#about-rule-layering)."
* Rulesets have statuses, so you can easily manage which rulesets are active in a repository without needing to delete rulesets.
* Anyone with read access to a repository can view the active rulesets for the repository. This means a developer can understand why they have hit a rule, or an auditor can check the security constraints for the repository, without requiring admin access to the repository.
* You can create additional rules to control the metadata of commits entering a repository, such as the commit message and the author's email address. For more information, see "**[Available rules for rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets#metadata-restrictions)**" in the GitHub Enterprise Cloud documentation.

## 5.	Creating rulesets for a repository

You can add rulesets to a repository to control how people can interact with specific branches and tags.

You can create rulesets to control how users can interact with selected branches and tags in a repository. You can control things like who can push commits to a certain branch and how the commits must be formatted, or who can delete or rename a tag. You can also prevent people from renaming repositories.

You can also create push rulesets to block pushes to a private or internal repository and the repository's entire fork network. Push rulesets allow you to block pushes based on file extensions, file path lengths, file and folder paths, and file sizes.

### 5.1.	Creating a branch or tag ruleset

1.	On GitHub.com, navigate to the main page of the repository.
2.	Under your repository name, click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.
3.	In the left sidebar, under "Code and automation," click Rules, then click Rulesets.
4.	Click New ruleset.
5.	To create a ruleset targeting branches, click New branch ruleset.
6.	Alternatively, to create a ruleset targeting tags, click New tag ruleset.
7.	Under "Ruleset name," type a name for the ruleset.
8.	Optionally, to change the default enforcement status, click  Disabled  and select an enforcement status. For more information about enforcement statuses, see "**[About rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets#using-ruleset-enforcement-statuses)**."

![](http://hdoc.csirt-tooling.org/uploads/upload_b18982787b99d492de6c951689543e3f.png)


This is how I can create rulesets for the project OSD4ISO:

![](http://hdoc.csirt-tooling.org/uploads/upload_777170280d8fe182028e3bfc4d21eac3.png)

### 5.2.	Granting bypass permissions for your branch or tag ruleset

You can grant certain roles, teams, or apps bypass permissions for your ruleset. 

1.	To grant bypass permissions for the ruleset, in the "Bypass list" section, click  Add bypass.
2.	In the "Add bypass" modal dialog that appears, search for the role, team, or app you would like to grant bypass permissions, then select the role, team, or app from the "Suggestions" section and click Add Selected.
3.	Optionally, to grant bypass to an actor without allowing them to push directly to a repository, to the right of "Always allow," click , then click For pull requests only.

OSD4ISO:

![](http://hdoc.csirt-tooling.org/uploads/upload_2825833d6f7e1c4d0d80ef7cdbcac274.png)

### 5.3.	Choosing which branches or tags to target

To target branches or tags, in the "Target branches" or "Target tags" section, select **Add a target**, then select how you want to include or exclude branches or tags. You can use fnmatch syntax to include or exclude branches or tags based on a pattern. For more information, see "[**Using fnmatch syntax**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository#using-fnmatch-syntax)." 

In case of the project OSD4ISO, the settings are as follows:

![](http://hdoc.csirt-tooling.org/uploads/upload_f01f5cc0188b40fbedb11a16d2442542.png)

### 5.4.	Selecting branch or tag protections

In the "Branch protections" or "Tag protections" section, select the rules you want to include in the ruleset. When you select a rule, you may be able to enter additional settings for the rule. For more information on the rules, see "**[Available rules for rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets)**."

### 5.5.	Finalizing your branch or tag ruleset and next steps

To finish creating your ruleset, click Create. If the enforcement status of the ruleset is set to "Active", the ruleset takes effect immediately.

### 5.6.	Creating a push ruleset

Push rulesets are in beta and subject to change.
This ruleset will enforce push restrictions for this repository's entire fork network.


The collaborator can make changes in the main brach: this can be very dangerous (since main is like your ’production’ environment). That is why we need to implement a ruleset: **[How to Add Collaborator to Repository in GitHub? | Importance Of GitHub Branch Protection Rules](https://www.youtube.com/watch?v=UoWKo6Kcnis)**

Adding a collaborator is a reposit-level change (the collaborator has access to the whole repo).

’**Require a pull request before merging**’ – when enabled all commits must be made to a bon-proteted branch and submitted via a pull request before they can be merged into a branch that matches this rule.

’**Do not allow bypassing the above settings**’ – there is no exclusion of any of the rulests: even the repo admin should obey the rules (and create pull request) to be able to edit the master branch (or the protected branch).
