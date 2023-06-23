# Linux notes

[https://github.com/dangduytung/linux](https://github.com/dangduytung/linux)

## Theme Clyell
Link: [http://jekyllthemes.org/themes/clyell](http://jekyllthemes.org/themes/clyell)

### Characteristics

- [x] Simple
- [x] Friendly to read

### Jekyll config file example

~~~ yml
# Site settings
title: "linux"
bye_message: "Thx!"
baseurl: "/linux"
url: "https://dangduytung.github.io"
disqus: dangduytung

# Build settings
markdown: kramdown
permalink: /:categories/:title
~~~

### Run Command
~~~
bundle exec jekyll serve      # http://localhost:4000  (--port 1234)
bundle exec jekyll build
~~~