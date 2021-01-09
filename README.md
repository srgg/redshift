# Creating a basic Redshift Cluster

## Prerequisites 

### Install and configure AWS Command Line Interface

[AWS Command Line Interface](https://aws.amazon.com/cli/) is used by 
[terraform aws provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) 
to interact with the many resources supported by AWS.

Install:
```
brew install awscli
```

Configure:
```
aws configure
```

### Create terraform user 
This user will be used by terraform to create a Redshift cluster.

Create user:
```
aws iam create-user --user-name 'terraform-user'
```

Grant access (attach required policies) to the user:
```
aws iam attach-user-policy \\
    --user-name 'terraform-user' \\ 
    --policy-arn 'arn:aws:iam::aws:policy/IAMFullAccess'
    
aws iam attach-user-policy \\
    --user-name 'terraform-user' \\
    --policy-arn 'arn:aws:iam::aws:policy/AmazonRedshiftFullAccess'
    
aws iam attach-user-policy \\
    --user-name 'terraform-user' \\
    --policy-arn 'arn:aws:iam::aws:policy/AmazonVPCFullAccess'
```

Create access key and copy returned *AccessKeyId* and *SecretAccessKey* to use on next step:
```
aws iam create-access-key --user-name 'terraform-user'
```

Modify [AWS credentials file](https://docs.aws.amazon.com/sdk-for-php/v3/developer-guide/guide_credentials_profiles.html)
(`~/.aws/credentials`) by adding the following section:

```
[redshift-cluster]
aws_access_key_id = <AccessKeyId>
aws_secret_access_key = <SecretAccessKey>
```


### Install terraform

```
brew install terraform
```


## Provision

```
terraform init
```

```
terraform plan
```
```
terraform apply
```

## Decommission 
```
terraform destroy
```
