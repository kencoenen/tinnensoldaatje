require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


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

    desc "Copying '_site'..."
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