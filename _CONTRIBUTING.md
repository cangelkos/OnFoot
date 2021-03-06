# Contributing

## Team Green-Dream's General Mistake-Proof-Spread-the-Pain-Out-So-It-Doesn't-Hit-You-All-At-Once™ Git Workflow

• Make sure all members of the team are STARTING from the correct local version of the Master. 

`git pull` to pull down the master. 

• Cut a namespaced feature branch from the master for the feature or bug you're going to be working on. If your team is using GitHub's Project Issue Tracker, create a new issue in the GUI and add the issue or bug number in your branch name. For example: 

`#74-procfile-port-variable` or `bug-#65-distance-list-view`
  
• Make sure you are working on the correct local branch. Type `git branch`. The branch you're working on should be green.

• Make commits to that feature branch. Code code code, work work work. `git add .` and `git commit -m "<your commit notes in quotes here>"`. Be descriptive in your commit notes. 

• Does your feature work? Test it in the browser. 

• IMPORTANT: AT EVERY COMMIT, YOU WILL BE REBASING. If your feature works or your bug is fixed, commit your changes. After you commit, SWITCH TO THE MASTER. 

`git checkout master`

If you type `git branch`, master should be green. ONCE ON THE MASTER, DO NOT COMMIT. The goal here is to make sure your local master is up to date with the rest of the team's. This way, the master stays pure. 

• `git pull` - there should be no merge conflicts.

• NOW, SWITCH BACK TO YOUR BRANCH. 

`git checkout <your-cool-branch-name>`

• REBASE ANY UPSTREAM CHANGES INTO YOUR BRANCH:

`git pull --rebase origin master`

Merge any changes on the master with the local branch you've been working on. See #10 below.

• CONFLICTS: In the terminal, if there are conflicts between your local feature/bug branch and the master, you'll see the word `CONFLICT` in all-caps with a reference to where you can find it in your code.

Many people use XCode or another mergetools product at this point. Our team finds that it's easiest simply to open up your code editor, and look for the HEAD of the CONFLICT in your code. It will be a super long number. The new stuff from the master will be on top. If you've been diligent in rebasing at every commit, this step should be pretty easy. If you've been working on your own for a while, it may be the case that you'll need to discuss with a team mate how best to "braid" your most recent changes into hers.

• Save your code editor file and switch back to the Terminal. ADD BUT DO NOT COMMIT.

`git add .`

• Continue the rebase process.

`git rebase --continue`

• You'll continue to make changes in your editor, saving, and adding (but not committing), and typing 

`git rebase --continue`

until there are no longer any changes to merge.

• Once you're finished merging your changes, push your changes onto the remote branch.

`git push origin <your-cool-branch-name>`

• Now it's time to make a Pull Request. Did your feature break the project, or does it still work? Make sure you know the answer to this question. Now navigate to GitHub, and submit a pull request directly to the master. Have another member of the team approve or reject the changes.

• Once the Pull Request is approved, every member of the team will checkout to the master branch and pull those changes down:

`git checkout master`

and then

`git pull`

• You're now back at step 1. Create a new issue, cut a new branch, and continue.

### API Keys and Database Config

You're going to need a few. There are *three* Google Maps API keys required: one for maps, one for directions, and one to use the photos in Google maps. The current version of the app requires keys for those Google Maps API endpoints and keys for hooking into the Facebook API for the authentication layer. There are a couple of links below for how to include your MongoDB URL credentials to hook up to the database and adding config vars to Heroku. If using MongoDB, we recommend mLab. The first url in the object below is the actual Google Maps search url. You can leave that url as-is (unless you decide to change the search filter). Here's the structure of our config file. (/path/to/your/app/server/env/config.js):

```
module.exports = {
  url : 'https://maps.googleapis.com/maps/api/place/nearbysearch/json?radius=1500&types=restaurant%7Cgas_station%7C&sensor=false',
  mapKey : 'API KEY HERE',
  dbUrl: 'mongodb://(username):(password).mlab.com:17348/(database-name)',
  imageKey: 'API KEY HERE',
  directionKey: 'API KEY HERE',
    facebook:{
      clientID: 'API KEY HERE',
      clientSecret: 'API KEY HERE',
      callbackURL: 'http://127.0.0.1:4040/auth/facebook/callback'
    }
}

```
https://devcenter.heroku.com/articles/mongolab#getting-your-connection-uri
https://devcenter.heroku.com/articles/facebook
http://docs.mlab.com/connecting/


### Guidelines

1. Uphold the current code standard:
    - Keep your code [DRY][].
    - Apply the [boy scout rule][].
    - Follow [STYLE-GUIDE.md](STYLE-GUIDE.md)
1. Run the [tests][] before submitting a pull request.
1. Tests are very, very important. Submit tests if your pull request contains
   new, testable behavior.
1. Your pull request is comprised of a single ([squashed][]) commit.

## Checklist:

This is just to help you organize your process

- [ ] Did I cut my work branch off of master (don't cut new branches from existing feature brances)?
- [ ] Did I follow the correct naming convention for my branch?
- [ ] Is my branch focused on a single main change?
 - [ ] Do all of my changes directly relate to this change?
- [ ] Did I rebase the upstream master branch after I finished all my
  work?
- [ ] Did I write a clear pull request message detailing what changes I made?
- [ ] Did I get a code review?
 - [ ] Did I make any requested changes from that code review?

If you follow all of these guidelines and make good changes, you should have
no problem getting your changes merged in.


<!-- Links -->
[style guide]: https://github.com/reactorcore/style-guide
[n-queens]: https://github.com/reactorcore/n-queens
[Underbar]: https://github.com/reactorcore/underbar
[curriculum workflow diagram]: http://i.imgur.com/p0e4tQK.png
[cons of merge]: https://f.cloud.github.com/assets/1577682/1458274/1391ac28-435e-11e3-88b6-69c85029c978.png
[Bookstrap]: https://github.com/reactorcore/bookstrap
[Taser]: https://github.com/reactorcore/bookstrap
[tools workflow diagram]: http://i.imgur.com/kzlrDj7.png
[Git Flow]: http://nvie.com/posts/a-successful-git-branching-model/
[GitHub Flow]: http://scottchacon.com/2011/08/31/github-flow.html
[Squash]: http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html
