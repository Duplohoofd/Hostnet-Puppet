1 # -*- mode: ruby -*
  2 # vi: set ft=ruby :
  3 Vagrant.configure(2) do |config|
  4     [ "puppet-server", ].each do | name |
  5         config.vm.provider "libvirt"
  6         config.vm.provider :libvirt do |libvirt|
  7             libvirt.cpus = 4
  8             libvirt.memory = 4096
  9         end
 10         config.vm.define name do |box|
 11             box.vm.box = "centos/7"
 12             box.vm.hostname = "#{name}.local"
 13             box.vm.network "public_network",
 14                 :dev => "lab"
 15             box.vm.provision :puppet do |puppet|
 16         puppet.environment_path = 'tests'
 17         puppet.environment = 'vagrant'
 18         puppet.binary_path = '/opt/puppetlabs/bin'
 19         puppet.options = "--verbose --debug --modulepath /etc/puppetlabs/code/project:/etc/puppetlabs/code/modules/"
 20         end
 21 
 22         end
 23         config.vm.provision "shell", inline: <<-SHELL
 24             ip r d default via 192.168.121.1 dev eth0
 25             if [ ! -f /root/.ikhebmijnrommelgeinstalleerd ]; then
 26                     yum -q -y install epel-release vim-enhanced
 27                     rpm -Uvh http://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm
 28                     yum -q -y install puppet-agent
 29                     puppet module install puppetlabs-stdlib
 30                     touch /root/.ikhebmijnrommelgeinstalleerd
 31             fi
 32         SHELL
 33             end
 34 end
~                           
