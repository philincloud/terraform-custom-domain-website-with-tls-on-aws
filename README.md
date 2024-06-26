# terraform-custom-domain-website-with-tls-on-aws

## This module creates aws resources to deploy static website, spa or (after addtional  configuration) any client side rendered frontend.


To use this module you need aws account, Terraform and AWS CLI installed end configured.

Before applying any changes to your infrastructure, please customize data in following files:

*register_domain.json*<br>
*/s3/admin_contact.json*<br>
*run.sh*

Terraform can only MANAGE a DNS DOMAIN that has been registered before but CAN NOT REGISTER it.<br>
Regarding that fact run.sh contains a AWS CLI command calling Route53 api to register custom domain.<br>

### WARNING!!!

### If chosen domain is available it will be registered and BILLED automaticaly.

Some TLD names are really expensive!

You can find list of new domains prices here: <br>https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf</p>


### List of resources created by module:

#### S3:
  - aws_s3_bucket          (as static file server)
  - aws_s3_bucket__acl
  - aws_s3_bucket_cors_configuration 
  - aws_s3_bucket_ownership_controls
  - aws_s3_bucket_policy
  - aws_s3_bucket_public_access_block
  - aws_s3_bucket_versioning
  - aws_s3_bucket_website_configuration
  - aws_s3_bucket_object
  
#### Route53:
  - aws_route53domains_registered_domain
  - aws_route53_hosted_zone (imported from existing hosted_zone created by rout53 when domain is registered)
  - aws_route53_record      (for TLS cert validation) 
  - aws_route53_record      (for Cloudfront distribution) 
   
#### ACM
  - aws_acm_certificate
  - aws_acm_certificate_validation

#### Cloudfront:
  - aws_acm_cloudfront_distribution
  - aws-acm_             

___

### Register domain with aws 

According to [AWS docs][1]

> *The following register-domain command registers a domain, retrieving all parameter values from a  
> JSON-formatted file.*
>
> *This command runs only in the us-east-1 Region. If your default region is set to us-east-1, you can omit 
> the region parameter.*
>
> ```bash
>      aws route53domains register-domain \
>         --region us-east-1 \
>         --cli-input-json file://register-domain.json
> ```




[1]: https://docs.aws.amazon.com/cli/latest/reference/route53domains/register-domain.html
