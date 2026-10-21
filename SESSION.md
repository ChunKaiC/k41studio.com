# Session Log

Newest first. Only the latest entry is loaded as context for the next session (see `CLAUDE.md`).

## 2026-10-21

- Wiped the old Flutter project from the repo and restarted it as a portfolio site for learning Angular and AWS.
- Designed the architecture in `README.md`. The user drove the design and Claude challenged it.
  - First design: Spring Boot on two EC2 instances behind an ELB in a VPC. Later replaced with TypeScript Lambdas behind API Gateway (HTTP API), no VPC, deployed with AWS SAM.
  - CloudFront is the single entry point. The S3 buckets for the site and images are private and readable only by CloudFront. The Angular app calls `/api/*` through relative paths.
  - Upload flow: the browser compresses the image, then `createFish` writes the fish to DynamoDB with the default image key, uploads the image to S3, and updates the key.
  - `GET /fish` returns all fish for now. Pagination, moderation (Rekognition), WAF, image-quality checks and fish deletion are listed under Future work.
- The old domain `chunkaichen.com` expired and was re-registered by someone else. Registered `k41studio.com` through Route 53 instead, and renamed the GitHub repo to `ChunKaiC/k41studio.com`.
- AWS account upgraded to a paid plan, with $100 in credits and a $20 budget. Estimated cost of the Lambda design: about $1/month.
- Created `TODO.md` (deliverables), `SESSION.md` (this log) and `CLAUDE.md` (session-loading rule).
