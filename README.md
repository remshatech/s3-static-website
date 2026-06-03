# S3 Static Portfolio Website

A personal portfolio website built with HTML and CSS, deployed and hosted on AWS S3 using static website hosting.

## Live Site

http://remsha-portfolio-2026.s3-website-us-east-1.amazonaws.com

## Architecture

Browser → S3 Website Endpoint → index.html + style.css

No server. No backend. AWS S3 serves the files directly.

## What This Demonstrates

- AWS S3 static website hosting configuration
- S3 bucket policy for public read access
- Disabling Block Public Access for a website bucket
- File deployment via AWS CLI

## Deployment Commands

1. Set public access on the bucket using `aws s3api put-public-access-block` with all four block settings set to false.

2. Enable website hosting with `aws s3 website s3://remsha-portfolio-2026/` specifying `index.html` as both the index and error document.

3. Upload files with `aws s3 cp index.html s3://remsha-portfolio-2026/` and `aws s3 cp style.css s3://remsha-portfolio-2026/`.

## Tech Stack

AWS S3 · HTML · CSS · AWS CLI

---

*Project 1 of 4 — 30-day cloud engineering portfolio · May 2026*