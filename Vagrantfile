# detailed instructions for installing
$script = <<SCRIPT

# Because this is an *ISOLATED* VM its "okay" to "sudo"
sudo -i
# Update will install any security patches
apt-get update -y
# see: https://gist.github.com/wingdspur/2026107
apt-get install openjdk-7-jre-headless -y

### Check elastic.co/downloads/elasticsearch for latest version of ElasticSearch and replace wget link below
wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.7.2.deb
dpkg -i elasticsearch-1.7.2.deb

curl -L http://github.com/elasticsearch/elasticsearch-servicewrapper/tarball/master | tar -xz
mkdir -p /usr/local/share/elasticsearch/bin/
mv *servicewrapper*/service /usr/local/share/elasticsearch/bin/
rm -Rf *servicewrapper*

# create a shortcut ("symbolic link") to the elasticsearch searvice
/usr/local/share/elasticsearch/bin/service/elasticsearch install
ln -s `readlink -f /usr/local/share/elasticsearch/bin/service/elasticsearch` /usr/local/bin/rcelasticsearch

# start, then wait 10 seconds, then use curl to check its is working as expected:
service elasticsearch start && sleep 10 && curl http://localhost:9200



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
