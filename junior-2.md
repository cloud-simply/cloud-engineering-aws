## AWS Cloud Engineering - Practical Guide, Junior 2
Level: `Basic`

---
### Exercise 1
Create (the first) Linux EC2 Instance 
  | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
<details><summary>Show details</summary>  

* **Details**
  * Use AWS Console
  * Use any of the created in the previous exercises IAM admin users 
  * Use AWS Region: `Europe (Frankfurt) eu-central-1` 
    | [reference](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/select-region.html)
  * Use the following EC2 instance settings (pre selected as default when applicable) 
     * Amazon Machine Image: `Amazon Linux 2 AMI (HVM), SSD Volume Type`
     * Instance type: `t2.micro` 
     * Security group name (wizard created): `launch-wizard-1` 
     * **Create a new key pair** as wizard prompted and download the private key file        
       * Key pair type: `RSA` 
       * Key pair name: `launch-wizard-1`
       * Downloaded private key file name: `launch-wizard-1.pem`
* **What we have as a result (to check/validate)**
  * **Running** Amazon Linux 2 EC2 instance (created within AWS account) in `eu-central-1` region
  * SSH RSA private key (downloaded and stored on the local disk) 
</details>

Connect to the created Linux EC2 instance using SSH
  | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html#AccessingInstancesLinuxSSHClient)
<details><summary>Show details</summary>

* **Details**
  * Use corresponding user name and the instance public DNS name (or IP address)
    | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-get-info-about-instance)
  * Use the downloaded private key 
    | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-private-key)
  * Use either terminal on your local Linux/MacOS workplace or the terminal of the created AWS Cloud9 IDE environment
    * Make sure local Linux/MacOS workplace has `ssh` program installed
* **What we have as a result (to check/validate)**
  * SSH session (to the created EC2 instance) established (with the ability to execute commands remotely)
</details>

Transfer a file from the created Linux EC2 instance to local Linux/MacOS host using SCP
  | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html#AccessingInstancesLinuxSCP)
<details><summary>Show details</summary>

* **Details**
  * Make sure local Linux/MacOS workplace has `scp` program installed
  * Use the same command parameters as ones used to connect to the instance via SSH above
  * Use the following file paths:
    * Remote file: `/etc/ssh/ssh_host_ecdsa_key.pub`
    * Local file: `~/.ssh/ssh_host_ecdsa_key.pub`
* **What we have as a result (to check/validate)**
  * `~/.ssh/ssh_host_ecdsa_key.pub` file presence (on the filesystem of local Linux/MacOS host) 
</details>

Clean up (terminate) the created instance
  | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html#ec2-clean-up-your-instance)
<details><summary>Show details</summary>

* **What we have as a result (to check/validate)**
  * No instance exists in AWS account (the created EC2 instance is terminated)
</details>  

---
### Exercise 2
Repeat the part of the above exercise creating a Linux EC2 Instance and connecting to it via SSH
<details><summary>Show details</summary>

* **Details**
  * To connect to the instance via SSH use **default user** name (user which is default for the Amazon Machine Image used to launch the instance) and the downloaded private key
* **What we have as a result (to check/validate)**
  * Ability to execute commands in shell of the created instance remotely via SSH
</details>

