---
layout:     post
title:      Automated publishing of Jekyll sites on GitHub
date:       2015-02-26 22:51:52
summary:    How to publish Jekyll based static web sites on GitHub Pages automatically.
categories: Jekyll GitHub-Pages publish Automated
---

Publishing a Jekyll based static website on GitHub Pages is quite easy once it is setup properly. This way you can trigger a publish on a different branch every time a change is pushed into the GitHub repository.


I will describe how to do it using `rake-jekyll`. For more detailed and probably updated information, please refer to the rake-jekyll documentation on [the  project page](https://github.com/jirutka/rake-jekyll)


If you already don't have one, create a `Gemfile` in your repository or update one you already have according to the following:

```ruby
source 'https://rubygems.org'

gem 'jekyll'
gem 'rake'
gem 'rake-jekyll'
```

Create or edit file `Rakefile` in your repository:

```rb
require 'rake-jekyll'

Rake::Jekyll::GitDeployTask.new(:deploy)
```


Create file `.travis.yml` in your repository:

```yaml
language: ruby
sudo: false
rvm: 2.2.0
script: bundle exec rake deploy
```


Install `travis` gem using shell:

```bash
$ gem install travis
```

Enable [Travis CI](https://travis-ci.org) for your github repository:

 * if you already don't have a Travis CI account, [sign up](https://travis-ci.org/) for one.
 * open your [profile page](https://travis-ci.org/profile/) on Travis
 * find your github repository for the website and turn on the switch
 ![the switch]({{ site.url }}/assets/Screenshot-2015-05-30-1.png)
 * click on the repository settings
 ![repository settings]({{ site.url }}/assets/Screenshot-2015-05-30-2.png)
 * enable the setting “Build only if .travis.yml is present.”
 ![enable setting]({{ site.url }}/assets/Screenshot-2015-05-30-3.png)

Generate a new personal access token on GitHub:

* Generate a new personal access token for your [Github profile](https://github.com/settings/tokens/new)
* select `public_repo` scope, enter description and generate. You will need the token displayed on the page for the next step.

Encrypt the token using the following shell command (replace the `<token>` part with your generated token from the previous step):

```bash
$ travis encrypt GH_TOKEN=<token> --add env.global
```

Following content will be added to your `.travis.yml` file:

```yaml
env:
  global:
    secure: YOUR-ENCRYPTED-TOKEN
```

Commit your changes and push to GitHub. Travis will trigger a build and publish your website in a couple of minutes.
