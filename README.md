# Managing development tools

I'm looking for a tool to manage development tools like linters, test runners, etc.

The current approaches available are
- install the tools in my system

    Here I'm left with manual management of tools versions. Even if pipx supports installation of multiple versions, there's no easy way to active the required versions for the project. And that's just for python tools.
    
- install the tools as dev dependencies
    
    It's really not what dev dependencies are meant for. Besides, only works for tools written in the same language as the project (or wrapped in a package for the language). But the bigger problem is that they share the execution environment with the project and with each other, which leads to dependency hell.

- use Nix

    I've had one encounter with Nix and I didn't like it. I was expecting `make`-grade tool, instead it took a couple of hours to install, it downloaded gigabytes of packages and sources to build. It was supposed to use some online cache on the way but that's failed. Oh, and it required root access, and created some extra users in the OS on the way.

- use pre-commit

    I like pre-commit a lot, but again, it's not intended as a dev-tool-manager.

    It does have some great features.
    It pulls packages from git repository (no bin repository needed), install them for a single user (no root access needed) together with dependencies in separated environments (no dependency hell) and use declared versions for the project (no need for manual version management).

    This is all great, but it's literal gits pre-commit utility, which means it wants to be really fast and have predictable executions. It's not intended as a general purpose dev-tool manager - it doesn't provide the tolls with full project environment (so it doesn't include dependencies) so it doesn't support test runners (also because testing is to slow for a pre-commit hook) and even support for some linters (see pythons `mypy`) is suboptimal (again, `mypy` works best with access to dependencies).

    It seems to have some issues with integrity checks that causes buggy package updates creep in and break executions.
    
I think pre-commit would be a either a good tool to wrap into a generic tool-manager, or a good starting point for a fork.

And it's pure python.