Configure SSH daemon of the created Linux EC2 Instance (remotely via SSH) to be more secure 
  | [reference](https://aws.amazon.com/ru/premiumsupport/knowledge-center/ec2-ssh-best-practices/)
<details><summary>Show details</summary>

* **Details**
  * Disallow SSH access for Linux `root` user
    * Backup Linux `root` user public key authentication settings
      | [reference](https://man.openbsd.org/sshd.8)
    * Setup public key authentication for Linux `root` user **to allow** to use the same public key as used for **default user** 
    * Try to connect to the instance via SSH with root user using public key of **default user**
    * Configure SSH daemon to **deny**  <span style="color:red">connecing</span> for Linux `root` user
      | [reference](https://man.openbsd.org/sshd_config.5)
    * Make sure it is not possible to connect to the instance via SSH for Linux `root` user
    * Restore Linux `root` user public key authentication settings from the backup
  * Disallow SSH access using passwords
    * Setup password for the **default user** in the Linux instance
      | passwd(1)
    * Try to connect to the instance via SSH with **default user** using password
    * Configure SSH daemon to **allow** connecting with password
      | [reference](https://man.openbsd.org/sshd_config.5)
    * Try to connect to the instance via SSH with **default user** using password
    * Configure SSH daemon to **deny** connecing with password
    * Make sure it is **not possible** to connect to the instance via SSH using password
  * Install `fail2ban` utility and enable and start it as a service  
     * fail2ban monitors log files and blocks consecutive unsuccessful access attempts
     * Update the EC2 instance software (all packages)
       | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-updates.html)
     * Try to find `fail2ban` software package
       | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/find-software.html)
     * Add EPEL repository for the EC2 instance running Amazon Linux 2
       | [reference 1](https://aws.amazon.com/ru/premiumsupport/knowledge-center/ec2-enable-epel/)
       | [reference 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/add-repositories.html)
     * Try to find `fail2ban` software package again
     * Install `fail2ban` software package
       | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-software.html)
     * Enable and start `fail2ban` service
       | [reference](https://www.redhat.com/sysadmin/getting-started-systemctl)
     * Leave the `fail2ban` utility configured by default
* **What we have as a result (to check/validate)**
  * SSH daemon is configured according to best practices for keeping Linux instance secure
</details>

Stop the created instance
 | [reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Stop_Start.html)
<details><summary>Show details</summary>

* **Details**
  * Use AWS Console
* **What we have as a result (to check/validate)**
  * Linux EC2 instance in **Stopped** state in AWS account in `eu-central-1` region
</details>

---
> TODO: group exercise to untis and fix their numbers

---
### Exercise 8
Start the EC2 instance stopped in the previous section and connect to it via SSH as **default user**
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Stop_Start.html)(*)
<details><summary>Show details</summary>

* **Details**
  * To start instance use AWS Console
  * Install `nginx` package on the EC2 Instance (remotely via SSH) and configure `http` access to it
  * Install `nginx` software package by repeating the same step for `nginx` package as for installing `fail2ban` utility in the previous section 
    * Update the EC2 instance software (all packages)
      | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-updates.html)(*)
    * Make sure EPEL repository is added
      | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/ec2-enable-epel/)(*)
      | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/add-repositories.html)(*) 
    * Find `nginx` software package
      | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/find-software.html)(*) 
    * Install `nginx` software package
      | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-software.html)(*)
    * Enable and start `nginx` service
      | [text](https://www.redhat.com/sysadmin/getting-started-systemctl)(*)
   * Use the following commands to configure Amazon Linux 2 OS firewall to allow ingress `http` traffic
     * `sudo firewall-cmd --zone=public --add-service=http --permanent`
     * `sudo firewall-cmd --reload`
   * If it is required use the following commands to configure Amazon Linux 2 OS firewall to allow ingress traffic on specific `<port>/<protocol>` (for example `8080/tcp`)
     * `sudo firewall-cmd --zone=public --add-port=<port>/<protocol> --permanent`
     * `sudo firewall-cmd --reload`
   * Allow `http` traffic to access `nginx` service running on TCP port `80`
     | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/connect-http-https-ec2/)
     * Use AWS Console
     * Configure the security group of the EC2 instance to allow `http` traffic by adding an inbound rule on TCP port `80` from the source address `0.0.0.0/0`
       | [text](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
       | [video](https://www.youtube.com/watch?v=UQLWYy-EpCg)  
* **What we have as a result (to check/validate)**
  * Ability to execute commands remotely (via SSH) in shell of the instance created in the previous section 
</details>

---
### Exercise 9
Stop the EC2 instance
<details><summary>Show details</summary>

* **Details**
  * Use AWS Console
* **What we have as a result (to check/validate)**
  * Linux EC2 instance in **Stopped** state in AWS account in `eu-central-1` region
</details> 
 
---
### Exercise 10
Start the EC2 instance stopped in the previous section and access it via SSH
<details><summary>Show details</summary>

* **Details**
  * See the previous section
* **What we have as a result (to check/validate)**
  * See the previous section
</details>   
  
---
### Exercise 11    
Start the EC2 instance stopped in the previous section and access it via SSH
  | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/new-user-accounts-linux-instance/)
  | [video](https://www.youtube.com/watch?v=khPGZYh73fo)
<details><summary>Show details</summary>

* **Details**
  * Use the following Linux OS user settings
    | adduser(8)
    * Username: `tutor-a`
    * Public key: `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIChvBKAJbIt0H0O26DbZnu2I0kHG+OJBEvR0UkgqWwFb tutor-a`
  * Provide user `tutor-a` with instance administrative privileges via `sudo`
    | [text](https://developers.redhat.com/blog/2018/08/15/how-to-enable-sudo-on-rhel)
    * Add user `tutor-a` to the group: `wheel`
      | usermod(8)
    * Use `visudo` command (which safely edits `/etc/sudoers` file with `vi` editor) to enable all users in group `wheel` to run any command with `sudo` **without a password**
      | visudo(8)
* **What we have as a result (to check/validate)**
  * User `tutor-a` has SSH access to the Linux EC2 instance (using its private key) with instance administrative privileges via `sudo`
</details>  
  
---
### Exercise 12  
Stop the EC2 instance
<details><summary>Show details</summary>

* **Details**
  * See the previous section
* **What we have as a result (to check/validate)**
  * **Stopped** Linux EC2 instance in `eu-central-1` region configured according to the following
    * Amazon Linux 2 OS installed
    * SSH daemon configured according to best practices
    * Web server `nginx` installed and accessible via `http` on TCP port `80`
    * User `tutor-a` created and provided SSH access (using its private key) with instance administrative privileges via `sudo`  
</details>   
  
---
### Exercise 13  
Create custom EC2 key pair using Amazon EC2
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)(Console)
<details><summary>Show details</summary>

* **Details**
  * Use AWS Console
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the following EC2 key pair settings
    * Key pair name: `student-rsa`
    * Key pair type: `RSA`
    * Private key file format: `.pem`
  * Save downloaded private key file (`student-rsa.pem`) as `~/.ssh/id_student_rsa` (in local Linux/MacOS workplace) and make appropriate permission changes
* **What we have as a result (to check/validate)**
  * EC2 key pair `student-rsa` in `eu-central-1` region, private key file `~/.ssh/id_student_rsa`
</details>   
 
---
### Exercise 14  
Create custom EC2 key pair using Amazon EC2
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)(AWS CLI)
<details><summary>Show details</summary>

* **Details**
  * Use AWS CLI
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the following EC2 key pair settings
    * Key pair name: `student-ed25519`
    * Key pair type: `ED25519`
    * Private key file format: `.pem`
  * Save private key file as `~/.ssh/id_student_ed25519` (in local Linux/MacOS workplace) and make appropriate permission changes
* **What we have as a result (to check/validate)**
  * EC2 key pair `student-ed25519` in `eu-central-1` region, private key file `~/.ssh/id_student_ed25519`
</details>   
  
---
### Exercise 15  
Create custom EC2 security group
  | [text](Create custom EC2 security group)
<details><summary>Show details</summary>

* **Details**
  * Use AWS Console
    | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html)(New console) 
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the following security group settings
    * Security group name: `public-ssh-and-http`
    * Description: `Allow SSH and HTTP access from the World`
    * VPC: use `default` VPC (the only VPC ID available at this stage)
    * Allow ingress `http` traffic on TCP port `80` from the source address `0.0.0.0/0`	
      | [text](https://developers.redhat.com/blog/2018/08/15/how-to-enable-sudo-on-rhel)(New console) 
    * Allow ingress `ssh` traffic on TCP port `22` from the source address `0.0.0.0/0`
    * Allow all egress traffic to the destination address `0.0.0.0/0`     
* **What we have as a result (to check/validate)**
  * EC2 security group `public-ssh-and-http in eu-central-1` region allowing SSH and HTTP access from the World
</details>   
  
---
### Exercise 16  
Create custom EC2 security group
<details><summary>Show details</summary>

* **Details**
  * Use AWS CLI
    | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html)(Command line) 
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the following security group settings
    * Security group name: `public-ssh-http-81`
    * Description: `Allow SSH, HTTP and 81/TCP access from the World`
    * VPC: use `default` VPC (the only VPC ID available at this stage)
    * Allow ingress `http` traffic on TCP port 80 from the source address `0.0.0.0/0`
      | [text](https://developers.redhat.com/blog/2018/08/15/how-to-enable-sudo-on-rhel)(Command line) 
    * Allow ingress traffic on TCP port `81` from the source address `0.0.0.0/0`  
    * Allow ingress `ssh` traffic on TCP port `22` from the source address `0.0.0.0/0`
    * Allow all egress traffic to the destination address `0.0.0.0/0`       
* **What we have as a result (to check/validate)**
  * EC2 security group `public-ssh-http-81`  in `eu-central-1` region allowing SSH, HTTP, and TCP on port `81` access from the World
</details>  
  
---
### Exercise 17   
Create Ubuntu EC2 Instance with custom EC2 security group and EC2 key pair
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html)
<details><summary>Show details</summary>

* **Details**
  * Use AWS Console 
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the following EC2 instance settings (all set as default with the exception of the specified)
    | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html)
    * Amazon Machine Image: `Ubuntu Server 20.04 LTS (HVM), SSD Volume Type`(Free tier eligible)
    * Instance type: `t2.micro` (Free tier eligible)
    * Instance tag key-value: `Name: ubuntu-console`
    * Security group name: `public-ssh-and-http`
    * **Choose an existing key pair** as wizard prompted
      * Select a key pair: `student-rsa|RSA` 
