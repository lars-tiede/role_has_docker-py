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

If your roles directory is part of a git repository as well, you can use git
subtree to include it. [A few caveats apply when using git
subtree](http://blogs.atlassian.com/2013/05/alternatives-to-git-submodule-git-subtree/),
however those shouldn't present a problem in this case.

```bash
you@your-project-dir$ git subtree add --prefix roles/has_docker-py https://github.com/lars-tiede/role_has_docker-py.git master
```

Just choose the right prefix so that the role lands in the right directory
alongside your other ansible roles.

Another possibility would be to use `git submodule` instead of `git subtree`.
