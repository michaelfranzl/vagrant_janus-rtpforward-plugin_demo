Vagrant.configure('2') do |config|
  config.vm.box = 'debian/buster64'
  config.vm.hostname = 'vagrant-janus-rtpforward-plugin-demo'
  config.vm.provider('libvirt') do |lv|
    lv.memory = 1500
    lv.machine_virtual_size = 20
  end
  config.vm.provision 'shell', path: 'provisioners/packages'

  config.vm.provision 'shell', path: 'provisioners/gencert', privileged: false
  config.vm.provision 'shell', path: 'provisioners/janus-gateway', privileged: false
  config.vm.provision 'shell', path: 'provisioners/janus-rtpforward-plugin', privileged: false

  config.vm.provision 'shell', path: 'provisioners/nvm', privileged: false
  config.vm.provision 'shell', path: 'provisioners/janus-rtpforward-plugin-demo', privileged: false

  config.vm.network "forwarded_port", guest: 8989, host: 8989 # wss
  config.vm.network "forwarded_port", guest: 8188, host: 8188 # ws
  config.vm.network "forwarded_port", guest: 8080, host: 8080 # http demo

  config.vm.post_up_message = "Run demo: `vagrant ssh -c 'cd /vagrant; tmuxinator --local'`"
end
