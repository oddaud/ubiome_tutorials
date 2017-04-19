# File transfer
***
Authored by Audra Devoto

***

## Overarching Goal  
* This tutorial will teach you how to transfer files between your local computer and **qiime**

## Learning Objectives
*	Transfer files too and from a community AWS server using `scp`
* Download publicly-hosted data to an EC2 instance using `wget`  

***

### 0.  Where am I?  
Sometimes, all the terminal screens sort of look the same. When you're copying files back and forth, it's important know which machine you're talking to:  your own laptop, or your EC2 instance in the cloud?

- Keep your terminal window open where you have `ssh` into the EC2 machine. 
- Now, start another, new terminal window.  
 - **NOTE** This new window is *NOT* connected to the EC2.  Instead it's just your regular ole laptop
- Verify that your these windows are connected to different machines examining the home directory in both your `ssh` and new terminal

``` 
pwd
```
See how they're different? One you've connected to EC2 (ubuntu), the other is just your local machine (whatever your user name is)

You can also look at the address of the machine using the command (Windows users, did this work?)
```
hostname
```
### 1. Using Downloading uBiome files

Next we will go over how to copy a file from your personal computer to your EC2 instance using `scp`. The usage is very similar to `ssh`. 

To begin, download the uBiome zipped fastq files to a directory named "ubiomeSamples" on your computer.
* Navigate to https://app.ubiome.com/samples
* Select your sample by clicking "Explore Sample"
* Under "Advanced", select "Downloads"
* Click "Download Sequence Data" (in red, below)
![ubiome download](pics/download-fastq.png)
* Save zipped file in ubiomeSamples folder

** IMPORTANT ** You must save the IDs in your sample spreadsheet. Notice each downloaded file (folder) has a name, such as "ssr_87372" (referred to from here on as a uBiome ID). Note the sample name associated with each folder name, and save this as a column in your sample spreadsheet. Be very careful when doing this, as it can be easy to mix up sample IDs and uBiome IDs, which will cause problems later on. 

### 2. Organizing uBiome files

The uBiome files require a little bit of processing before they can be transfered to the qiime community server. 

* Open the ubiomeSamples folder in finder, unzip each of the folders. Each folder should have a name starting with ssr
* Within each folder, you will find 8 different fastq.gz files 
  * ssr\_87372\_R1\_L001.fastq



Organize it 
Download the following file onto your laptop's Desktop by clicking [this link] (https://www.dropbox.com/s/9y41he4ol62gu0b/cloud.txt?dl=0)

Now we're going to copy this file you downloaded from your laptop onto the remote EC2 machine.  

Find your terminal window that's just your local machine (see above) and run the appropriate version 
of the command below.  
*NOTE* you have to adapt this command to give it the right paths and DNS info!
```
scp -i **/path/to/your/keyfile.pem** **path/to/the/file/you/want/to/copy** ubuntu@"your public DNS":**/path/where/to /copy/the/file**
```
How do you know where you want to put the file?  
- Look first at the directory structure on your EC2 machine
- Type `pwd` once you've navigatated where you want to put this file!
- put that path after the colon in the example above

An example from my file structure and EC2 instance!
```
scp -i /Users/ewilbanks/Desktop/amazon.pem /Users/ewilbanks/Desktop/cloud.txt ubuntu@ec2-52-5-171-50.compute-1.amazonaws.com:/home/ubuntu/
```
