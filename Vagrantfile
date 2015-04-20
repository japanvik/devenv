# -*- mode: ruby -*-
# vi: set ft=ruby :

# Location where we want to keep the data files
APPS = "/apps"

Vagrant.configure("2") do |config|

    config.vm.define "mongo" do |v|
        v.vm.provider "docker" do |d|
            d.image = "mongo:latest"
            d.name = "mongo"
            d.expose = [27017]
            d.ports = ["27017:27017"]
            # Mongo doesn't like shared volumes...
            #d.volumes = ["#{APPS}/mongo/data/db:/data/db", "#{APPS}/mongo/logs:/var/log/mongodb" ]
            d.vagrant_vagrantfile = "./docker-host/Vagrantfile"
        end
    end

    config.vm.define "deployd" do |v|
        v.vm.provider "docker" do |d|
            d.image = "japanvik/deployd"
            d.ports = ["2403:2403"]
            # Not sure if we need this for deployd
            #d.volumes = ["#{APPS}/deployd/:/app/src"]
            d.link("mongo:mongo")
            d.vagrant_vagrantfile = "./docker-host/Vagrantfile"
        end
    end

end
