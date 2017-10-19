# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "ceph-deploy" do |d|
    d.vm.box = "ubuntu/xenial64"
    d.vm.hostname = "ceph-deploy"
    d.vm.network "private_network", ip: "172.16.16.16", netmask: "255.240.0.0"
    d.vm.provision :shell, inline: "sed 's/127\.0\.0\.1.*ceph\-deploy.*/172\.16\.16\.16 ceph\-deploy/' -i /etc/hosts"
    d.vm.provider "virtualbox" do |v|
      v.name = "ceph-deploy"
      v.memory = 1024
      v.gui = false
    end
  end
  (1..1).each do |i|
    config.vm.define "mon#{i}" do |m|
      m.vm.box = "ubuntu/xenial64"
      m.vm.hostname = "mon#{i}"
      m.vm.network "private_network", ip: "172.16.17.#{i}", netmask: "255.240.0.0"
      m.vm.provision :shell, inline: "sed 's/127\.0\.0\.1.*mon.*/172\.16\.17\.#{i} mon#{i}/' -i /etc/hosts"
      m.vm.provider "virtualbox" do |v|
        v.name = "mon#{i}"
        v.memory = 1024
        v.gui = false
      end
    end
  end
  (1..2).each do |i|
    config.vm.define "osd#{i}" do |o|
      o.vm.box = "ubuntu/xenial64"
      o.vm.hostname = "osd#{i}"
      o.vm.network "private_network", ip: "172.16.18.#{i}", netmask: "255.240.0.0"
      o.vm.provision :shell, inline: "sed 's/127\.0\.0\.1.*osd.*/172\.16\.18\.#{i} osd#{i}/' -i /etc/hosts"
      o.vm.provider "virtualbox" do |v|
        v.name = "osd#{i}"
        v.memory = 1024
        v.gui = false
      end
    end
  end
end
