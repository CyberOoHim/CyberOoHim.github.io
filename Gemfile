# 1. First, create a Gemfile in your root directory
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins
gem "jekyll"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end

# 2. Create/update _config.yml
title: Your Site Title
description: Your site description
domain: your-username.github.io
url: https://your-username.github.io
baseurl: ""

# Build settings
markdown: kramdown
remote_theme: pages-themes/minimal@v0.2.0
plugins:
  - jekyll-feed
  - jekyll-remote-theme
  - jekyll-seo-tag

# 3. Update index.html with proper spacing