* **What we have as a result (to check/validate)**
  * **Running** Ubuntu EC2 instance (`ubuntu-console`) in `eu-central-1` region
</details>   

---
### Exercise 18  
Connect to the created instance via SSH using **default user**
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html)(*)
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * Ability to execute commands in shell of the created instance remotely via SSH
</details>   
  
---
### Exercise 19  
Configure SSH daemon of the created instance to be more secure 
  | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/ec2-ssh-best-practices/)(*)
<details><summary>Show details</summary>

* **Details**
  * Make sure that SSH access for Linux `root` user is prohibited
  * Make sure that SSH access using passwords is prohibited
  * Make sure that SSH access using passwords is prohibited
* **What we have as a result (to check/validate)**
  * SSH daemon is configured according to best practices
</details>   
 
---
### Exercise 20   
Install `nginx` web server and set up a basic website (custom static page) over `http` on TCP port `81` — according to the referenced [tutorial](https://ubuntu.com/tutorials/install-and-configure-nginx#1-overview)(*)
  | [text](https://ubuntu.com/tutorials/install-and-configure-nginx#1-overview)
<details><summary>Show details</summary>

* **Details**
  * Make sure both default `nginx` welcome page (*Welcome to nginx*) and basic website (*Hello, Nginx!*) are accessible from all over the world  
* **What we have as a result (to check/validate)**
  * http request to TCP port 80 to public IP address or DNS name of the EC2 instance returns default nginx welcome page of Ubuntu AMI (*Welcome to nginx!*); http request to TCP port 81 to public IP address or DNS name of the EC2 instance returns custom static page (*Hello, Nginx!*)
</details>   
 
---
### Exercise 21   
Add OS user to the Linux instance and provide it with SSH access (using its private key) with instance administrative privileges via `sudo`  
  | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/new-user-accounts-linux-instance/)(*)
<details><summary>Show details</summary>
 
* **Details**
  * Use the following Linux OS user settings
    | [adduser(8)](http://manpages.ubuntu.com/manpages/trusty/man8/adduser.8.html) 
    * Username: `tutor-a`
    * Public key: `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIChvBKAJbIt0H0O26DbZnu2I0kHG+OJBEvR0UkgqWwFb tutor-a`
  * Provide user `tutor-a` with instance administrative privileges via `sudo`
    | [text](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file)(add) 
    * Add user `tutor-a` to the group: `sudo`
    * Use `visudo` command to enable all users in group `sudo` to run **any command as any user or member of any group** with `sudo` **without a password**
* **What we have as a result (to check/validate)**
  * User `tutor-a` has SSH access to the Linux EC2 instance (using its private key); user `tutor-a` is a member of  `sudo` group; members of group `sudo` can run any command as any user or member of any group with `sudo` without a password
</details>  
 
---
### Exercise 22   
Stop the created EC2 instance
<details><summary>Show details</summary>
 
* **What we have as a result (to check/validate)**
  * **Stopped** Linux EC2 instance in `eu-central-1` region configured according to the following
    * Ubuntu Server 20.04 LTS OS installed
    * SSH daemon configured according to best practices
    * Web server `nginx` installed and accessible via `http` on TCP ports `80` and `81`
    * Members of the group `sudo` can run any command as any user or member of any group with `sudo` without a password
    * User `tutor-a` created and provided SSH access (using its private key) with instance administrative privileges via the group `sudo` membership  
</details>   
 
---
### Exercise 23   
Start (just before the check) the created above (and now stopped) Amazon Linux 2 and Ubuntu instances and provide their public **IP addresses** (or DNS names) 
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html)(*)
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * **Checkpoint**(01): please, **stop here** to check the results of your work before moving on
</details>  
 
---
### Exercise 24   
Terminate the created above Amazon Linux 2 and Ubuntu instances
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>  
 
---
### Exercise 25   
Сreate Ubuntu EC2 instance repeating the steps in the previous section, but using **AWS CLI**
<details><summary>Show details</summary>
 
* **Details**
  * Use **AWS CLI**
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the following custom EC2 instance settings 
    | [text](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-instances.html) 
    * Platform: `EC2-VPC`
      * Note: In this course we work only with `EC2-VPC`, and never with `EC2-Classic`
    * AMI ID: `ami-05f7491af5eef733a`
    * Instance type: `t2.micro`
    * Key pair name: `student-ed25519`
    * **Security group ID**: ID of `public-ssh-http-81` security group
      * Use the following command to find out **security group ID** (by known `<group name>)`
      *  aws ec2 describe-security-groups --group-names <group_name> --query 'SecurityGroups[*].GroupId' --output text
         | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-vpcs.html)
    * **Subnet ID**: ID of any one of the subnets in the `default` VPC
      * Use the following command to find out **VPC ID** of the `default` VPC
      *  aws ec2 describe-vpcs --filters "Name=isDefault, Values=true" --query "Vpcs[*].VpcId" --output text
         | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-vpcs.html)
      * Use the following command to find out **VPC subnets' IDs** (by known `<VPC ID>`)
      *  aws ec2 describe-subnets --filters "Name=vpc-id,Values=<VPC ID>" --query "Subnets[*].SubnetId" --output text
         | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-subnets.html)
    * Instance tag key-value: `Name: ubuntu-cli`
      | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html)
  * Repeat all the configuration steps from the previous section for the following components
    * sshd daemon
    * nginx daemon
    * tutor-a user
* **What we have as a result (to check/validate)**
  * **Running** Ubuntu EC2 instance (`ubuntu-cli`) in `eu-central-1` region
</details>    
 
---
### Exercise 26 
Stop the created EC2 instance
<details><summary>Show details</summary>
     
* **Details**
  * Use **AWS CLI**
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/stop-instances.html) 
    * Use the following command to find out `ubuntu-cli` **instance ID**
      * `aws ec2 describe-instances --filters "Name=tag:Name,Values=ubuntu-cli" --query "Reservations[].Instances[].InstanceId" --output text`
* **What we have as a result (to check/validate)**
  * **Stopped** Ubuntu EC2 instance (`ubuntu-cli`) in `eu-central-1` region
</details>  
 
---
### Exercise 27   
Create (one more) Ubuntu EC2 instance repeating the steps in the previous section, but using **User data**
<details><summary>Show details</summary>
     
* **Details**
  * Use **AWS CLI**
  * Use any of the created IAM admin users
  * Use AWS Region: `Europe (Frankfurt) eu-central-1`
  * Use the same EC2 instance settings as in the previos section (see above) with only the following modifications
    * Instance tag key-value: `Name: ubuntu-ud1`
  * Setup the following components the same way as in the previous section but using only **User data** to configure the instance by scripts during launch
    | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html) 
    * sshd daemon
    * nginx daemon
    * tutor-a user
