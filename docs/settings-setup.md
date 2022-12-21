<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/reference-architecture/blob/master/docs/settings-setup.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# Settings Setup

[![Watch the video](https://img.boltops.com/boltopspro/video-preview/multiple/aws-profile-setup.png)](https://www.youtube.com/watch?v=G_rPzbILsgQ)

The BoltOps Pro blueprints support both single and multiple AWS account setups. The multiple AWS account approach has the benefit of complete isolation between development and production environments.  Learn More: [Lono Multiple vs Single Accounts Setups](https://lono.cloud/docs/extras/multiple-vs-single-aws-account/).

We'll show you how to configure things with an AWS multiple account strategy.

## ~/.aws configs

There are many ways to configure `~/.aws` for a multiple-account setup.  The AWS docs cover all the options: [Configuration and Credential Files](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html).

Here's a simple example that can be used for the BoltOps Pro reference architecture.

~/.aws/config:

    [profile main-account]
    output = json
    region = us-west-2

    [profile dev]
    output = json
    region = us-west-2

    [profile mgt]
    output = json
    region = us-west-2

    [profile prd]
    output = json
    region = us-west-2

~/.aws/credentials:

    # The main-account is the parent account. The child accounts belong to the main-account AWS organization.
    [main-account]
    aws_access_key_id = ZXBABCIAXCGZMIEXAMPLE
    aws_secret_access_key = ASDFu7hWIj3iHwFV90iOIrXCvj2uCASDCEXAMPLE

    [dev]
    role_arn = arn:aws:iam::111111111111:role/Admin
    source_profile = main-account

    [mgt]
    role_arn = arn:aws:iam::222222222222:role/Admin
    source_profile = main-account

    [prd]
    role_arn = arn:aws:iam::333333333333:role/Admin
    source_profile = main-account

In this setup, there is a main parent account.  The other AWS Named Profiles use the credentials from the main parent account to assume an `Admin` role the child AWS accounts.

## Lono configs/settings.yml

Lono has an [aws_profile settings](https://lono.cloud/docs/configuration/settings/) so you don’t forget to also set `AWS_PROFILE` (and AWS accounts) when switching between `LONO_ENV` values. Example:

configs/settings.yml:

```yaml
development:
  aws_profile: dev

management:
  aws_profile: mgt

production:
  aws_profile: prd
```

With this `settings.yml`, these commands will work the same:

    LONO_ENV=development lono cfn deploy BLUEPRINT # will use AWS_PROFILE=dev
    AWS_PROFILE=dev lono cfn deploy BLUEPRINT      # will use LONO_ENV=development

These commands will also work the same.

    LONO_ENV=production lono cfn deploy BLUEPRINT  # will use AWS_PROFILE=prd
    AWS_PROFILE=prd lono cfn deploy BLUEPRINT      # will use LONO_ENV=production

This prevents you from switching `AWS_PROFILE` or `LONO_ENV` and forgetting also to switch the other setting.

Many of the BoltOps Pro blueprints will take advantage of the `aws_profile` lono setting to deploy to different accounts.

If you're using a One AWS Account strategy, you can use a `configs/settings.yml` that looks like this: [settings-one.md](settings-one.md).

## Switch AWS Accounts with the AWS Console

Refer to the AWS Docs: [Switching to a Role (Console)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-console.html)
