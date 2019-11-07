# bugReproductionPackage03

Bug reproduction package for ROSE issue #48

## Usage

This is a repo containing a [vagrant](https://www.vagrantup.com/) description
of a virtual machine.

1. Install vagrant
1. `cd` into this directory
1. Run `$ vagrant up`

Vagrant will now build up a virtual machine and run a
complete setup. The environment of the virtual machine
can then be used to reproduce ROSE issue #48.

To reproduce run

1. `cd` into this directory
1. Run `$ vagrant ssh`
1. Change into directory `/vagrant/rose-github`
1. Then run `$ makepkg`

Expected: `$ makepkg` fails with a compiler error described in [#48](https://github.com/rose-compiler/rose/issues/48)

## Trick

If you happen to have a very fast PC, consider changing
[this line](https://github.com/forflo/bugReproductionPackage03/blob/f6902b22e8ba47fd457bbedce1991d24f52bf3e9/makepkg.conf#L44)
in `makepkg.conf` to the double amount of cores you have on your system!
