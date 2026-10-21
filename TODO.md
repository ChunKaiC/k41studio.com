# TODO

Rough estimate: about 3 weeks at 2–3 hours a day.

## Setup

- [x] Wipe repo and document the architecture (`README.md`)
- [ ] Turn on MFA for the AWS root user
- [ ] Create an admin user in IAM Identity Center and stop using the root user
- [ ] Confirm the budget alert covers actual and forecasted spend
- [ ] Install AWS CLI, SAM CLI, Node.js and Angular CLI

## Week 1: Static site live

- [ ] Scaffold the Angular app with routing and five tabs (About Me, Experience, Contact, Hobbies, Aquarium)
- [ ] Build the four static pages and basic styling
- [ ] Create a private S3 bucket and a CloudFront distribution that reads it through Origin Access Control
- [ ] Deploy the site and check it at the `*.cloudfront.net` URL

## Week 2: Backend

- [ ] Write a SAM template with API Gateway (HTTP API) and the `listFish` and `createFish` Lambdas (TypeScript)
- [ ] Create the DynamoDB table and the private fish images bucket, with the default fish image uploaded
- [ ] `listFish`: scan all fish, following `LastEvaluatedKey` until every page is read
- [ ] `createFish`: write the fish with the default image key, upload the image to S3, then update the key
- [ ] `createFish`: size limit, check that the file is really an image, a timeout above 3 seconds, and the `cloudfront:CreateInvalidation` permission
- [ ] Test locally with `sam local start-api`

## Week 3: Aquarium and wiring

- [ ] Upload form with browser-side image compression
- [ ] Fish PNGs bouncing around the screen, with metadata on hover
- [ ] Angular dev proxy from `/api` to the local SAM API
- [ ] CloudFront behaviors: `/api/*` to API Gateway (POST not cached) and images bucket through OAC
- [ ] Invalidate the cached `GET /fish` after each upload
- [ ] `sam deploy` and an end-to-end test through CloudFront

## Domain

- [ ] Register a new domain through Route 53, with auto-renew on
- [ ] ACM certificate in us-east-1, validated through Route 53
- [ ] Attach the domain to CloudFront with alias records for the root domain and `www`

## Later (see Future work in `README.md`)

- [ ] Check image quality after compression
- [ ] Moderation with Rekognition
- [ ] Pagination and virtual scrolling
- [ ] WAF rules
- [ ] Fish modification and deletion (auth)
- [ ] CI/CD (GitHub Actions)
