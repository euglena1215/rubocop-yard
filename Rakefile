# frozen_string_literal: true

require "bundler/gem_tasks"
require "rake/testtask"
require "rubocop/rake_task"

RuboCop::RakeTask.new

task default: [:test]

Rake::TestTask.new do |task|
  task.warning = false
  task.libs = ["lib", "test"]
  task.test_files = FileList["lib/**/*_test.rb"]
end

desc 'Generate a new cop with a template'
task :new_cop, [:cop] do |_task, args|
  require 'rubocop'

  cop_name = args.fetch(:cop) do
    warn 'usage: bundle exec rake new_cop[Department/Name]'
    exit!
  end

  generator = RuboCop::Cop::Generator.new(cop_name)

  generator.write_source
  generator.inject_require(root_file_path: 'lib/rubocop/cop/yard_cops.rb')
  generator.inject_config(config_file_path: 'config/default.yml')

  puts generator.todo
end
