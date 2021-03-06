dir = File.dirname(__FILE__)
$LOAD_PATH.unshift(File.expand_path("#{dir}/lib"))
require "rspec/git"

def git
  RSpec::Git.new
end

namespace :git do
  desc "Update rspec-dev & sub-projects"
  task :update do
    git.update
  end

  desc "Update rspec-dev & sub-projects"
  task :pull => :update

  desc "Reset rspec-dev and sub-projects"
  task :hard_reset do
    git.hard_reset
  end
end

if git.plugins_fetched?
  $LOAD_PATH.unshift(File.expand_path("#{dir}/pre_commit/lib"))
  require "pre_commit"
  
  task :default => :pre_commit
  
  desc "Runs pre_commit_core and pre_commit_rails"
  task :pre_commit do
    pre_commit.pre_commit
  end
  
  desc "Makes sure the correct versions of gems are on the system"
  task :check_for_gem_dependencies do
    pre_commit.check_for_gem_dependencies
  end
  
  desc "Runs pre_commit against rspec (core)"
  task :pre_commit_core do
    pre_commit.pre_commit_core
  end
  
  desc "Runs textmate bundle specs"
  task :pre_commit_textmate_bundle do
    pre_commit.pre_commit_textmate_bundle
  end
  
  desc "Runs pre_commit against example_rails_app (against all supported Rails versions)"
  task :pre_commit_rails do
    pre_commit.pre_commit_rails
  end
  
  task :ok_to_commit do |t|
    pre_commit.ok_to_commit
  end
  
  desc "Touches files storing revisions so that svn will update $LastChangedRevision"
  task :touch_revision_storing_files do
    pre_commit.touch_revision_storing_files
  end
  
  desc "Deletes generated documentation"
  task :clobber do
    rm_rf 'doc/output'
  end
  
  desc "Installs dependencies for development environment"
  task :install_dependencies do
    pre_commit.install_dependencies
  end
  
  desc "Updates dependencies for development environment"
  task :update_dependencies do
    pre_commit.update_dependencies
  end

  desc "Build the website, but do not publish it"
  task(:website) {core.website}

  def pre_commit
    PreCommit::Rspec.new(self)
  end
  
  desc "Fix line endings"
  task(:fix_cr_lf) {pre_commit.fix_cr_lf}
  
  namespace :git do
    desc "Commit rspec-dev & sub-projects"
    task :commit do
      git.commit
    end
    
    desc "Show status of rspec-dev & sub-projects"
    task :status do
      git.status
    end
  
    desc "Push rspec-dev & sub-projects to github"
    task :push do
      git.push
    end

    desc "Add remote references to rspec-dev & sub-projects"
    task :add_remotes do
      git.add_remotes
    end
  end
end