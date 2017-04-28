# Introduction
***
Authored by Audra Devoto

[Adapted from Elizabeth Wilbanks](https://github.com/ewilbanks/micdiv2017/blob/master/tutorials/2017-02-16-launch-community-ami.md) for Swarthmore College BIOL133, Spring 2017
All images from [ewilbanks](https://github.com/ewilbanks/micdiv2017/blob/master/tutorials/2017-02-16-launch-community-ami.md)
***

## Overarching Goal  
* This tutorial will teach you how to launch an AWS community server with **qiime**

## Learning Objectives
*	Understand what AWS is and how to use it
* Launch the community qiime AMI
* Become familiar with the command line
***

## Command Line Tutorial
* These tutorials make extensive use of the command line. While there is a steep learning curve to figuring out the "language" of the command line, you will quickly find that it is worth it! Some tasks that are impossible using a user interface are made simple with the command line. 
* [Complete this excellent tutorial provided by Elizabeth Willbank](https://github.com/ewilbanks/2015-tutorials/blob/master/final/2015-06-22-introduction_to_the_shell.md)
Citation:
Authored by Tracy Teal with [Software Carpentry](http://software-carpentry.org/lessons.html), with minor modifications by Ashley Shade, Joshua Herr, and Paul Wilburn 
[EDAMAME-2015 wiki](https://github.com/edamame-course/2015-tutorials/wiki)

***
Software Carpentry has a CC-BY [license](https://github.com/swcarpentry/shell-novice/blob/gh-pages/LICENSE.md)   
EDAMAME tutorials have a CC-BY [license](https://github.com/edamame-course/2015-tutorials/blob/master/LICENSE.md).   
_Share, adapt, and attribute please!_   


# Launching a community AMI

## What is a community AMI?
* A community AMI is a remote machine that comes pre-installed with necessary software.
* Individuals or groups can set up and maintain these AMIs, and then make them available for use.
* We will be using the Qiime AMI, which is maintained by the Qiime developers. 

## What is Qiime? (pronounced chime)
* Qiime stands for Quantitative Insights Into Microbial Ecology. http://qiime.org/
* From the website: "QIIME is an open-source bioinformatics pipeline for performing microbiome analysis from raw DNA sequencing data. QIIME is designed to take users from raw sequencing data generated on the Illumina or other platforms through publication quality graphics and statistics. This includes demultiplexing and quality filtering, OTU picking, taxonomic assignment, and phylogenetic reconstruction, and diversity analyses and visualizations. QIIME has been applied to studies based on billions of sequences from tens of thousands of samples."

### Navigate to the Qiime AMI
[Adapted from ewilbanks](https://github.com/ewilbanks/micdiv2017/blob/master/tutorials/2017-02-16-launch-community-ami.md)

* Double check you are in the N. Virginia range
![Edit security rules](pics/ec2-range.png)
* Go to [EC2 management console](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard:)
* Click 'launch and instance'
* Click on the sidebar that says "Community AMI"
* Search for "qiime" to pull up machines the qiime community AMI
* Select the first one listed, qiime-191 - ami-1918ff72
* If you are curious what the most recent server is, click [here](http://qiime.org/home_static/dataFiles.html) under "Latest Amazon Web Services (AWS) virtual machine identifier"
![Select qiime](pics/qiime-ami-01.png)
* For the instance type, select m1.large
* Click through to review & launch (but don't finalize)

### Set a new security rule for your instance 
Loging on to the EC2 isntance requires the ssh access to port 22, but we also need another port to use iPython notebooks (later in the tutorial).
* Add another security rule by clicking the link circled:
![Edit security rules](pics/qiime-ami-02.png)
* Click `Add rule`
* For the new secturity rule fill out the fields as shown below
* The Type should be Custom TCP Rule
  * Protocol =  TCP
  * Port Range = 8888
  * Source = Anywhere
![](pics/qiime-ami-03.png)

* Click 'Review and Launch' and then 'Launch'
* You will be prompted to create a security key (or use an exisiting security key if you have already made one)
* A security key is a unique file you save on your computer that acts as a password, this means only you can log into the EC2 instance you just created. 
* Select "Create a new key pair', give it a name, and download it to a stable directory that is easy to find. 
![](pics/create-key.png)


### Now log into your QIIME EC2 instance
- On the EC2 console, look up the public DNS for your instance.
- Open a terminal window (of Mobaxterm for Windows users) and `ssh` into your instance

#### Find your EC2's Public DNS:
Each EC2 instance has a Public DNS. This is an address for your EC2 instance that allows your local computer to access it. Go to [AWS](http://aws.amazon.com/), select EC2, and then view your running instances. On this page, click on your instance and find it's public DNS under the "Description" tab.

![PublicDNS](https://github.com/ewilbanks/2015-tutorials/blob/master/img/EC2_Public_DNS.png?raw=true)

In the image above the full Public DNS of the highlighted instance is **ec2-52-5-171-50.compute-1.amazonaws.com**

#### 1. Open a Terminal:
- **Windows users** Use MobaXterm [here](http://mobaxterm.mobatek.net/download.html) to use as your terminal. 
- **MAC Users:** Search for Terminal in spotlight
- **Linux Users:** Press Ctrl + Alt + t

Now you need the key pair you created. Find it using cd
 
```
cd /Downloads
```

#### 2. Change your keyfile permisions to read only:

```
chmod 400 **/path/to/your/keyfile/**.pem
```
You need to change the permissions because if a keyfile is edited it can no longer be used to access an EC2 instance. 

#### 3. Connecting to your EC2 instance using ssh:

```
ssh -i **/path/to/your/keyfile/**eda.pem ubuntu@"your public DNS"
```

Type 'yes' to continue. 

Great! You are logged into the cloud. 

### 4. After the first login

For consecutive connections, you do not need to modify the permissions of the key each time. Simply ssh in using the public DNS. 

```
ssh -i **/path/to/your/keyfile/**EDAMAME.pem ubuntu@"your public DNS"
```

### [NEXT: transfering files and launching an iPython notebook](https://github.com/oddaud/ubiome_tutorials/blob/master/tutorial_2_transfer_files.md)
