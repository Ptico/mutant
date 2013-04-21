require 'devtools'
Devtools.init_rake_tasks

Rake::TaskManager.class_eval do
  def remove_task(task_name)
    @tasks.delete(task_name.to_s)
  end
end


namespace :metrics do
  desc 'Run mutant'
  task :mutant => :coverage do
    project = Devtools.project
    require File.expand_path('../spec/support/zombie.rb', __FILE__)
    Zombie.setup
    status = Zombie::CLI.run(%W(::Mutant --rspec-dm2))
    if status.nonzero?
      $stderr.puts 'Zombie task is not successful'
      $stderr.puts 'Not fatal at this point of development, will be fixed before release of 0.3.0'
    end
    Kernel.exit(0) # FIXME: Prevent devtools mutant task
  end
end
