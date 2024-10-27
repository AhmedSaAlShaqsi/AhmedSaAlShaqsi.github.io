We are going to build our Arch Linux OS in a VM(virtual machine) in VirtualBox:

# Installation:
Head to [Downloads](https://archlinux.org/download/), To download the iso file depending on your country or you can also the download the Worldwide iso version. If you are not sure what .iso file to Download here is a good You tube video that might help [Help](https://www.youtube.com/watch?v=paJWYGjBwbQ).
After downloading the ISO file open VirtualBox and Click on New(to create a new VM), and this screen should pop up:![[create-vm-1.png]]
Change the Name for what ever you want to name it, change the ISO image by clicking at it and choosing the ISO file that we have downloaded in the previous step. Finally, if the Type and version didn't change automatically you should set them up as Type: Linux, Version: Arch Linux (64-bit). Run the VM :)

# Setting up the Arch Linux System in the VM and Adding Users:
After starting the VM, this screen will pull up click on the first option as showed:![[virtualbox-booting-arch-linux.webp]]
Then, it will lead you an root@archiso terminal.
The first thing to do is check your network connection by writing this command:
```bash
ping archlinux.org
```

then run this code to Synchronize the package database or list:
```bash
pacman -Sy
```
To install the keyring package that contains the latest keys run:
```bash
pacman -Sy archlinux-keyring
```
Setting up the Arch settings and testing connectivity to the Arch Linux mirrors, the archinstall command makes the installation more faster an easier than building it manually, we run the following command:
```bash
archinstall
```
and a similar screen should appear like this one:![[17.archinstall-Install.jpg]]
==Note: You can navigate through this list by the up and bottom arrows and pressing enter to access the options. also clicking enter to pick the choices for the options that you want and return to the menu== 
**Archinstall language:** you can choose the language that is better for you English is preferred.
**Keyboard layout:** US by default, you can change it.
**mirror region:** you can leave it as default.
**Local language, encoding:** also keep it as it is, **en_US/UTF-8**
**Drive(s):** The click in the drive option and choose the hard drive in which you want to install Arch Linux. You can select the options by TAB key or space bar, to verify that its selected  you should see an asterisk beside the option that you chose. click enter to choose it and to go back to the main menu.
**Disk layout:** In this option choose the second choice that says wipe all selected drives to wipe all the drives then use the default partition layout (btrfs) then click yes.
**Encryption password:** We can use this to encrypt our installation by setting an encryption password, but it's not needed for now.
**Bootloader:** Leave it as default option..
**Swap:** Make it Ture.
**Hostname:** You can enter any any name. I did Archlinux.
**Root password:** Set a root password.
**User account:** In this option we can add(create) users and there passwords, also we can add users in the console after we are done setting up the system and set them as sudo.
**Profile:** This option will install the DE(desktop environment), click on the profile option then inside this options click in the option that says "desktop: Provides a selection of desktop environments and tailing windows manage," after that it will appear for you several options for DE I chose GNOME. Then select "VMware /VirtualBox (open-source)" as a graphical driver.
**Audio:** It is recommended to use pipewire.
**Kernels:** You can leave it as default.
**Additional packages:** In this option we can specify  packages and separate them with a space ex: git sudo neofetch.
**Network configuration:** Choose network manager.
**Timezone:** Choose your time zone that you want to set the correct time in your system.
**Automatic time sync (NTP):** True
**optional repositories:** You can leave it as it is.

After all these steps make sure that you fill all the options and then click **Install.**
This question will appear to you after installation "Would you like to chroot into the newly created installation perform post-in?" Click YES.

Now it will open a root@archiso terminal and we can install some useful tools ex:
```bash
pacman -Sy firefox make libreoffice-fresh
```
 After that type "exit" the root environment and then shutdown the VM and open it again. you can use the command:
 ```bash
 shutdown now
 ```
  Go to the settings of the VM and then Storage and then remove the .iso file. This is important if you are using VirtualBox. 
Run the VM now and start Arch Linux experience by entering your account password.

**Talking about users:** If you didn't add users in the first step as I did there is another way to do it by running this command:
```bash
sudo useradd -m username
```
Now lets set a password for these users and make them expire after the first login from the user, to force the user to change it when he enters:
```bash
echo "username:password" | sudo chpasswd
```
and to give them sudo permission type:
```bash
sudo usermod -aG wheel username
```
As I said that I did most of these steps while setting up the system because it is more simple and easier to do it.
# Installing Zsh instead of Bash shell:
First of all get used to update your package database continuously, here is the command for it:
```bash
sudo pacman -Syu
```
Then install the Zsh shell and make it running instead of the Bash shell by running these two commands:
```bash
sudo pacman -S zsh
chsh-s /bin/zsh
```
One problem that I faced is: I tried to check the shell type after entering these commands and it was still Bash so I figured out that I should reboot the VM to make the shell changes.

After rebooting we can check the new shell type by entering this command:
```zsh
echo $SHELL
```
and the output should be **/bin/zsh**

# Installing SSH:
SSH stand for Secure Shell protocol that sets up encrypted for remote logins and file transfer between computers. and we can install it by running this command:
```zsh
sudo pacman -S openssh
```
Then we should verify that SSH exists in our system, by writing this command:
```zsh
ssh -V
```
this command should output the SSH version, but if you get a message that says:
```zsh
ssh: command not found
```
then you should install it again.

# Adding color coding to the terminal:
To make the terminal more interesting lets add some colors to it. To add colors to the terminal we should install some tools that might help such as Oh My Zsh tool that will make us change the default color scheme to a popular scheme that is called "agnoster". Here is the command to install Oh My Zsh tool:
```zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Once you have installed this tool enter the ~/.zshrc file using nano and look for ZSH_THEME variable and make it equal to "agnoster". and then add another variable above the ZSH_THEME variable and that should look like this:
```zsh
POWERLEVEL9K_MODE='nerdfont-complete'
ZSH_THEME="agnoster"
```
exit the file and save you work, also don't forget this command to enable your changes:
```zsh
source ~/.zshrc
```

After these steps now we install Plugins, with the following command:
```zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```
and add this variable to the .zshrc file:
```zsh
plugins=(zsh-syntax-highlighting)
```
Adding more to the .zshrc file, now add this syntax to the file so it will output the username in Green color and the host name in Blue color:
```zsh
GREEN='%F{green}'
BLUE='%F{blue}'
NC='%f' #No color

export PS1="${GREEN}%n${NC}@${BLUE}%m${NC} $ "
```
Now after modifying the .zshrc file we should run this command to enable our modification:
```zsh
source ~/.zshrc
```
and we are done from coloring the terminal :)

# GUI (graphical user interface):
I have done the GUI from the first step while running archinstall command. I have added the GNOME desktop environment. To check your Desktop environment run this command:
```zsh
echo $XDG_CURRENT_DESKTOP
```
# Adding aliases to the shell:
Aliases makes the terminal easier to use by shortening the commonly used commands. You can customize them as you which. You can add your aliases in the .zshrc file. In this task i have done Five aliases and here they are:
```zsh
alias c='clear' # by typing c in the console in will clear the console
alias ..='cd ..' # by typing .. it will change directory ine step back
alias update='sudo pacman -Syu' # by typing update it will update the package manager
alias q='exit' # by typing q it will exit the console
alias doc='cd Documents' # by typing doc it will change the directory to Documents
alias downloads='cd Downloads' # by typing downloads it will change thedirectory to Downloads.
```
A mistake that I did is that I forgot to source the file after modifying it and that made the aliases didn't work so:
Pro tip: After modifying the .zshrc file Don't forget to use this command to enable your modifications:
```zsh
source ~/.zshrc
```

**Questions:**
Here are some questions that came to my mind while I was installing Arch Linux:
Q: Why do we use Arch Linux?
A: I found that Arch Linux is more simple and it's most customizable, and it is for advanced users that want to have more control over the system.
Q:What are the best DE(desktop Environments) to use in Arch Linux?
A: I can't say a specific one because it depends on the user but for me I think that GNOME is the most user friendly one.

# References:
- https://hn.mrugesh.dev/how-do-i-make-zsh-look-good
- https://wiki.archlinux.org/title/Installation_guide#Select_the_mirrors
- https://publish-01.obsidian.md/access/09cfa50ec31c0f01873549787f02a7e0/assets/Markdown%20Cheat%20Sheet.pdf
- https://archlinux.org/download/
