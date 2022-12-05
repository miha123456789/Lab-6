ENV["VAGRANT_EXPERIMENTAL"] = "disks"
Vagrant.configure("2") do |config|
  config.vm.define "mmm6" do |mmm6|
    mmm6.vm.hostname = "mmm6"
    mmm6.vm.box = "ubuntu/focal64"
    mmm6.vm.network "private_network", ip: "192.168.33.10"
    mmm6.vm.network "forwarded_port", guest: 80, host: 8888

    config.vm.disk :disk, size: "300MB", name: "additional_size1"
    config.vm.disk :disk, size: "300MB", name: "additional_size2"
    config.vm.disk :disk, size: "300MB", name: "additional_size3"
    config.vm.disk :disk, size: "300MB", name: "additional_size4"  


    
  end
  config.vm.provision "shell", inline: <<-SHELL
  
    pvcreate /dev/sdc /dev/sdd /dev/sde /dev/sdf

    vgcreate vg00 /dev/sdc /dev/sdd /dev/sde /dev/sdf
  
    lvcreate -l 100%FREE vg00 /dev/sdc /dev/sdd -n lv1
    lvcreate -l 100%FREE vg00 /dev/sde /dev/sdf -n lv2

    mkfs.ext4 /dev/vg00/lv1  
    mkfs.ext4 /dev/vg00/lv2

    mkdir /mnt/vol1 /mnt/vol2
    
    echo '/dev/vg00/lv1 /mnt/vol1 ext4 defaults 0 0' >>/etc/fstab
    echo '/dev/vg00/lv2 /mnt/vol2 ext4 defaults 0 0' >>/etc/fstab

    mount -a


  SHELL
  
end
