###################
Change Transparency
###################

TODO: This needs to be given an OEP number if it remains as an OEP/

Abstract
********

Developers should describe the changes they make.  This information is valuable to many audiences: deployers, integrators, end-users, operators, and so on. Developers are in the best position to accurately describe the motivations, substance, and implications of their work.


Motivation
**********

Goals
=====

We propose a few ways to make it easy for developers to describe the changes they make to software.  The nearer to the change that information is captured, the easier it will be to write, and the more accurate it will be.  Changes made by developers are consumed by many people.  The more the developer can explain the change, the more easily the change will be understood and used, and the more efficient the overall development process will be.


Audiences
=========

When describing changes, it helps to consider the diverse audiences who will be using the information:

- Engineers reviewing the change.

- Course teams using the updated code once it is deployed.

- Other engineers when upgrading dependencies.

- Other engineers when trying to understand the history of a component.

- The edX SRE team when understanding how to help deploying code.

- Open edX operators, when upgrading their installations, re-applying their own patches, or developing their own deployment systems.

- Open edX developers, when learning how to update their use of a component.

- Support teams, when giving guidance to learners or instructors.

- Authors of release notes.

- People writing documentation or support guidance for learners/educators/administrators using the edx.org site, or other Open edX sites.


Information Needed
==================

These are the types of information needed when describing changes.  In general, it is fine to link to information rather than copy it.

- Describe the change.  What is new, what has been removed?  

- Describe why the change was made. This can help people understand the implications, or reconstruct the logic behind the change.

- If there are existing issues, Jira tickets, or supporting discussion elsewhere, provide links. The more information the better.  Often there are details in these discussions that can deepen the understanding of the change, or the reason for the change.

- Breaking changes should describe what feature or compatibility has been lost, and should be clearly labeled as a breaking change.  What replaces the lost behavior? What updates do consumers of the change need to make?
  
- User impact: what user roles are affected by this change, and how? This simple categorization helps people looking through changes for ones that might affect them.

- Testing instructions. These are primarily intended to speed up the review cycle, avoiding the reviewer wasting time trying to infer the steps to test from the description. Instructions can also be useful for later reference if a future developer is researching regression. Writing step-by-step instructions may also help the developer to remember details they had overlooked.

- Specialized concerns:

  - Are there deprecations?

  - Are there database migrations?

  - Does the change affect security or accessibility?


Features
--------

For feature changes, changes should also be accompanied by:

- Description of how to use the feature. 

- For UI changes, screenshots are immensely helpful.

- Are there configuration changes or settings needed? Describe them.


Bug Fixes
---------

Bug fix changes should also include:

- Describe the problem you are fixing.  It should be detailed enough that a reader can determine if they are encountering the problem. "Fix registration" is not sufficient.


Reverts
-------

If a change is a revert of a previous change, describe why it needed to be reverted.  Often reverts happen under time pressure.  It is fine to update the change description after the fact.


Chores
------

Generally, chores such as internal refactoring, requirements updates, removing unused code, and so on, do not need to be described beyond a simple git commit message.


Specification
*************

Developers can provide change information in a number of ways.


Conventional Commits
====================

`Conventional Commits`_ (also known as semantic commits) is "a specification for adding human and machine readable meaning to commit messages." It's a style of writing Git commits that encodes useful information about the commit in a structured shorthand.

.. _Conventional Commits: https://conventionalcommits.org

The advantages of conventional commits:

- Structured messages can be used by tools to aggregate change information.

- Structured messages can be checked automatically by conformance tools.

Gaps in conventional commits:

- Git commit messages are rarely longer than one line.  Focusing on conventional commits can miss an opportunity to encourage richer information about changes.


Pull Request Descriptions
=========================

A pull request description is a good place to put the change description.  In addition, there is information to help the review:

- Merge deadline: is there a particular deadline for merging the change?

- Suggested reviewers, either people or teams.


Changelogs
==========

A changelog file is "a curated, chronologically ordered list of notable changes for each version of a project."  

TK


GitHub Releases
===============

GitHub Releases are popular as places to find out what has changed in a project.  We recommend that they be produced from other information rather than being created and edited directly.

TK

Related Documents
*****************

These are documents which are related, or perhaps obsoleted, by this document:


`OEP-47: Semantic Versioning`__

__ https://open-edx-proposals.readthedocs.io/en/latest/oep-0047-bp-semantic-versioning.html

`Draft OEP-40: Git Best Practices`__

__ https://github.com/edx/open-edx-proposals/pull/121

`Draft OEP-44: Changelogs`__

__ https://github.com/edx/open-edx-proposals/pull/140

`Changelogs`__ in the Open edX wiki.

__ https://openedx.atlassian.net/wiki/spaces/AC/pages/1776877820/ChangeLogs
