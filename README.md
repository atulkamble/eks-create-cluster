# 📖 AWS IAM User & EKS Cluster Setup on Windows/Linux/Mac

This guide walks through the process of creating an IAM user with full administrative access, setting up AWS CLI and `eksctl` on Windows, and creating/deleting an EKS cluster.

---
## 📸 Screenshot

![EKS](https://github.com/atulkamble/eks-create-cluster/blob/main/eks.png)

---


## 📌 Prerequisites

* AWS Management Console access with admin privileges
* Windows system with **PowerShell** or **Command Prompt**
* [Chocolatey Package Manager](https://chocolatey.org/install)

---

## 👤 Create IAM User `atul` with Full Admin Access

1. Go to **AWS Management Console** → **IAM**.
2. Navigate to **Users** → **Add users**.
3. Enter **User name:** `atul`.
4. Select **Access type:** ✅ Programmatic access.
5. Click **Next: Permissions**.
6. Attach **AdministratorAccess** policy:

   * Select **Attach existing policies directly**
   * Search for `AdministratorAccess`
   * ✅ Check the box
7. Click **Next: Tags** → **Next: Review**.
8. Click **Create user**.

---

## 🔑 Create Access Key for User `atul`

1. In **IAM Users**, click on `atul`.
2. Go to **Security credentials** tab.
3. Under **Access keys**, click **Create access key**.
4. Note down the **Access Key ID** and **Secret Access Key** securely.

---

## 🖥️ Install AWS CLI on Windows

Follow official AWS documentation:
👉 [Install AWS CLI v2 on Windows](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

**Quick steps:**

1. Download installer:
   [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
2. Run the installer and follow the prompts.
3. Verify installation:

   ```bash
   aws --version
   ```

---

## ⚙️ Configure AWS CLI

Run:

```bash
aws configure
```

When prompted:

* **AWS Access Key ID:** *your-access-key*
* **AWS Secret Access Key:** *your-secret-key*
* **Default region name:** `us-east-1` *(or your preferred region)*
* **Default output format:** `json`

---

## 📦 Install `eksctl` on Windows

Install via **Chocolatey**:

```bash
choco install eksctl
```

Verify installation:

```bash
eksctl version
```

---

## ☸️ Create EKS Cluster

Run the following command to create an EKS cluster named `mycluster` in `us-east-1`:

```bash
eksctl create cluster --name mycluster --region us-east-1
```
```
eksctl create cluster \
--name mycluster \
--region us-east-1 \
--nodegroup-name mynodes \
--node-type t3.micro \
--nodes 2 \
--nodes-min 2 \
--nodes-max 2 \
--managed
```
# cluster-config.yaml
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: mycluster
  region: us-east-1

nodeGroups:
  - name: mynodes
    instanceType: t3.small
    desiredCapacity: 2
    minSize: 2
    maxSize: 2
    amiFamily: AmazonLinux2
    ssh:
      allow: true
```
```
eksctl create cluster -f cluster-config.yaml
```

**Note:** This will take several minutes. It creates:

* EKS control plane
* Managed node group
* Networking resources

## create eks manually 
```
EKS - manually 

1. search eks 
2. create cluster 
3. name cluster - mycluster 
4. create AmazonEKSAutoClusterRole Role 
5. create AmazonEKSAutoNodeRole Role 
6. Create node group - mynodegroup
7. min- 2, max- 2, desired - 2 | managed/spot | type- t3.micro
8. open cloud shell 

aws eks update-kubeconfig --region us-east-1 --name mycluster
kubectl get nodes
```
---

## ❌ Delete EKS Cluster

To delete the cluster:

```bash
eksctl delete cluster --name mycluster --region us-east-1
```

---

## 📚 Summary

| Task                       | Command / Action                                                                                      |
| :------------------------- | :---------------------------------------------------------------------------------------------------- |
| Create IAM User            | AWS Console → IAM → Users → Add User `atul`                                                           |
| Create Access Key          | AWS Console → IAM → Users → `atul` → Security credentials                                             |
| Install AWS CLI            | [AWS CLI v2 Installer](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |
| Configure AWS CLI          | `aws configure`                                                                                       |
| Install `eksctl` via Choco | `choco install eksctl`                                                                                |
| Create EKS Cluster         | `eksctl create cluster --name mycluster --region us-east-1`                                           |
| Delete EKS Cluster         | `eksctl delete cluster --name mycluster --region us-east-1`                                           |

---

## 👨‍💻 Author

**Atul Kamble**

- 💼 [LinkedIn](https://www.linkedin.com/in/atuljkamble)
- 🐙 [GitHub](https://github.com/atulkamble)
- 🐦 [X](https://x.com/Atul_Kamble)
- 📷 [Instagram](https://www.instagram.com/atuljkamble)
- 🌐 [Website](https://www.atulkamble.in)
