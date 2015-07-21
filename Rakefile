require 'rubygems'
    require 'rake'
    require 'rdoc'
    require 'date'
    require 'yaml'
    require 'tmpdir'
    require 'jekyll'

    desc "Generate blog files"
    task :generate do
      Jekyll::Site.new(Jekyll.configuration({
        "source"      => ".",
        "destination" => "_site"
      })).process
    end


    # It seems like github-pages doesn't allow the use of plugins
    # So, we'll have to generate the files and push the result to 
    # gh-pages.
    desc "Generate and publish blog to gh-pages"
    task :publish => [:generate] do
      Dir.mktmpdir do |tmp|
        system "mv _site/* #{tmp}"
        system "git checkout master"
        system "rm -rf *"
        system "mv #{tmp}/* ."
        message = "Site updated at #{Time.now.utc}"
        system "git add ."
        system "git commit -am #{message.shellescape}"
        system "git push origin master --force"
        system "git checkout gh-pages"
        system "echo publish...DONE!"
        system "echo Checkout http://code-travel-adventures.com/ to see if your changes have been reflected!"
      end
    end

task :default => :publish