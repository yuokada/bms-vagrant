#!/usr/bin/env rake

desc "Runs knife cookbook test"
task :knife do
  Rake::Task[:prepare_sandbox].execute

  sh "bundle exec knife cookbook test cookbook -c test/.chef/knife.rb  -o #{sandbox_path}/../"
end

desc 'foodcritic'
task :foodcritic do |t|
  if Gem::Version.new( '1.9.3' ) <= Gem::Version.new( RUBY_VERSION.dup )
    # "FC008: Generated cookbook metadata needs updating" is for handson
    sh "foodcritic -f any #{File.dirname( __FILE__ )}"
  else
    puts "WARN: foodcritic run is skipped as Ruby #{RUBY_VERSION} is < 1.9.2."
  end
end

task :prepare_sandbox do
  files = %w{*.md *.rb attributes definitions files libraries providers recipes resources templates}

  rm_rf sandbox_path
  mkdir_p sandbox_path
  cp_r Dir.glob("{#{files.join(',')}}"), sandbox_path
end

private
def sandbox_path
  File.join(File.dirname(__FILE__), %w(tmp cookbooks cookbook))
end

