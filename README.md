# Installation and Setup for Vagrant, VirtualBox, and Ruby

## Ruby Installation and Setup

[Windows Installation](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe)

[Mac Installation](https://www.ruby-lang.org/en/downloads/)

- Ensure to download x64 for your OS

- Check version on your git-bash terminal

```
ruby --version
```

![](https://github.com/khanmaster/vb_vagrant_installtion/blob/master/images/ruby_version.png)


## Vagrant Installation and Setup

[Vagrant Installation](https://www.vagrantup.com/)

Check Vagrant version with
```
vagrant -v
```
> Version 2.2.7 Used


If you are running this on Windows, you will have to do the following things:

> * Make sure that if they have **Hyper-V** disabled. Check via **Turn Windows features on or off**, and disable it and restart if need be.
> * From this point onward to the end of the course, make sure they're **ALWAYS** running their terminal as an administrator, to make sure they have the rights to access whatever they need.



Once you have vagrant installed you can test it by opening a terminal and typing the following:

```bash
vagrant

# You should see the following

vagrant
Usage: vagrant [options] <command> [<args>]

    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.

Common commands:
     box             manages boxes: installation, removal, etc.
     connect         connect to a remotely shared Vagrant environment
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     hosts           Information about hostnames managed by the vagrant-hosts plugin
     hostsupdater    
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           log in to HashiCorp\'s Atlas
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     rebuild         plugin: vagrant-digitalocean: destroys and ups the vm with the same ip address
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     share           share your Vagrant environment with anyone in the world
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     vbguest         
     version         prints current and latest Vagrant version

For help on any individual command run `vagrant COMMAND -h`

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
`vagrant list-commands`.
```

## Potential Errors

**ERROR: HOSTSUPDATER**
```
There are errors in the configuration of this machine. Please fix
the following errors and try again:

Vagrant:
* Unknown configuration section 'hostsupdater'.
```
**FIX**
```
vagrant plugin install vagrant-hostsupdate
```

**ERROR: VBoxManage**
```
Stderr: VBoxManage.exe: error: Not in a hypervisor partition (HVP=0) (VERR_NEM_NOT_AVAILABLE).
```
**FIX**
- Try turning Hypervisor off, running from command prompt (Admin) with **Windows** + **X**, and rebooting after the following command
```
bcdedit /set hypervisorlaunchtype off
```

- Alternatively, the cause could be due to virtualization not being enabled on the current Windows computer.
	- Restart and enable virtualization in BIOS settings (different for different systems)
