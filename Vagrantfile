################################
# Author: F. Mayer (6. Nov 2019)
################################

$packages = <<-SCRIPT
  pacman -Syu --noconfirm
  pacman -Sy --noconfirm htop git perl binutils patch
  pacman -Sy --noconfirm jq gcc expac fakeroot
  pacman -Sy --noconfirm make cmake pkgconfig
  pacman -Sy --noconfirm meson gtest gmock
  pacman -Sy --noconfirm texlive-most wget python-numpy python2-numpy openmpi
SCRIPT

$packagesDevel = <<-SCRIPT
  pacman -Sy --noconfirm vim ranger
SCRIPT

$installAuracle = <<-SCRIPT
  curl -s -o auracle.tar.gz https://aur.archlinux.org/cgit/aur.git/snapshot/auracle-git.tar.gz
  tar -xvf auracle.tar.gz
  cd auracle-git/
  makepkg --noconfirm
  sudo pacman --noconfirm -U *.tar.*
  cd
SCRIPT

$installPacaur = <<-SCRIPT
  curl -s -o p.tar.gz https://aur.archlinux.org/cgit/aur.git/snapshot/pacaur.tar.gz
  tar -xvf p.tar.gz
  cd pacaur
  makepkg --noconfirm
  sudo pacman --noconfirm -U *.tar.*
  cd
SCRIPT

$cleanHome = <<-SCRIPT
  rm -rf ~/*
SCRIPT

$cleanPac = <<-SCRIPT
  pacaur --noconfirm -Scc
  sudo pacman --noconfirm -Scc
SCRIPT

$buildRoseAndDeps = <<-SCRIPT
  # THESE ARE ROSES additional dependencies
  sudo pacman -Sy --noconfirm flex bison unzip gdb autoconf automake graphviz
  sudo pacman -Sy --noconfirm jdk8-openjdk
  pacaur -Sy --noconfirm gcc7

  cd /vagrant/boost-65-compat
  makepkg -f --noconfirm
  sudo pacman --noconfirm -U *.tar.xz
  cd

  # cd rose-github
  # makepkg --noconfirm
  # #sudo pacman --noconfirm
  # cd
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024*32
    v.cpus = 4
  end

  # enable -j4 builds
  config.vm.provision "file", source: "makepkg.conf", destination: "~/makepkg.conf"
  config.vm.provision "file", source: "rose-github", destination: "~/rose-github"
  config.vm.provision "shell", inline: "cp makepkg.conf /etc/makepkg.conf"

  config.vm.provision "shell", inline: $packages
  config.vm.provision "shell", inline: $packagesDevel
  config.vm.provision "shell", inline: $installAuracle, privileged: false
  config.vm.provision "shell", inline: $installPacaur, privileged: false

  config.vm.provision "shell", inline: $buildRoseAndDeps, privileged: false

  config.vm.provision "shell", inline: $cleanPac

end
