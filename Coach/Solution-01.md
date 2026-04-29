# Challenge 01 - Create a Linux Virtual Machine - Coach's Guide 

**[Home](./README.md)** - [Next Solution >](./Solution-02.md)

## Notes & Guidance

There are multiple paths to accomplish the creation of an Ubuntu 24.04 Linux environment. Below are examples for each option.

### Option 1: Azure

Using the Azure CLI from Cloud Shell:

- Create the resource group:

```bash
az group create --name rg-linux-fundamentals --location eastus
```

- Create the Virtual Machine

```bash
az vm create \
  --resource-group rg-linux-fundamentals \
  --name myVM \
  --image Canonical:ubuntu-24_04-lts:server:latest \
  --admin-username student \
  --generate-ssh-keys
```

- Connect to virtual machine

```bash
ssh student@[public-ip]
```

### Option 2: AWS

Using the AWS CLI:

```bash
aws ec2 run-instances \
  --image-id resolve:ssm:/aws/service/canonical/ubuntu/server/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id \
  --instance-type t3.micro \
  --key-name my-key-pair \
  --security-group-ids sg-xxxxxxxx \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=myVM}]'
```

Then connect via SSH:

```bash
ssh -i my-key-pair.pem student@[public-ip]
```

### Option 3: GCP

Using the gcloud CLI:

```bash
gcloud compute instances create myvm \
  --zone=us-central1-a \
  --machine-type=e2-micro \
  --image-family=ubuntu-2404-lts-amd64 \
  --image-project=ubuntu-os-cloud
```

Then connect via SSH:

```bash
gcloud compute ssh student@myvm --zone=us-central1-a
```

### Option 4: Local VM

Download the Ubuntu 24.04 LTS ISO from [ubuntu.com/download](https://ubuntu.com/download) and create a VM using VirtualBox, UTM (macOS), Hyper-V, or VMware. During installation, set the username to **student**.

### Option 5: WSL2

On a Windows machine, open PowerShell as Administrator and run:

```powershell
wsl --install -d Ubuntu-24.04
```

Follow the prompts to create a **student** user.

