# Azure Setup

Follow these instructions _step-by-step_ to setup your Azure environment. The screenshots may look a bit different than what you are seeing, but the flow is the same.

## Task 1: Find your Azure Subscription (one time only)

1. Click on _Home_ in the top left
2. Click on _Subscrptions_ (the key icon)
3. Uncheck the checkbox that says _Show only subscriptions selected in the global subscriptions filter_
4. You will either see a subscription name called _Microsoft Azure Subscription 2_ or _course-name-semester_
5. You can rename it if you wish

## Task 2: Create a Resouce Group (one time only)

A resource group (RG) is a logical grouping of cloud resources. You can 


1. Click on _Microsoft Azure_ in the top left to go to the Azure Portal home screen
2. Click on _Resource groups_
3. Click on the Subscription Filter and make sure your subscription is selected
4. Click _Create_
5. In the _Create a resource group_ page:
	* Select the subscription that was created for you
	* Enter a name for the resource group. It can be anything you want
	* Select _(US) East US 2_ from the dropdown
1. Click _Review + create_ at the bottom left
2. After validation passes, click _Create_
1. Once the RG is created, you'll see it in the RG list (if your right subscriptions are selected in the filter)

**The following tasks are optional**

## Task 3: Upload your Public key to Azure (do this one time only)

1. Click on _Home_ in the top left
2. Enter `ssh keys` in the blue search bar, and clicl on _SSH Keys_ service
3. Click _Create_
4. Select the right subscription from the dropdown
5. Select the RG you created in Task 3
6. Give the key a name (it's just a name, it doesn't matter what it is as long as you know what it is)
6. Select _Upload existing public key_ from the _SSH public key source_ dropdown
1. In the **Upload key** box, paste the contents of your **public key**  in the file `.ssh/id_rsa.pub` on your local machine
2. Click _Review + create_
2. After validation passes, click _Create_
1. Once the SSH Key is uploaded, you'll see it in the SSH Key list (if your right subscriptions are selected in the filter)


## Task 4: Launch your first Linux virtual machine on Azure

1. Click on _Home_ in the top left
2. Click the _Create a resource_ icon
3. In the _New_ screen, click on the _Ubuntu Server 18.04 LTS_ (second one down from the top under the _Popular_ column)
4. In the _Create a virtual machine_ page:
	* Select the right subscription
	* Select the right RG
	* Give your VM a name, and leave all other values in the _Instance Details_ except size as they are
	* Click _see all sizes_
	* Select size _B2s_
	* In the _Administrator account_ section, select _Use existing key stored in Azure_ from the _SSH public key source_, and select the proper keyname
	* Click _Review + create_
	* After validation passes, click _Create_
	* Once the VM is created you'll see a notice and click _Go to resource_


## Task 5: Connect to the remote server using Secure Shell `ssh`

1. Go to the VM Overview page for the VM you just created. You can get there multiple ways.
2. In the _Essesntials_ section on the right, copy the public IP address
3. Open a terminal on your laptop. If you have one already open, type `cd ~` to navigate back to your home directory
1. Type `ssh azureuser@` and paste your DNS address
* If everything is configured correctly, the first time you connect to a host that you've never connected to, you will see something like this:

```
The authenticity of host 'xxx.xxx.xxx.xxx (xxx.xxx.xxx.xxx)' can't be established.
ECDSA key fingerprint is SHA256:TeYrgHLkYHvD/zcp23bO3wozsLMyPSiSn+edPPo88zE.
Are you sure you want to continue connecting (yes/no)?
```
Note: your values for DNS, IP address and fingerprint will be different

* Enter `yes` and press enter. You will only need to enter yes once.
* If you are successful, you will see something like this:

```
Warning: Permanently added 'xxx.xxx.xxx.xxx' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 5.4.0-1039-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue Feb  9 19:11:22 UTC 2021

  System load:  0.02              Processes:           127
  Usage of /:   4.5% of 28.90GB   Users logged in:     0
  Memory usage: 5%                IP address for eth0: 10.0.0.4
  Swap usage:   0%

0 packages can be updated.
0 of these updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@vm-name-given:~$
```
**Congratulations, you have successfully connected to your VM on Azure**

## Task 6: Stop or terminate your virtual machine

There are two concepts you need to understand:

* Stopping a VM is like turning the machine off. The current state is saved and you can turn it on again later.
* Deleting a VM completely removes it. This cannot be undone.

### To stop/pause a VM

1. Go to the VM Overview page for the VM you just created. You can get there multiple ways.
2. Click on _Stop_
1. Confirm you want to stop it by clicking _OK_
2. To start again in the future, click on _Restart_, though the IP address will change
2. 
### To delete a VM

1. Go to the VM Overview page for the VM you just created. You can get there multiple ways.
2. Click on _Delete_
1. Confirm you want to delete it by clicking _OK_
2. Remove additional VM related resources from the RG:
	* the resource ending in `ip` (the IP address)
	* the resource ending in `nsg` (the Network security group)
	* the resource ending in `vm_disk1_xxxxxxxxxxxxxxxxxxxxxxx` (the Disk attached to the vm)
	* the resource ending in a three digit number (the Network interface)
