# detailed instructions for installing
$script = <<SCRIPT

sudo -i
# add repo for Java 8
add-apt-repository -y ppa:webupd8team/java
# update ubuntu (security etc.)
apt-get update

#in stall Java 8
apt-get -y install oracle-java8-installer

### Check http://www.elasticsearch.org/download/ for latest version of ElasticSearch and replace wget link below
wget -O - http://packages.elasticsearch.org/GPG-KEY-elasticsearch | sudo apt-key add -

# wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.6.0.deb
echo 'deb http://packages.elasticsearch.org/elasticsearch/1.7.2/debian stable main' | sudo tee /etc/apt/sources.list.d/elasticsearch.list


# curl -L http://github.com/elasticsearch/elasticsearch-servicewrapper/tarball/master | tar -xz
# sudo mkdir -p /usr/local/share/elasticsearch/bin/
# sudo mv *servicewrapper*/service /usr/local/share/elasticsearch/bin/
# rm -Rf *servicewrapper*
#
# sudo /usr/local/share/elasticsearch/bin/service/elasticsearch install
# sudo ln -s `readlink -f /usr/local/share/elasticsearch/bin/service/elasticsearch` /usr/local/bin/rcelasticsearch

# curl http://localhost:9200

SCRIPT

Vagrant.configure("2") do |config|

  # config.vm.box = "base"
  config.vm.box = "ubuntu-nodejs-server"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :forwarded_port, guest: 9200, host: 9200
  config.vm.network :forwarded_port, guest: 9300, host: 9300
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.provision :shell, :inline => $script

end
