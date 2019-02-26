# Content Delivery Network <small>- AWS</small>

## S3 Bucket

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/VQztyuW6X24?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

!!! info "S3"

    S3 is a service that enables users to load your website’s media faster.

**S3 bucket creation**

:    * Go on your AWS management console, search for the service *S3* and click on it.
:    * Now that you are in the S3 interface, click on {==Create bucket==}.
:    * Name your bucket and choose the same region that you choose for your Lightsail instance.
:    * Click on {==Next==}.
:    * Leave the option by default and click on {==Next==}.
:    * Uncheck all the boxes so your bucket becomes public.
:    * Click on {==Next==}.
:    * Check that everything is good and click on {==Create bucket==}.

!!! success "A storage S3 public bucket is now available! It will enable faster loading of your media on Wordpress."

***

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/R1d245Z0Z0k?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**S3 bucket permissions**

:    * Click on your S3 bucket, then click on {==Permissions==}.
:    * Click on {==Bucket Policy==}.
:    * Copy / paste the following policy on the editor : 
``` sh
{
 "Version": "2008-10-17",
 "Statement": [
 {
  "Sid": "AllowPublicRead",
  "Effect": "Allow",
  "Principal": {
   "AWS": "*"
  },
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::YourBucketName/*"
 }
 ]
}
```

:    * Don't forget to switch *YourBucketName* with the name you gave your bucket.
:    * Once the policy edited, click on {==Save==}.

***

## IAM Policy

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/0hcbrfL1JCU?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**IAM policy initialization**

:    * Go back to the Management Console by clicking on the AWS top left logo.
:    * Search for the IAM service and click on the result.
:    * In the left menu, click on {==Policies==}.
:    * Click on {==Create policy==}.
:    * To access the online editor, click on the {==JSON==} menu.
:    * Once in the editor, delete the existing content and copy / paste the IAM policy below:
``` sh
{
 "Version": "2012-10-17",
 "Statement": [
 {
  "Effect": "Allow",
  "Action": [
   "s3:CreateBucket",
   "s3:DeleteObject",
   "s3:Put*",
   "s3:Get*",
   "s3:List*"
  ],
  "Resource": [
   "arn:aws:s3:::YourBucketName",
   "arn:aws:s3:::YourBucketName/*"
  ]
 }
 ]
}
```

:    * Don't forget to replace two times *YourBucketName* by the name you chose for your bucket.
:    * Click on {==Review policy==}.
:    * Name the IAM policy.
:    * Click on {==Create policy==}.

!!! success "The IAM policy is now ready to be used for your future IAM user."

***

## IAM User

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/eC6ZIXPpCeI?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**IAM policy and IAM user linking**

:    * In the left menu, click on {==Users==}.
:    * Click on {==Add user==}.
:    * Choose a name for your IAM user.
:    * Check the *Programmatic access* box.
:    * Click on {==Next: Permissions==}.
:    * Click on *Attach existing policies*.
:    * Type your IAM policy name in the search bar.
:    * Check the box to select your IAM policy and click on {==Next: Tags==}.
:    * Click on {==Next: Review==}.
:    * Click on {==Create user==}.
:    * To keep your access in a separate file, click on {==Download .csv==}.

!!! warning "Keep this window open for the next step and don't forget to copy/paste and save your Access key ID and Secret access key in a secure place."

!!! success "Congratulations! Your IAM user is now liked to the right IAM policy and you have the two access keys."

***

## IAM key injection

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/_mJp7YdtVEk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**IAM access key injection in Wordpress**

:    * Go to your Runcloud.io homepage
:    * On the left menu, click on *Web Applications* and click on your Wordpress application.
:    * Click on {==File Manager==} in the left menu.
:    * Select the *wp-config.php* file, then click on the {==View/Edit==} menu.
:    * Once in the editor, copy/paste the command below after `define('WP_DEBUG', false);` : 
``` sh
define( 'AS3CF_SETTINGS', serialize( array(
    'provider' => 'aws',
    'access-key-id' => 'YourAccessKeyID',
    'secret-access-key' => 'YourAccessKeySecret',
) ) );
```

