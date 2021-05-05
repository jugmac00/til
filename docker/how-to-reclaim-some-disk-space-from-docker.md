# How can you reclaim some disk space from Docker?

If you use Docker containers,
and who doens't these times,
you need to take care that Docker does not accumulate a lot of cruft.

## remains of `docker run`

If you start a container via `docker run`,
and without the highly recommended option `--rm`,
the exited Docker container will still leave some remains on your system.

In my case oO...

```
❯ docker ps -a
CONTAINER ID   IMAGE                                         COMMAND                  CREATED         STATUS                      PORTS     NAMES
c14c0bd0d850   jetbrains/youtrack:2020.3.12000               "/bin/bash /run.sh"      6 months ago    Exited (0) 6 months ago               youtrack
81aa523801b4   python:3.8-slim-buster                        "python3"                7 months ago    Exited (0) 7 months ago               intelligent_nobel
319b210462b7   python:3.8-slim-buster                        "python3"                7 months ago    Exited (0) 7 months ago               happy_wilbur
7eca121738aa   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-4.0p1…"   7 months ago    Exited (255) 7 months ago             relaxed_chaplygin
66d7a0c97f87   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-4.0p1…"   7 months ago    Exited (255) 7 months ago             jovial_williamson
7c4fb679cf7e   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-4.0p1…"   7 months ago    Exited (255) 7 months ago             amazing_franklin
ae4d0d88a412   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               kind_einstein
0f678273bd4e   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               awesome_khorana
327facd36000   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               friendly_goldberg
f5ed4e767ece   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               friendly_kowalevski
0b8fc88d22f1   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             hopeful_chaplygin
e4c1688e9863   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             wonderful_napier
60da4fd07a85   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             ecstatic_bohr
3ef736caa432   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             lucid_pare
f7a53057535a   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               gallant_ritchie
f0a2a4733984   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             elastic_villani
9232a99320d9   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             goofy_johnson
4f6d726e1ca1   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             magical_shtern
856296da2b4a   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             laughing_cannon
20f7eda16e9d   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             intelligent_chaplygin
d3d244294e49   positronsecurity/ssh-audit-test-framework:3   "/usr/bin/tcpserver …"   7 months ago    Exited (0) 7 months ago               admiring_greider
d9a66f1961a8   positronsecurity/ssh-audit-test-framework:3   "/dropbear/dropbear-…"   7 months ago    Exited (1) 7 months ago               beautiful_benz
5ed520b3399b   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               confident_bohr
843f75aa7d83   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               upbeat_shaw
865ec1914303   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-8.0p1…"   7 months ago    Exited (0) 7 months ago               blissful_montalcini
bd20edc7842c   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             funny_kirch
03e92fe5df44   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             sharp_poincare
9670da0dba75   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             eager_elgamal
df9f2f1b0e10   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             happy_keldysh
506207c05a27   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-5.6p1…"   7 months ago    Exited (255) 7 months ago             priceless_cartwright
bb3bccbef26a   positronsecurity/ssh-audit-test-framework:3   "/openssh/sshd-4.0p1…"   7 months ago    Exited (255) 7 months ago             relaxed_shirley
25d1ac6f3d85   odoo                                          "/entrypoint.sh odoo"    7 months ago    Exited (0) 7 months ago               odoo
af28c470db77   postgres:10                                   "docker-entrypoint.s…"   7 months ago    Exited (0) 7 months ago               db
a6d8dfc2b2ad   plone                                         "/docker-entrypoint.…"   15 months ago   Exited (0) 15 months ago              ppp
4ad4fd1802e2   plone                                         "/docker-entrypoint.…"   15 months ago   Exited (0) 15 months ago              youthful_hoover
97deaec9f63e   plone                                         "/docker-entrypoint.…"   15 months ago   Created                               objective_rubin
c5b24788ce3f   plone                                         "/docker-entrypoint.…"   15 months ago   Exited (0) 15 months ago              brave_newton
```

This cruft and much more can be cleaned up by running...

```
❯ docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

Are you sure you want to continue? [y/N] 
```

## old images

Do you always delete a Docker image when you do not need it any more?

It seems that I don't do this!

```
❯ docker images
REPOSITORY                                  TAG               IMAGE ID       CREATED         SIZE
redis                                       latest            de974760ddb2   3 weeks ago     105MB
adminer                                     latest            211f88f2c454   3 months ago    89.7MB
postgres                                    13.1              4ea2949e4cb8   3 months ago    314MB
shopyo                                      latest            be9ba0472b07   5 months ago    880MB
ubuntu                                      latest            f643c72bc252   5 months ago    72.9MB
jetbrains/youtrack                          2020.3.12000      c5c1a2632420   7 months ago    596MB
python                                      3.8-slim-buster   62297c9f4e5c   7 months ago    113MB
postgres                                    10                e8abca8f194e   7 months ago    200MB
odoo                                        latest            f018911ebd84   7 months ago    1.2GB
plone                                       latest            bfe83a632704   15 months ago   619MB
jetblackpope/pybuntu                        1.6.1-disco       f208c0abcd07   18 months ago   94.7MB
positronsecurity/ssh-audit-test-framework   3                 66b1bd47c052   20 months ago   190MB
alpine                                      latest            055936d39205   24 months ago   5.53MB
danlynn/bat                                 latest            0bfded85e55c   2 years ago     238MB
quay.io/python-devs/ci-image                latest            e4147b2d6ddc   2 years ago     1.67GB
python                                      3.5.1             a00e9008965a   4 years ago     698MB
python                                      3.5.0             de8fe124331e   5 years ago     689MB
```

I can't even remember what for I used all those images,
except Python 3.5, which I used to reproduce a [problem reported on StackOverflow](https://stackoverflow.com/a/64219816/672833).

You can delete unused images with `docker image rm <image name>`.

e.g. `docker image rm redis`
