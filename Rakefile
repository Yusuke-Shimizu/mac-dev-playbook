require 'rake'

namespace :inspec do
  desc "Run Inspec tests"
  task :default do
    sh 'inspec exec spec/common_spec.rb'
  end

  desc "Run first ansible Inspec tests"
  task :first do
    sh 'inspec exec spec/ansible_build_spec.rb'
  end

  desc "Run second ansible Inspec tests"
  task :second do
    sh 'inspec exec spec/ansible_second_build_spec.rb'
  end
end

namespace :ansible do
  desc "syntax check"
  task :syntax do
    sh 'ansible-playbook main.yml -i inventory -K --syntax-check'
  end

  desc "build check"
  task :check do
    sh 'ansible-playbook main.yml -i inventory -K -vv --check'
  end

  desc "build"
  task :build do
    sh 'ansible-playbook main.yml -i inventory -K -vv'
  end

  desc "install requirements from galaxy"
  task :install do
    sh 'ansible-galaxy install -r requirements.yml'
  end

  desc "install from homebrew"
  task :homebrew do
    sh 'ansible-playbook main.yml -i inventory -K --tags "homebrew"'
  end
end

namespace :ci do
  desc "Run CI test"
  task :default do
    Rake::Task["inspec:first"].invoke()
    Rake::Task["inspec:default"].invoke()
    Rake::Task["inspec:second"].invoke()
  end
end
