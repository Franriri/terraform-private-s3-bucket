# Terraform: Private S3 Bucket

My first Infrastructure as Code (IaC) project. It uses **Terraform** to create a private **Amazon S3 bucket** with **Block Public Access** enabled in AWS (Sydney, `ap-southeast-2`).

This is the code version of a setup I first built by hand in the AWS console. See my companion project: **aws-s3-cloudfront-static-site**.

## What it creates

| Resource | Purpose |
|---|---|
| `aws_s3_bucket.demo` | An S3 bucket named `fran-terraform-demo-2026` |
| `aws_s3_bucket_public_access_block.demo` | Turns on all four Block Public Access settings for that bucket |

## Files

| File | Purpose |
|---|---|
| `main.tf` | The Terraform code |
| `.terraform.lock.hcl` | Locks the AWS provider version (6.71.0) so every run uses the same one |

The state file (`terraform.tfstate`) is intentionally **not** in this repository, because state files can contain sensitive details.

## How to run it

I ran this in **AWS CloudShell**, which signs in with my console session, so no access keys were needed.

```bash
terraform init     # download the AWS provider
terraform plan     # preview the changes (creates nothing)
terraform apply    # create the resources after typing "yes"
```

Bucket names are globally unique, so change `bucket` in `main.tf` if the name is already taken.

## Results

- `terraform plan` showed **2 to add, 0 to change, 0 to destroy**.
- `terraform apply` finished with **Apply complete! Resources: 2 added**.
- In the S3 console, the bucket existed in Sydney and **Block all public access** was **On**.

## Clean up

```bash
terraform destroy  # removes everything this code created
```

## What I learned

- The difference between a **provider**, a **resource**, and the **state file**.
- Why `plan` comes before `apply`: review first, then build.
- Why the provider lock file is committed but the state file is not.
- CloudShell keeps files in the home folder, but the Terraform program itself may need to be reinstalled after a session resets.

## Next steps

- [ ] Add Terraform code for the CloudFront distribution and bucket policy from my website project
- [ ] Add a GitHub Actions workflow to check the code automatically
- [ ] Practice remote state storage

---

*Built by Fran. README drafted with help from Claude.*
