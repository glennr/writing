# The Siyelo Flow

We've been using git for several years at Siyelo, made lots of mistakes, and learned quite a few
things along the way. We've used nvie's git-flow, been weirdly miltant about always
having merge commits, and battled some pretty gnarly merge conflicts. In hindsight, a lot of what we 
did was rather unnecessary.

We've settled on a simple (and productive) workflow that suits the way we work: 
small teams, rapid iterations and short feedback loops with our clients.
This manifests in a git workflow that is characterized by short-lived feature branches, 
a clean and useful git log, and favouring communication to avoid/resolve integration problems.

The Siyelo Flow looks like this;

  * `master` is always stable & production-ready
  * Make single-purpose feature branches, branched off of `master`
  * Commit early and often. Use semantic commit messages
  * Push your branch to the server regularly
  * Avoid subway maps - interactively rebase to keep history sane
  * Use pull requests, when you need to
  * Use CI to make sure `master` (and branches) builds are 'green'
  * Automatically deploy `master`

Let's look into each of these steps in more detail;

##  `master` is always stable & production-ready

We treat `master` as our mainline. Everybody is working off of `master`, it must be stable, 
and it can be deployed anytime. This branch should never be rolled back or rebased.

Keeping `master` stable not only enables Continuous Deployment, it means that every developer
can trust they are working off of a stable base.

Breaking `master` means you broke the #1 rule, and should generally involve some kind of ridicule 
or shaming. Waterboarding should not be ruled out for repeat offenders. 


## Make single-purpose feature branches, branched off of `master`

When you start a new feature or fix, make a new branch off of `master`, prefixed with your initials.
For example if your name is Lil' Jon, and you are working on adding payment integration to your app, you 
might call your branch `lj_add_payments`.

We don't work on the master branch. We are not savages.
 
As for the 'single-purpose' thing, well, try to keep the branch on-topic, so that it can be finished and merged
sooner than later (you'll see why soon). Keep to (un)related bugfixes/features/chores on their own branches.

Single purpose branches are;
1) easier to prep for a pull request (no shuffling/groupling/renaming of commits), and 
2) easier for a reviewer to reason about, and thus 
3) easier to merge.

Single purpose branches are as short-lived as they can be, and short-lived branches are easier to get 
merged. These are very good things. To put in another way, merging (well, rebasing) your long-lived-ass 
branch is your problem. If `master` moves on while you
go yak shaving, then you're gonna have a bad time integrating later on.

With this branching model (and with any distributed SCM), integration problems can and will arise.
Sometimes long-lived branches can't be avoided. My advice is to communicate with your team if you are 
likely going to be making changes that are likely to 
impact others (or vice versa). Ask your colleagues "Hey, I'm gonna be working on X, is anyone else 
working on/around X too?". Work out a plan. Use your words.

- avoid production / development / staging branches
  - leads to branch spaghetti / subway tracks
    - if you have to - use ff merges to avoid 
  - we prefer git remotes wherever possible



We trust our devs and encourage them to 'own' their work. Work together, collaborate, use pull requests. 
However if you don't think you need someone to review a fix or a feature, merge it. It's your call. 
If it breaks the build (or production!), it's on you. If all goes well, you receive all the Glory Points.
 Exercise your judgement.


We dont like a lot of ceremony around new features, releases or fixes. We tend to avoid using branches
to describe where something is deployed e.g. `staging` or `production` branches. Often it's possible to use
remotes as a better way to track that. Similarly the concept of a `develop` branch is redundant 
in our workflow, given our feature branches stay close to `master`.


- visualize!
  - gitx
  - git log --graph


- use semantic commit messages
  - fteem's repo
  - cosmetic commits are great


- push to your branch constantly
  - your branch - push whenever you like!
  - handy form of backup!
  - keeps everyone informed. git fetch!
  - integrate with FD - so your team sees the activity.
  - gpo :your_branchname like a boss - keep origin clean

- interactive rebase before you merge

- test before merge 
  - CI platform -  e.g. travis/circle
  - Shows in GHub
  - let GH/Travis/Circle build all branches - show you if your branch is stable. 

- use pull requests, but only when it needs review
  - its up to YOU to make sure it merges cleanly
    - if the reviewer fucks about and delays reviewing, then its not so clear cut. They should rebase, or ask you super nicely.
  - rebase and squash your branch first
  - only the branch needs peer review (chores, small fixes, no)
  - using GHub 
    - use the merge and delete buttons
    - will create a merge 'bubbles', but hey
    - GH will handle force-pushed feature branches much better than it used to.


== Tips

- dont complicate your life with -no-ff flags
  - we used to
  - if it fast-forward merges, then great. We dont need to see every branch that ever existed. Also, the lack of merge commits makes git bisect much easier to reason about.

- keep local clean 
  - git prune 
  - kill merged branches
   
     git branch --merged | grep -v "\*" | xargs -n 1 git branch -d 

- be a good citizen 
  - own your branches
    - gr_add_blah
    - hitch-style (alphabetical) pair naming 
      - gr_ny_some_branch
  - keep origin clean
    - gpo :branch


== Visualizing

- visualize you repo
  - avoid subway track madness
  - gitX 

== ProTips

- fetch dont pull
  - gf
  - grom

=== Shortcuts

- avoid rsi - use zsh/git plugins/aliases
  - gf
  - grom
  - griom
  - gpom
  - gs
  - gb
  - grh!

=== Track down regressions

- git bisect