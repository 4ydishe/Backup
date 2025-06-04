# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Общие настройки для обеих ВМ
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  #
  # 1) Настройка backup-server
  #
  config.vm.define "backup-server" do |backup|
    backup.vm.hostname = "backup-server"
    backup.vm.network "private_network", ip: "192.168.56.10"

    # Здесь внутри этой ВМ Ansible запускается локально (ansible_local),
    # чтобы не пытаться SSH‐подключаться к самому себе по IP
    backup.vm.provision "ansible_local" do |ansible|
      ansible.playbook       = "/vagrant/ansible/playbook.yml"
      ansible.inventory_path = "/vagrant/ansible/inventory.ini"
      ansible.limit          = "backup_server"
      ansible.extra_vars     = {
        ansible_python_interpreter: "/usr/bin/python3"
      }
    end
  end

  #
  # 2) Настройка client
  #
  config.vm.define "client" do |client|
    client.vm.hostname = "client"
    client.vm.network "private_network", ip: "192.168.56.11"

    # И внутри client Ansible запускается локально
    client.vm.provision "ansible_local" do |ansible|
      ansible.playbook       = "/vagrant/ansible/playbook.yml"
      ansible.inventory_path = "/vagrant/ansible/inventory.ini"
      ansible.limit          = "client"
      ansible.extra_vars     = {
        ansible_python_interpreter: "/usr/bin/python3"
      }
    end
  end
end
