---
description: Notes/Links to working with AWS
---

# AWS

## CLI Snippets


Create a stack

```sh
aws cloudformation create-stack --stack-name NAME --template-body file://home/testuser/mytemplate.json
```

Assume a role and export envrinment variables

```sh
# From: https://gitlab.com/gitlab-examples/aws-sam/-/blob/master/assume-role.sh

REGION=$1
TAG=$2
ROLE=$3

echo "===== checking for tag and presence in master branch ====="
([ -z $TAG ] || (git branch -r --contains `git rev-list -n 1 $TAG` | grep master))
echo "===== assuming permissions => $ROLE ====="
KST=(`aws sts assume-role --role-arn $ROLE --role-session-name "deployment-$TAG" --query '[Credentials.AccessKeyId,Credentials.SecretAccessKey,Credentials.SessionToken]' --output text`)
unset AWS_SECURITY_TOKEN
export AWS_DEFAULT_REGION=$REGION
export AWS_ACCESS_KEY_ID=${KST[0]}
export AWS_SECRET_ACCESS_KEY=${KST[1]}
export AWS_SESSION_TOKEN=${KST[2]}
export AWS_SECURITY_TOKEN=${KST[2]}
```

or

```sh
export $(printf "AWS_ACCESS_KEY_ID=%s AWS_SECRET_ACCESS_KEY=%s AWS_SESSION_TOKEN=%s"
        $(aws sts assume-role
        --role-arn "$CI_SERVICE_ROLE"
        --role-session-name DevOpsAccountDeploy
        --query "Credentials.[AccessKeyId,SecretAccessKey,SessionToken]"
        --output text))
```

## Localstack

[Localstack]()

[Using the AWS cli with localstack](https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line)

TLDR: Use the `--endpoint` flag to route aws cli to the local stack you want to use. e.g

```bash
$> aws --endpoint-url=http://localhost:4576 sqs create-queue --queue-name test_queue
```

## Resource Types

### Security Groups

- Virtual firewall, attached to ec2 instances
- Can only specify allow rules, not deny
- Inbound and Outbound are seperate
- Can filter based on protocols, ports/cidrs