* **What we have as a result (to check/validate)**
  * **Running** Ubuntu EC2 instance (`ubuntu-ud1`) in `eu-central-1` region
</details>  
 
---
### Exercise 28   
Stop the created EC2 instance
<details><summary>Show details</summary>
     
* **Details**
  * Use **AWS CLI**
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/stop-instances.html)(*)
* **What we have as a result (to check/validate)**
  * **Stopped** Ubuntu EC2 instance (`ubuntu-ud1`) in `eu-central-1` region
</details>  
 
---
### Exercise 29   
Start (just before the check) both the created above (and now stopped) Ubuntu instances (`ubuntu-cli, ubuntu-ud1`) and provide their public IP addresses (or DNS names) 
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html)(*)
<details><summary>Show details</summary>
     
* **What we have as a result (to check/validate)**
  * **Checkpoint** (02): please, **stop here** to check the results of your work before moving on
</details>  
 
---
### Exercise 30   
Terminate both the created above Ubuntu instances (`ubuntu-cli, ubuntu-ud1`)
  | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/terminate-instances.html)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS CLI 
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>  
 
---
### Exercise 31   
Create IAM role and EC2 **instance profile** to grant applications running on the instance (which will be created below) full access permissions to Amazon S3 service (within AWS account)
  | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS CLI 
  * Use the following settings 
    * Role name: `EC2toS3FullAccess`
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-role.html)
    * Role description: `Allow EC2 to do everything with any S3 buckets`
    * Inline access policy name: `S3FullAccess`
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/put-role-policy.html)
    * **Instance profile** name: `EC2toS3FullAccessProfile`
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-instance-profile.html)
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/add-role-to-instance-profile.html)
* **What we have as a result (to check/validate)**
  * Instance profile `EC2toS3FullAccessProfile` with the corresponding permissions
</details>  
 
---
### Exercise 32   
Create S3 bucket
  | [text](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS CLI 
    | [text](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html)
  * Use the following S3 bucket settings 
    * Bucket name: `cec-<AWS account ID>-j2`
      | [text](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html)
      * Use the following command to find out `<AWS account ID>`
      *  aws sts get-caller-identity --query Account --output text
    * AWS Region: `EU (Frankfurt) eu-central-1`
    * **All other settings**: default
* **What we have as a result (to check/validate)**
  * S3 bucket with the name: `s3://cec-<AWS account ID>-j2`
</details>  
 
---
### Exercise 33   
Put the **launch script** used as **User data** in the previous section into the created bucket
  | [text](https://docs.aws.amazon.com/AmazonS3/latest/userguide/uploading-an-object-bucket.html)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS CLI 
    | [text](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html)
  * Put the launch script into `user-data` folder in the created bucket
* **What we have as a result (to check/validate)**
  * File on S3 bucket: `s3://cec-<AWS account ID>-j2/user-data/<ubuntu launch script>`
</details>  
 
---
### Exercise 34  
Create Ubuntu EC2 instance repeating the steps in the previous section using AWS CLI, but with the following modifications
<details><summary>Show details</summary>
  
* **Details**
  * Changes in EC2 instance settings
    * Instance tag key-value: Name: `ubuntu-ud2`
    * Use **instance profile** (the created above): `EC2toS3FullAccessProfile`
      | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)
  * Use **User data** to perform the following operations
    * Install AWS CLI version 2 on the EC2 instance
      | [text](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
    * Download launch script from the created above S3 bucket
      | [text](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html)(*)
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html)(*)
      * Make this step independent on the AWS account — determine S3 bucket name dynamically by requesting **AWS account ID** using AWS CLI command 
    * Initialize the instance by running the downloaded launch script as `root`
* **What we have as a result (to check/validate)**
  * **Running** Ubuntu EC2 instance (`ubuntu-ud2`) in `eu-central-1` region
</details>  
 
---
### Exercise 35   
Stop the created EC2 instance
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS CLI
* **What we have as a result (to check/validate)**
  * **Stopped** Ubuntu EC2 instance (`ubuntu-ud2`) in `eu-central-1` region
</details>  
 
---
### Exercise 36   
Create **launch script** similar to the one created for Ubuntu in the previous section but for Amazon Linux 2 and put it to the same bucket/folder as in the previous section 
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * File on S3 bucket: `s3://cec-<AWS account ID>-j2/user-data/<al2 launch script>`
</details>  
 
---
### Exercise 37   
Create Amazon Linux 2 EC2 instance repeating the steps in the previous section for Ubuntu using AWS CLI, but with the following modifications
<details><summary>Show details</summary>]
  
* **Details**
  * Changes in EC2 instance settings
    * Instance tag key-value: `Name: al2-ud2`
    * AMI ID: `ami-07df274a488ca9195`
  * Changes in configurations performed by the **User data**
    * To initialize the instance download from the S3 bucket (and run) the created above **launch script** for Amazon Linux 2  
* **What we have as a result (to check/validate)**
  * **Running** Amazon Linux 2 EC2 instance (`al2-ud2`) in `eu-central-1` region
</details>  
 
---
### Exercise 38   
Stop the created EC2 instance
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
* **What we have as a result (to check/validate)**
  * **Stopped** Amazon Linux 2 EC2 instance (`al2-ud2`) in `eu-central-1` region
</details>  
 
---
### Exercise 39   
Start (just before the check) both the created above (and now stopped) Ubuntu and Amazon Linux 2 instances (`ubuntu-ud2, al2-ud2`) and provide their public IP addresses (or DNS names) 
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * **Checkpoint** (03): please, **stop here** to check the results of your work before moving on
</details>  
 
---
### Exercise 40   
Terminate both the created above Ubuntu instances (`al2-ud2, ubuntu-ud2`)
  | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/terminate-instances.html)(*)
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>  
 
---
### Exercise 41   
Create local shell script create.sh which creates two EC2 instances repeating the steps in the previous sections, but with the following modifications
<details><summary>Show details</summary>]
  
