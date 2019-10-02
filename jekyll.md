---
layout: page
title: "Jekyll"
permalink: /jekyll/
---

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