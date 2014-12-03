---
title: Launching my blog
date: 2014-12-03 14:09 UTC
tags: middleman
---

github 先產生一個 repository, 例如 blog2
git clone https://github.com/bcswlmpke/blog2.git
gem install middleman-blog
cd blog2
middleman init

此時的目錄下有這些檔案(含 layouts folder)
-----
      create  .gitignore
      create  config.rb
      create  source/index.html.erb
      create  source/layouts/layout.erb
      create  source/stylesheets
      create  source/stylesheets/all.css
      create  source/stylesheets/normalize.css
      create  source/javascripts
      create  source/javascripts/all.js
      create  source/images
      create  source/images/background.png
      create  source/images/middleman.png
-----

此時 Gemfile 內容有
-----
# If you do not have OpenSSL installed, update
# the following line to use "http://" instead
source 'https://rubygems.org'

gem "middleman", "~>3.3.7"

# Live-reloading plugin
gem "middleman-livereload", "~> 3.1.0"

# For faster file watcher updates on Windows:
gem "wdm", "~> 0.1.0", :platforms => [:mswin, :mingw]

# Windows does not come with time zone data
gem "tzinfo-data", platforms: [:mswin, :mingw]
-----

然後 Gemfile 加入下面這一行
gem "middleman-blog"
執行 bundle

再執行 middleman init --template=blog
此時的目錄下有這些檔案
-----
   identical  .gitignore
      update  config.rb
       exist  source
      create  source/2012-01-01-example-article.html.markdown
      create  source/calendar.html.erb
      create  source/feed.xml.builder
      update  source/index.html.erb
      create  source/layout.erb
      create  source/tag.html.erb
       exist  source/stylesheets
       exist  source/javascripts
       exist  source/images
-----

這時候 Gemfile 已被改過，
必須要再加回之前已有的項目

然後再補上
gem "middleman-gh-pages"
bundle

vim Rakefile add require 'middleman-gh-pages'

middleman article "Launching my blog"

middleman build
middleman server


說明一下：
因為 Github 只支援一個 User Page,
但可以有多個 Project Pages

因為我原本已經有一個 User Page 了，
所以這次我是用 Project Page 的方式來 deploy middleman blog,
因此必須安裝 middleman-gh-pages 這個 gem
(雖然還不了解它幫忙做了什麼，也還不了解 Rakefile)


git add .
git commit -m "first commit"
git push origin master
rake build & rake publish
