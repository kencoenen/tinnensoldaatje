require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"

gem 'jekyll', '3.3.1'

group :jekyll_plugins do
  gem 'jekyll-archives', '2.1.1'
  gem 'jekyll-paginate', '1.1.0'
  gem 'jekyll-sitemap', '0.12.0'
  gem 'jekyll-seo-tag', '2.1.0'
  gem 'jekyll-feed', '0.8.0'
end

desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    pwd = Dir.pwd
    Dir.chdir tmp

    desc "Cloning into #{tmp}..."
    system "git clone https://github.com/kencoenen/tinnensoldaatje.git #{tmp}"
    desc "Switching to 'master'..."
    system "git clone https://github.com/kencoenen/tinnensoldaatje.git #{tmp}"

    desc "Copying '_site' content to #{tmp}..."
    Dir.chdir pwd
    cp_r "_site/.", tmp
    Dir.chdir tmp

    desc "Pushing to Github..."
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git push --all -u"

    Dir.chdir pwd
  end
end