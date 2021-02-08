# AWS Setup

You will be using an AWS account created through the AWS Educate Program. To logon to the AWS Console, you must logon to AWS Educate first, go to your AWS Classroom, and then click on AWS Console.

## Select N. Virginia as the Region

The first time you logon to your AWS console, **make sure that the region selected is _N. Virgina_. You can see the region on the top right, next to _Support_. If any other value other than _N. Virginia_ is selected, please select _N. Virgina_. You only need to do this one time.

## Upload your Public key to AWS

* Logon to your AWS Console if you are not already logged in
* Go to the EC2 Dashboard. You can get here by clicking on **Services** in the top left and choosing **EC2** under the **Compute** heading
* Click on **Key Pairs** on the left hand side of the EC2 console. If you don't see it, scroll down the left side panel until you see the **NETWORK & SECURITY** heading, and you will see the following:

<img src='images/create-keypair-1.png'>

* Click on **Import Key Pair** at the top of the screen and the "Import Key Pair" dialog will show:

<img src='images/create-keypair-2.png'>

* In the **Key pair name** box, enter `mykeypair` or a name that is meaningful to you. It can be anything, just make sure you know what it is.
* In the **Public Key Contents** box, paste the contents of the **public key** that you got before.

<img src='images/create-keypair-3.png'>

* Click **Import** and you will see your key in the console.

<img src='images/create-keypair-4.png'>

You will use your key to connect to AWS resources later.


## Create a Security Group

Before we launch our first AWS EC2 instance, we will setup a _Security Group_ in the AWS Console. Each account comes with a default security group, but we will create a specific one that we will use to connect to our EC2 instance via ssh, which means it will open up port 22 on your instance.

* Log on to your [AWS Console](https://console.aws.amazon.com/) if you are not already logged in
* Go to the EC2 Dashboard. You can get here by clicking on **Services** in the top left and choosing **EC2** under the **Compute** heading
* Click on **Security Groups** on the left hand side of the EC2 console. If you don't see it, scroll down the left side panel until you see the **NETWORK & SECURITY** heading, and you will see the following:

<img src='images/create-security-group.png'>

* Click on **Create Security Group**. 
	* Enter a name for your security group (you can call it whatever you want; I called it **open-22** to make it easy.) 
	* Enter a description for your group
	* Leave the VPC value unchanged (your number will be different than the one shown below.)
	* Click on **Add Rule** towards the bottom
	* Select **SSH** from **Type**
	* Select **Anywhere** from **Source**
	* Click **Create**

	<img src='images/security-group-settings.png'>

* You have just created a security group that opens up port 22 and allows you to connect from anywhere, and you should see it in the Security Groups console (again, the group id will be different for each of you). You will use this group that you just created when you launch an instance for this assignment

<img src='images/security-group-console.png'>


## Launch your first Linux instance on AWS

This is a step-by-step guide on how to launch an instance.

* From the **EC2 Dashboard**, click on the **Launch Instance** button

<img src='images/launch-instance-01.png'>

* _Step 1: Choose an Amazon Machine Image:_ 

Click on **Quick Start** on the left hand side and select the first image **Amazon Linux 2 AMI**

<img src='images/launch-instance-02.png'>


* _Step 2: Choose an Instance Type:_ Select the **t2.micro** instance type (this one is eligible for the free tier), and click **Next: Configure Instance Details**

<img src='images/launch-instance-03.png'>

* _Step 3: Configure Instance Details:_ Nothing to do here, click **Next: Add Storage**

<img src='images/launch-instance-04.png'>

* _Step 4: Add Storage:_ Nothing to do here, click **Next: Add Tags**

<img src='images/launch-instance-05.png'>

* _Step 5: Add Tags:_ Nothing to do here, click **Next: Configure Security Group**

<img src='images/launch-instance-06.png'>

* _Step 6: Configure Security Group:_ Click on **Select an existing security group** radio button, and then select the **open-22 (or whichever name you gave it)** Security Group that you created eariler, click **Review and Launch**

<img src='images/launch-instance-07.png'>

* _Step 7: Review Instance Launch:_ You will see a warning about your security group being open to the world. You can ignore it, we know. Make sure that the AMI, the Instance Type, and the Security Group is what you wanted. Click **Launch**

<img src='images/launch-instance-08.png'>

* _Select an existing key pair or create a new key pair:_ In this screen select **choose an existing keypair** from the dropdown, and make sure you select the keypair that you uploaded to AWS, otherwise you will not be able to connect to your machine. Click **Launch Instances**

<img src='images/launch-instance-09.png'>

* _Launch Status:_ Click **View Instances** to go back to the EC2 Instances page

<img src='images/launch-instance-10.png'>

* In the EC2 Console, you will see the status of your instance. Sometimes the instances are launched immediately, but sometimes you have to wait. While waiting, you will see the Instance Status showing a yellow dot with "pending", otherwise it will be a green dot with "running"

* When the instance is in "running" state, it is ready to be used!

## Connect to the remote server using Secure Shell `ssh`

We will be using the terminal with Secure Shell to connect to our remote instance. 

* Open a terminal on your laptop. If you have one already open, type `cd ~` to navigate back to your home directory
* Go to the EC2 Instances page (click on EC2, then on Instances on the left)
* Click on your running instance such that the select box is blue
* Click in the **Description** tab in the bottom if not already selected
* Hover with your mouse over the **Public DNS** text, and you will see a "Copy to Clipboard" icon to the right. Click on that to copy your instances DNS address.

<img src='images/ec2-running.png'>

* In the terminal, type `cd ~` to make sure you are in your home directory
* Type `ssh ec2-user@` and paste your DNS address
* If everything is configured correctly, the first time you connect to a host that you've never connected to, you will see something like this:

```
The authenticity of host 'ec2-54-163-133-120.compute-1.amazonaws.com 
(54.163.133.120)'can't be established.
ECDSA key fingerprint is SHA256:TeYrgHLkYHvD/zcp23bO3wozsLMyPSiSn+edPPo88zE.
Are you sure you want to continue connecting (yes/no)?
```
Note: your values for DNS, IP address and fingerprint will be different

* Enter `yes` and press enter. You will only need to enter yes once.
* If you are successful, you will see something like this:

```
The authenticity of host 'ec2-54-163-133-120.compute-1.amazonaws.com (54.163.133.120)' 
can't be established.
ECDSA key fingerprint is SHA256:TeYrgHLkYHvD/zcp23bO3wozsLMyPSiSn+edPPo88zE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-54-163-133-120.compute-1.amazonaws.com,54.163.133.120' (ECDSA) to the list of known hosts.
Last login: Thu Jan 25 01:41:17 2018 from pool-108-45-73-252.washdc.fios.verizon.net

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
[ec2-user@ip-172-31-59-103 ~]$
```

**Congratulations, you have successfully connected to your remote instance!**
