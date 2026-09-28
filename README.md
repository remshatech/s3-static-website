# S3 Static Portfolio Website

Deploy a personal portfolio site with zero server maintenance, minimal ongoing cost, and a deployment process repeatable in under 5 minutes from any machine with AWS CLI configured.

## The Solution

Static HTML and CSS site hosted on AWS S3 using the static website hosting feature. No server, no backend, no framework.

## Live Site

http://remsha-portfolio-2026.s3-website-us-east-1.amazonaws.com

## Why S3 Static Hosting

No server to maintain — no EC2 to patch, scale, or pay for when idle. S3 is managed infrastructure.

Cost — effectively $0/month at personal portfolio traffic. S3 charges $0.023/GB storage and $0.0004 per 1,000 GET requests.

Deployment speed — two CLI commands to update the live site after initial setup. No build pipeline needed for static files.

Trade-off accepted — S3 website endpoints support HTTP only. HTTPS requires adding CloudFront with an ACM certificate. Planned as the next iteration.

## Architecture

Developer
    ↓
AWS CLI (aws s3 cp)
    ↓
S3 Bucket (public read bucket policy)
    ↓
S3 Static Website Endpoint (HTTP)
    ↓
Browser


## What This Demonstrates

- AWS S3 static website hosting configuration
- S3 bucket policy for public read access
- Disabling Block Public Access for a website bucket
- File deployment via AWS CLI

## Deployment Commands

1. Disable Block Public Access on this bucket only:

```
aws s3api put-public-access-block --bucket remsha-portfolio-2026 --public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false"
```

2. Enable website hosting:

```
aws s3 website s3://remsha-portfolio-2026/ --index-document index.html --error-document index.html
```

3. Attach a public read-only bucket policy (`file://` avoids PowerShell quoting problems):

```
aws s3api put-bucket-policy --bucket remsha-portfolio-2026 --policy file://bucket-policy.json
```

4. Upload the site files:

```
aws s3 cp index.html s3://remsha-portfolio-2026/
aws s3 cp style.css s3://remsha-portfolio-2026/
```

1. Set public access on the bucket using `aws s3api put-public-access-block` with all four block settings set to false.

2. Enable website hosting with `aws s3 website s3://remsha-portfolio-2026/` specifying `index.html` as both the index and error document.

3. Upload files with `aws s3 cp index.html s3://remsha-portfolio-2026/` and `aws s3 cp style.css s3://remsha-portfolio-2026/`.


## Tech Stack

AWS S3 · IAM bucket policy · HTML · CSS · AWS CLI

---


*September 2026*