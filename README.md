# infrastructure

**Prerequisite:**
- aws-cli v2 install
- aws account of 'dev'&'prod' with respectively 3 IAM users?
- vscode 

1. To start configure, first check  by `aws ec2 describe-vpcs` and remove default AWS profile.
2. Configure keys of 'dev'&'prod' in `./aws/configure` 
3. in ZSH, set env variable by `export AWS_PROFILE=${current_account}` and `export AWS_REGION=us-east-1`

4. During create-vpc, `--dry-run` act like status check
5. `aws cloudformation create-stack --stack-name ${myvpc} --template-body file://vpc.yml --parameters ParameterKey=VpcCidrBlock,ParameterValue="10.1.1.0/24"`
6. After finish work with the infra, clear keys configured in ./aws/