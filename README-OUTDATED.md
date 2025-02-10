Windows Environment Setup
=========================

## WARNING - ansible on windows sucks! Even using the WSL, it still sucks. I ended up switching back to Linux and everything worked as expected.


### Steps

1. "Turn Windows features on or off"
2. Check "Windows Subsystem for Linux" and press OK. "Restart!"
3. Open the "Microsoft Store" and search for "Ubuntu"
4. I installed Ubuntu 20.04 LTS. Smash the Get button.
5. Open Ubuntu and wait "Installing, this may take a few minutes..." indeed
6. Set a username and password for the default UNIX user.

    Enter new UNIX username:
    New password: 

7. Become the root user
  $ sudo su
8. Set the root password
  # passwd 

    New password: ...

8. Drop back to the regular user and install updates

  $ sudo apt update
  $ sudo apt upgrade

9. Install ansible + dependencies

  $ sudo apt install python3-pip
  $ sudo apt install git libffi-dev libssl-dev
  $ pip3 install pywinrm
  $ pip3 install --user ansible

10. Ensure ansible is working (I had to restart the Ubuntu WSL for the path register...)

  $ ansible --version


11. Create some symbolic links for convenience

```bash
ln -s /mnt/c ~/C
ln -s /mnt/d ~/D
ln -s '/mnt/c/Users/Dev' ~/Dev
```

12. Run the ansible playbook

  $ cd ~/Dev/repos/windows-ansible-playbook
  $ ansible-playbook hello.yml --connection=local

NOTE - if you are using Ubuntu 20.04 and face an issue like "Failed to create temporary directory..." it's probably due to GNU C library 'glibc' which is not compatible with the WSL. So basically sleep commands don't work and ansible "needs" that. Here's a quick workaround fix...

  # mv /usr/bin/sleep /usr/bin/sleep.orig
  # ln -s /bin/true /usr/bin/sleep
  
13. Open the PowerShell as Administrator

  Enter the following command and answer *yes* to every question:
    `WinRM qc`
	
  Now enter the following command:
    `Set-ExecutionPolicy`
	
	Enter the policy to be used as "Bypass"
	Answer *yes* to change the policy.

