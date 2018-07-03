$privscript = <<-SCRIPT
  echo Installing mcpelauncher-linux
  cp /vagrant/*.service /etc/systemd/system/
  systemctl daemon-reload

  dpkg --add-architecture i386
  apt update
  apt install -y \
    cmake gcc-multilib g++-multilib zlib1g-dev:i386 libx11-dev:i386\
    libzip-dev:i386 libpng-dev:i386 libcurl4-openssl-dev:i386 libssl-dev:i386\
    libgles2-mesa-dev:i386 libudev-dev:i386 libevdev-dev:i386 libgtk2.0-0:i386\
    libgtkglext1:i386 libasound2:i386 libnss3:i386 libxss1:i386 libgconf2-4:i386\
    libxtst6:i386 libudev1:i386 protobuf-compiler libprotobuf-dev:i386
SCRIPT

$script = <<-SCRIPT
  git clone --recursive https://github.com/MCMrARM/mcpelauncher-linux.git
  cd mcpelauncher-linux
  cp /vagrant/server.properties .
  ./download_icon.sh
  ./setup_bin_libs.sh
  ./setup_cef.sh
  mkdir build
  cd build
  cmake ../
  make -j$(nproc)
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.ssh.forward_x11 = true
  config.vm.network "forwarded_port", guest: 19132, host: 19132, protocol: "udp"
  config.vm.network "forwarded_port", guest: 19132, host: 19132, protocol: "tcp"
  config.vm.provision "shell", inline: $privscript, privileged: true
  config.vm.provision "shell", inline: $script, privileged: false
end
