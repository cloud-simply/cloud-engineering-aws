---
> TODO
> Draft, Here are only subjects designated
---

## AWS Cloud Engineering - Practical Guide, Junior 3
Level: `Intermediate`

---
### Exercise 1
Creating Linux EC2 Instances using cloud-init as User data for configuration
<details><summary>Show details</summary>

* **Details**
  * Using AWS CLI
  * Default/Custom VPCs, Subnets, Security groups
* Advanced configuration for the created Linux EC2 Instances
  * Security
    * SSH: non-standard port, limit allowed OS users, connection rate-limiting
    * `sudo` for multi-user environment
    * OS level firewalling (`firewalld, ufw, iptables, nftables`) for system and applications
   * Containerization
     * CRI: `containerd, docker daemon`
     * Best practices
   * Container-based multi-tier app (super simple example)
     * Edge proxy: nginx
     * FE: node
     * BE: flask
     * STORE: redis, mysql/postgresql
* **What we have as a result (to check/validate)**
  * ResultDescription
</details>

---
### Exercise 2
Repeating the above exercise but with applying immutable principles
<details><summary>Show details</summary>

* **Details**
  * Deployment and configuration tools (basic level)
    * Infra-level: IaS (CloudFormation)
    * OS-level: Packer
    * App-level: Containers
* **What we have as a result (to check/validate)**
  * ResultDescription
</details>

---
### Exercise 3
Repeatinng the above exercise but with applying CI/CD (for app **life cycle management**)
  | [text](url)
  | [text](url)
<details><summary>Show details</summary>

* **Details**
  * CI/CD tools (basic level)
    * GitLab
    * BitBucket
    * GitHub Actions
* **What we have as a result (to check/validate)**
  * ResultDescription
</details>
