## About this role

This role installs docker-py.

It can be used as a prerequisite for roles that use Ansible's 'docker' module,
which requires docker-py.


## How to install

Simply clone this repository in your roles directory into a directory named
`has_docker-py`.

```bash
you@your-role-dir$ git clone https://github.com/lars-tiede/role_has_docker-py.git has_docker-py
```

If your roles directory is itself in a git repository, you can't do the above.
You have two options (that I know of) then, which are outlined below.


## Include in another git repository

If your roles directory is part of a git repository as well, you can use `git
subtree` or `git submodule` to add this role to your repository. Both methods
behave differently, and both are not perfect. For stuff like this, which I
expect to be fairly static and which I expect to be mostly a dependency in
projects using it, I prefer `git submodule`. Your mileage may vary, of course.


### Using `git subtree`

In a nutshell, `git subtree` copies files and their history from another repo
into your repository.

This is how you get a subtree:

```bash
you@your-project-dir$ git subtree add --prefix roles/has_docker-py https://github.com/lars-tiede/role_has_docker-py.git master --squash
```

Just choose the right prefix so that the role lands in the right directory
alongside your other ansible roles.

When you want to update the subtree, use the same command, just replace `add`
with `pull`.

Users who clone and pull from your repository need not be aware of the subtree;
nothing changes for them.

The main caveat with this method is that when you do this in a branch inside
your repository, you can't rebase that branch later... ouch. An additional
(minor) caveat is that all files from the subtree'd repository will also be
stored in your repository. And their whole history as well, unless you use the
--squash option.

There is much more to say about subtrees. Good reads are
[here](https://medium.com/@v/git-subtrees-a-tutorial-6ff568381844) and
[here](http://blogs.atlassian.com/2013/05/alternatives-to-git-submodule-git-subtree/).


### Using `git submodule`

'git submodule' adds a reference to another repository and a commit therein to
your repository. Unlike with `git subtree`, files or their histories are not
stored in your repository.

This is how you get a submodule:

```bash
you@your-project-dir$ git submodule add [-b BRANCH] https://github.com/lars-tiede/role_has_docker-py.git roles/has_docker-py 
```

When you want to update the submodule from its origin, first go into its
directory and `git pull`.

```bash
you@roles/has_docker-py$ git pull
```

Then, cd back into your project directory and commit - the reference to the
submodule will be updated.

Users who clone and pull from your repository must do things a little
differently, sadly. When cloning your repo, they must add the `--recursive`
option to `git clone`:

```bash
git clone --recursive URL DEST
```

And when they pull in changes from you, the following invocation after `git
pull` makes sure that all submodules are in place and at their correct
versions.

```bash
git submodule update --init --recursive
```

The main caveat of this method is that users can't just `git clone` and `git
pull` your project, they must remember to deal with submodules as well... ouch.
Another drawback is that if you are doing development on the 'main' and 'sub'
repos at the same time (never mind 'together with other devs'), things tend to
get very nasty. If you use submodules mostly for dependencies, though, you
should be okay.

There is much more to say about submodules. Good reads are
[here](http://www.speirs.org/blog/2009/5/11/understanding-git-submodules.html)
and [here](http://git-scm.com/book/en/v2/Git-Tools-Submodules).
