## Ansible Rails Box
#### An Ansible powered Rails development box
##### By Michael Sherron
###### *MIT License*

Need an environment to develop a Rails app with a Sqlite DB? Spin up this vagrant box, provision it with the Ansible scripts and you should be all set!

#### Dependencies:
  * [Vagrant 1.7.2](https://www.vagrantup.com/download-archive/v1.7.2.html)
  * [VirtualBox 4.3](https://www.virtualbox.org/wiki/Download_Old_Builds)
  * [Homebrew](http://brew.sh/)
  * [Ansible](http://docs.ansible.com/ansible/intro_installation.html)

#### Detailed instructions:
  1. Make sure that you have the dependencies installed on your host machine (see links above)
  1. Vagrant will automatically update your hosts file, if you install the hostsupdater plugin (`vagrant plugin install vagrant-hostsupdater`).
  1. Once Homebrew is installed, installing Ansible is as easy as `brew install ansible`.
  1. Clone the repo: `git clone https://github.com/msherron/ansible-railsbox.git`
  1. `cd ansible-railsbox`
  1. Copy example.config.yml to config.yml. Change any of the default values you wish.
  1. Start the guest  VM with 'vagrant up'. This process should take no more than 10 minutes on a decent connection.
  1. Once completed, go to [railsapp.local](http://railsapp.local) in a browser - you are all set!
  1. Note that your apps' files can be reached via your text editor at ~/ansible-railsbox/railsapp (you can change this in config.yml).


***
