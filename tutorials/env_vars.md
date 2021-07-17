---
layout: default
title:  OS Environment Variables
parent: Tutorials
nav_order: 2
has_children: false
---

# Set System-wide Environment Variables in Ubuntu-20


OS environment variables used for consistency between updates through vcs and security.

<p class="text-red-300">Do not edit `/etc/environment` or `/etc/profile` or `/etc/bash.bashrc` as some may say so. 
Why? Check the doc page linked bellow</p>

Create a file named `freightapp.sh` in `/etc/profile.d`.
<br>Put appropriate values in `repo/freightapp-envvars.sh` and copy it to `/etc/profile.d`.

```shell
# assuming you are in the repo root directory
sudo cp freightapp-envvars.sh /etc/profile.d/freightapp.sh
```

<br>There put the values as:

```shell
# inside /etc/profile.d/freightapp.sh
export ENVVARS=value
```

**There is already a file with the required env-vars, check `repo_root/freightapp-envvars.sh`. 
Set your values there and move it to `/etc/profile.d`**
```shell
# assuming you are in project root and set your values in the file
sudo mv freightapp-envvars.sh /etc/profile.d/freightapp.sh
```

## Modify a System-wide environment variable already set
Sometimes you may need to update one or more values in `/etc/profile.d/freightapp.sh`, e.g., database change.
Simply edit the file with updated values. Then do logout-login.

<br>


### Beware of sudo caveat.
### <span class="text-red-100">Server needs logout-login to take in effect for all processes. No shortcut for that!</span>

<br>
<p class="text-grey-dk-300">Read More:</p>
[Ubuntu Community Help: System-wide environment variables][ubuntu_systemwide_env_var]{:target="_blank"}

[ubuntu_systemwide_env_var]: https://help.ubuntu.com/community/EnvironmentVariables#System-wide_environment_variables
