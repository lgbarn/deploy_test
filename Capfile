# Load DSL and set up stages
#require 'capistrano/setup'

# Include default deployment tasks
#require 'capistrano/deploy'

# Include tasks from other gems included in your Gemfile
#
# For documentation on these, see for example:
#
#   https://github.com/capistrano/rvm
#   https://github.com/capistrano/rbenv
#   https://github.com/capistrano/chruby
#   https://github.com/capistrano/bundler
#   https://github.com/capistrano/rails
#   https://github.com/capistrano/passenger
#
# require 'capistrano/rvm'
# require 'capistrano/rbenv'
# require 'capistrano/chruby'
# require 'capistrano/bundler'
# require 'capistrano/rails/assets'
# require 'capistrano/rails/migrations'
# require 'capistrano/passenger'
#

role :linux_all, "root@172.29.33.11", "root@172.29.33.12", "root@172.29.33.13"

desc "Show Kernel"
task :show_kernel, :roles => :linux_all do
  run "uname -a"
end
desc "Install Spacewalk"
task :install_spacewalk, :roles => :linux_all do
  run "rpm -Uvh http://yum.spacewalkproject.org/2.3-client/RHEL/6/x86_64/spacewalk-client-repo-2.3-2.el6.noarch.rpm && BASEARCH=$(uname -i) && rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm"
  run "yum -y install rhn-client-tools rhn-check rhn-setup rhnsd m2crypto yum-rhn-plugin"
  run "rpm -Uvh http://usalfd0spcmst01.corp.jabil.org/pub/rhn-org-trusted-ssl-cert-1.0-1.noarch.rpm"
  run "rhnreg_ks --serverUrl=https://usalfd0spcmst01.corp.jabil.org/XMLRPC --sslCACert=/usr/share/rhn/RHN-ORG-TRUSTED-SSL-CERT --activationkey=1-centos6-x86_64"
end
desc "Install Puppet"
task :install_puppet, :roles => :linux_all do
  run "curl -k https://10.15.21.178:8140/packages/current/install.bash | /bin/bash"
end


# Load custom tasks from `lib/capistrano/tasks` if you have any defined
#Dir.glob('lib/capistrano/tasks/*.rake').each { |r| import r }
