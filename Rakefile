require "bundler/setup"

namespace :assets do
  task :precompile do
    system "rakep build"
  end
end

desc "Deploy the website to github pages"
task :deploy do
  require "highline/import"
  message = ask("Provide a deployment message:  ") do |q|
    q.validate = /\w/
    q.responses[:not_valid] = "Can't be empty."
  end

  system "rakep clean"
  system "rakep build"

  Dir.chdir "output" do
    if File.exist?(".git")
      system "git checkout master"
    else
      system "git init"
      system "git remote add origin git@github.com:emberjs/emberjs.github.com.git"
    end
    system "git pull origin master"
    system "git add -A"
    system "git commit -m '#{message.gsub("'", "\\'")}'"
    system "git push origin master" unless ENV['NODEPLOY']
  end
end