* **Details**
  * Use the procedure to deterimine the latest version of AMI IDs for the requested OS type with help of `aws ssm get-parameters` command
    | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)
    * 1-st instance
      * OS type: `Ubuntu 20.04`
        | [text](https://discourse.ubuntu.com/t/finding-ubuntu-images-with-the-aws-ssm-parameter-store/15507)
    * 2-nd instance
      * OS type: Amazon Linux 2
        | [text](https://aws.amazon.com/ru/blogs/compute/query-for-the-latest-amazon-linux-ami-ids-using-aws-systems-manager-parameter-store/)
  * Both instances should use the same **User data** to perform the following operations 
    * Determine OS type of the instance being configured and install appropriate AWS CLI of version 2
      * It is possible to use the /etc/os-release file both in AL2 and Ubuntu to determine the OS type
    * Download the created in the previous section **launch script** (appropriate for the OS) from corresponding S3 bucket to initialize and configure the instance
      * Initialize the instance by running the downloaded **launch script** as `root`
  * Initialize the instance by running the downloaded **launch script** as `root`
  * Instances should have the following tags corresponding to their OS types
    * 1-st instance
      * Instance tag key-value: `Name: ubuntu-ud3`
    * 2-nd instance
      * Instance tag key-value: `Name: al2-ud3`
  * Both instances shoud additionally be tagged with key-value: `Type: cec`
* **What we have as a result (to check/validate)**
  * Shell script `create.sh`
</details>  
  
---
### Exercise 42   
Create local shell script `list.sh` which lists all running EC2 instances tagged with key-value: `Type: cec` providing the following information for each instance
<details><summary>Show details</summary>]
  
* **Details**
  * Instance ID
  * Instance public IP
  * Instance OS type
* **What we have as a result (to check/validate)**
  * Shell script `list.sh`
</details>  
   
---
### Exercise 43   
Create local shell script `delete.sh` which deletes all running EC2 instances taggeted with key-value: `Type: cec`
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * Shell script `delete.sh`
</details>  
  
---
### Exercise 44   
Use created `create.sh` script to create Ubuntu and Amazon Linux 2 instances (`ubuntu-ud3, al2-ud3`). Use created `list.sh` script to determine and provide public IP addresses of the created instances. Perform these steps just before the check.
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * **Checkpoint** (04): please, **stop here** to check the following results of your work before moving on
  * Two EC2 instances, one of Ubuntu Server 20.04 LTS (`ubuntu-ud3`) and second one of Amazon Linux 2 (`al2-ud3`)
    * Installed with **latest versions** of AMI for the corresponding OS'es
    * Configured with corresponding **instance profile** used for both instances
    * **Tagged** with corresponding key-value tags
    * Configured with corresponding **user data** launch scripts downloaded from the specified S3 bucket
</details>  
  
---
### Exercise 45   
Use created `delete.sh` script to terminate both the created above Linux instances (`al2-ud3, ubuntu-ud3`)
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>  
  
---
### Exercise 46   
Create IAM role which provides read only access to all EC2 instances and all S3 buckets using **AWS managed policies**
  | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-role.html)(*)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/attach-role-policy.html)
  * Use the following settings 
    * Role name: `CloudEngJ2Ch05Role`
    * Role description: `Provides read only access to all EC2 instances and S3 buckets`
    * Includes the following **AWS managed policies**
      | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)
      * AmazonEC2ReadOnlyAccess
      * AmazonS3ReadOnlyAccess
* **What we have as a result (to check/validate)**
  * IAM role `CloudEngJ2Ch05Role` with the corresponding permissions
</details>  
  
---
### Exercise 47   
Create EC2 instance profile for the created above IAM role
  | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2_instance-profiles.html)
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-instance-profile.html)(*)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/add-role-to-instance-profile.html)(*)
  * Use the following settings 
    * Instance profile name: `CloudEngJ2Ch05Profile`
    * Role to store in the instance profile: `CloudEngJ2Ch05Role`
* **What we have as a result (to check/validate)**
  * Instance profile `CloudEngJ2Ch05Profile` containing the corresponding IAM role
</details>  
  
---
### Exercise 48   
Enable versioning of the bucket created earlier in this course
  | [text](https://docs.aws.amazon.com/AmazonS3/latest/userguide/manage-versioning-examples.html)
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-bucket-versioning.html)
  * Bucket name: `cec-<AWS account ID>-j2`
    * Use the following command to find out `<AWS account ID>`
      * aws sts get-caller-identity --query Account --output text
* **What we have as a result (to check/validate)**
  * S3 bucket `cec-<AWS account ID>-j2` versioning enabled
</details>  
  
---
### Exercise 49   
Sign up with free account of `noip.com` — dynamic DNS service provider
  | [text](https://www.noip.com/free)
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * Free account of `noip.com` service
</details>  
  
---
### Exercise 50   
Create two public **DNS Host names** (`No-IP Hostnames`) with `noip` service: one for Ubuntu instance and one for Amazon Linux instance
<details><summary>Show details</summary>]
  
* **Details**
  * Use any available domain name, like e.g. `ddns.net`
  * Use any available hostnames in the chosen domain, like e.g. `ubuntu-ud5-abc` and `al2-ud5-def`
* **What we have as a result (to check/validate)**
  * Two **DNS Hostnames** in `noip.com` service
</details>  
  
---
### Exercise 51   
Change the last version of local shell script `create.sh`(created above in this course) and corresponding **OS-dependent launch scripts** to make the following modifications while creating EC2 instances
<details><summary>Show details</summary>]
  
* **Details**
  * Both instances should use the created in the previous section instance profile: `CloudEngJ2Ch05Profile`
  * Instances should have the following tags corresponding to their OS types
    * 1-st instance
      * Instance tag key-value: `Name: ubuntu-ud5`
    * 2-nd instance
      * Instance tag key-value: `Name: al2-ud5`
  * Local `hostnames` of the instances shoud be set to the value of their `Name` tag in some exemplary domain, like e.g. `example.com`
    * To fulfill this requirement, initialization procedure can do the following
      * Get the `instance ID` from the **instance metadata**
        | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-retrieval.html)
        | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-categories.html)
      * For the given `instance ID` get the value of the instance tag `Name` using `aws ec2 describe-instances` command
        | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-instances.html)
      * Set the instance `hostname` to `<name>.example.com` (using for example `hostnamectl set-hostname` command)
        | [text](https://man7.org/linux/man-pages/man1/hostnamectl.1.html)
        | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-hostname.html)
   * noip **Dynamic Update Client** should be installed and configured as a systemd service to perform dynamic DNS update the created noip.com service **DNS Hostnames** with public IP addresses of the instances
     | [text](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dynamic-dns.html)
     | [text](https://www.noip.com/support/knowledgebase/installing-the-linux-dynamic-update-client-on-ubuntu/)
     * Use local shell script `list.sh` (created above in this course) to validate that instance IP addresses correspond to the IP addresses of the No-IP **DNS Hostnames**
* **What we have as a result (to check/validate)**
  * Shell script `create.sh` and corresponding OS-dependent launch scripts modified according to the requirements
</details>  
   
---
### Exercise 52   
Use modified `create.sh` script to create Ubuntu and Amazon Linux 2 instances (`ubuntu-ud5, al2-ud5`). Perform these steps just before the check. Provide instances' public DNS hostnames created in `noip.com` service.
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * **Checkpoint** (05): please, **stop here** to check the following results of your work before moving on
  * Two EC2 instances, one of Ubuntu Server 20.04 LTS (`ubuntu-ud5`) and second one of Amazon Linux 2 (`al2-ud5`) with the following differencies related the **checkpoint** (04)
    * Configured with required permissions via **instance profile**
    * **Tagged** with required key-value tags
    * OS `hostnames` taken from the instance's `Name` tag
    * noip service installed and configured to update the created **DNS Hostnames** of noip.com service with instance public IPs
</details>  
  
---
### Exercise 53   
Use created `delete.sh` script (created above in this course) to terminate both the created above Linux instances (`al2-ud5, ubuntu-ud5`)
<details><summary>Show details</summary>]
  
