# openelb_on_k3s_vagrant_libvirt_ansible

Vagrant-libvirt setup that creates a VM with [k3s](https://k3s.io/), the minimal
lightweight Kubernetes distribution.

On top of k3s, this setup installs [OpenELB](https://openelb.io/).

Default OS is openSUSE Leap 15.6, but that can be changed in the Vagrantfile.
Please be aware, that this might break the Ansible provisioning.

## Warning regarding the IP address range

Due to limitations in vagrant-libvirt, this setup hardcodes the IPs that OpenELB
can hand out to Kubernetes services of type `LoadBalancer`. If your network
setup uses a different IP address range than `192.168.121.0/24`, feel free to
adjust the IP in the file `ansible/group_vars/all/ip_addresses.yml`.

## Vagrant

1. You need `vagrant`, obviously. And `git`. And Ansible...
1. Fetch the box, per default this is `opensuse/Leap-15.6.x86_64`, using
   `vagrant box add opensuse/Leap-15.6.x86_64`.
1. Make sure the git submodules are fully working by issuing
   `git submodule init && git submodule update`
1. Run `vagrant up`
1. If the deployment finishes successfully and outputs the Nginx URL at the end,
   the the `traefik` service has properly received a loadbalancer IP from
   OpenELB and is reachable from the outside.
1. Party!

## Cleaning up

The VMs can be torn down after playing around using `vagrant destroy`. This will
also remove the kubeconfig file `ansible/k3s-kubeconfig`.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via git@johannes-kastl.de
