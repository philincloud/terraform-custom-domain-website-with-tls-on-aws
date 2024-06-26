<h2>terraform-custom-domain-website-with-tls-on-aws</h2>

<h3>This Terraform module creates aws resources neccessery to deploy static website, spa or (after addtional  configuration) any client side rendered frontend.</h3> 

<p>Before applying any changes to your infrastructure, please customize data in following files:</p>

register_domain.json
/s3/admin_contact.json 
run.sh

<p>Terraform can only MANAGE a DNS domain that has been registered before but CAN NOT REGISTER it.<br>
Regarding that fact run.sh contains a AWS CLI command calling Route53 api to register custom domain.
WARNING!!!

If chosen domain is available it will be registered and BILLED automaticaly.<br> 
You can find list of new domains prices here: <br>https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf</p>


<p>List of resources created by module:

S3:
  -aws_s3_bucket
  -aws_s3_bucket__acl
  -aws_s3_bucket_cors_configuration
  -aws_s3_bucket_ownership_controls
  -aws_s3_bucket_policy
  -aws_s3_bucket_public_access_block
  -aws_s3_bucket_versioning
  -aws_s3_bucket_website_configuration
  -aws_s3_bucket_object
Route53:
  -aws_route53domains_registered_domain
  -aws_route53_hosted_zone    # imported from existing hosted_zone created by rout53 when domain is registered
  -aws_route53_record         # for TLS cert validation 
  -aws_route53_record         # for Cloudfront distribution  
ACM
  -aws_acm_certificate
  -aws_acm_certificate_validation
Cloudfront:
  -aws_acm_cloudfront_distribution
  -aws-acm_             
</p>