require 'bundler/gem_tasks'
require 'rspec/core/rake_task'
require 'tty-command'

RSpec::Core::RakeTask.new(:spec)

task default: :spec

namespace :docs do
  desc 'Libera el sitio de documentación'
  task :release do
    home = __dir__
    dist = File.join(home, 'docs', '.vuepress', 'dist')

    cmd = TTY::Command.new
    url = `git config --get remote.origin.url`.strip

    cmd.run 'yarn docs:build', chdir: home
    Dir.chdir dist do
      cmd.run 'git init'
      cmd.run 'git add -A'
      cmd.run 'git commit -m deploy'
      cmd.run 'git', 'push', '-f', url, 'master:gh-pages'
    end
  end
end
