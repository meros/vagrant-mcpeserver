# Requirements
A recent vagrant: https://www.vagrantup.com/docs/installation/
An X11 server. For linux this is usually provided. For OS X, install https://www.xquartz.org/

# Booting up
 This will take a while, be patient
```bash
vagrant up
```

# First time setup
Enter VM:
```bash
vagrant ssh
```

Enter ~/mcpelauncher-linux and edit server.properties (see https://github.com/MCMrARM/mcpelauncher-linux/wiki/Dedicated-Server)

Trigger first time setup (to download APK)

```bash
./build/mcpelauncher.sh
```

Enable and start server daemon
```bash
sudo systemctl start mcpeserver
sudo systemctl enable mcpeserver
```