Vagrant.configure('2') do |config|
  config.vm.box = 'debian/bookworm64'
  config.vm.hostname = 'vagrant-janus-rtpforward-plugin-demo'
  config.vm.provider('libvirt') do |lv|
    lv.memory = 1500
    lv.machine_virtual_size = 20
  end
  config.vm.provision 'shell', path: 'provisioners/packages'

  config.vm.provision 'shell', path: 'provisioners/gencert', privileged: false
  config.vm.provision 'shell', path: 'provisioners/janus-gateway', privileged: false
  config.vm.provision 'shell', path: 'provisioners/janus-rtpforward-plugin', privileged: false

  config.vm.network "forwarded_port", guest: 8989, host: 8989 # wss
  config.vm.network "forwarded_port", guest: 8188, host: 8188 # ws
  config.vm.network "forwarded_port", guest: 7188, host: 7188 # ws for admin API
  config.vm.network "forwarded_port", guest: 5173, host: 5173 # http demo (vite default port)

  config.vm.post_up_message = %Q(
    The setup was successful.

    1. start the services in the virtual machine:

    vagrant ssh -c 'env -C /vagrant tmuxinator --local'

    2. access the web application from your host's browser: http://localhost:5173
  )
end
