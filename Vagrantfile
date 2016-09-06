# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # install the 'dummy' box by running the following
  # vagrant box add dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box
  config.vm.box = "dummy"
  # config.vm.box = "trusty64"
  # config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # config.vm.network :private_network, ip: "192.168.20.115"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--name", "MyCoolApp", "--memory", "512"]
  end

  config.vm.provider :aws do |aws, override|
    # get these from env AWS_ACCESS_KEY, AWS_SECRET_KEY
    # or from ~/.aws/credentials and enter under [default] aws_access_key_id and aws_secret_access_key
    # aws.access_key_id = ""
    # aws.secret_access_key = ""
    # aws.session_token = ""

    # enter the name of the keypair (without .pem)
    #######################
    aws.keypair_name = ""

    # open ssh to the universe, but need to find out how to create a security group with my ip address
    #######################
    aws.security_groups = [ 'home-ssh-world-http-s' ]
    aws.region = "eu-west-1"
    aws.instance_type = "t2.micro"

    # Ubuntu AMIs https://cloud-images.ubuntu.com/locator/ec2/
    # eu-west-1 trusty  14.04 LTS amd64 hvm:ebs 20160809.1  ami-a7412ad4
    aws.ami = "ami-a7412ad4"
    override.ssh.username = "ubuntu"

    # enter the full path to the keypair pem file (with .pem extension)
    ##################################
    override.ssh.private_key_path = ""
  end


  # Shared folder from the host machine to the guest machine. Uncomment the line
  # below to enable it.
  #config.vm.synced_folder "../../../my-cool-app", "/webapps/mycoolapp/my-cool-app"

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.host_key_checking = false
    ansible.verbose = "vvv"
  end
end