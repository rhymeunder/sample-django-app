$bootstrap = <<BOOTSTRAP
echo "Configuring environment"
echo 'export WORKON_HOME=\$HOME/.virtualenvs' > /home/ubuntu/.bash_environment
echo 'export PROJECT_HOME=/vagrant' >> /home/ubuntu/.bash_environment
echo 'source /usr/local/bin/virtualenvwrapper.sh' >> /home/ubuntu/.bash_environment
echo 'workon senior-project' >> /home/ubuntu/.bash_environment

echo  >> /home/ubuntu/.bashrc
echo '######' >> /home/ubuntu/.bashrc
echo 'source \$HOME/.bash_environment' >> /home/ubuntu/.bashrc
source /usr/local/bin/virtualenvwrapper.sh; mkvirtualenv --system-site-packages senior-project
BOOTSTRAP

Vagrant.configure("2") do |config|
  config.vm.box = "senior-project"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = ENV['AWS_ACCESS_KEY_ID']
    aws.secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']
    aws.ami = ENV['AWS_AMI_ID']
    aws.region = ENV['AWS_REGION']
    aws.keypair_name = ENV['AWS_KEYPAIR_NAME']
    aws.instance_type = "t1.micro"
    aws.security_groups = [ ENV['AWS_SECURITY_GROUP'] ]

    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = ENV['AWS_PRIVATE_KEY_PATH']
    override.vm.provision :shell, :inline => $bootstrap, privileged: false
  end
end
