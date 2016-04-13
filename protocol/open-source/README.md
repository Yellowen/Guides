Open Source Protocol
====================

A guide for releasing and maintaining open source projects.

Accepting a GitHub Pull Request
-------------------------------

Given you have this in your `~/.gitconfig`:

    [alias]
      co-pr = !sh -c 'git fetch origin pull/$1/head:pr/$1 && git checkout pr/$1' -

Check out the code by its GitHub pull request number:

    git co-pr 123

Rebase interactively, squash, and potentially improve commit messages:

    git rebase -i master

Look at changes:

    git diff origin/master

Run the code and tests. For example, on a Ruby project:

    bundle
    rake

Merge code into master:

    git checkout master
    git merge pr/123 --ff-only

Push:

    git push origin master

Clean up:

    git branch -D pr/123

Releasing a Ruby Gem
--------------------

* Edit the `VERSION` constant.
* Run `bundle install` to update `Gemfile.lock`.
* Run the test suite.
* Edit `NEWS`, `Changelog`, or `README` files if relevant.
* Commit changes. Use the convention "v2.1.0" in your commit message.
* Run `rake release`, which tags the release, pushes the tag
  to GitHub, and pushes the gem to Rubygems.org.
