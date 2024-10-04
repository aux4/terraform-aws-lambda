# terraform-aws-lambda

AWS Lambda Terraform Module

## Usage

### Terraform

terraform/main.tf

```hcl
module "lambda" {
  source = "git@github.com:aux4/terraform-aws-lambda.git?ref=main"

  env = var.env

  file = "HelloWorld"
  environment_variables = {
    EXAMPLE_TABLE_NAME = data.aws_dynamodb_table.example.name
  }

  policies = [
    data.aws_iam_policy.lambda_logging_policy.arn,
    data.aws_iam_policy.table_example_get_policy.arn
  ]
}
```

### Code

src/function/HelloWorld.js

```js
export async function handler(event) {
  return {
    statusCode: 200,
    body: JSON.stringify({
      message: "Hello World!"
    }),
  };
}
```

### Build

```bash
mkdir -p dist
zip -r dist/api.zip src node_modules package.json package-lock.json
```
