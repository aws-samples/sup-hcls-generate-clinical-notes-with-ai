# sup-hcls-generate-clinical-notes-with-ai

These notebooks demonstrate how to generate clinical notes using AWS HealthScribe APIs and how to extend HealthScribe output with Amazon Comprehend Medical and Bedrock. It also provides an option for the same use case with Amazon Transcribe and Transcribe Medical for regions where HealthScribe is not yet available.

## Prerequisites
- Verify that model access to Anthropic's Claude v3 models is granted to the account being used, see documentation here: [Amazon Bedrock Model Access](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html)

## Setup Instructions
1. These notebooks were designed to run with Amazon SageMaker Studio or SageMaker Notebooks instances. To use Studio, you will need to setup a SageMaker Domain. For instructions on how to onboard to a Sagemaker domain, refer to this [link](https://docs.aws.amazon.com/sagemaker/latest/dg/gs-studio-onboard.html).

2. Check for an **AmazonTranscribeServiceRole** in your [IAM console](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles). If you don't have one, you can create it by starting a transcription job on the [HealthScribe console](https://us-east-1.console.aws.amazon.com/transcribe/home?region=us-east-1#createJobHealthScribe) or manually creating the role with necessaryt permissions on the [IAM console](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/create). Have in mind this role will need access to the S3 buckets used for input and output.

3. Update your SageMaker execution role (created when you initially setup the domain) to assume the HealthScribe role with a policy similar to the one below:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole",
                "iam:PassRole"
            ],
            "Resource": [
                "[HEALTHSCRIBE_IAM_ROLE]]"
            ]
        }
    ]
}
```

## Usage Instructions
1. Open SageMaker Studio and import all notebook files from this project. The notebooks files are numbers and 1-3 need to be executed sequentially given the second and third files uses outputs from the first file. Notebooks 4.1 and 4.2 do not have dependencies and can be executed separately.
2. Run all cells in the Jupyter Notebooks provided. Each notebook will have a Setup section in the beginning with additional installation instructions.