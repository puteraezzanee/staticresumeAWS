AWS S3 upload

1. Create an S3 bucket with a globally unique name.
2. In the bucket Properties tab, enable Static website hosting and set the index document to index.html.
3. Upload index.html from this folder.
4. Make the site publicly readable only if you intend this resume to be public refer below. Otherwise, use CloudFront with restricted access.

To host it directly from the S3 website endpoint, would need a bucket policy allowing public read access to the site files. Also need to turn off Block all public access for that specific bucket.
Replace YOUR-BUCKET-NAME with your bucket name:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadWebsiteFiles",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}


To use cloudfront, create a new Cloudfront distribution.
Keep Block all public access ON.
Don’t use the S3 “Static website hosting” endpoint.
Create a CloudFront distribution:Origin: select your S3 bucket
Origin access: Origin access control (OAC) → create one
Default root object: index.html

This site is self-contained: it does not need a server, build process, or external files.
