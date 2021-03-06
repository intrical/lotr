# Intrical Wiki App
Adapted from [LOTR](https://github.com/arbales/lotr), this is a small Sinatra application that applies Google Apps authentication to Github's [Gollum Wiki](https://github.com/github/gollum) engine.

## Deployment
This app is meant to be deployed to a t1.micro AWS Ubuntu machine and presented for company use at http://wiki.intrical.us

Getting the machine ready (adapted from [a post by Martin Foot](http://www.mfoot.com/blog/2013/05/19/setting-up-a-personal-wiki-with-aws-and-gollum/)):

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install vim build-essential ruby ruby-dev libxslt1-dev git-core libxml2-dev bundler libicu-dev zlib1g-dev
```

Deploying the app:

```bash
git clone https://github.com/intrical/int-wiki-app
cd int-wiki-app
bundle update
```

## Content repo
As configured in ```config/application.yml```, a repo for wiki content (int-wiki-content) is expected alongside the int-wiki-app repo. After initial deployment, this should probably be cloned from the (private) Github remote (unless we're purging for some reason).

```bash
git clone https://github.com/intrical/int-wiki-content
```

## Running
Launches with foreman; probably want to use port 80:

```bash
sudo foreman start -p 80
```

## Committing content
Gollum automatically commits changes to the content repo locally, but this is ephemeral; there should be a cron job running on the box to occasionally push this content to the remote repo (daily is probably sufficient).