* **Details**
* *A brief introduction to the exercise purpose*
  * Every time any on-demand EC2 instance is started, AWS infrastructure assigns the instance a dynamic public IP address. In such a configuration the instance IP address changes every time when restart occurs
  * One way to access the created instance using its dynamic public IP address is to register the IP address as DNS records of type 'A' for particular domain name in the corresponding DNS zone (using, for example, instance launch script upon every instance restart)
  * Amazon Route 53 is managed DNS service used to register domain names and host DNS zones within AWS
  * Domain name registration and DNS zone hosting are not covered by the AWS Free Tier
  * Due to the above fact the exercise assumes using separate dedicated AWS account for these purposes
    | [text](https://gavinlewis.medium.com/managing-route-53-in-a-multi-account-environment-5d95a3cb67c5)
  * The following configuration components are used in this exercise
    * ID of AWS account to register domain name and host all the necessary DNS zones
      * 272304640086
    * The registered domain name
      * cirruscloud.click
    * Student's managed DNS zone in the registered domain name (where `<AccountID>` is ID of student AWS account )
      * <AccountID>.cirruscloud.click
  * In the mentioned `272304640086` AWS account all necessary Roles and Policies are created to provide student accounts access to create/update resourse records in their corresponding DNS zones hosted in this (272304640086) account
    * For the folowing **actions related to public hosted DNS zones** of `272304640086` AWS account the permissions are provided (for corresponding student accounts)
      | [text](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/r53-api-permissions-ref.html)
      * route53:GetHostedZone
      * route53:ListHostedZones
  * For the folowing **actions related to resource records in the hosted DNS zones dedicated for particular students** in `272304640086` AWS account the permissions are provided (for corresponding student accounts) 
    | [text](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/r53-api-permissions-ref.html)
    * route53:ChangeResourceRecordSets
    * route53:GetChange
    * route53:ListResourceRecordSets
    * route53:ListHostedZonesByName
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>  
  
---
### Exercise 54   
Create IAM customer managed policy which allows student account to assume cross-account role with corresponding permissions (to be able to create/update resource records in the appropriate DNS zone)
  | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-cli.html)
  | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-policy.html)  
<details><summary>Show details</summary>]
  
* **Details**
  * Policy name
    * CloudEngJ2Ch06CrossAccount
  * Cross-account ID
    * 272304640086
  * Cross-account role name (dedicated roles for each student account are created in `272304640086` account)
    * `CloudEngJ2Ch06UpdateDNSZone<AccountID>`
      * where `<AccountID>` is ID of student AWS account
* **What we have as a result (to check/validate)**
  * IAM customer managed policy CloudEngJ2Ch06CrossAccount with the corresponding content
</details>  
  
---
### Exercise 55   
Create IAM role which allows: read only access to all EC2 instances, read only access to all S3 buckets, assuming mentioned above cross-account role
  | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)(*)
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-role.html)(*)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/attach-role-policy.html)(*)
  * Use the following settings 
    * Role name: `CloudEngJ2Ch06Role`
    * Role description: `Allows read only access to all EC2 instances and S3 buckets, assume Update DNS Zone role in 272304640086 Account`
    * Includes the following **AWS managed and customer managed** policies
      | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)(*)
      | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)
      * AmazonEC2ReadOnlyAccess
      * `AmazonS3ReadOnlyAccess`
      * `CloudEngJ2Ch06CrossAccount`
* **What we have as a result (to check/validate)**
  * IAM role `CloudEngJ2Ch06Role` with the corresponding permissions
</details>  

---
### Exercise 56   
Create EC2 instance profile for the created above IAM role
  | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2_instance-profiles.html)(*)
<details><summary>Show details</summary>]
  
* **Details**
  * Use AWS CLI
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-instance-profile.html)(*)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/add-role-to-instance-profile.html)(*)
  * Use the following settings 
    * Instance profile name: `CloudEngJ2Ch06Profile`
    * Role to store in the instance profile: `CloudEngJ2Ch06Role`
* **What we have as a result (to check/validate)**
  * Instance profile `CloudEngJ2Ch06Profile` containing the corresponding IAM role
</details>  
  
---
### Exercise 57   
Change the last version of local shell script create.sh (created above in this course) and corresponding **OS-dependent launch scripts** to make the following modifications while creating EC2 instances
<details><summary>Show details</summary>]
  
