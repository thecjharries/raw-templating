# `shell-solution`

I'd suggest you take some time looking at the source code before you decide to install and use this.

## Installation

Personally I'm a huge fan of putting small projects like this in my `~/.config` or `~/.local`.

```shell-session
$ mkdir -p $XDG_CONFIG_HOME/wotw/raw-templating && cd $_
$ git clone https://github.com/thecjharries/raw-templating .
$ ln -s $XDG_CONFIG_HOME/wotw/raw-templating/shell-solution/delete-project $HOME/.local/bin
$ ln -s $XDG_CONFIG_HOME/wotw/raw-templating/shell-solution/project-generator $HOME/.local/bin
$ ln -s $XDG_CONFIG_HOME/wotw/raw-templating/shell-solution/new-projects $XDG_CONFIG_HOME/git
```

## Set Up

You'll need up to three things:

1. A GitHub personal access token
2. A CircleCI personal access token
3. A Coveralls personal access token

You can't do anything without a GH token; the others can be skipped. THese need to be available to the script as environment variables; how you do that is up to you. You can see their specific names [in the source](./project-generator#L20-L40).

You'll also want to manually edit the settings at [the top of the generator](./project-generator#L10-#20). They aren't exposed and I don't want to encourage myself to use this POS by doing that.

Finally, make sure you understand [the generated env file](./project-generator#L99-L105). It should provide you quick and easy nuke powers. You can still nuke things manually but it's way faster with [the delete script](./delete-project).

You might also want to look at [the contents of `new-projects`](./new-projects) if you're going to use the starter directory stuff. While `git init` fleshes out the `.git` directory, this pads out the visible repo root. Adding all the GitHub community stuff is one of the reasons why I finally built a template script.  

## Usage

Assuming the variables are right, it's a breeze to use.

### Creation

```shell-session
# all the input is in the first few lines because it was faster
$ project-generator

...

# serious wall; things weren't cooperating so I dumped it all
$ cd your/repo
$ git status
# should have some edits in the README
```

### Deletion

```shell-session
$ delete-project ../a/relative/or/absolute/path/to/owner/repo
# we're looking for its .git/wotw-env
# without it it's all manual so the script stops
# with it GH is nuked followd by the directory
```

Both Coveralls and CircleCI require you to manually remove integrations. Something about the whole "manual" doesn't seem very cash money of them but whatev.

## Things that get seeded

* EditorConfig
* LICENSE file
* Contributor doc, issue templates, and a PR thing
* A hello world Circle CI to get the builds going
