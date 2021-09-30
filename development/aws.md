---
description: Notes/Links to working with AWS
---

# AWS

## CLI Snippets


Create a stack

```sh
aws cloudformation create-stack --stack-name NAME --template-body file://home/testuser/mytemplate.json
```

## Localstack

[Localstack]()

[Using the AWS cli with localstack](https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line)

TLDR: Use the `--endpoint` flag to route aws cli to the local stack you want to use. e.g

```bash
$> aws --endpoint-url=http://localhost:4576 sqs create-queue --queue-name test_queue
```

