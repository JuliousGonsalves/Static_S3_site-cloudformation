# Static S3 Bucket Website using Cloudfront for CDN  

## Description

The CloudFront network has 169 points of presence (PoPs), and leverages the highly-resilient Amazon backbone network for superior performance and availability for your end users.
In a way cloudfront is a CDN network.

![image](https://user-images.githubusercontent.com/98936958/167264143-fc041016-0a96-448d-ace1-cb7706b4fe3b.PNG)


Here we are going to host a simple html site in a s3 Bucket static hosting with cloudfront and ACM SSL.  

### Download html website from tooplate.com
~~~sh
https://www.tooplate.com/zip-templates/2121_wave_cafe.zip 
~~~
### Create a static site in S3 bucket

#### 1. Create s3 bucket and upload website files to it.

![objectss3](https://user-images.githubusercontent.com/98936958/159854614-c877af72-635e-4afb-97ed-74a26414b47b.PNG)

#### 2. Go to "properties" of s3 bucket and enable "Static website hosting"

![staticwebsitesettings](https://user-images.githubusercontent.com/98936958/159854629-499b7d7a-74b1-44d4-99b9-dcd8e4b7acf6.PNG)

#### 3. Go to "permissions" and Edit Block public access (bucket settings)

![publicaccess](https://user-images.githubusercontent.com/98936958/159854619-8e5677bd-143f-4597-9cf3-33977f41643b.PNG)

### Create Cloudfront distribution

#### 1. Origin domain - 
you will be able to see S3 static site in drop down, select it.

![origindomain](https://user-images.githubusercontent.com/98936958/159854616-baf92522-5490-4cd4-8cdb-4cd9e1525b8b.PNG)

#### 2. S3 bucket access - 
- select "Yes use OAI (bucket can restrict access to only CloudFront)"
- create new OAI and select "Yes, update the bucket policy" in bucket policy
Note : This will automatically update bucket policy (refer the image under "Go to "permissions" and Edit Block public access (bucket settings)")

![OAI](https://user-images.githubusercontent.com/98936958/159854612-d27a2ad3-34f9-4d4b-85b9-25a7d03ace85.PNG)

#### 3. Default cache behavior - 
You can set "Viewer" protocol policy (HTTP and HTTPS / Redirect HTTP to HTTPS / HTTPS only). Here I choose Redirect HTTP to HTTPS.

#### 4. Alternate domain name (CNAME) - 
Under settings, I have added CNAME.

![Cnam](https://user-images.githubusercontent.com/98936958/159854603-53ce93dc-40a6-40e5-99ae-097517afa6f8.PNG)

#### 5. SSL Certificate - 
Under settings, You can add a custom SSL certificat. Here I have added a ACM certificate. 

![ACM](https://user-images.githubusercontent.com/98936958/159854599-15b80783-cee2-4d97-8348-80fe8c4b1db3.PNG)

#### 6. Default root object - 
I have added it as "index.html"

![rootobject](https://user-images.githubusercontent.com/98936958/159854620-7ca64818-f20c-46e0-ac3d-efd0f45d1871.PNG)

### Cloudfront Distribution Listing

![cloudfrontdistribution](https://user-images.githubusercontent.com/98936958/159854601-74c8e068-9f4d-4dd8-8898-18efa00b33b8.PNG)

### DNS Update - Route 53

I have hosted my domain DNS zone in Route53. Add an alias for your domain name to "Distribution domain name". You can obtain you cloudfront name from general details fo your cloudfront distribution. 

![route53](https://user-images.githubusercontent.com/98936958/159854624-95bba6b6-fb41-4427-9317-477291fa58f8.PNG)

### Conclusion

When someone load the website for the firt time , The Cloudfront will cache the website in edge locations so that the next time the site will be loaded faster.

##### You can see the X cache as Miss when we curl the website url for first time

![Curlfirst](https://user-images.githubusercontent.com/98936958/159854604-51691059-9ec5-4ffd-ac45-36b161efe07c.PNG)

##### The second time, You can see it as Hit from cloudfront. ie, Its a  cached result.

![curlsecond](https://user-images.githubusercontent.com/98936958/159854607-3811cafd-8b1c-49ef-b573-9a441e24caae.PNG)

##### The Website preview Image

![website](https://user-images.githubusercontent.com/98936958/159854631-85ab4eb9-5c6c-4484-9fff-135b49bedf84.PNG)

