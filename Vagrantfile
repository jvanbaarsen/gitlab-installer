# -*- mode: ruby -*-
# vi: set ft=ruby :

# Author: Tuomo Tanskanen <tumi@tumi.fi>

Vagrant.configure("2") do |config|

  config.vm.define :gitlab do |config|
    # As default, only expose port 80 for GitLab
    config.vm.network :forwarded_port, guest: 80, host: 80

    # Uncomment if you use SSL
    # config.vm.network :forwarded_port, guest: 443, host: 443

    # config.vm.provision :shell, :path => "install-gitlab.sh"

    # Uncomment these if you want CI too
    config.vm.provision :shell, :path => "install-gitlab-ci.sh"
    config.vm.network :forwarded_port, guest: 3000, host: 3000

    # CI Runner cannot be automated in a full install as it needs a token from CI
    # Install it (from here to by hand), then go to ~gitlab_ci_runner/gitlab-ci-runner
    # and execute as root: "../register-runner.sh <token>"
    # config.vm.provision :shell, :path => "install-gitlab-ci-runner.sh"
  end

  # GitLab recommended specs
  config.vm.provider "virtualbox" do |v, override|
    override.vm.box = "precise64"
    override.vm.box_url = "http://files.vagrantup.com/precise64.box"
    v.customize [ "modifyvm", :id, "--cpus", "2" ]
    v.customize [ "modifyvm", :id, "--memory", "1536" ]
  end

  config.vm.provider "vmware_fusion" do |v, override|
    override.vm.box = "precise64_fusion"
    override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
    v.vmx["numvcpus"] = "2"
    v.vmx["memsize"] = "1536"
  end
end
