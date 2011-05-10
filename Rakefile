require 'bundler'
require 'rake'
require 'rake/testtask'
require File.expand_path('../lib/treeline/version', __FILE__)

Bundler::GemHelper.install_tasks

Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/*_test.rb'
end

# namespace :test do
#   Rake::TestTask.new(:lint) do |test|
#     test.libs << 'lib' << 'test'
#     test.pattern = 'test/test_active_model_lint.rb'
#   end
# 
#   task :all => ['test', 'test:lint']
# end

# task :default => 'test:all'
task :default => 'test'

desc 'Builds the gem'
task :build do
  sh "gem build mongomapper_id2.gemspec"
end

desc 'Builds and installs the gem'
task :install => :build do
  sh "gem install mongomapper_id2-#{MongomapperId2::VERSION}"
end

desc 'Tags version, pushes to remote, and pushes gem'
task :release => :build do
  sh "git tag v#{MongomapperId2::VERSION}"
  sh "git push origin master"
  sh "git push origin v#{MongomapperId2::VERSION}"
  sh "gem push mongomapper_id2-#{MongomapperId2::VERSION}.gem"
end