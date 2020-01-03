---
title: "Identity and Access Management"
weight: 1
# bookFlatSection: false
# bookToc: 6
# bookHidden: false
---
# Identity and Access Management

## IAM Essentials
__IAM__ controls access to AWS services via __policies__, that can be attached to users, groups and roles.

### ARN (Amazon Resource Name)
Each resource at _AWS_ has unique identifier named __ARN (Amazon Resource Name)__, which has following format

    arn:partition:service:region:account_id:[resource|resourecetype/resource|resourcetype/resource/qualifier|resourcetype/resource:qualifier|resourcetype:resource:qualifier]

partition = _aws_ or _aws-cn_
service = AWS service (s3, ec2, rds, dynamodb)
region = region code: us-east-1, us-west-2

[AWS ARN documentation](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)

Wildcards are supported
    `arn:aws:s3:::my_corporate_bucket/*`

### Credentials
1. Username/password - longterm credential which can be used to access console
1. Access keys - longterm credentials, which can be used with AWS CLI
3. Short term - used by roles

**NB:** By default IAM identity does not have permissions to do anything (_Deny_ by default)

## IAM policies
[IAM Policies AWS doc](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)

**IAM policy** is a document, which can be attached to Identity or Resource

**IAM Policy Document**

- Version
- Statement(s)
    - SID (id of policy)
    - Effect (Allow or Deny)
    - Action - list of Actions (wildcards are supported)
    - Resource - ARN
    - Conditions (?)

**Example**
   ```
   {
    "Version": "2012-10-17",
    "Statement": [
        {
        "Sid": "FirstStatement",
        "Effect": "Allow",
        "Action": ["iam:ChangePassword"],
        "Resource": "*"
        },
        {
        "Sid": "SecondStatement",
        "Effect": "Allow",
        "Action": "s3:ListAllMyBuckets",
        "Resource": "*"
        },
        {
        "Sid": "ThirdStatement",
        "Effect": "Allow",
        "Action": [
            "s3:List*",
            "s3:Get*"
        ],
        "Resource": [
            "arn:aws:s3:::confidential-data",
            "arn:aws:s3:::confidential-data/*"
        ],
        "Condition": {"Bool": {"aws:MultiFactorAuthPresent": "true"}}
        }
    ]
    }
```
### Types of IAM Policies
* **Inline** - attached directly to user/role/group
* **Managed**
    * __AWS Managed__
    * __Customer Managed__

### **NB** Exam Tips
* Implicit default Deny is applied by default
* Explicit Deny overrides anything
* All policies are merged during verification (user, group, role)

## IAM Users
[AWS IAM Users doc](https://docs.amazonaws.cn/en_us/IAM/latest/UserGuide/id_users.html)
**IAM Users** are type of IAM identity suitable for long-term access for known entity (human, service, app)


### Authentication
Principals authenticate to IAM with username/password or Access Keys
Iam user has ARN assigned. Also, user can have tags (like many other AWS resources)

### Limits
* **Hard Limit** - **5000** IAM susers per account
* IAM user can be member of up to 10 groups
* Inline policies size should not exceen 2048 character
* 1 MFA pper user
* 2 Access key

## IAM Groups
[AWS IAM groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html)
**IAM Group** is a collections of IAM users, which allow easier administration over users. Groups *can not* be principle in a policy, so they can't be used in Resource policy
Group can be associated with managed policy or can have inline policy.

### Exam Facts
* Groups are admin feature to group users
* User can be member of multiple groups (up to 10)
* Groups can not be referenced from from resource policies
* Groups have no credentials

## Access Keys
[AWS CREDENTIAL](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html)
* **Access Key Id** - public part of the key
* **Secret Access Key** private part
    * Can not be restored
    * Can not be changed
* There are two keys per user max
* User keys don't expire

## IAM Roles

[IAM ROLES AWS DOC](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)

IAM role can have two types of policies
* Trust Policy
* IAM Permission Policy

[STS (Simple token Service)](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html) creates temporary credentials when identity Assumes role

### Roles Example scenarios
* Emergency resource access for a person, who usually does not have that access
* For Service to perform action. Following services can do **sts:AssumeRole**:
    - IAM User
    - AWS Service
    - External Account
    - Web identities
* Cross-acount access
* Web Identity Federation