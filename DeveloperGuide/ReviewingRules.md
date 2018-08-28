# Reviewing, Merging and Declining Pull Requests

Before a patch is merged into an official branch (master or a release branch like 2.1.x, 2.2.x, ...), it needs to be reviewed by a commiter. The reviewer should make sure that the patch merges without conflicts, that it works as expected and that it does not break anything else.

If the reviewer discovers any kind of issue, he should leave a comment in the pull request view of GitHub and let the contributor fix the problem. Reviewer and contributor should work together to fix any problem with the pull requests before it is ready to go into the codebase.

## Reviewing Rules

* Reviews and merges need to be done by committers
* Reviewers should come from a different institution than the contributor
* Feature pull requests are only allowed to be merged into the master branch
* Pull requests that change translation keys are only allowed to be merged into the master branch
* After taking up a review (or being assigned to one), a basic review has to be done within the following 14 days for a bug fix or 21 days for a feature. A basic review means that either some issues should be pointed out or the pull request should be approved
* No pull request shall be without a reviewer for more than 14 days. If no committer is willing to take up the review on their own, the review will be assigned
* Any committer may merge an arbitrary set of *approved* pull requests, even if he is not the official reviewer, given that:
    * The committer sends an announcement to the development list 24 hours in advance, including a list of the pull requests to be merged and no other committer objects to that
    * The committer checks that all the patches are working (which basically means to review the patch set as a whole)
* A reviewer may decline a pull request if issues were pointed out but were neither fixed nor discussed for more than 14 days. It is generally suggested to try to contact the contributor before declining the pull request and to additionally bring the problem up at the technical meeting


## Reviewing a Pull Request

There is no list of things you are required to do as reviewer of a pull request. Our primary goals in doing reviews for all pull requests are to ensure that:

* There are no bugs in the pull request
    * The feature works as advertised
    * It does not break any other features
* There are no obvious legal problems
    * Licensing is fine
* Feature documentation is in place
* An upgrade path exists (usually relevant for database changes)

The exact review process heavily depends on the type, size and purpose of the pull request.

Here are some things a reviewer should usually do:

* Check if the code looks sensible (e.g. no nonsensical files, no obvious formatting errors, no large binary files, …**
** The [CONTRIBUTING.md](CONTRIBUTING.md) file has some guidelines regarding code formatting.
* Locally run Galicaster and verify that the issue has been fixed (as described in the pull request and/or the Github issue) or the feature does what it is supposed to do
* Check the documentation of the new feature
