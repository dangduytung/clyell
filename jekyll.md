---
layout: page
title: "Jekyll"
permalink: /jekyll/
---

// Install
~~~
1. Ruby https://www.ruby-lang.org/en/downloads/
2. Bundler : gem install bundler
3. Git init or checkout from Github
4. Gemfile :
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
5. Generate Gemfile.lock : bundle install
6. Serve local : bundle exec jekyll serve (http://localhost:4000)
~~~

// Command
~~~
bundle install
bundle update
bundle exec jekyll build --trace
bundle exec jekyll serve --port 1234
~~~

// Fix GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.
~~~ bash
export JEKYLL_GITHUB_TOKEN=[github token]
echo $JEKYLL_GITHUB_TOKEN
JEKYLL_GITHUB_TOKEN=[github token] bundle exec jekyll serve
~~~