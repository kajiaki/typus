require 'bundler'
Bundler::GemHelper.install_tasks

require 'rubygems'
require 'rake/testtask'
require 'rake/rdoctask'

task :default => :test

desc 'Test the typus plugin.'
Rake::TestTask.new(:test) do |t|
  t.libs << 'lib'
  t.libs << 'test'
  t.pattern = 'test/**/*_test.rb'
  t.verbose = true
end

=begin
desc 'Generate plugin documentation.'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title    = 'Typus'
  rdoc.options << '--line-numbers' << '--inline-source'
  rdoc.rdoc_files.include('README.rdoc')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
=end

task :deploy do
  system "cd test/fixtures/rails_app && cap deploy"
end

RUBIES = ["ruby-1.8.7-p330", "ruby-1.9.2-p136", "ree-1.8.7-2010.02", "jruby-1.5.6"]

namespace :setup do

  desc "Setup test environment"
  task :test_environment do
    RUBIES.each { |ruby| system "rvm install #{ruby}" }
  end

  desc "Setup CI Joe"
  task :cijoe do
    system "git config --replace-all cijoe.runner 'rake test:all'"
  end

end

namespace :test do

  task :all do
    RUBIES.each do |ruby|
      system "rvm use #{ruby}"
      system "rm -f Gemfile.lock"
      system "bundle install"
      system "rake"
      # system "rake DB=postgresql"
      # system "rake DB=mysql"
    end
  end

end
