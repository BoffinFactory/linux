### Boffin Linux night

Welcome to Boffin Factory's Linux install night.  In ascending order of
difficulty here are the things we are going to introduce tonight:

1. Install and use the Windows Subsystem for Linux (WSL): Beginner
2. Installing a virtual machine using VirtualBox: Beginner
3. Creating SSH public and private keys for passwordless logins
4. Amazon Web Services (AWS)

#### Windows Subsystem for Linux (WSL)

The easiest way to begin playing with linux is to install the Windows Subsystem
for Linux or WSL.  The Windows Subsystem for Linux is a compatibility layer for running linux
executables natively in Windows 10 and Windows Server 2019. [Read more on the WSL
Wikipedia page here](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux).

In essence, WSL will give you a linux environment running within windows to
experiment with.  Due to security issues not all linux features and programs are
capable of being run in the WSL but for beginners most will work just fine.

There are many options out there for installing and configuring this, and you 
are free to use whichever one you want; however, the instructions below are a 
great starting environment for someone new to linux.

If you have any recommendations or issues with the instructions please submit an
issue in github!

##### Instructions for WSL

* [Install Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* Install Ubuntu 18.04 LTS from the Windows store
* Launch Ubuntu 18.04 LTS Bash to finish configuring your account
  (username/password)
* Optional (but really cool): [Install MobaXterm Home Edition](https://mobaxterm.mobatek.net/download.html)
* Optional (I havnet tested this yet): [Enable WSL2 for your given
  distro](https://docs.microsoft.com/en-us/windows/wsl/wsl2-install)


#### VirutalBox and linux virtual machines

Virtualization gives you much more control of the resources and environment for
your linux virtual machine at the cost of some initial complexity in setting it
up.

For starters you will need a Virtual Machine Hypervisor.  The two most common
ones for windows are VirtualBox and VMware.  We will be recommending virtualbox.
A rough guide is provided below for setting up a virtual machine if you have
never done so, if you have any issues

* [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads). 
  I recommend downloading the x64-bit version for your given OS.
  
  When installing you will have one or more pop up windows that request access to
  install additional packages for various virtual *device software*.  These are
  necessary for virtual box to run virtualized systems, I recommend selecting the
  checkbox by *Always trust software from "Oracle Corporation".* then click **Install**.
* Choose a linux distro to download and install (note: you could use the same
  `.iso` installtion media to install on your laptop or desktop)
  * [Ubuntu Desktop](https://ubuntu.com/download/desktop) (download version 18.04.3) linux desktop for beginners
  * [Elementary OS](https://elementary.io/) pretty linux desktop for beginners
  * [Ubuntu Server](https://ubuntu.com/download/server) server distro advanced (no desktop environment, command
    line only, again download 18.04.3)
  * [Parrot Security OS](https://parrotlinux.org/download-security.php) cyber
    security pen-testing / advanced
  * [Qubes OS](https://www.qubes-os.org/) A reasonably secure operating
    system...
  * There are many others out there, feel free to try something new! (and if its
    cool submit an issue with the link to get it added here).
* Start VirtualBox and create a new Virtual Machine (VM)
* Follow the new VM wizard, I recommend 2 cores and 2GB RAM for all linux
  distributions that include a desktop (most of the above)
* Edit the VM settings and attach your downloaded `.iso` image as a virtual
  CD/DVD device
* Start your VM and go through the installation procedure

#### SSH keys for passwordless logins

I'm sure by now you are familiar with usernames and passwords.  Linux provides
you with another secure method of logging in, a related public and private key
pair.  Public and Private key pairs are the only way to sign into an Amazon Web
Services linux system.

Secure Shell (SSH) is the standard way to make a remote connection to a linux
system.  This is typically a command line only connection but does support
sending graphical displays with the `-X` option (more on this later).  To
simplify signing in on multiple systems we can create an SSH key pair that will
allow us to sign in without requiring a password, so long as we have access to
the private key.

To create a key pair simply run the following command: `ssh-keygen` and accept
the defaults.

This will create 2 files, `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`.  So long as
you keep `id_rsa` (which is your **private** key) secure it will uniquely
identify you when signing into a system that has the contents of your `id_rsa.pub` 
file (your **public** key) on it.  

The contents of `id_rsa.pub` should be considered public information and could
be sent to any number of people without risk of them gaining access to your
systems.  If you want to use the SSH private key so sign in to a remote system, simply
take the contents of you `id_rsa.pub` file and put them on the remote system
under `~/.ssh/authorized_keys` (you may need to create this file).

#### Amazon Web Services (AWS) [advanced]
**WARNING** Amazon Web Services costs money, like real money.  While there are a
good amount of free credits available, if you create a system and forget about
it you will likely get charged at some point.  Please be sure to delete all AWS
environments when you are finished with them.

AWS is a cloud provider that allows you to run virtual machines on their
hardware.  They offer a good deal more but that will be covered in a future
Boffin night.  For now head over to AWS and create an account.

While you are at it you might as well [register for AWS
educate](https://aws.amazon.com/education/awseducate/).  This service is used 
in several of our cyber classes and allows for additional free credits beyond
what is normally allotted.  **Be sure to use your @wright.edu email address!**

Once you have an AWS account, sign in and go to the console.  The following
instructions will create a demo environment that you can play around with.

* Before you create your environment you must first create a SSH key pair via AWS 
  Browse to the [EC2 service from the AWS console](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Home:).
  In the center area you should see a list of all Resources you have
  available (you will be returning here often).  Right now they should all be 0.
* Click on [0 Key Pairs](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#KeyPairs:sort=keyName)
  From here you should see no existing SSH key pairs.
* Click on the `Create Key Pair` blue button.  This will create a
  public/private key pair, stores the public key in AWS, and downloads the
  private key to your local machine.
* **Do not lose this private key.**  Doing so will prevent you from being
  able to access any labs created with it.  If you do lose it simply delete it
  from AWS and create a new one.
* [Once you have created your SSH key, click here to create your demo environment](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=CEG-4900Lab01&templateURL=https:%2F%2Fs3.amazonaws.com%2Fwsu-cecs-cf-templates%2FAWS-demo.yml)
* From the AWS console, browse to [EC2 then Running Instances](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Instances:sort=instanceState)
  to see information about the servers created as a part of the cloud formation
  template.  You will need to retrieve the Elastic IP of the Ubuntu instance by
  selecting it and looking at the information in the Description below.

**You are now ready to make an SSH connection to your AWS server.**  Using
MobaXterm perform the following actions:
* Create/copy the AWS private SSH key to your home directory
* Make the key only readable by your user (`chmod 600 private-key`)
* SSH into your AWS server with the following, replacing **/path/to/private/key**
  and **ElasticIP** with your information):
  `ssh -i /path/to/private/key ubuntu@ElasticIP`

* **Be sure that when you are done you go back to AWS CloudFormation and delete
  this stack so you are not charged a fee**
