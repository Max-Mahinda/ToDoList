require_relative './config/environment'
require 'sinatra/activerecord/rake'
desc "Runs a Pry console"
task :console do
  # This line turns on logging of the SQL generated by Active Record
  ActiveRecord::Base.logger = Logger.new(STDOUT)
  # Open a Pry session
  Pry.start
end
desc 'Reset seeds and primary keys'
task :reset_seeds do
  Rake::Task['db:drop'].invoke        # Drop the database
  Rake::Task['db:create'].invoke      # Recreate the database
  Rake::Task['db:migrate'].invoke     # Run migrations to recreate the tables
  Rake::Task['db:seed'].invoke        # Seed the database
end
desc "Start the server"
task :server do
  if ActiveRecord::Base.connection.migration_context.needs_migration?
    puts "Migrations are pending. Make sure to run `rake db:migrate` first."
    return
  end
  # rerun allows auto-reloading of server when files are updated
  # -b runs in the background (include it or binding.pry won't work)
  exec "bundle exec rerun -b 'rackup config.ru'"
end


























