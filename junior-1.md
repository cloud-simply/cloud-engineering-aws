## AWS Cloud Engineering - Practical Guide, Junior 1
Level: `Elementary`

---
### Exercise 1
Create a new AWS (***Amazon Web Services***) account (and AWS account *root user*)
  | [reference 1](https://aws.amazon.com/getting-started/guides/setup-environment/module-one/)
  | [reference 2](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
<details><summary>Show details</summary>

* **What we have as a result (to check/validate)**
  * AWS account *root user* credentials
    * email
    * password
  * AWS account name (to be recognized in your invoices)
</details>

---
### Exercise 2
Sign in to AWS Console (***AWS Management Console***) as an AWS account *root user*
  | [reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html#root-user-sign-in-page)
<details><summary>Show details</summary>

* **What we have as a result (to check/validate)**
  * Access to AWS Cloud resources under the AWS account *root user* via web interface
</details>

Find your AWS account ID being logged in as the AWS account *root user*
  | [reference](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingYourAccountIdentifiers)
<details><summary>Show details</summary>

* **What we have as a result (to check/validate)**
  * 12-digit AWS account ID
</details>

---
### Exercise 3
Create (the first) IAM *admin user*
  | [reference 1](https://catalog.us-east-1.prod.workshops.aws/workshops/13304db2-f715-48bf-ada0-92e5c4eea945/en-US/020-landingzone/prepare/aws-side/30-create-user)
  | [reference 2](https://www.youtube.com/watch?v=wRzzBb18qUw)
  | [reference 3](https://aws.amazon.com/getting-started/guides/setup-environment/module-two/)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS Console
* **What we have as a result (to check/validate)**
  * The first IAM *admin user* credentials
    * username
    * password
    * access key ID
    * secret access key 
</details>

---
### Exercise 4
Install AWS CLI (***Command Line Interface***) for local Linux/MacOS
  | [reference 1](https://catalog.us-east-1.prod.workshops.aws/workshops/13304db2-f715-48bf-ada0-92e5c4eea945/en-US/020-landingzone/prepare/local-side/10-aws-cli)
  | [reference 2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * AWS CLI (`aws` command) is available in local environment  
</details>

Setup AWS credentials for local Linux/MacOS shells
  | [reference 1](https://catalog.us-east-1.prod.workshops.aws/workshops/13304db2-f715-48bf-ada0-92e5c4eea945/en-US/020-landingzone/prepare/local-side/11-aws-profile)
  | [reference 2](https://aws.amazon.com/getting-started/guides/setup-environment/module-three/)
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * AWS CLI in local environment is configured with access to the created AWS account resources under the first IAM *admin user*
</details>

---
### Exercise 5
Sign in to AWS Console using an IAM user
  | [reference 1](https://catalog.us-east-1.prod.workshops.aws/workshops/13304db2-f715-48bf-ada0-92e5c4eea945/en-US/020-landingzone/prepare/aws-side/40-sign-in-iam)
  | [reference 2](https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html#user-sign-in-page)
<details><summary>Show details</summary>
  
* **What we have as a result (to check/validate)**
  * Access to AWS Cloud resources under the first IAM *admin user* via web interface
</details>

---
### Exercise 6
Create AWS Cloud9 IDE environment
  | [reference 1](https://docs.aws.amazon.com/cloud9/latest/user-guide/create-environment-main.html#create-environment-console)
  | [reference 2](https://aws.amazon.com/getting-started/guides/setup-environment/module-four/)
<details><summary>Show details</summary>
  
* **Details**
  * Use either AWS Console or AWS CLI
  * Set all the following Cloud9 IDE environment settings as default
    * Environment type
    * Instance type
    * Platform
    * Cost-saving setting
    * Network settings
* **What we have as a result (to check/validate)**
  * Cloud9 IDE environment is created and configured with access to the created AWS account resources under the first IAM *admin user*	
</details>

---
### Exercise 7
Configure an IAM user permissions through membership in an IAM group
  | [reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html#getting-started_create-admin-group-console)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS Console
  * Create (the first) IAM *admin group*
  * Place the first IAM *admin user* into the first IAM *admin group*
  * Remove `AdministratorAccess` policy from the first IAM *admin user*
* **What we have as a result (to check/validate)**
  * No `AdministratorAccess` policy is directly assigned to the first IAM *admin user*, but the user has administrative access to the created AWS account resources provided via membership in the IAM group with the corresponding permissions
</details>

---
### Exercise 8
Create IAM group and user using AWS CLI
  | [reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html#getting-started_create-admin-group-cli)
<details><summary>Show details</summary>
  
* **Details**
  * Use AWS CLI
  * Create (the second) IAM *admin group*
  * Create (the second) IAM *admin user* by placing it into the second IAM *admin group*
* **What we have as a result (to check/validate)**
  * The second IAM *admin user* credentials
    * username
    * password
    * access key ID
    * secret access key
</details>
