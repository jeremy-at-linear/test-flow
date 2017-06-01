# test-flow
A test of maintaining a project in git with multiple contributers.

This readme is becoming a place for notes on how the flow works.
We are modeling the flow off of [this article][git-flow]. With some changes.

## Setup
### Admin
1. Create the repo on Github. 
2. Clone the repo on a networked machine behind the firewall. This repo is called "origin" because it should be the origin repo for all users
   * `$ git clone https://github.com/jeremy-at-linear/test-flow.git`
3. Make a "develop" branch
   * `$ git branch develop`

### User
1. Clone the origin repo
   * `$ git clone [MACH_NAME]/test-flow`
2. Checkout the "develop" branch (users should **never** commit to origin/master)
   * `$ git checkout -b develop origin/develop`

## Workflow
### User
1. Make a topic (feature) branch to work on
  * `$ git checkout -b [FEATURE]`
2. Work on feature and commit often.
3. When feature is finished and commited merge into develop
4. Delete feature branch (if all work is done)
5. Do testing to make sure it works
6. Push develop up to origin/develop
7. Repeat

### Admin
1. When enough good features are ready in develop make a release branch (in the origin repo)
2. Test the release branch and make bugfixes as necessary
3. Merge the bugfixes into origin/develop
4. Merge the release branch into origin/master
5. Make a tag from origin/master
6. Push origin/master up to Github/master
7. Delete the release branch
8. Repeat

[git-flow]: http://nvie.com/posts/a-successful-git-branching-model/
