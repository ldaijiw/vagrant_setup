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

```bash
    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.
```

## VirtualBox Installation and Setup

Vagrant uses another program called VirtualBox to actually create this "virtual" machine. Vagrant basically pulls together a few tools to setup and start a virtual machine. VirtualBox is the tool that actually creates the virtual machine.

Let's install that now too.
- if you face any errors please read the instruction/steps thoroughly

[VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Ensure to install vitual box 6.1 version

![](https://github.com/khanmaster/vb_vagrant_installtion/blob/master/images/VB_Version.png)

We won't actually use VirtualBox directly. Vagrant will handle everything.

> NOTE: Windows user, after installing Virtual Box, you will need to manually install the drivers:

> 1. In File Explorer, navigate to `C:\Program Files\Oracle\VirtualBox\drivers\vboxdrv`
> 2. Right click on the **VBoxDrv.inf** Setup Information file and and select Install
> 3. When it's finished installing, open up a new terminal window and run `sc start vboxdrv`
> 4. Press the Windows Key and search for **Control Panel**, go from there to **Network and Internet**, then **Network and Sharing Centre**, then **Change Adapter Settings**.
> 5. Right click on **VirtualBox Host-Only Network** and choose **Properties**
> 6. Click on **Install => Service**
> 7. Under **Manufacturer** choose **Oracle Corporation** and under **Network Service**, choose **VirtualBox NDIS6 Bridged Networking driver**

> This should install all the drivers you need to run Virtual Box on Windows.

## Test Running Vagrant

**THERE MUST BE A VAGRANTFILE IN WHICHEVER DIRECTORY YOU RUN VAGRANT FROM**

Vagrantfile used for this exercise
```

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

 config.vm.box = "ubuntu/xenial64"
# creating a virtual machine ubuntu 

 config.vm.network "private_network", ip: "192.168.10.100"
# creating a private ip to access our nginx server on the web from inside the VM

# redirect the above to the specific web address
 config.hostsupdater.aliases = ["development.local"]


end
```

- Start Vagrant with ``vagrant up``
- Check status with ``vagrant status``
- Enter the VM with ``vagrant ssh``
- After exiting VM, stop Vagrant with ``vagrant halt`` or suspend with ``vagrant suspend``


## Potential Errors

### ERROR: HOSTSUPDATER
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

### ERROR: VBoxManage: Hypervisor Partitions
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
