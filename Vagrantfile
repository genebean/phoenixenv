$utf8 = <<UTF8
update-locale LANG=en_US.UTF-8
update-locale LANGUAGE=en_US.UTF-8
update-locale LC_ALL=en_US.UTF-8
locale-gen en_US.UTF-8
UTF8

$install_script = <<SCRIPT
export DEBIAN_FRONTEND=noninteractive
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
curl -sL https://deb.nodesource.com/setup_7.x | bash -
dpkg -i erlang-solutions_1.0_all.deb
apt-get update
yes | apt-get install esl-erlang elixir inotify-tools nodejs postgresql postgresql-contrib
cd / && sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'postgres';"
su - vagrant -c 'yes | mix local.hex'
su - vagrant -c 'yes | mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez'
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "puppetlabs/ubuntu-16.04-64-puppet"
  config.vm.provision "shell", inline: $utf8
  config.vm.provision "shell", inline: $install_script
  config.vm.network "forwarded_port", guest: 4000, host: 4000
end

