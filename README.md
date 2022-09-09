# Ansible Role: Package Installation

This role can be used to install a bunch of packages on different Linux
distributions (so far Arch Linux and Ubuntu). I use it as part of my
laptop/desktop setup process. This way the same software packages are installed
on all my machines. Well, actually depending on what I use a specific computer
for, I install different sets of packages. That's why I split all packages up
into groups:

- **ansible**: Packages needed for Ansible (on a controlling machine).
- **bluetooth**: Packages needed to use Bluetooth.
- **browser**: Some browsers that I like to use. Either for day-to-day use or
  for testing.
- **development**: Packages needed for (software) development (cmake, make,
  ...).
- **email**: Packages needed for emailing. Right no this is just thunderbird,
  but since I might switch to (Neo)Mutt in the future, I let it in here.
- **essential**: Packages that I pretty much need on every machine that I work
  on (e.g. neovim, or git).
- **font**: Some font that I use.
- **multimedia**: Packages to work with different media files (e.g. music
  players, or image viewers)
- **network**: Packages needed for networking.
- **nice_to_have**: Some packages I could probably live without, but that are
  nice to have :-).
- **office**: Packages needed for document generation like latex and pandoc,
  but also libreoffice, and some others.
- **python**: Python packages that I want to have installed system wide. I
  don't like to install them with **pip** (I use pip only for virtual
  environments). Therefore these packages are also installed via the distro's
  package manager.
- **secret**: Packages for password management.
- **virtualization**: Packages to use containers or virtual machines.
- **x_related**: Packages related to the X server. Of corse **xorg** itself,
  but also for example **xmobar** that I use in my **xmonad** configuration.

So far it has only be tried on two virtual (Vagrant) machines. There hasn't
been any real testing. If I find the time to really test everything, I will do
that, but for now, I just use it as it is.


## Requirements

This role was written to setup Arch Linux and Ubuntu machine. I would think it
should also work any other Arch- or Debian-based distro as well, but I haven't
tried. If you use it on an Arch machine **pacman** needs to be installed; if
you use it on Ubuntu **apt** has to be installed. Well, I guess there is
actually no need to mention that, because these are the default packages
managers in those distros.


## Role Variables

The following variable is in vars/main.yml:

- package_types: It's a list of the different package types that I defined to
  group packages together by a common subject (s. above).

The following variables are in vars/list\_of\_{{ ansible_os_family }}\_packages.yml.
They each define a list of distro depended packages that I wanted to have for
each type defined in package\_types.

- list_of_ansible_packages
- list_of_bluetooth_packages
- list_of_browser_packages
- list_of_development_packages
- list_of_email_packages
- list_of_essential_packages
- list_of_font_packages
- list_of_multimedia_packages
- list_of_network_packages
- list_of_nice_to_have_packages
- list_of_office_packages
- list_of_python_packages
- list_of_secret_packages
- list_of_virtualization_packages
- list_of_x_related_packages

On Ubuntu not all packages that I want to install are in the official (apt)
repositories. Therefore they have to be installed using pip or snap. Therefore
the following lists are also in vars/list\_of\_Debian\_packages.yml:

- list_of_ansible_pip_packages
- list_of_multimedia_pip_packages

- list_of_browser_snap_packages
- list_of_development_snap_packages
- list_of_essential_snap_packages

On Ubuntu the pip packages uberzug needs some dependencies that have to be
installed separately. That's what the following list in
vars/list\_of\_Debin\_packages.yml is for.

- list_of_ueberzug_dependencies

In defaults/main.yml are the following boolean variables. They determine
whether or not the packages that belong to a certain type are installed or not.
If you don't want to install the packages of a certain type, you disable the
installation of these packages by overwriting the specific variable with
"false". Per default they are all set to "true", so all packages are installed.

- install_ansible_packages: true
- install_bluetooth_packages: true
- install_browser_packages: true
- install_development_packages: true
- install_email_packages: true
- install_essential_packages: true
- install_font_packages: true
- install_multimedia_packages: true
- install_network_packages: true
- install_nice_to_have_packages: true
- install_office_packages: true
- install_python_packages: true
- install_secret_packages: true
- install_virtualization_packages: true
- install_x_related_packages: true

There are are also the following variable in defaults/main.yml, that let you
decide whether or not you want to install a lists of snap packages.

- install_browser_snap_packages: true
- list_of_development_snap_packages: true
- install_essential_snap_packages: true

## Dependencies

None


## Example Playbook

    - hosts: localhost
      roles:
         - { role: schuam.package_installation }


## License

MIT


## Author Information

This role was created in 2022 by [Andreas Schuster](https://www.schuam.de/).

