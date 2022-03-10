# infrastructure

**Prerequisite:**
- aws-cli v2 install
- aws under 'dev'&'prod' account with programmatic access 'dev&demo' IAM-users(access-key-Id pairs) is ready  [In later VM process, use IAM role rather than the credential]
- vscode 

- Create key-pair for OpenSSH only with .pem
  1. create new .pem key from AWS
  2. extract public key from pem file `ssh-keygen -y -f private_key1.pem > public_key1.pub` 


## Building and Deploy Instructions
1. To start configure, first check  by `aws ec2 describe-vpcs` and remove default AWS profile.
2. Configure keys of 'dev'&'prod' in `./aws/configure` 
3. in ZSH, set env variable by `export AWS_PROFILE=${current_account}` and `export AWS_REGION=us-east-1`
4. Validate template syntax by `aws cloudformation validate-template --template-body file://csye6225-infra.yml`

**Demo5**
`aws cloudformation create-stack --stack-name demo-ec2 --template-body file://csye6225-infra.yml --parameters ParameterKey=EnvironmentName,ParameterValue="prod"`

**Demo4**
1. Create Stack and EC2 instance `aws cloudformation create-stack --stack-name demo-ec2 --template-body file://csye6225-infra.yml --parameters ParameterKey=CustomAMI,ParameterValue="${ami-id}"`
   

**Demo3**
1. cd into repo of infrastructure, run `aws cloudformation create-stack --stack-name ${myvpc} --template-body file://csye6225-infra.yml --parameters ParameterKey=VpcCidrBlock,ParameterValue="10.1.1.0/24"` 
   Name stack-name as 'csye6225-dev' or 'csye6225-prod' 
    Update by `aws cloudformation update-stack ...`
2. If switch to 'us-east-2' region, `--parameters ParameterKey=Subnet1AZ,ParameterValue="us-east-2a" ParameterKey=Subnet2AZ,ParameterValue="us-east-2b" ParameterKey=Subnet3AZ,ParameterValue="us-east-2c"`
3. To clear the whole stack, `aws cloudformation delete-stack --stack-name <name>`
4. After finish work with the infra, clear keys configured in ./aws/
   