:    * Then go to your IAM interface so you can replace *YourAccessKeyID* with your access key ID and *YourAccessKeySecret* with your secret access key.

:    * Type <kbd>Ctrl</kbd> + <kbd>S</kbd> to save your changes.

***

## Certificate Manager

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/PK7f-W6ZzCU?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**AWS Certificate creation**

:    * Go back to the Management Console by clicking on the AWS top left logo.
:    * On the top right corner, select *US East (N. Virginia)* location. (I)
:    * Search for the AWS service *Certificate Manager* and click on it.
:    * In the left section *Provision certificates*, click on {==Get started==}.
:    * Check the *Request a public certificate* box and click on {==Request a certificate==}.
:    * Enter your domain name this way : `*.exemple.com` and click on {==Next==}.
:    * Check the *DNS validation* box and click on {==Review==}.
:    * Make sure the information on the screen are correct and click on {==Confirm and request==}.

***

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/CM8FkHJJoOI?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**Domain name DNS validation**

:    * Wait for a moment, AWS is going to generate a DNS CNAME configuration. It will enable you to verify your domain name.
:    * Copy the beginning of the CNAME like so : `_55deac851379bd6906fd5f90ed2e95b3`
:    * Go to your Amazon Lightsail interface. Click on {==Networking==} then on your DNS zone.
:    * Click on {==Add record==}.
:    * Select *CNAME* as a record type. Paste the beginning of the CNAME you copied on the *Subdomain* field. Then copy the *Value* you can find on the *AWS Certificate Manager* page and paste it in the *Maps to* field.
:    * Click on the green button to save.
:    * Go back to the *AWS Certificate Manager*, click on {==Continue==} and wait while your domain name gets validated.

!!! success "Congratulations, you now have generated an AWS certificate for your domain name."

***

## Cloudfront

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/5atjyQXHVJw?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**Content Delivery Network Creation**

:    * Go back to the homepage by clicking on the top left AWS logo.
:    * Search the AWS service *Cloudfront* and click on it.
:    * Click on {==Create distribution==}.
:    * In the *Web* section, click on {==Get started==}.
:    * For the *Origin domain name* filed, select your S3 bucket.
:    * In *Alternate domain name (CNAMEs)*, write this: `cdn1.example.com`. Replace *example.com* with your domain name.
:    * Check the *Custom SSL Certificate (example.com)* box.
:    * Select the ACM certificate matching your domain name.
:    * Click on {==Create distribution==}.

***

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/j10DD5tqosw?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**CNAME Cloudfront and Amazon Lightsail Mapping**

:    * Click on the Cloudfront distribution ID.
:    * Copy *Domain name* content.
:    * Go back to the Lightsail interface, in the Networking section then in your domain name's DNS zone.
:    * Add a record and choose *CNAME record* on the first field. For the *subdomain* field type `cdn1` and for the *Maps to* field paste the content you just copied. Then save.

***

## WP Offload Media

<iframe width="100%" height="405" src="https://www.youtube-nocookie.com/embed/jbT2s1piWME?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture setPlaybackQuality(hd1080);" allowfullscreen></iframe>

***

**WP Offload Media plugin installation**

:    * Go to your Wordpress administration homepage.
:    * Click on {==Plugin > Add New==} on the left menu.
:    * Type *Amazon S3* on the search bar.
:    * Install and activate the *WP Offload Media Lite for Amazon S3* plugin.
:    * In the *Installed Plugins* menu, delete the by default applications.
:    * In the plugins menu, click on *Settings*.
:    * Once there, put your S3 bucket name in the field and click on *Save Bucket Setting*.
:    * In the *URL REWRITING* tab, enable the *Custom Domain (CNAME)* option and put `cdn1.example.com`. Replace `example.com` by your domain name.
:    * Enable *Force HTTPS* option.
:    * Click on *Save changes*.

!!! success "Congratulations, you have correctly set your CDN Amazon Cloudfront for your Wordpress website!"

***