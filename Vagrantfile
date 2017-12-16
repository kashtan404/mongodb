# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = 2

ldap_domain = 'MAIN\\'
ldap_username = ldap_domain + ENV['VCENTER_USER']
ldap_password = ENV['VCENTER_PASS']
vcenter = ENV['VCENTER_HOST']

cluster = [{ hostname: 'c00test01', ip: '<IP>', cpus: '2', vram: '4096'},
           { hostname: 'c00test02', ip: '<IP>', cpus: '2', vram: '4096'},
           { hostname: 'c00test03', ip: '<IP>', cpus: '2', vram: '4096'},
           { hostname: 'c00test04', ip: '<IP>', cpus: '2', vram: '4096'},
		   { hostname: 'c00test05', ip: '<IP>', cpus: '2', vram: '4096'},
		   { hostname: 'c00test06', ip: '<IP>', cpus: '2', vram: '4096'},
		   { hostname: 'c00test07', ip: '<IP>', cpus: '2', vram: '4096'},
		   { hostname: 'c00test08', ip: '<IP>', cpus: '2', vram: '4096'},
		   { hostname: 'c00test09', ip: '<IP>', cpus: '2', vram: '2048'},
		   { hostname: 'c00test10', ip: '<IP>', cpus: '2', vram: '2048'},
		   { hostname: 'c00test11', ip: '<IP>', cpus: '2', vram: '2048'},
		   { hostname: 'c00test12', ip: '<IP>', cpus: '2', vram: '2048'},
		   { hostname: 'c00test00', ip: '<IP>', cpus: '2', vram: '2048'},
          ]

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'dummy'
  config.vm.box_url = './box/dummy.box'
  config.ssh.insert_key = false
  cluster.each do |node|
    config.vm.define node[:hostname] do |h|
      h.vm.hostname = node[:hostname]
      h.vm.network :private_network, ip: node[:ip]
      h.vm.provider :vsphere do |vs|
        vs.name = node[:hostname]
        vs.host = vcenter
        vs.compute_resource_name = '<resource_name>'
        vs.resource_pool_name = '<resource_pool>'
        vs.customization_spec_name = '<customisation_spec_name>'
        vs.template_name = '<template_name>'
        vs.vm_base_path = '<path>'
		vs.memory_mb = node[:vram]
		vs.cpu_count = node[:cpus]
        vs.user = ldap_username
        vs.password = ldap_password
        vs.insecure = 'true'
      end
	end
  end
end