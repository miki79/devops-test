# Initial setup

## Requirement

- aws eb cli tool installed on the local machine https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html
- aws credentials setup on the local machine
- VPC with 3 public subnets in eu-west-1 region

## Create environment

In the file .elasticbeanstalk/saved_configs/nodeapp.cfg.yml replace:

- vpc-xxxxx: with vpcId where to deploy the loadbalancer and application
- subnet-xxxxx,subnet-yyyyy,subnet-zzzzz with 3 public subnets of vpcId specified above

Run the command `eb create [environment name] -c [subdomain-name] --cfg=nodeapp --elb-type=application`
This command is necessary to setup the basic environment to deploy the application

After created the environment you can access the application via loadbalancer at the url http://[subdomain-name].eu-west-1.elasticbeanstalk.com

## Configure CircleCI for auto-deployment

Setup following variables:

- ENVIRONMENT_NAME = [environment name] used during creation environment

Set AWS permissions in CircleCI with a user that has "AWSElasticBeanstalkService" policy attached to it

# Automatic deployment

Every time a new pull request is opened the application is tested and deployed to the environment http://[subdomain-name].eu-west-1.elasticbeanstalk.com
