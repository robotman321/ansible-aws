# Ansible Playbooks Repo

The following are a collection of playbooks for ansible.

The initial design was meant to work on AWS assets through the use of built-in functions.

## AWS S3 Bucket management

The roles enclosed, aws_s3 and aws_iam are basic playbooks that allow the user to manage policies and s3 buckets. By design the script assumes that no users need to be setup, that the users will already be in their groups and all that is changing are the policy assignments.

Further development will be done to manage users, groups and further bucket management will be broken out.

Also note, if the bucket maintains a lifecycle rule(s), the playbook will maintain them as well.

The aws s3 bucket management will utilize both IAM policies and S3 Policies. This ends up being so that broad support will go into the s3 bucket policies (think of it as a base) and the IAM specific policies can go into the iam policies.

Yes, I agree this adds some complexity, but IAM policies don't need any fancy root account numbers to associate with s3 buckets. Whereas s3 bucket assignment needs to use the root account number. Technically, this is not the end of the world, but in a "Keep It Simple Stupid" world, this (to me) appears to be unneeded.

## Installation/Requirements

With a default ansible install you will also need to install awscli, boto and boto3.

```
pip3 install awscli boto boto3
```

Ansible should also be on the latest version, due to community nature of the aws plugins, utilizing the latest version of ansible ensures that no bug rear their heads. The playbooks have been tested and confirmed working on version 2.9.11.

## Usage

Before running the playbooks, ensure that your aws_access_key and aws_secret_keys are encypted and updated in aws.yaml.

Select an encryption key and build the vault data using the following commands.

```
# ansible-vault encrypt_string 'ACCESS_KEY' --ask-vault-pass
# ansible-vault encrypt_string 'aws_secret_keys' --ask-vault-pass
```

Update the values stored in aws.yaml, then proceed with running the playbooks.

```
# ansible-playbook aws.yaml --ask-vault-pass
```