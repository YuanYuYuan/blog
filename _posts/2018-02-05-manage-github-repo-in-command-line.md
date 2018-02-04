---
title: "Manage Github Repo in Command Line"
header:
  teaser: /assets/images/unsplash-5.jpg
  image: /assets/images/unsplash-5.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Linux
tags:
  - Git
---

Every time I have to create a github repository, 
it took a lot of time using Web UI to make a new one.

So I wrote down this post to note the process of manage the github repo in command line.

And the following is a script which automatically handles the job.

```sh
#! /usr/bin/env bash

echo -n "Enter name of repository:  "
read REPO

echo -n "Enter name of user: "
read USERNAME

mkdir $REPO
cd $REPO
git init 
echo init > README.md
git add .
git commit -m "init"

eval "curl -u '$USERNAME' https://api.github.com/user/repos -d '{\"name\":\"$REPO\"}'"

git remote add origin git@github.com:$USERNAME/$REPO.git
git push --set-upstream origin master
```



## Create Local Git Project

First, initialize a git.

REPO is the repository to be created, 
and the USERNAME is the owner on the github.

```sh
mkdir REPO && cd REPO
git init
echo init > README.md
git add .
git commit -m "init"
```

## Create & Link Remote Github Repo

Call github api

```sh
curl -u 'USERNAME' https://api.github.com/user/repos -d '{"name":"REPO"}'
```

Use HTTPS to link

```sh
git remote add origin https://github.com/USERNAME/REPO.git
```

Or use SSH to link

```sh
git remote add origin git@github.com:USERNAME/REPO.git
```

Finally set the orgin and push 

```sh
git push --set-upstream origin master
```
## Delete Remote Github Repo

```sh
curl -X DELETE -u 'USERNAME' https://api.github.com/repos/USERNAME/REPO
```


{% include toc title="Outline" icon="file-text" %}


