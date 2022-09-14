# Takomo Demo

This project demonstrates multi-account deployment with Takomo Deployment Targets.

To make the setup easier, only one AWS account is needed.

# Getting started

## Install dependencies

Go to project root dir and run:

```
npm install
```

Verify installation:

```
npx tkm --version
```

You should see Takomo version information.

## Configure AWS credentials

Go to your test AWS account and create an IAM user with admin permissions. Create access keys for the user.

Store the access keys to file `~/.aws/credentials` like so:

```
[takomo]
aws_access_key_id=XXXXXXX
aws_secret_access_key=YYYYYY
```

## Configure Test account id

Modify `my-variables.yml` file and set there id of your test AWS account.

# Deploy core infrastructure

Change to core-accounts dir and run:

```
npx tkm stacks deploy --profile takomo
```

This will deploy a Transit Gateway.

# Deploy standard accounts

Change to standard-accounts dir and run:

```
npx tkm targets deploy --profile takomo
```

This deploys VPCs and attaches them to the Transit Gateway.

# Remove all deployed configuration

To remove all configuration from standard accounts change to standard-accounts dir and run:

```
npx tkm targets undeploy --profile takomo
```

Then, remove the TGW stack by changing to core-accounts dir and running:

```
npx tkm stacks undeploy --profile takomo
```

# Standard accounts configuration

Standard accounts are found from `standard-accounts/accounts` dir. The directory hierarchy should match with the AWS organization's organizational units hierarchy. Each `.yml` file in the hierarchy represents an AWS account.

Deployment configuration is specified in `standard-accounts/deployment/targets.yml` file.

Configuration is explained in documentation https://takomo.io/targets/intro

# Command line usage 

Deploy all targets:

```
npx tkm targets deploy --profile takomo
```

Deploy just one target:

```
npx tkm targets deploy --target example-dev --profile takomo
```

Skip review step:

```
npx tkm targets deploy --profile takomo --yes
```

Deploy targets in a specific deployment group:

```
npx tkm targets deploy Workload/Test --profile takomo 
```

More options ava is explained in documentation https://takomo.io/targets/intro

