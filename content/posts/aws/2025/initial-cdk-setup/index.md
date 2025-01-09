---
title: "Initial Cdk Setup"
date: 2025-01-05T10:15:24-08:00
menu:
  sidebar:
    name: "Initial Cdk Setup"
    identifier: "initial-cdk-setup"
    parent: AWS-2025
    weight: 10
tags: ["aws", "certification", "cdk"]
categories: ["aws"]
draft: false
---
### Installing CDK

[Installing CDK](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html) is pretty simple:
```bash
$ sudo npm install -g aws-cdk
[sudo] password for iwidlinski: 
added 1 package in 2s
```

It worked:
```bash
$ cdk --version
2.174.0 (build 9604329)
```

### Bootstrap CDK

We can now bootstrap the account:
```bash
 $ cdk bootstrap aws://047719662517/us-west-2 --cloudformation-execution-policies arn:aws:iam::aws:policy/AdministratorAccess
 ⏳  Bootstrapping environment aws://047719662517/us-west-2...
Trusted accounts for deployment: (none)
Trusted accounts for lookup: (none)
Execution policies: arn:aws:iam::aws:policy/AdministratorAccess
CDKToolkit: creating CloudFormation changeset...
CDKToolkit |  0/12 | 12:35:13 PM | REVIEW_IN_PROGRESS   | AWS::CloudFormation::Stack | CDKToolkit User Initiated
CDKToolkit |  0/12 | 12:35:19 PM | CREATE_IN_PROGRESS   | AWS::CloudFormation::Stack | CDKToolkit User Initiated
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | LookupRole 
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | CloudFormationExecutionRole 
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::ECR::Repository    | ContainerAssetsRepository 
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::SSM::Parameter     | CdkBootstrapVersion 
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | FilePublishingRole 
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | ImagePublishingRole 
CDKToolkit |  0/12 | 12:35:21 PM | CREATE_IN_PROGRESS   | AWS::S3::Bucket         | StagingBucket 
CDKToolkit |  0/12 | 12:35:22 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | ImagePublishingRole Resource creation Initiated
CDKToolkit |  0/12 | 12:35:22 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | LookupRole Resource creation Initiated
CDKToolkit |  0/12 | 12:35:22 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | CloudFormationExecutionRole Resource creation Initiated
CDKToolkit |  0/12 | 12:35:22 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | FilePublishingRole Resource creation Initiated
CDKToolkit |  0/12 | 12:35:22 PM | CREATE_IN_PROGRESS   | AWS::ECR::Repository    | ContainerAssetsRepository Resource creation Initiated
CDKToolkit |  0/12 | 12:35:22 PM | CREATE_IN_PROGRESS   | AWS::SSM::Parameter     | CdkBootstrapVersion Resource creation Initiated
CDKToolkit |  0/12 | 12:35:23 PM | CREATE_IN_PROGRESS   | AWS::S3::Bucket         | StagingBucket Resource creation Initiated
CDKToolkit |  1/12 | 12:35:23 PM | CREATE_COMPLETE      | AWS::SSM::Parameter     | CdkBootstrapVersion 
CDKToolkit |  2/12 | 12:35:23 PM | CREATE_COMPLETE      | AWS::ECR::Repository    | ContainerAssetsRepository 
CDKToolkit |  3/12 | 12:35:36 PM | CREATE_COMPLETE      | AWS::S3::Bucket         | StagingBucket 
CDKToolkit |  3/12 | 12:35:37 PM | CREATE_IN_PROGRESS   | AWS::S3::BucketPolicy   | StagingBucketPolicy 
CDKToolkit |  3/12 | 12:35:38 PM | CREATE_IN_PROGRESS   | AWS::S3::BucketPolicy   | StagingBucketPolicy Resource creation Initiated
CDKToolkit |  4/12 | 12:35:38 PM | CREATE_COMPLETE      | AWS::S3::BucketPolicy   | StagingBucketPolicy 
CDKToolkit |  5/12 | 12:35:39 PM | CREATE_COMPLETE      | AWS::IAM::Role          | ImagePublishingRole 
CDKToolkit |  6/12 | 12:35:40 PM | CREATE_COMPLETE      | AWS::IAM::Role          | FilePublishingRole 
CDKToolkit |  7/12 | 12:35:40 PM | CREATE_COMPLETE      | AWS::IAM::Role          | CloudFormationExecutionRole 
CDKToolkit |  8/12 | 12:35:40 PM | CREATE_COMPLETE      | AWS::IAM::Role          | LookupRole 
CDKToolkit |  8/12 | 12:35:40 PM | CREATE_IN_PROGRESS   | AWS::IAM::Policy        | FilePublishingRoleDefaultPolicy 
CDKToolkit |  8/12 | 12:35:40 PM | CREATE_IN_PROGRESS   | AWS::IAM::Policy        | ImagePublishingRoleDefaultPolicy 
CDKToolkit |  8/12 | 12:35:41 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | DeploymentActionRole 
CDKToolkit |  8/12 | 12:35:41 PM | CREATE_IN_PROGRESS   | AWS::IAM::Policy        | FilePublishingRoleDefaultPolicy Resource creation Initiated
CDKToolkit |  8/12 | 12:35:41 PM | CREATE_IN_PROGRESS   | AWS::IAM::Policy        | ImagePublishingRoleDefaultPolicy Resource creation Initiated
CDKToolkit |  8/12 | 12:35:42 PM | CREATE_IN_PROGRESS   | AWS::IAM::Role          | DeploymentActionRole Resource creation Initiated
CDKToolkit |  9/12 | 12:35:56 PM | CREATE_COMPLETE      | AWS::IAM::Policy        | FilePublishingRoleDefaultPolicy 
CDKToolkit | 10/12 | 12:35:57 PM | CREATE_COMPLETE      | AWS::IAM::Policy        | ImagePublishingRoleDefaultPolicy 
CDKToolkit | 11/12 | 12:35:59 PM | CREATE_COMPLETE      | AWS::IAM::Role          | DeploymentActionRole 
CDKToolkit | 12/12 | 12:36:01 PM | CREATE_COMPLETE      | AWS::CloudFormation::Stack | CDKToolkit 
 ✅  Environment aws://047719662517/us-west-2 bootstrapped.
```

