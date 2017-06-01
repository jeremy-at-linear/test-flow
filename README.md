# test-flow
A test of maintaining a project in git with multiple contributers.

This readme is becoming a place for notes on how the flow works.
We are modeling the flow off of [this article], with some changes.
The examples below assume the project is "test-flow" and the machine that hosts the origin is called "CENTRAL"

## Setup
### Admin
1. Create the repo on Github. 
2. Clone the repo on CENTRAL. This repo is called "origin" because it should be the origin repo for all users
   * `$ git clone https://github.com/jeremy-at-linear/test-flow.git`
3. Share the folder test-flow with read/write permissions so people can access it.
4. Make a "develop" branch
   * `$ cd test-flow`
   * `$ git branch develop`

### User
1. Clone the origin repo
   * `$ git clone //CENTRAL/test-flow`
   * `cd test-flow`
2. Checkout the "develop" branch (users should **never** commit to origin/master)
   * `$ git checkout -b develop origin/develop`

## Workflow
### User
1. Make a topic (feature) branch to work on
   * `$ git checkout -b feature`
2. Work on feature and **[commit often]**.
3. When feature is finished and commited merge into develop
   * `$ git checkout develop`
   * `$ git merge feature`
4. Delete feature branch (if all work is done)
   * `$ git branch -d feature`
5. Do testing to make sure it works
6. Push develop up to origin/develop
   * `$ git push origin`
      1. If someone else has pushed to develop since you checked it out do a pull
         * `$ git fectch origin` <- this may be unnecessary
         * `$ git pull`
      2. If there are conficts they will show up in the file, edit the file to get rid of the conflict and all the <<< === >>> stuff
      3. Merge the changes
         * `$ git -a -m"merge external changes"` <- carefull with -a, it adds everything to the commit
      4. Then do the push again
         * `$ git push origin`
7. Repeat for next feature

### Admin
1. When enough good features are ready in develop make a release branch (in the origin repo)
   * `$ git checkout -b release`
2. Test the release branch and make bugfixes as necessary
3. Merge the bugfixes into origin/develop
   * `$ git checkout develop`
   * `$ git merge release`
   * `$ git checkout release`
   * repeat above until all bugs are gone
4. Merge the release branch into origin/master
   * `$ git checkout master`
   * `$ git merge release`
5. Make a tag from origin/master
   * `$ git tag -a v0.1.0 -m"release version 0.1.0"`
6. Push origin/master up to Github/master
   * `$ git push origin` <- in this case "origin" is the GitHub repo
   * `$ get push origin v0.1.0` <- push the tag (not pushed by default)
7. Delete the release branch
   * `$ git checkout -b release`
8. Repeat for next release

[this article]: http://nvie.com/posts/a-successful-git-branching-model/
[commit often]: https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
