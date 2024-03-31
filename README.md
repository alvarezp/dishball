dishball
========

Small script to compare the contents of a released tarball and a
generated git archive against a git commit as it lives in the git
repository. It should be useful to check if they match and audit
for release-time attacks.


Sample run
==========

```
$ export REPO_URL=https://gitlab.com/alvarezp2000/superkb.git
$ export REPO_TAG=v0.23
$ export TARBALL_URL=https://gitlab.com/alvarezp2000/superkb/-/archive/v0.23/superkb-v0.23.tar.gz
$ ./dishball

Cloning git repository...
+ git clone -b v0.23 --depth 1 https://gitlab.com/alvarezp2000/superkb.git git-repo
Cloning into 'git-repo'...
remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Compressing objects: 100% (44/44), done.
remote: Total 45 (delta 1), reused 29 (delta 0), pack-reused 0
Receiving objects: 100% (45/45), 59.83 KiB | 29.92 MiB/s, done.
Resolving deltas: 100% (1/1), done.
Note: switching to '83a0bd56de9cfce918a47bdf601a9ecdb5cd56de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

Fetching tarball and extracting...
+ wget -O - https://gitlab.com/alvarezp2000/superkb/-/archive/v0.23/superkb-v0.23.tar.gz
--2024-03-30 18:03:27--  https://gitlab.com/alvarezp2000/superkb/-/archive/v0.23/superkb-v0.23.tar.gz
Resolving gitlab.com (gitlab.com)... 172.65.251.78, 2606:4700:90:0:f22e:fbec:5bed:a9b9
Connecting to gitlab.com (gitlab.com)|172.65.251.78|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/octet-stream]
Saving to: ‘STDOUT’

-                                                   [ <=>                                                                                                 ]  50.68K  --.-KB/s    in 0.009s  

2024-03-30 18:03:27 (5.30 MB/s) - written to stdout [51892]

Generating archive from git repository...
+ git archive --remote=./git-repo/.git --format=tgz v0.23
Calculating differences between the git repository and the generated archive...
+ diff -u -r -x .git git-repo git-archive
Calculating differences between the git repository and the tarball...
+ diff -u -r -x .git git-repo tarball/superkb-v0.23

===== Differences from git repository to generated archive:
None found.

===== Differences from git repository to published tarball:
None found.
```
