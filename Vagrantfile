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

curl -L https://github.com/elasticsearch/elasticsearch-servicewrapper/tarball/master | tar -xz
mkdir -p /usr/local/share/elasticsearch/bin/
mv *servicewrapper*/service /usr/local/share/elasticsearch/bin/
rm -Rf *servicewrapper*

# create a shortcut ("symbolic link") to the elasticsearch searvice
/usr/local/share/elasticsearch/bin/service/elasticsearch install
ln -s `readlink -f /usr/local/share/elasticsearch/bin/service/elasticsearch` /usr/local/bin/rcelasticsearch

# start, then wait 7 seconds (while it starts), then curl to check its working:
service elasticsearch start && sleep 7 && curl http://localhost:9200

# Now the Fun Part!
wget https://download.elastic.co/kibana/kibana/kibana-4.1.2-linux-x64.tar.gz
gunzip kibana-4.1.2-linux-x64.tar.gz
tar -xvf kibana-4.1.2-linux-x64.tar

# update the configuration file:
# vim kibana-4.1.2-linux-x64/config/kibana.yml
rm kibana-4.1.2-linux-x64/config/kibana.yml
# see: https://github.com/nelsonic/learn-kibana/blob/master/kibana.yml
wget -O kibana-4.1.2-linux-x64/config/kibana.yml https://git.io/vcpyt

# create a new folder to store the kibana files:
mkdir -p /opt/kibana

# copy all the files to the new directory we just created:
cp -Rrvf kibana-4.1.2-linux-x64/* /opt/kibana/
rm kibana-4.1.2-linux-x64.tar
# Download init.d script for kibana service.
cd /etc/init.d/
wget https://gist.githubusercontent.com/thisismitch/8b15ac909aed214ad04a/raw/bce61d85643c2dcdfbc2728c55a41dab444dca20/kibana4
sudo chmod +x /etc/init.d/kibana4
sudo update-rc.d kibana4 defaults 96 9
sudo service kibana4 start && sleep 7 && curl http://localhost:5601

SCRIPT

Vagrant.configure("2") do |config|

  # config.vm.box = "base"
  config.vm.box = "ubuntu-nodejs-server"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :forwarded_port, guest: 5601, host: 5601
  config.vm.network :forwarded_port, guest: 9200, host: 9200
  config.vm.network :forwarded_port, guest: 9300, host: 9300
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.provision :shell, :inline => $script

end
