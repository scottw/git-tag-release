git-tag-release
===============

This utility creates a unique git tag in the current repository with
the year, month, day and username of the person creating the tag. It
is meant to be called from, say, a `Makefile` as part of an automated
release system, but you can also call it by hand. If used in a
`Makefile`, you can have nice sequential and meaningful tags leaving a
history of your work and recording the state of the repo when you made
your release.

## installation ##

Put the file somewhere in your `$PATH` and `chmod 0755
git-tag-release`.

In your `Makefile` target, do something like this:

    install:
        @git-tag-release
        (the rest of your install target here)

## options ##

* label

  defaults to 'release'. Other common labels: 'bugfix', 'emergency', etc.

* who

  defaults to the name before the '@' in `git config user.email`. You
  might prefer 'build' or something similar to indicate the deployment
  was automatic (if it was).

* sign

  if specified, `git-tag-release` will create a signed, annotated tag.

* separator (sep)

  if specified, the components of the tag will be separated with this
  character. Defaults to a hyphen ('-')

## usage ##

Normally just:

    git-tag-release

but possibly:

    git-tag-release --label=bugfix --sep=/

or even:

    git-tag-release --sign --who jenkins

This will create a new tag with the current date, label, and
user. Like this:

    130912a-release-jenkins

If you run it more than once in a day, the 'a' increments:

    130912b-release-jenkins

If you get to 'z', then it will still increment (carry the 'z'):

    130912aa-release-jenkins

etc.

Go ahead and try it. If you don't like the tag, you can delete it:

    git tag --delete 130912b-release-jenkins

## author ##

Scott Wiersdorf: <scott@perlcode.org>, <scott@betterservers.com>