This should create s3 bucket, which it did:
```bash
$  aws s3 ls
2025-01-05 12:35:39 cdk-hnb659fds-assets-047719662517-us-west-2
```

But also we can see CDKToolkit cloudformation template was deployed:
```bash
$ aws cloudformation list-stacks
{
    "StackSummaries": [
        {
            "StackId": "arn:aws:cloudformation:us-west-2:047719662517:stack/CDKToolkit/908f24f0-cba4-11ef-a2ae-063840ba6313",
            "StackName": "CDKToolkit",
            "TemplateDescription": "This stack includes resources needed to deploy AWS CDK apps into this environment",
            "CreationTime": "2025-01-05T20:35:13.375000+00:00",
            "LastUpdatedTime": "2025-01-05T20:35:19.222000+00:00",
            "StackStatus": "CREATE_COMPLETE",
            "DriftInformation": {
                "StackDriftStatus": "NOT_CHECKED"
            }
        }
    ]
}
```

### Creating first CDK App
We are still using `root` aws account to perform work on our AWS accounts. So our first CDK app will be to create new user accounts. The CDK app will be called `users` ( yes very imaginative.. thank you).

For this I created new git repo [cdk-playground](https://github.com/iwidlinski/cdk-playground) which will contain this and other CDK apps.

    $ cdk init app --language python
    Applying project template app for python

    # Welcome to your CDK Python project!

    This is a blank project for CDK development with Python.

    The `cdk.json` file tells the CDK Toolkit how to execute your app.

    This project is set up like a standard Python project.  The initialization
    process also creates a virtualenv within this project, stored under the `.venv`
    directory.  To create the virtualenv it assumes that there is a `python3`
    (or `python` for Windows) executable in your path with access to the `venv`
    package. If for any reason the automatic creation of the virtualenv fails,
    you can create the virtualenv manually.

    To manually create a virtualenv on MacOS and Linux:

    ```
    $ python3 -m venv .venv
    ```

    After the init process completes and the virtualenv is created, you can use the following
    step to activate your virtualenv.

    ```
    $ source .venv/bin/activate
    ```

    If you are a Windows platform, you would activate the virtualenv like this:

    ```
    % .venv\Scripts\activate.bat
    ```

    Once the virtualenv is activated, you can install the required dependencies.

    ```
    $ pip install -r requirements.txt
    ```

    At this point you can now synthesize the CloudFormation template for this code.

    ```
    $ cdk synth
    ```

    To add additional dependencies, for example other CDK libraries, just add
    them to your `setup.py` file and rerun the `pip install -r requirements.txt`
    command.

    ## Useful commands

    * `cdk ls`          list all stacks in the app
    * `cdk synth`       emits the synthesized CloudFormation template
    * `cdk deploy`      deploy this stack to your default AWS account/region
    * `cdk diff`        compare deployed stack with current state
    * `cdk docs`        open CDK documentation

    Enjoy!

    Please run 'python3 -m venv .venv'!
    Executing Creating virtualenv...
    ✅ All done!


Once that is complete, we need to create virtual env and activate it
```bash
$ python3 -m venv .venv
# activate
$ source .venv/bin/activate
(.venv) $
```

Then install pip requirements
```bash
(.venv) $ pip install -r requirements.txt 
Collecting aws-cdk-lib==2.174.0 (from -r requirements.txt (line 1))
  Downloading aws_cdk_lib-2.174.0-py3-none-any.whl.metadata (60 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.0/60.0 kB 2.1 MB/s eta 0:00:00
Collecting constructs<11.0.0,>=10.0.0 (from -r requirements.txt (line 2))
  Downloading constructs-10.4.2-py3-none-any.whl.metadata (2.9 kB)
Collecting aws-cdk.asset-awscli-v1<3.0.0,>=2.2.208 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading aws_cdk.asset_awscli_v1-2.2.218-py3-none-any.whl.metadata (1.1 kB)
Collecting aws-cdk.asset-kubectl-v20<3.0.0,>=2.1.3 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading aws_cdk.asset_kubectl_v20-2.1.3-py3-none-any.whl.metadata (1.1 kB)
Collecting aws-cdk.asset-node-proxy-agent-v6<3.0.0,>=2.1.0 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading aws_cdk.asset_node_proxy_agent_v6-2.1.0-py3-none-any.whl.metadata (1.1 kB)
Collecting aws-cdk.cloud-assembly-schema<40.0.0,>=39.0.1 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading aws_cdk.cloud_assembly_schema-39.1.42-py3-none-any.whl.metadata (3.9 kB)
Collecting jsii<2.0.0,>=1.104.0 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading jsii-1.106.0-py3-none-any.whl.metadata (79 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 79.5/79.5 kB 5.8 MB/s eta 0:00:00
Collecting publication>=0.0.3 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading publication-0.0.3-py2.py3-none-any.whl.metadata (8.7 kB)
Collecting typeguard<4.3.0,>=2.13.3 (from aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading typeguard-4.2.1-py3-none-any.whl.metadata (3.7 kB)
  Downloading typeguard-2.13.3-py3-none-any.whl.metadata (3.6 kB)
Collecting attrs<25.0,>=21.2 (from jsii<2.0.0,>=1.104.0->aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading attrs-24.3.0-py3-none-any.whl.metadata (11 kB)
Collecting cattrs<24.2,>=1.8 (from jsii<2.0.0,>=1.104.0->aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading cattrs-24.1.2-py3-none-any.whl.metadata (8.4 kB)
Collecting importlib-resources>=5.2.0 (from jsii<2.0.0,>=1.104.0->aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading importlib_resources-6.5.2-py3-none-any.whl.metadata (3.9 kB)
Collecting python-dateutil (from jsii<2.0.0,>=1.104.0->aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading python_dateutil-2.9.0.post0-py2.py3-none-any.whl.metadata (8.4 kB)
Collecting typing-extensions<5.0,>=3.8 (from jsii<2.0.0,>=1.104.0->aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading typing_extensions-4.12.2-py3-none-any.whl.metadata (3.0 kB)
Collecting six>=1.5 (from python-dateutil->jsii<2.0.0,>=1.104.0->aws-cdk-lib==2.174.0->-r requirements.txt (line 1))
  Downloading six-1.17.0-py2.py3-none-any.whl.metadata (1.7 kB)
Downloading aws_cdk_lib-2.174.0-py3-none-any.whl (38.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 38.8/38.8 MB 4.5 MB/s eta 0:00:00
Downloading constructs-10.4.2-py3-none-any.whl (63 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.5/63.5 kB 6.2 MB/s eta 0:00:00
Downloading aws_cdk.asset_awscli_v1-2.2.218-py3-none-any.whl (17.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.8/17.8 MB 19.2 MB/s eta 0:00:00
Downloading aws_cdk.asset_kubectl_v20-2.1.3-py3-none-any.whl (25.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 25.5/25.5 MB 37.6 MB/s eta 0:00:00
Downloading aws_cdk.asset_node_proxy_agent_v6-2.1.0-py3-none-any.whl (1.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.5/1.5 MB 30.1 MB/s eta 0:00:00
Downloading aws_cdk.cloud_assembly_schema-39.1.42-py3-none-any.whl (184 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 184.5/184.5 kB 13.1 MB/s eta 0:00:00
Downloading jsii-1.106.0-py3-none-any.whl (554 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 554.8/554.8 kB 22.9 MB/s eta 0:00:00
Downloading publication-0.0.3-py2.py3-none-any.whl (7.7 kB)
Downloading typeguard-2.13.3-py3-none-any.whl (17 kB)
Downloading attrs-24.3.0-py3-none-any.whl (63 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.4/63.4 kB 5.5 MB/s eta 0:00:00
Downloading cattrs-24.1.2-py3-none-any.whl (66 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 66.4/66.4 kB 5.4 MB/s eta 0:00:00
Downloading importlib_resources-6.5.2-py3-none-any.whl (37 kB)
Downloading typing_extensions-4.12.2-py3-none-any.whl (37 kB)
Downloading python_dateutil-2.9.0.post0-py2.py3-none-any.whl (229 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 229.9/229.9 kB 18.9 MB/s eta 0:00:00
Downloading six-1.17.0-py2.py3-none-any.whl (11 kB)
Installing collected packages: publication, typing-extensions, typeguard, six, importlib-resources, attrs, python-dateutil, cattrs, jsii, constructs, aws-cdk.cloud-assembly-schema, aws-cdk.asset-node-proxy-agent-v6, aws-cdk.asset-kubectl-v20, aws-cdk.asset-awscli-v1, aws-cdk-lib
Successfully installed attrs-24.3.0 aws-cdk-lib-2.174.0 aws-cdk.asset-awscli-v1-2.2.218 aws-cdk.asset-kubectl-v20-2.1.3 aws-cdk.asset-node-proxy-agent-v6-2.1.0 aws-cdk.cloud-assembly-schema-39.1.42 cattrs-24.1.2 constructs-10.4.2 importlib-resources-6.5.2 jsii-1.106.0 publication-0.0.3 python-dateutil-2.9.0.post0 six-1.17.0 typeguard-2.13.3 typing-extensions-4.12.2
(.venv) $ 
```

CDK Synth shows that our app can generate cloudformation just fine:
```bash
(.venv) $ cdk  synth
Resources:
  CDKMetadata:
    Type: AWS::CDK::Metadata
### output cut
```

Then we can deploy this app that doesn't do anything yet.
```bash
(.venv) $ cdk deploy

✨  Synthesis time: 5.3s

current credentials could not be used to assume 'arn:aws:iam::047719662517:role/cdk-hnb659fds-deploy-role-047719662517-us-west-2', but are for the right account. Proceeding anyway.
UsersStack: start: Building f69126b922d56178d8112ba4e2d879fc39c05dc44a46776d54bd32132bc700ac:current_account-current_region
UsersStack: success: Built f69126b922d56178d8112ba4e2d879fc39c05dc44a46776d54bd32132bc700ac:current_account-current_region
UsersStack: start: Publishing f69126b922d56178d8112ba4e2d879fc39c05dc44a46776d54bd32132bc700ac:current_account-current_region
current credentials could not be used to assume 'arn:aws:iam::047719662517:role/cdk-hnb659fds-file-publishing-role-047719662517-us-west-2', but are for the right account. Proceeding anyway.
UsersStack: success: Published f69126b922d56178d8112ba4e2d879fc39c05dc44a46776d54bd32132bc700ac:current_account-current_region
current credentials could not be used to assume 'arn:aws:iam::047719662517:role/cdk-hnb659fds-lookup-role-047719662517-us-west-2', but are for the right account. Proceeding anyway.
Lookup role arn:aws:iam::047719662517:role/cdk-hnb659fds-lookup-role-047719662517-us-west-2 was not assumed. Proceeding with default credentials.
UsersStack: deploying... [1/1]
current credentials could not be used to assume 'arn:aws:iam::047719662517:role/cdk-hnb659fds-deploy-role-047719662517-us-west-2', but are for the right account. Proceeding anyway.
UsersStack: creating CloudFormation changeset...
UsersStack | 0/2 | 8:08:55 PM | REVIEW_IN_PROGRESS   | AWS::CloudFormation::Stack | UsersStack User Initiated
UsersStack | 0/2 | 8:09:01 PM | CREATE_IN_PROGRESS   | AWS::CloudFormation::Stack | UsersStack User Initiated
UsersStack | 0/2 | 8:09:03 PM | CREATE_IN_PROGRESS   | AWS::CDK::Metadata | CDKMetadata/Default (CDKMetadata) 
UsersStack | 0/2 | 8:09:04 PM | CREATE_IN_PROGRESS   | AWS::CDK::Metadata | CDKMetadata/Default (CDKMetadata) Resource creation Initiated
UsersStack | 1/2 | 8:09:04 PM | CREATE_COMPLETE      | AWS::CDK::Metadata | CDKMetadata/Default (CDKMetadata) 
UsersStack | 2/2 | 8:09:05 PM | CREATE_COMPLETE      | AWS::CloudFormation::Stack | UsersStack 

 ✅  UsersStack

✨  Deployment time: 11.9s

Stack ARN:
arn:aws:cloudformation:us-west-2:047719662517:stack/UsersStack/717047a0-ce3f-11ef-b888-0a2aa41805d9

✨  Total time: 17.19s
```

The `UsersStack` stack is deployed along the `CDKToolKit` stack.
```bash
(.venv) $ aws cloudformation list-stacks --query 'StackSummaries[*].[StackName,StackStatus]'
[
    [
        "UsersStack",
        "CREATE_COMPLETE"
    ],
    [
        "CDKToolkit",
        "CREATE_COMPLETE"
    ]
]
```

Now we need to make the app to do something useful