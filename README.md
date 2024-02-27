# Network Load Balancer Ingress for Application Load Balancer fronted AWS Fargate service

Fully inspired by https://containersonaws.com/pattern/nlb-ingress-alb-load-balancer-fargate-service-cdk

### Pre-prequisites

- node (via `nvm use`)
- pnpm (via `corepack enable`)
- awscli (`brew install awscli`)
- docker ?

:warning: on MacOS Silicon, docker will build for an ARM and not AMD, then the service will never start properly

### AWS creds

create an AWS account obviously

configure creds, replacing the profile with your chosen profile name

```bash
aws configure --profile tsamaya
```

### Get started

clone the repo

```bash
pnpm install

# TODO once per account, per region: cdk bootstrap
npx cdk bootstrap aws://ACCOUNT-NUMBER-1/REGION-1 --profile tsamaya

npx cdk deploy \
 --all \
 --require-approval never --profile tsamaya

DNS_NAME=$(aws cloudformation describe-stacks --profile tsamaya --stack-name shared-resources --query "Stacks[0].Outputs[?OutputKey=='dns'].OutputValue" --output text) && echo $DNS_NAME

curl $DNS_NAME/
```

### cleanup

```bash
npx cdk destroy --all -f --profile tsamaya
```
