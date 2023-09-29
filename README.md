# local_dev
Docker container for local development without installing gcc, rust, mysql, nodejs, scdev, etc.

## Assumptions
* Your scale-product directory is under ~/src/ Note: you can also set a symlink to your project directory.

## Setup
* [Install Docker](https://docs.docker.com/get-docker/)
* [Login to our local docker container registry](https://github.lab.local/dev/dev/wiki/dev-ctr-Developer-Container-Registry)
* Make sure you have the build_rsa key in ~/.ssh/
* Make sure you have $USER or $SC_SCREWI_USER set to your screwi username
* Set your email & name in git locally (not globally) in scale-product:
```
cd ~/src/scale-product/
git config user.name "FIRST_NAME LAST_NAME"
git config user.email "MY_NAME@example.com"
```

## Installing
1. Clone this repo 
```
cd local_dev
chmod +x ./bin/* 
bin/start
```

# Running tests
```
bin/npm run test
# coverage is available here: http://127.0.0.1:9003/
```

# Getting into the containter
```
bin/bash
```

## scdev
scdev commands can be run from your native command line like so:

Build your current git tree via build farm:
```
docker exec -it local_dev scdev build
```

SSH to a build farm container with a build of your current git tree:
```
docker exec -it local_dev scdev build ssh
```

Copy the scdev script into your path somewhere for that local feel:

Example:
```
17:08:44 ➜  scale-product git:(2ce00c8b97) scdev build
Agent pid 390
Identity added: /root/.ssh/build_rsa (/root/.ssh/build_rsa)
Error doing autocommit; there may be nothing to commit:

Requesting build...
Build already complete for yesui-68166f36702cfa2ab3f862a1e1772ce79351765d

Error: prepare build mount: locking new build: SomeoneElseSucceeded

17:08:55 ➜  scale-product git:(2ce00c8b97)
```

## mysql

alias the docker exec command for that local feel:
```
alias mysql="docker exec -it local_dev mysql"
```

Example:
```
➜ mysql -t -ubuild -pbuild -h builddb.lab.local -e 'select count(*) from testbeds' re_ci
+----------+
| count(*) |
+----------+
|      245 |
+----------+
```

The .mysql_history is stored in your ~/src directory to prevent it from getting clobbered on container rebuild.