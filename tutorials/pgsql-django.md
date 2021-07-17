---
layout: default
title:  PostgreSQL and Django
parent: Tutorials
nav_order: 1
has_children: false
---
# Use PostgreSQL database in your Django project, Ubuntu-20

## Method 1: Using `ident` based authentication of pg
Install the PostgreSQL server and client:
```shell
apt update
apt install postgresql postgresql-contrib postgresql-client
```

After install, PostgreSQL has a default user `postgres`. This user is admin level.

Now we'll be creating a database named `freightforward` with user(role) `freightforward` and password `freightapp-pass`.

### The `ident` authentication of PostgreSQL
When there are users with identical username in both Linux and PostgreSQL, 
postgresql automatically authenticates to the database user when the Linux user(identically named) logs in to shell. 
When an identically named database exists(so that linux username, postgresql username and database name all identical), 
PostgreSQL authenticates to the database too.

### Now create Linux user, PostgreSQL user and Database
all with identical username as `freightforward` and database name as `freightforward`
```shell
#provide other info when asked for
sudo adduser freightforward #Linux user, when asked for password set anything you want, `freightapp-pass` is not necessary here
sudo -u postgres createuser --interactive #Database user
sudo -u postgres createdb freightforward #Database
```
Here:
- The Linux user password set, not the database user
- As Linux system user created, it will show up in login screen, which is <span class="text-red-300">unwanted and annoying</span>

### Set a password for the database user
Now set a password for the PostgreSQL database user `freightapp`. This user has no user modify access. 
So we'll be working as `postgres` user.
<br>Launch `psql` shell
<table>
<tr><th colspan="2">Follow any one of the two methods below</th></tr>
<tr>
<td>
sudo su - postgres
<br>psql
</td>
<td>
sudo -u postgres psql
</td>
</tr>
</table>

Now `ALTER USER` command in the `psql` shell:

```postgresql
ALTER USER freightforward WITH PASSWORD 'freightapp-pass';
```
<p class="text-red-300">If you have set environment variables already, then edit `/etc/profile.d/freightapp.sh` for the new password</p>

### ALTER some optional but important parameters for the PostgreSQL Database User
In the `psql` shell
```postgresql
ALTER ROLE freightforward SET client_encoding TO 'utf8';
ALTER ROLE freightforward SET default_transaction_isolation TO 'read committed';
ALTER ROLE freightforward SET timezone TO 'UTC';
```