* **Details**`
  * Both instances should use the created in the previous section instance profile: `CloudEngJ2Ch06Profile`
  * Instances should have the following tags corresponding to their OS types
    * 1-st instance
      * Instance tag key-value: Name: `ubuntu-ud6`
    * 2-nd instance
      * Instance tag key-value: `Name: al2-ud6`
  * Local `hostnames` of the instances shoud be set according to the following
    * **Host part** of the `hostnames` should correspond to the value of the instance `Name` tag
    * **Domain part** of the `hostnames` should correspond to the DNS zone dedicated for particular student in the registered domain name: `<AccountID>.cirruscloud.click`, where `<AccountID>` is ID of student AWS account
  * The instance dynamic public IP addresses should be registered as DNS resource records of type 'A' in the corresponding DNS zone `(<AccountID>.cirruscloud.click)` with the record names set to **host part** of the instance `hostnames` above (FQDN)
    * To create, delete, or change (upsert) a resource record set in a configured hosted zone it is possible to use `aws route53 change-resource-record-sets` command
      | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/simple-resource-record-route53-cli/)
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/route53/change-resource-record-sets.html)
    * To get ID for zones hosted in the AWS account it is possible to use `aws route53 list-hosted-zones` command
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/route53/list-hosted-zones.html)
    * To be able to use the above command in your accounts **(trusted account)** with resources in different account **(trusting account)** it is neccery to switch to the corresponding role in the **trusting account**. To do this in scripts or from command line it is possible to use `aws sts assume-role` command to get the appropriate role credentials and then use them for API calls. This approach is called **cross-account access**
      | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)
* **What we have as a result (to check/validate)**
  * Shell script `create.sh` and corresponding OS-dependent launch scripts modified according to the requirements
</details>  
  
---
### Exercise 58   
Use modified `create.sh` script to create Ubuntu and Amazon Linux 2 instances (`ubuntu-ud6, al2-ud6`). Perform these steps just before the check (instance FQDN's will be used to access them)
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * **Checkpoint** (06): please, stop here to check the following results of your work before moving on
  * Two EC2 instances, one of Ubuntu Server 20.04 LTS (`ubuntu-ud6.<AccountID>.cirruscloud.click`) and second one of Amazon Linux 2 (`al2-ud6.<AccountID>.cirruscloud.click`) with the following differencies related the **checkpoint (05)**
    * Configured with required permissions via **instance profile**
    * **Tagged** with required key-value tags
    * OS `hostnames` set according to their FQDN formed by instance's `Name` tag and corresponding domain name
    * Accessible via instances FQDN after OS restart
</details>  
  
---
### Exercise 59   
Use created `delete.sh` script (created above in this course) to terminate both the created above Linux instances (`al2-ud6, ubuntu-ud6`)
<details><summary>Show details</summary>]
  
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>  
  
---
### Exercise 60
Сreate a local file named `regions-allowed.conf` which will contain a list of AWS regions where it is allowed to deploy infrastructure, and should be used to limit all the used scripts to work with only the specified regions 
<details><summary>Show details</summary>
  
* **Details**
  * Сreate a local file named `regions-allowed.conf` which will contain a list of AWS regions where it is allowed to deploy infrastructure, and should be used to limit all the used scripts to work with only the specified regions 
    * Use the command `aws ec2 describe-regions` ... to find out and filter corresponding regions
      | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-regions.html)
* **What we have as a result (to check/validate)**
  * Local file `regions-allowed.conf` with list of allowed AWS regions — each region value on a new line
</details>
  
---
### Exercise 61
Create local **infrastructure script** (named `infra.sh`) which should ensure that every AWS region from `regions-allowed.conf` is ready for infrastructure deployments according to requirements (for example it should be ready for creation EC2 instances by current and future versions of the `create.sh` script)
<details><summary>Show details</summary>
  
* **Details**
  * The following are the requirements to be fulfilled
    * for all the corresponding regions there are default VPC and default subnets (in each region availability zone)
      | [text](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html)
    * required EC2 security groups exist in the default VPC of all the corresponding regions
    * required EC2 key pairs exist in all the corresponding regions 
  * The script should be idempotent (reenterable) — the script should check if the required component exists and create it only if it is not present (not re-create existing components)
    | [text](https://en.wikipedia.org/wiki/Idempotence)
    | [text](https://ru.wikipedia.org/wiki/Идемпотентность)(ru)  
* **What we have as a result (to check/validate)**
  * Shell script `infra.sh`
</details>
  
---
### Exercise 62
Use the create `infra.sh` script to create all the necessary components in regions specified in `regions-allowed.conf` file
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * For all `opt-in-not-required` regions there are default VPC and default subnets (in each region availability zone)
  * EC2 key pair `student-rsa` exists in all `opt-in-not-required` regions (corresponding to the private key in the local file `~/.ssh/id_student_rsa)`
  * EC2 key pair `student-ed25519` exists in all `opt-in-not-required` regions (corresponding to the private key in the local file `~/.ssh/id_student_ed25519)`
  * EC2 security group `public-ssh-and-http` exists in all `opt-in-not-required` regions allowing SSH and HTTP access from the World (in the region default VPC)
  * EC2 security group `public-ssh-http-81` exists in all `opt-in-not-required` regions allowing SSH, HTTP, and TCP on port `81` access from the World (in the region default VPC)
</details>
  
---
### Exercise 63
Change the last version of local shell script `create.sh` (created above in this course) and corresponding **OS-dependent launch scripts** to make the following modifications while creating EC2 instances
<details><summary>Show details</summary>
  
* **Details**
  * create.sh script should take two arguments with help of the following flags
    * --region flag: specifies region where the EC2 instance should be created
      * --region flag: specifies region where the EC2 instance should be created
      * if the value is not from the list in the `regions-allowed.conf` file, the script should exit without instance creation providing a complaint message
    * --os flag: specifies OS type of the created instance
      * **possible values** for this argument are from the following list
        *   `al2` — for the last AWS AMI version of `Amazon Linux 2` OS
        *   `ubuntu` — for the last AWS AMI version of `Ubuntu 20.04` OS
        * if the value is not from the above list, the script should exit without instance creation providing a complaint message
      * create.sh script should create **one** EC2 instance of the specified OS type in the specified region (according to **possible values** of the corresponding arguments) with the following modifications according to its last version (created previously in this course)
        * The instances should have the following tag corresponding to its OS type (where `<OSType>` is the value of `--os` argument, e.g. `ubuntu-ud7` for Ubuntu 20.04)
          * Instance tag key-value: `Name: <OSType>-ud7`
        * Note that the instance shoud additionally be tagged with key-value: `Type: cec`
        * Note that the instance should use the same instance profile as was used for the checkpoint (06): `CloudEngJ2Ch06Profile` 
* **What we have as a result (to check/validate)**
  * Shell script `create.sh` and corresponding OS-dependent launch scripts modified according to the requirements
</details>
  
---
### Exercise 64
Modify local shell scripts `list.sh` and `delete.sh` which should list and delete all running EC2 instances tagged with key-value: `Type: cec` in all the regions specified in the file `regions-allowed.conf`
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * Shell scripts `list.sh` and `delete.sh` modified according to the requirements
</details>
  
---
### Exercise 65
Use modified `create.sh` script to create two EC2 instances according to the following requirements in any different AWS regions specified in `regions-allowed.conf` file (`eu-west-1` and `eu-west-2` regions are used in the requirements as examples)
<details><summary>Show details</summary>
  
* **Details**
  * Ubuntu 20.04 instance (`ubuntu-ud7`) in `eu-west-1` region, using the following command
    * ./create.sh --region eu-west-1 --os ubuntu
  * Amazon Linux 2 instance (`al2-ud7`) in `eu-west-2` region, using the following command
    * ./create.sh --region eu-west-2 --os al2
  * Perform these steps just before the check  
* **What we have as a result (to check/validate)**
  * **Checkpoint** (07): please, **stop here** to check the following results of your work before moving on
  * Two EC2 instances: Ubuntu Server 20.04 LTS (`ubuntu-ud7.<AccountID>.cirruscloud.click`) in `eu-west-1` region and Amazon Linux 2 (`al2-ud7.<AccountID>.cirruscloud.click`) in `eu-west-2` region with the following differencies related the **checkpoint** (06)
    * **Tagged** with required key-value tags
    * Created in the specified **regions**  
</details>
  
---
### Exercise 66
Use created `delete.sh` script (created above in this course) to terminate both the created above Linux instances (`al2-ud7, ubuntu-ud7`)
<details><summary>Show details</summary>
  
* **Details**
* *A brief introduction to the exercise purpose*
  * According to the current requirements (specified in the section corresponding to Checkpoint 06) the created instances register their IP addresses as DNS records of type 'A' for particular domain name in the corresponding DNS zone on every instance restart
  * Having such a method we can get a configuration where more than one instance register their IP addresses in the same domain name — a possible way of providing high ailability and/or load balancing for a certain service located on these instances (via round-robin DNS)
    | [text](https://en.wikipedia.org/wiki/Round-robin_DNS)
  * To use such an approach it is also necessary to ensure that old (stale) IP addresses are removed as corresponding instances are no more available, - an instance could restart (and get new IP) or die for any reasons
  * To remove stale IP addresses the following techniques can be used
    * A shutdown script removing instance IP address from DNS zone as instance restarts or shuts down
    * A readiness service running on live instances (participating in certain HA service), monitoring an availability of certain services via their corresponding IP addresses, and removing the IP addresses from DNS zones for the services which are not available
  * Feasible ways to have **multiple IP addresses for one domain name** in Amazon Route 53 zones is to use one of the following routing policies
    * **Simple routing** policy — it is possible to specify multiple values in the same record, such as multiple IP addresses
      | [text](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)
    * **Multivalue answer routing** policy — it is possible to specify multiple values for a record
      | [text](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)
      * Please don't use optional health check feature of Route 53 service for now, we will discuss this feature further
    * In the subsequent exercise use the following **domain name for registering multiple IP addresses** of the created instances in student's managed DNS zone (where `<AccountID>` is ID of student AWS account)
      * ha.<AccountID>.cirruscloud.click
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>
  
---
### Exercise 67
Change the last version of local shell script `create.sh` (created above in this course) and corresponding **OS-dependent launch scripts** to make the following modifications while creating EC2 instances
<details><summary>Show details</summary>
  
* **Details**
  * On an instance start the instance dynamic public IP address should be registered in the corresponding DNS zone with the resource record used for **multiple IP addresses for one domain name** with name of `ha.<AccountID>.cirruscloud.click`
  * On an instance restart/shutdown the instance IP address registered on instance startup in the DNS zone (resource records of `ha.<AccountID>.cirruscloud.click`) should be removed from DNS
    | [text](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files)
  * nginx web server to be configured to respond with HTTP response status code
200 on the following path (where ServerIP is instance dynamic public IP address registered in the DNS zone on startup with resource records of ha.<AccountID>.cirruscloud.click) 
    * http://ServerIP:80/healthz
  * **Readiness service** should be installed and configured as a `systemd` service to perform readiness monitoring according to the following logic
    * Every server ready to participate in serving some application traffic should appropriately answer to the **readiness probe** — respond with HTTP response status code `200` on the following path (where `ServerIP` is server public IP)  
    * http://ServerIP:80/healthz 
    * **Readiness service** checks that all servers, which registered their IP addresses in corresponding DNS zone (resource records of `ha.<AccountID>.cirruscloud.click`), answer to the **readiness probe** appropriately
    * **Readiness service** runs **readiness probe** in period of `<periodSeconds>` seconds (default 600)
    * **Readiness probe** should have timeout of `<timeout>` seconds (default 10) — if response is not returned during this time, the probe considered as failed
    * If **readiness probe** is failed it should be repeated in `<retrySeconds>` seconds (default 20)
    * If **readiness probe** has failed for `<failureThreshold>` times sequentially (default 3) corresponding server is considered as **not ready**
    * If a server becomes **not ready** its IP should be removed by **readiness service** from the DNS zone (resource records of `ha.<AccountID>.cirruscloud.click)`
  * To add/remove IP addresses to/from DNS zone resource records choose **routing policy** most suitable for the task
    | [text](https://aws.amazon.com/ru/premiumsupport/knowledge-center/multivalue-versus-simple-policies/)
    | [text](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/route53/change-resource-record-sets.html)(*)
  * Note that the following configurations should be fulfilled according to the previous requirements
    * The script should create an instance in a region and of OS type specified by corresponding command line arguments
    * The created instance should use the same instance profile as was used for the checkpoint (06): `CloudEngJ2Ch06Profile`
    * The created instance should be tagged accordingly to their OS type with the following tag key-value:
      * Name: <OSType>-ud8
    * The created instance shoud also be tagged with key-value: `Type: cec`
    * The created instance local hostname should be set accordingly
      * **Host part** of the `hostname` should correspond to the value of the instance `Name` tag
      * **Domain part** of the `hostname` should correspond to the DNS zone dedicated for particular student in the registered domain name: `<AccountID>.cirruscloud.click`, where `<AccountID>` is ID of student AWS account
    * The created instance dynamic public IP address should also be registered as DNS resource records of type 'A' in the corresponding DNS zone (`<AccountID>.cirruscloud.click`) with the record name set to **host part** of the instance `hostnames` above (FQDN)
  * Also remember that to be able to change resource records in account of `cirruscloud.click` DNS zone (**trusting** account with ID of `272304640086`) from your (**trusted**) accounts, it is necessary to switch to the corresponding role in the **trusting** account, the same way it was done in the previous section
    | [text](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)(*)
* **What we have as a result (to check/validate)**
  * Shell script `create.sh` and corresponding OS-dependent launch scripts modified according to the requirements
</details>
  
---
### Exercise 68
Use modified `create.sh` script to create two EC2 instances according to the following requirements in any different AWS regions allowed by the corresponding configuration file (`us-east-1` and `us-east-2` regions are used here as examples)
<details><summary>Show details</summary>
  
* **Details**
  * Ubuntu 20.04 instance (`ubuntu-ud8`) in `eu-east-1` region
  * Amazon Linux 2 instance (`al2-ud8`) in `eu-east-2` region
* Perform these steps just before the check  
* **What we have as a result (to check/validate)**
  * **Checkpoint** (08): please, **stop here** to check the following results of your work before moving on
  * Two EC2 instances: Ubuntu Server 20.04 LTS (`ubuntu-ud8.<AccountID>.cirruscloud.click`) in `eu-east-1` region and Amazon Linux 2 (`al2-ud8.<AccountID>.cirruscloud.click`) in `eu-east-2` region with the following differencies related the **checkpoint** (07)
    * **Tagged** with required key-value tags
    * Created in the specified **regions**
    * Public IP addresses of both instances are registered for the same domain name — `ha.<AccountID>.cirruscloud.click`
    * **Readiness service** installed and configured according to the requirements
    * nginx web server configured to serve **readiness probes**
</details>
  
---
### Exercise 69
Use created `delete.sh` script (created above in this course) to terminate both the created above Linux instances (`al2-ud8, ubuntu-ud8`)
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * No instances exist in AWS account (all the instances previously created are terminated)
</details>
