# Network Load Balancer Ingress for Application Load Balancer fronted AWS Fargate service

Fully inspired by https://containersonaws.com/pattern/nlb-ingress-alb-load-balancer-fargate-service-cdk

### Pre-prequisites

- node (via `nvm use`)
- pnpm (via `corepack enable`)
- cdk (`brew install cdk`)
- awscli (`brew install awscli`)
- docker ?

### Get started

clone the repo

```bash
pnpm install

# TODO once per region: cdk bootstrap

npx cdk deploy \
 --all \
 --require-approval never --profile tsamaya

DNS_NAME=$(aws cloudformation describe-stacks --profile tsamaya --stack-name shared-resources --query "Stacks[0].Outputs[?OutputKey=='dns'].OutputValue" --output text) && echo $DNS_NAME

curl $DNS_NAME/

npx cdk destroy --all -f --profile tsamaya
```
