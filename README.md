# Ansible Role: Package Installation

This role can be used to install a bunch of packages on different linux
distributions (so far Arch Linux and Ubuntu). I use is as part of my
laptop/desktop setup process. This way the same software packages are installed
on all my machines. Well, actually depending on what I use a specific computer
for, I install different sets of packages. That's why I split all packages up
into groups:

- **bluetooth**: Packages needed to use Bluetooth.
- **browser**: Some browser that I like to use. Either for day-to-day use or
  for testing.
- **essential**: Packages that I pretty much need on every machine that I work
  on (e.g. neovim, or git).
- **multimedia**: Packages to work with different media files (e.g. music
  player, or image viewer)
- **network**: Packages needed for networking.
- **python**: Python packages that I want to have installed system wide. I
  don't like to install them with **pip** (I use pip only for virtual
  environments). Therefore these packages are also installed via the distro's
  package manager.
- **x-related**: Packages related to the X server. Of corse **xorg** itself,
  but also for example **xmobar** that I use in my **xmonad** configuration.


So far it has only be tried on two virtual (vagrant) machines. There hasn't
been any real testing. If I find the time to really test everything, I will do
that, but for now, I just use it as it is.


## Requirements

This role was written to setup Arch Linux and Ubuntu machine. I would think it
should work on Debian as well, but I haven't tried. If you use it on an Arch
machine **pacman** needs to be installed; if you use it on Ubuntu **apt** has
to be installed. Well, I guess there is actually no need to mention that,
because these are the default packages managers in those distros.


## Role Variables

The following variable is in vars/main.yml:

- package_types: It's a list of the different package types that I defined to
  group packages together by a common subject.

The following variables are in vars/list\_of\_{{ ansible_os_family }}\_packages.yml.
They each define a list of packages that I wanted to have for each type defined
in package\_types.

- list_of_bluetooth_packages
- list_of_browser_packages
- list_of_essential_packages
- list_of_multimedia_packages
- list_of_network_packages
- list_of_python_packages
- list_of_x-related_packages

In defaults/main.yml are the following boolean variables. They determine
whether or not the packages that belong to a certain type are installed or not.
If you don't want to install the packages of a certain type, you disable the
installation of these packages by overwriting the specific variable with
"false". Per default they are all set to "true", so all packages are installed.

- install_bluetooth_packages: true
- install_browser_packages: true
- install_essential_packages: true
- install_multimedia_packages: true
- install_network_packages: true
- install_python_packages: true
- install_x-related_packages: true


## Dependencies

None


## Example Playbook

    - hosts: localhost
      roles:
         - { role: schuam.package-installation }


## License

MIT


## Author Information

This role was created in 2022 by [Andreas Schuster](https://www.schuam.de/).

