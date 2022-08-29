MACHINES = {
:inetRouter => {
        :box_name => "centos7",
        :net => [
                   {ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {ip: '192.168.50.10', adapter: 8},
                ]
  },
  :centralRouter => {
        :box_name => "centos7",
        :net => [
                   {ip: '192.168.255.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {ip: '192.168.10.1', adapter: 3, netmask: "255.255.255.240", virtualbox__intnet: "dir-net"},
                   {ip: '192.168.10.33', adapter: 4, netmask: "255.255.255.240", virtualbox__intnet: "hw-net"},
                   {ip: '192.168.10.65', adapter: 5, netmask: "255.255.255.192", virtualbox__intnet: "mgt-net"},
                   {ip: '192.168.255.9', adapter: 6, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"},
                   {ip: '192.168.255.5', adapter: 7, netmask: "255.255.255.252", virtualbox__intnet: "office2-central"},
                   {ip: '192.168.50.11', adapter: 8},
                ]
  },
  
  :centralServer => {
        :box_name => "centos7",
        :net => [
                   {ip: '192.168.10.2', adapter: 2, netmask: "255.255.255.240", virtualbox__intnet: "dir-net"},
                   {ip: '192.168.50.12', adapter: 8},
                ]
  },
  :office1Router => {
        :box_name => "centos7",
        :vm_name => "office1Router",
        :net => [
              {ip: '192.168.255.10', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"},
              {ip: '192.168.2.1', adapter: 3, netmask: "255.255.255.192", virtualbox__intnet: "dev1-net"},
              {ip: '192.168.2.65', adapter: 4, netmask: "255.255.255.192", virtualbox__intnet: "test1-net"},
              {ip: '192.168.2.129', adapter: 5, netmask: "255.255.255.192", virtualbox__intnet: "managers-net"},
              {ip: '192.168.2.192', adapter: 6, netmask: "255.255.255.192", virtualbox__intnet: "office1-net"},
              {ip: '192.168.50.20', adapter: 8},
                ]
    },
 :office1Server => {
        :box_name => "centos7",
        :vm_name => "office1Server",
        :net => [
              {ip: '192.168.2.130', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "managers-net"},
              {ip: '192.168.50.21', adapter: 8},
                ]
    },
  :office2Router => {
        :box_name => "centos7",
        :vm_name => "office2Router",
        :net => [
              {ip: '192.168.255.6', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office2-central"},
              {ip: '192.168.3.1', adapter: 3, netmask: "255.255.255.128", virtualbox__intnet: "dev2-net"},
              {ip: '192.168.3.129', adapter: 4, netmask: "255.255.255.192", virtualbox__intnet: "test2-net"},
              {ip: '192.168.3.193', adapter: 5, netmask: "255.255.255.192", virtualbox__intnet: "office2-net"},
              {ip: '192.168.50.30', adapter: 8},
                ]
    },
   :office2Server => {
        :box_name => "centos7",
        :vm_name => "office2Server",
        :net => [
              {ip: '192.168.3.2', adapter: 2, netmask: "255.255.255.128", virtualbox__intnet: "dev2-net"},
              {ip: '192.168.50.31', adapter: 8},
                ]
    },

  
}

Vagrant.configure("2") do |config|
  config.vbguest.auto_update = false # disable VirtualBox Guest Additions
  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        
        if boxconfig.key?(:public)
          box.vm.network "public_network", boxconfig[:public]
        end

        box.vm.provision "ansible" do |ansible|
        ansible.playbook = "main.yaml"
      end
    end
  end
  
  
end